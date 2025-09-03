



[[System Design]]
[[CCGSC_System_Design]]
[[0 CCGSC_Manuscript_Organizer_Dashboard]]
[[Computing Cluster Interconnect]]
[[Cluster Computing]]

[[WebSocket vs WebRTC vs HTTP HTTPS]]




# Protocol Definitions and Similar Protocols

**Main Takeaway:** HTTP, HTTPS, WebRTC, and MQTT serve distinct roles in web and IoT communication—HTTP/HTTPS for resource transfer, WebRTC for peer-to-peer real-time media, and MQTT for lightweight publish/subscribe messaging. Other notable protocols include CoAP, AMQP, and XMPP, each optimized for specific use cases.

## 1. HTTP (Hypertext Transfer Protocol)

An application-layer protocol for fetching resources (HTML, images, etc.) over the web.

- Stateless client–server model over TCP
- Messages: requests (GET, POST, etc.) and responses
- Base protocol for web browsing and RESTful APIs[1]


## 2. HTTPS (HTTP Secure)

HTTP over TLS (formerly SSL)

- Encrypts HTTP messages via TLS handshake and symmetric encryption
- Ensures confidentiality, integrity, and server authentication
- Required for login pages, e-commerce, and sensitive data[2][3]


## 3. WebRTC (Web Real-Time Communications)

Peer-to-peer framework enabling real-time audio, video, and data exchange in browsers and apps.

- Uses JavaScript APIs: RTCPeerConnection, RTCDataChannel, MediaStream
- NAT traversal via STUN and TURN servers
- Mandatory encryption of media streams[4][5]


## 4. MQTT (Message Queuing Telemetry Transport)

Lightweight publish/subscribe messaging protocol for constrained devices and unreliable networks.

- Clients (publishers/subscribers) connect to a broker over TCP
- Topics: hierarchical strings; broker routes messages accordingly
- Three QoS levels:

1. At most once
2. At least once
3. Exactly once

- Minimal packet overhead; ideal for IoT telemetry and control[6][7]


## 5. CoAP (Constrained Application Protocol)

RESTful web-transfer protocol for resource-constrained devices and networks.

- Runs over UDP for low overhead
- Request/response model with four message types: Confirmable, Non-confirmable, Acknowledgement, Reset
- Built-in resource discovery via “.well-known/core” URI
- Supports multicast, block-wise transfers, and simple reliability[8][9]


## 6. AMQP (Advanced Message Queuing Protocol)

Open, binary, application-layer protocol for message-oriented middleware.

- Broker-based architecture with exchanges (route messages) and queues (store messages)
- Guarantees reliable, secure, and interoperable messaging
- Features message orientation, queuing, routing patterns (point-to-point, pub/sub), and transactions[10][11]


## 7. XMPP (Extensible Messaging and Presence Protocol)

XML-based, decentralized protocol for instant messaging, presence, and structured data exchange.

- Client–server architecture; federation akin to email
- Uses XML “stanzas” (message, presence, IQ) over TCP
- Extensible via XMPP Extension Protocols (XEPs) for multi-party chat, file transfer, and more
- Enables end-to-end, transport, and server security via SASL and TLS[12][13]


# Summary Table

| Protocol | Layer | Transport | Model | Encryption | Key Features |
| :-- | :-- | :-- | :-- | :-- | :-- |
| HTTP | Application | TCP | Client–Server | Optional | Stateless requests/responses; RESTful APIs[1] |
| HTTPS | Application | TLS/TCP | Client–Server | TLS | Encrypted HTTP; certificates; integrity[2][3] |
| WebRTC | Application | UDP/TCP | Peer-to-Peer | DTLS/SRTP | Real-time audio/video/data; STUN/TURN[4][5] |
| MQTT | Application | TCP | Publish–Subscribe | Optional TLS | Lightweight; QoS levels; topic routing[6][7] |
| CoAP | Application | UDP | Request–Response | DTLS | RESTful; multicast; resource discovery[8][9] |
| AMQP | Application | TCP | Broker-Mediated | TLS/SASL | Exchanges/queues; reliable, secure messaging[10][11] |
| XMPP | Application | TCP | Client–Server/Federated | TLS/SASL | XML stanzas; presence; extensibility[12][13] |

