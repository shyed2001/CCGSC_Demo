


<%
// File Path: prime_distributed_projectPrlCc1B V5(10K)/public/director.js
// This script acts as the main controller for the director's dashboard (director.html).
// It handles communication with the WebSocket server, manages the UI updates,
// and displays real-time statistics about the distributed computation.

// --- DOM ELEMENT SELECTION ---
// Here, we get references to the HTML elements we need to interact with.
// Storing them in constants at the top makes the code cleaner and more performant,
// as we don't need to search the DOM for these elements repeatedly.

// document.getElementById('id') is a method to select a single HTML element by its unique 'id' attribute.
const startBtn = document.getElementById('start-btn'); // The "Start Computation" button.
const logDiv = document.getElementById('log'); // The text area for displaying log messages.
const progressContainer = document.getElementById('progress-container'); // The container where individual task progress bars will be added.
const tasksCompletedSpan = document.getElementById('tasks-completed'); // The <span> to show "X / Y" tasks completed.
const runningTotalSpan = document.getElementById('running-total'); // The <span> to show the total number of primes found so far.
const workerCountSpan = document.getElementById('worker-count'); // The <span> to display the number of currently connected workers.

// document.querySelector('selector') is a more versatile method to select the first element that matches a CSS selector.
// Here, we select the <tbody> element inside the element with id="worker-table".
const workerTableBody = document.querySelector('#worker-table tbody');

// --- GLOBAL STATE MANAGEMENT ---
// These variables hold the state of the application.

// Data Structure (DSA): This is an object used as a hash map or dictionary.
// The keys will be the unique `workerId` strings, and the values will be objects
// containing information and status for each worker. This provides O(1) average time complexity for lookups.
const workers = {};

// A constant defining the total number of tasks for the computation. This must match the server's configuration.
const TOTAL_TASKS = 25000;

// A variable to store the cumulative sum of primes found.
// It is initialized as a BigInt (using the 'n' suffix) because the total number of primes
// can easily exceed the maximum safe integer value in standard JavaScript (2^53 - 1),
// which would lead to precision errors. BigInt can handle arbitrarily large integers.
let runningTotal = 0n;

// --- HELPER FUNCTIONS ---

/**
 * A utility function to append a message to the log display area.
 * @param {string} message - The text message to be logged.
 */
const log = (message) => {
    // Appends the new message and a newline character to the existing text content of the log div.
    logDiv.textContent += message + '\n';
    // This line automatically scrolls the log div to the bottom so the latest message is always visible.
    // It sets the vertical scroll position to the total scrollable height of the element.
    logDiv.scrollTop = logDiv.scrollHeight;
};

// --- WEBSOCKET COMMUNICATION SETUP ---

// The WebSocket constructor creates a new WebSocket object, initiating a connection to the server.
// The URL starts with 'wss://' which stands for "WebSocket Secure," the encrypted version of the 'ws://' protocol.
// This is the primary communication channel between the director's browser and the backend server.
// The commented-out lines are examples of URLs used during different stages of development (localhost, local network IP, etc.).
const socket = new WebSocket('wss://ccgsc-director.digitalbd.org/ws'); // Your production server URL

// The 'onopen' event handler is a function that is automatically called when the
// WebSocket connection is successfully established.
socket.onopen = () => {
    // Log a confirmation message to the UI.
    log('✅ Connected. Registering as Director...');
    // Send a message to the server to identify this client.
    // JSON.stringify() converts a JavaScript object into a JSON string, which is the standard format for WebSocket messages.
    // This tells the server that this specific client is the director and should receive all control-related messages.
    socket.send(JSON.stringify({ type: 'registerDirector' }));
};

// The 'onmessage' event handler is the most critical part of the client-side logic.
// It is called every time a message is received from the WebSocket server.
socket.onmessage = (event) => {
    // The `event.data` property contains the message sent by the server, which is a JSON string.
    // `JSON.parse()` converts this string back into a JavaScript object so we can easily access its properties.
    const data = JSON.parse(event.data);

    // Control Flow: A `switch` statement is used to handle different types of messages from the server
    // based on the `type` property of the received data object. This is a clean way to manage different server events.
    switch(data.type) {
        // Case: The server sent a simple log message to be displayed.
        case 'log':
            log(data.message);
            break;

        // Case: A new worker client has connected to the server.
        case 'workerConnected':
            // Add the new worker to our `workers` object. The worker's unique ID is used as the key.
            // The value is an object storing its initial information, status, and a placeholder for task timing.
            workers[data.workerId] = { info: data.info, status: 'Idle', lastTaskTime: '---' };
            // Call the function to redraw the worker table with the new data.
            updateWorkerTable();
            log(`Worker #${data.workerId} connected.`);
            break;
            
        // Case: A worker has disconnected from the server.
        case 'workerDisconnected':
            // The `delete` operator removes the property (the worker) from our `workers` object.
            delete workers[data.workerId];
            // Redraw the worker table to reflect the change.
            updateWorkerTable();
            log(`Worker #${data.workerId} disconnected.`);
            break;

        // Case: A worker has completed a task and sent its progress update.
        case 'progress':
            // Find the specific progress bar div for this task using its ID.
            const bar = document.getElementById(`bar-${data.taskId}`);
            // If the bar element exists...
            if (bar) {
                // ...change its background color to green to visually mark it as complete.
                bar.style.backgroundColor = '#2ecc71';
                // ...and update its text to show it's done and how many primes were found in that task.
                // `toLocaleString()` formats the number with commas for better readability.
                bar.textContent = `Task ${data.taskId}: Done (${BigInt(data.count).toLocaleString()})`;
            }
            
            // --- Update global totals ---
            // Add the primes found in this task to our running total. This must use BigInt arithmetic.
            runningTotal += BigInt(data.count);
            // Update the UI span showing the number of completed tasks.
            tasksCompletedSpan.textContent = `${data.totalCompleted} / ${TOTAL_TASKS}`;
            // Update the UI span showing the new grand total of primes.
            runningTotalSpan.textContent = runningTotal.toLocaleString();

            // --- Update the specific worker's status in the table ---
            // Check if the worker who sent this progress is still in our list (it should be).
            if (workers[data.workerId]) {
                // Set its status back to 'Idle', as it's now ready for a new task.
                workers[data.workerId].status = 'Idle';
                // Record how long the task took, formatted to two decimal places.
                workers[data.workerId].lastTaskTime = data.taskDuration.toFixed(2);
                // Redraw the table to show the worker's new status and task time.
                updateWorkerTable();
            }
            break;

        // Case: The server has declared that all tasks are complete.
        case 'complete':
            log(`\n🎉 ALL TASKS COMPLETE! Final Total: ${BigInt(data.totalPrimes).toLocaleString()}`);
            // Re-enable the start button so a new computation can be started.
            startBtn.disabled = false;
            startBtn.textContent = 'Start Computation';
            // Loop through all workers in our list and set their status to 'Idle'.
            for (const id in workers) {
                workers[id].status = 'Idle';
            }
            // Redraw the worker table one last time.
            updateWorkerTable();
            break;
    }
};

