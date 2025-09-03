


CCGSC NGINX V1 
Nginx configuration file with comprehensive, line-by-line explanatory comments detailing its syntax, function, and data flow.

---

Nginx

 <%
```
# This is an Nginx configuration file, located at /etc/nginx/sites-available/prime-distributor.
# Nginx uses a block-based syntax. Directives (like 'server_name' or 'listen') are followed by their parameters and a semicolon.
# Blocks (like 'server' or 'location') are enclosed in curly braces {} and group directives for a specific context.

#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# Server Block for the Director Interface (ccgsc-director.digitalbd.org)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#

# The 'server' block defines a virtual server. Nginx chooses which server block to use for a request based on the 'listen' and 'server_name' directives.
server {

    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#
    # Server Identification
    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#

    # The 'server_name' directive specifies the domain name(s) that this server block will respond to.
    # When a request comes in, Nginx checks its 'Host' header against the server_name values in all configuration files.
    # This block will handle all requests for "ccgsc-director.digitalbd.org".
    server_name ccgsc-director.digitalbd.org;


    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#
    # Serving Static Files
    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#

    # The 'root' directive sets the root directory for requests handled by this server block.
    # For a request like https://ccgsc-director.digitalbd.org/css/style.css, Nginx will look for the file at "/home/ccgsc-user1/CCGSC/.../public/css/style.css".
    # This path is absolute on the server's file system.
    root "/home/ccgsc-user1/CCGSC/PA10KT2/prime_distributed_projectPrlCc1B_V5_10K/public";

    # The 'index' directive defines the file that will be served if a directory is requested.
    # If a user requests https://ccgsc-director.digitalbd.org/, Nginx will serve the 'director.html' file from the root directory defined above.
    index director.html;


    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#
    # SSL/TLS Configuration (HTTPS)
    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#

    # The 'listen' directive tells Nginx which IP address and port to listen on for incoming connections.
    # '443' is the standard port for HTTPS traffic.
    # 'ssl' tells Nginx that all connections on this port must use the SSL/TLS protocol.
    # The comment "# managed by Certbot" indicates that this line was automatically added or modified by the Let's Encrypt Certbot tool.
    listen 443 ssl; # managed by Certbot

    # The 'ssl_certificate' directive specifies the path to the public SSL certificate file (fullchain.pem).
    # This certificate is sent to the client (browser) to prove the server's identity.
    ssl_certificate /etc/letsencrypt/live/ccgsc-demo.digitalbd.org/fullchain.pem; # managed by Certbot

    # The 'ssl_certificate_key' directive specifies the path to the private key for the SSL certificate.
    # This key is kept secret on the server and is used to decrypt incoming data from the client.
    ssl_certificate_key /etc/letsencrypt/live/ccgsc-demo.digitalbd.org/privkey.pem; # managed by Certbot

    # The 'include' directive allows you to include another configuration file.
    # This is useful for keeping common configurations in one place. Here, it includes Certbot's recommended SSL settings for enhanced security.
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot

    # The 'ssl_dhparam' directive specifies the path to a file containing Diffie-Hellman parameters.
    # These parameters are used for Perfect Forward Secrecy (PFS), which ensures that even if the server's private key is compromised in the future, past encrypted sessions cannot be decrypted.
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#
    # Request Routing Logic
    #~~~~~~~~~~~~~~~~~~~~~~~~~~~#

    # The 'location' block defines how Nginx should process requests for different URIs.
    # 'location /' is a prefix match that catches all requests for this server, as all URIs start with '/'.
    location / {
        # The 'try_files' directive is a powerful way to handle requests. It checks for the existence of files or directories in a specific order and serves the first one it finds.
        # Data Flow:
        # 1. '$uri': Nginx first checks for a file that exactly matches the request URI (e.g., /images/logo.png).
        # 2. '$uri/': If no file is found, it checks for a directory with that name (e.g., /about/). If found, it will serve the index file (director.html) from that directory.
        # 3. '@proxy': If neither a file nor a directory is found, the request is passed internally to the named location '@proxy' as a final fallback.
        # This setup is perfect for web applications that have both static assets (like CSS, JS, images) and a dynamic backend (like a Node.js API).
        try_files $uri $uri/ @proxy;
    }

    # This is a 'named location' block. It's not accessible directly via a URL but can be used as a target for internal redirects from other location blocks (like 'try_files').
    # The '@' symbol distinguishes it as a named location.
    location @proxy {
        # The 'proxy_pass' directive is the core of a reverse proxy. It forwards the request to another server.
        # Here, any request that falls through 'try_files' is sent to a server running on the same machine (127.0.0.1) at port 8080, which is your Node.js application.
        proxy_pass http://127.0.0.1:8080; # Your Node.js app

        # The following 'proxy_set_header' directives modify or add headers to the request before it is sent to the backend Node.js server.
        # This is crucial because the backend app needs to know about the original request from the client, not just the proxied request from Nginx.

        # 'proxy_http_version 1.1' is necessary for enabling keep-alive connections and is required for WebSocket connections to work properly.
        proxy_http_version 1.1;

        # These two headers are essential for proxying WebSocket connections. WebSockets use the HTTP Upgrade mechanism.
        # 'proxy_set_header Upgrade $http_upgrade;' passes the 'Upgrade' header from the client to the backend.
        proxy_set_header Upgrade $http_upgrade;
        # 'proxy_set_header Connection 'upgrade';' tells the backend server to upgrade the connection.
        proxy_set_header Connection 'upgrade';

        # 'proxy_set_header Host $host;' passes the original 'Host' header from the client's request to the backend.
        # Without this, the Node.js app would see the host as '127.0.0.1:8080' instead of 'ccgsc-director.digitalbd.org'.
        proxy_set_header Host $host;

        # 'proxy_set_header X-Real-IP $remote_addr;' creates a new header 'X-Real-IP' and sets its value to the client's actual IP address.
        # The '$remote_addr' variable in Nginx holds the IP of the connecting client.
        proxy_set_header X-Real-IP $remote_addr;

        # 'proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;' is a standard header for identifying the originating IP address of a client.
        # The '$proxy_add_x_forwarded_for' variable takes the value of the incoming 'X-Forwarded-For' header and appends the client's IP address to it.
        # This is useful if the request passes through multiple proxies.
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}


#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# Server Block for the Worker Interface (ccgsc-demo.digitalbd.org)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#

# This second 'server' block is very similar to the first one but is configured for a different subdomain.
# This demonstrates how Nginx can host multiple websites or web application interfaces on a single server.
server {
    # This block will handle all requests for "ccgsc-demo.digitalbd.org".
    server_name ccgsc-demo.digitalbd.org;

    # The 'root' directive is the same, meaning both subdomains share the same directory for static files.
    root "/home/ccgsc-user1/CCGSC/PA10KT2/prime_distributed_projectPrlCc1B_V5_10K/public";

    # The 'index' file is different. This allows you to serve a different default page for this subdomain.
    # A request to https://ccgsc-demo.digitalbd.org/ will serve 'worker.html'.
    index worker.html;


    # The SSL configuration is identical to the first block.
    # Note: Certbot often uses a single certificate that is valid for multiple subdomains. Here, the certificate issued for 'ccgsc-demo.digitalbd.org' is being used for both subdomains.
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/ccgsc-demo.digitalbd.org/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/ccgsc-demo.digitalbd.org/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


    # The request routing logic is also identical.
    # It first tries to serve static files, and if it can't find them, it forwards the request to the same Node.js application on port 8080.
    # Your Node.js application will need to use the 'Host' header (which we are passing) to differentiate between requests for the director and worker interfaces.
    location / {
        try_files $uri $uri/ @proxy;
    }

    # The proxy logic is identical, forwarding requests to the backend and setting the necessary headers.
    location @proxy {
        proxy_pass http://127.0.0.1:8080; # Your Node.js app
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}


#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# HTTP to HTTPS Redirects
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~#
# These server blocks are set up by Certbot to ensure that any user trying to access the site via unencrypted HTTP (port 80) is automatically and permanently redirected to the secure HTTPS version (port 443).

# This server block handles port 80 requests for 'ccgsc-demo.digitalbd.org'.
server {
    # Control Flow: An 'if' directive checks a condition. Here, it checks if the '$host' variable (the hostname from the request) matches 'ccgsc-demo.digitalbd.org'.
    if ($host = ccgsc-demo.digitalbd.org) {
        # The 'return 301' directive sends an HTTP 301 "Moved Permanently" redirect response to the client.
        # This tells the browser to make a new request to the specified URL: 'https://' followed by the original host and the original request URI ('$request_uri').
        # This is the preferred method for SEO (Search Engine Optimization) as it tells search engines that the HTTPS version is the canonical one.
        return 301 https://$host$request_uri;
    }

    # This directive tells Nginx to listen on port 80, the standard port for HTTP.
    listen 80;

    # This specifies the domain name this block applies to.
    server_name ccgsc-demo.digitalbd.org;

    # This 'return 404' is a fallback. In this configuration, since the server_name matches the 'if' condition, this line will never be reached for valid requests.
    # It's a safety measure included by Certbot to ensure that if the server block were somehow to process a request for a different host, it would return a 'Not Found' error.
    return 404;
}

# This server block does the exact same thing as the one above, but for the 'ccgsc-director.digitalbd.org' subdomain.
server {
    if ($host = ccgsc-director.digitalbd.org) {
        return 301 https://$host$request_uri;
    }

    listen 80;
    server_name ccgsc-director.digitalbd.org;
    return 404;
}
```
%>