Each protocol addresses unique requirements—from high-bandwidth web content (HTTP/HTTPS) to low-power IoT telemetry (MQTT, CoAP), reliable enterprise messaging (AMQP), and real-time peer communication (WebRTC, XMPP).

---

# How Core Web and IoT Protocols Work

**Key Takeaway:**
HTTP/HTTPS underpin resource exchange on the web (with HTTPS adding encryption, integrity, and authentication), WebRTC creates end-to-end real-time streams via peer-to-peer connections using ICE and DTLS/SRTP, MQTT enables lightweight publish/subscribe messaging with minimal overhead and three QoS levels, and protocols like FTP, SMTP, and DNS provide foundational file transfer, email delivery, and name resolution services.

## 1. HTTP: Stateless Data Transfer on the Web

HTTP (Hypertext Transfer Protocol) is an **application-layer**, **stateless** request–response protocol over TCP. A client (e.g., browser) sends an HTTP request (method, URL, headers), the server processes it, and returns an HTTP response (status code, headers, body).

- Resource typing and negotiation via headers allow clients and servers to agree on formats (HTML, JSON, images)[^2_1].
- Statelessness means each request is independent, simplifying scalability but requiring cookies or tokens for session state[^2_2].


## 2. HTTPS: HTTP over TLS for Security

HTTPS adds a **TLS (Transport Layer Security)** layer atop HTTP, providing:

1. **Encryption** of all data in transit, preventing eavesdropping.
2. **Integrity** via message authentication codes, ensuring data isn’t altered.
3. **Server (and optionally client) authentication** using X.509 certificates issued by trusted Certificate Authorities, thwarting impersonation and man-in-the-middle attacks.
4. **Forward secrecy** when using ephemeral key exchanges, limiting impact of key compromise[^2_3][^2_4].

## 3. WebRTC: Real-Time Peer-to-Peer Communication

WebRTC (Web Real-Time Communication) enables browsers and apps to exchange audio, video, and arbitrary data directly without relaying through application servers (once the connection is established). Key mechanisms:

- **Signaling** (external) exchanges session descriptions (SDP) and ICE candidates.
- **ICE (Interactive Connectivity Establishment)** gathers host, server-reflexive (via STUN), and relay (via TURN) candidates to traverse NATs/firewalls[^2_5].
- **DTLS** secures data channels and **SRTP** secures media streams, both providing encryption, integrity, and replay protection.
- **RTCPeerConnection** API manages offers/answers, candidate exchange, and stream delivery[^2_6].


## 4. MQTT: Lightweight IoT Messaging

MQTT (Message Queuing Telemetry Transport) is a **publish/subscribe** protocol over TCP designed for constrained devices and networks:

- **Broker-mediated**: clients connect to a central broker that routes messages based on hierarchical topics (e.g., `sensors/temperature`).
- **Very low overhead** with fixed 2-byte header, minimal packet size.
- **Three QoS levels**:
– **0 (at most once)**: best effort, no acknowledgment
– **1 (at least once)**: ensures delivery but may duplicate
– **2 (exactly once)**: two-phase handshake, highest overhead
- Supports persistent sessions, last-will messages, and optional TLS for encryption[previous summary].


## 5. Other Common Internet Protocols

| Protocol | Purpose | Transport | Model | Key Features |
| :-- | :-- | :-- | :-- | :-- |
| FTP | File Transfer Protocol | TCP | Client–Server | Separate control/data channels; active/passive modes |
| SMTP | Simple Mail Transfer Protocol | TCP | Store-and-forward | Relay mail between servers; extensions (STARTTLS, authentication) |
| DNS | Domain Name System | UDP/TCP | Hierarchical lookup | Caching resolvers; records (A, MX, CNAME, TXT, etc.); zone delegation |

Each protocol targets specific requirements—HTTP/HTTPS for web resources, WebRTC for real-time media, MQTT for resource-efficient IoT messaging, and FTP/SMTP/DNS for essential file transfer, email routing, and name resolution services.

<div style="text-align: center">⁂</div>

[^2_1]: https://www.rfc-editor.org/info/rfc2068

[^2_2]: https://developer.mozilla.org/en-US/docs/Web/HTTP

[^2_3]: https://www.upguard.com/blog/what-is-https