// --- EVENT LISTENERS for UI CONTROLS ---

// The 'onclick' event handler is a function that runs when the start button is clicked.
startBtn.onclick = () => {
    log('Sending command to start computation...');
    // Disable the button to prevent multiple clicks while a computation is running.
    startBtn.disabled = true;
    startBtn.textContent = 'Computation Running...';
    
    // --- Reset the UI for a new computation ---
    // Clear any progress bars from the previous run.
    progressContainer.innerHTML = '';
    // Reset the running total back to zero (as a BigInt).
    runningTotal = 0n;
    // Reset the text displays for completed tasks and the running total.
    tasksCompletedSpan.textContent = `0 / ${TOTAL_TASKS}`;
    runningTotalSpan.textContent = '0';

    // --- Create placeholder UI elements ---
    // This loop creates a visual placeholder `div` for every single task.
    // This gives the user immediate feedback that the process has started and shows the scale of the computation.
    for (let i = 0; i < TOTAL_TASKS; i++) {
        const bar = document.createElement('div'); // Create a new <div> element.
        bar.className = 'progress-bar'; // Assign it a class for styling.
        bar.id = `bar-${i}`; // Assign a unique ID so we can find and update it later.
        bar.textContent = `Task ${i}: Waiting...`; // Set its initial text.
        progressContainer.appendChild(bar); // Add the new div to the container in the HTML.
    }

    // --- Update worker statuses ---
    // Mark all currently connected workers as 'Assigning...' to show they are about to receive tasks.
    for (const id in workers) {
        workers[id].status = 'Assigning...';
    }
    updateWorkerTable(); // Redraw the table with the new statuses.

    // Finally, send the 'startComputation' command to the server.
    socket.send(JSON.stringify({ type: 'startComputation' }));
};

/**
 * Renders the entire worker status table based on the current state of the `workers` object.
 * This function is called whenever there's a change in the workers list or their status.
 */
function updateWorkerTable() {
    // A simple and effective way to clear the table is to set the `innerHTML` of its body to an empty string.
    workerTableBody.innerHTML = '';
    // Update the worker count display. `Object.keys()` returns an array of the object's keys (the worker IDs).
    workerCountSpan.textContent = Object.keys(workers).length;

    // Control Flow: A `for...in` loop iterates over all the properties (keys) of the `workers` object.
    for (const id in workers) {
        const worker = workers[id]; // Get the worker's data object.
        const row = workerTableBody.insertRow(); // Create a new table row `<tr>` element.
        
        // Use a template literal (backticks ``) to easily construct the HTML for all the cells `<td>` in this row.
        // This populates the row with the worker's ID, status, and other information.
        // The ternary operator `(condition ? value_if_true : value_if_false)` is used to gracefully handle
        // cases where a property might not exist, showing '---' as a fallback.
        row.innerHTML = `
            <td>${id}</td>
            <td>${worker.status}</td>
            <td>${worker.info.cpuCores}</td>
            <td>${worker.info.deviceMemory}</td>
            <td>${worker.assignedTask ? worker.assignedTask.taskId : '---'}</td>
            <td>${worker.lastTaskTime}</td>
            <td>${worker.info.userAgent}</td>
        `;
    }
}

// --- Logic for the Clear State button ---
// Get a reference to the 'Clear State' button.
const clearStateBtn = document.getElementById('clear-state-btn');
// Check if the button actually exists on the page to avoid errors.
if (clearStateBtn) {
    // Add a 'click' event listener to the button.
    clearStateBtn.addEventListener('click', () => {
        // `confirm()` shows a native browser dialog with "OK" and "Cancel" buttons.
        // It returns `true` if the user clicks "OK". This is a safeguard against accidental clicks.
        if (confirm('Are you sure you want to delete the computation state file? This cannot be undone.')) {
            log('Sending command to clear server state...');
            // If confirmed, send the 'clearState' message to the server.
            socket.send(JSON.stringify({ type: 'clearState' }));
        }
    });
}

%>