[^2_4]: https://www.cloudflare.com/learning/ssl/what-is-https/

[^2_5]: https://webrtc.org/getting-started/peer-connections-advanced

[^2_6]: https://webrtc.org/getting-started/peer-connections

[^2_7]: https://www.sec.gov/Archives/edgar/data/1868419/000164117225010025/forms-1a.htm

[^2_8]: https://www.sec.gov/Archives/edgar/data/1868419/000164117225009084/forms-1.htm

[^2_9]: https://www.sec.gov/Archives/edgar/data/1905660/000121390025038038/ea0237776-20f_hubcyber.htm

[^2_10]: https://www.sec.gov/Archives/edgar/data/1903145/000121390025037703/ea0239609-20f_gorilla.htm

[^2_11]: https://www.sec.gov/Archives/edgar/data/896493/000121465925006430/y425252s1.htm

[^2_12]: https://www.sec.gov/Archives/edgar/data/1725033/000141057825000892/xyf-20241231x20f.htm

[^2_13]: https://www.sec.gov/Archives/edgar/data/1946703/000121390025033933/ea0238515-20f_webuy.htm

[^2_14]: https://ieeexplore.ieee.org/document/9573978/

[^2_15]: https://www.mdpi.com/2076-3417/11/16/7188

[^2_16]: https://ieeexplore.ieee.org/document/8909150/

[^2_17]: https://www.semanticscholar.org/paper/afdf0cc6146e9e8e786eb93b2774d55874385496

[^2_18]: http://www.scirp.org/journal/doi.aspx?DOI=10.4236/jcc.2017.55008

[^2_19]: https://www.rfc-editor.org/info/rfc7480

[^2_20]: https://ieeexplore.ieee.org/document/9199895/

[^2_21]: https://www.tutorchase.com/answers/ib/computer-science/how-does-the-http-protocol-transmit-data-packets

[^2_22]: https://www.cloudflare.com/learning/ssl/why-use-https/

[^2_23]: https://getstream.io/resources/projects/webrtc/architectures/p2p/

[^2_24]: https://www.lenovo.com/us/en/glossary/hypertext-transfer-protocol/

[^2_25]: https://peerjs.com

[^2_26]: https://www.w3schools.com/tags/ref_httpmethods.asp

[^2_27]: https://www.7signal.com/http-hypertext-transfer-protocol

[^2_28]: https://www.techtarget.com/searchsoftwarequality/definition/HTTPS

[^2_29]: https://blog.logrocket.com/webrtc-video-streaming/

[^2_30]: https://www.geeksforgeeks.org/html/what-is-http/

[^2_31]: https://www.geeksforgeeks.org/html/explain-working-of-https/

[^2_32]: https://iopscience.iop.org/article/10.1088/1742-6596/513/3/032034

[^2_33]: http://ieeexplore.ieee.org/document/5197305/

[^2_34]: https://www.epj-conferences.org/10.1051/epjconf/202024504025

[^2_35]: https://arxiv.org/pdf/2305.02049.pdf

[^2_36]: https://www.mdpi.com/2673-4591/59/1/1/pdf?version=1702266404

[^2_37]: https://www.epj-conferences.org/articles/epjconf/pdf/2019/19/epjconf_chep2018_04039.pdf

[^2_38]: https://www.e3s-conferences.org/articles/e3sconf/pdf/2021/28/e3sconf_pgsge2021_01027.pdf

[^2_39]: https://www.epj-conferences.org/articles/epjconf/pdf/2024/05/epjconf_chep2024_01001.pdf

[^2_40]: https://arxiv.org/pdf/2212.07475.pdf

[^2_41]: https://ijece.iaescore.com/index.php/IJECE/article/download/28192/16713

[^2_42]: https://www.maxwellsci.com/announce/RJASET/7-2946-2953.pdf

[^2_43]: http://arxiv.org/pdf/2410.06066.pdf

[^2_44]: https://verpex.com/blog/privacy-security/what-is-https-and-why-is-it-so-important

[^2_45]: https://stackoverflow.com/questions/29416431/is-webrtc-really-peer-to-peer-protocol

[^2_46]: https://en.wikipedia.org/wiki/HTTP

[^2_47]: https://en.wikipedia.org/wiki/HTTPS





