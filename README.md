<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Tracker</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

    <div class="app-container">

        <h1>📋 Task Tracker</h1>

        <!-- Add Task Form -->
        <form id="task-form">

            <input
                type="text"
                id="task-title"
                placeholder="Enter a new task..."
                autocomplete="off"
                maxlength="100"
                required
            >

            <button
                type="submit"
                id="add-btn"
            >
                Add
            </button>

        </form>

        <!-- Action Buttons -->
        <div class="action-bar">

            <button
                id="complete-all-btn"
                class="action-btn"
                type="button"
            >
                ✓ Mark All Completed
            </button>

            <button
                id="delete-all-btn"
                class="action-btn danger-btn"
                type="button"
            >
                🗑 Delete All
            </button>

        </div>

        <!-- Task Counter -->
        <div class="task-counter">

            <span id="total-count">
                Total : 0
            </span>

            <span id="pending-count">
                Pending : 0
            </span>

            <span id="completed-count">
                Completed : 0
            </span>

        </div>

        <!-- Filters -->
        <div class="filter-bar">

            <button
                class="filter-btn active"
                data-filter="all"
                type="button"
            >
                All
            </button>

            <button
                class="filter-btn"
                data-filter="pending"
                type="button"
            >
                Pending
            </button>

            <button
                class="filter-btn"
                data-filter="completed"
                type="button"
            >
                Completed
            </button>

        </div>

        <!-- Empty State -->
        <div
            id="empty-state"
            class="empty-state"
        >
            <h3>No tasks available</h3>

            <p>
                Add your first task to get started.
            </p>
        </div>

        <!-- Task List -->
        <div id="task-list"></div>

    </div>

    <!-- Toast Notification -->
    <div
        id="toast"
        class="toast"
    >
        Message
    </div>

    <script src="script.js"></script>

</body>
</html>





* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}

body {
    background: #ececec;
    color: #111;
    padding: 40px 20px;
    display: flex;
    justify-content: center;
}

.app-container {
    width: 100%;
    max-width: 600px;
    display: flex;
    flex-direction: column;
    gap: 18px;
}

h1 {
    text-align: center;
    color: #222;
}

form {
    display: flex;
    gap: 10px;
}

input[type="text"] {
    flex: 1;
    padding: 12px;
    border: 1px solid #d5d5d5;
    border-radius: 8px;
    font-size: 15px;
    outline: none;
}

input[type="text"]:focus {
    border-color: #0078ff;
}

button {
    cursor: pointer;
    transition: 0.25s;
}

#add-btn {
    background: #0078ff;
    color: white;
    border: none;
    border-radius: 8px;
    padding: 0 20px;
    font-weight: 600;
}

#add-btn:hover {
    background: #0060d4;
}

#add-btn:active {
    transform: scale(.95);
}

.action-bar {
    display: flex;
    gap: 10px;
}

.action-btn {
    flex: 1;
    border: none;
    padding: 10px;
    border-radius: 8px;
    background: #444;
    color: white;
    font-weight: 600;
}

.action-btn:hover {
    background: #2f2f2f;
}

.danger-btn {
    background: #d93025;
}

.danger-btn:hover {
    background: #b42318;
}

.task-counter {
    display: flex;
    justify-content: space-between;
    background: white;
    padding: 12px;
    border-radius: 8px;
    box-shadow: 0 2px 6px rgba(0,0,0,.08);
    font-size: 14px;
    font-weight: 600;
}

.filter-bar {
    display: flex;
    gap: 12px;
}

.filter-btn {
    background: white;
    color: #666;
    border: none;
    padding: 8px 18px;
    border-radius: 20px;
    box-shadow: 0 1px 5px rgba(0,0,0,.08);
}

.filter-btn.active {
    background: #0078ff;
    color: white;
}

#task-list {
    display: flex;
    flex-direction: column;
    gap: 14px;
}

.task-item {
    background: white;
    border-radius: 12px;
    padding: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 3px 10px rgba(0,0,0,.08);
    transition: .25s;
    cursor: grab;
}

.task-item:hover {
    transform: translateY(-2px);
}

.task-item.dragging {
    cursor: grabbing;
    opacity: .7;
}

.task-left {
    display: flex;
    align-items: center;
    gap: 12px;
}

.task-left span {
    font-size: 15px;
}

.task-item.completed .task-left {
    opacity: .45;
}

.task-item.completed span {
    text-decoration: none;
}

.task-item.completed input {
    opacity: .8;
}

.delete-btn {
    border: none;
    background: #ffebee;
    color: #d93025;
    padding: 8px 14px;
    border-radius: 6px;
    font-weight: 600;
    opacity: 1 !important;
}

.delete-btn:hover {
    background: #ffd6d6;
}

.drag-over {
    border: 2px dashed #0078ff;
}

.empty-state {
    display: none;
    text-align: center;
    background: white;
    border-radius: 10px;
    padding: 35px;
    color: #666;
    box-shadow: 0 2px 8px rgba(0,0,0,.08);
}

.toast {
    position: fixed;
    bottom: 30px;
    right: 30px;
    background: #333;
    color: white;
    padding: 14px 20px;
    border-radius: 8px;
    opacity: 0;
    transform: translateY(30px);
    transition: .35s;
    pointer-events: none;
    z-index: 1000;
}

.toast.show {
    opacity: 1;
    transform: translateY(0);
}

input[type="checkbox"] {
    width: 18px;
    height: 18px;
    cursor: pointer;
}

@media(max-width:600px){

    body{
        padding:20px 10px;
    }

    form{
        flex-direction:column;
    }

    #add-btn{
        width:100%;
        padding:12px;
    }

    .action-bar{
        flex-direction:column;
    }

    .task-counter{
        flex-direction:column;
        gap:8px;
        text-align:center;
    }

    .task-item{
        flex-direction:column;
        align-items:flex-start;
        gap:12px;
    }

    .delete-btn{
        align-self:flex-end;
    }

}






// ==============================
// Task Tracker - Part 1
// Variables, DOM Elements,
// Helper Functions & Toast
// ==============================

// Load tasks from Local Storage
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

// Current filter
let filter = "all";

// Drag & Drop Variables
let draggedTaskId = null;
let touchDraggedId = null;

// ==============================
// DOM Elements
// ==============================

const form = document.getElementById("task-form");

const input = document.getElementById("task-title");

const list = document.getElementById("task-list");

const toast = document.getElementById("toast");

const emptyState = document.getElementById("empty-state");

const totalCount = document.getElementById("total-count");

const pendingCount = document.getElementById("pending-count");

const completedCount = document.getElementById("completed-count");

const deleteAllBtn = document.getElementById("delete-all-btn");

const completeAllBtn = document.getElementById("complete-all-btn");

const filterButtons =
    document.querySelectorAll(".filter-btn");

// ==============================
// Toast Notification
// ==============================

function showToast(message) {

    toast.textContent = message;

    toast.classList.add("show");

    setTimeout(() => {

        toast.classList.remove("show");

    }, 2500);

}

// ==============================
// Save Tasks
// ==============================

function saveTasks() {

    localStorage.setItem(

        "tasks",

        JSON.stringify(tasks)

    );

}

// ==============================
// Task Counter
// ==============================

function updateCounter() {

    const total = tasks.length;

    const completed = tasks.filter(

        task => task.completed

    ).length;

    const pending = total - completed;

    totalCount.textContent =
        `Total : ${total}`;

    pendingCount.textContent =
        `Pending : ${pending}`;

    completedCount.textContent =
        `Completed : ${completed}`;

}

// ==============================
// Empty State
// ==============================

function updateEmptyState() {

    if (tasks.length === 0) {

        emptyState.style.display = "block";

        list.style.display = "none";

        deleteAllBtn.disabled = true;

        completeAllBtn.disabled = true;

    }

    else {

        emptyState.style.display = "none";

        list.style.display = "flex";

        deleteAllBtn.disabled = false;

        completeAllBtn.disabled = false;

    }

}

// ==============================
// Sync UI
// ==============================

function sync() {

    saveTasks();

    updateCounter();

    updateEmptyState();

    render();

}

// ==============================
// Validation
// ==============================

function taskExists(title) {

    return tasks.some(

        task =>

            task.title.toLowerCase()

            ===

            title.toLowerCase()

    );

}

// ==============================
// Continue with Part 2...
// ==============================
// ==============================
// Part 2
// Add Task
// Delete All
// Mark All Completed
// Filter Buttons
// ==============================

// ------------------------------
// Add Task
// ------------------------------

form.addEventListener("submit", (e) => {

    e.preventDefault();

    const title = input.value.trim();

    if (title === "") {

        showToast("⚠ Please enter a task.");

        return;
    }

    if (taskExists(title)) {

        showToast("⚠ Task already exists.");

        return;
    }

    tasks.push({

        id: Date.now().toString(),

        title,

        completed: false

    });

    input.value = "";

    showToast("✅ Task added successfully.");

    sync();

});

// ------------------------------
// Delete All Tasks
// ------------------------------

deleteAllBtn.addEventListener(

    "click",

    () => {

        if (tasks.length === 0) {

            showToast("No tasks available.");

            return;

        }

        const confirmDelete = confirm(

            "Are you sure you want to delete all tasks?"

        );

        if (!confirmDelete) return;

        tasks = [];

        showToast("🗑 All tasks deleted.");

        sync();

    }

);

// ------------------------------
// Mark All Completed
// ------------------------------

completeAllBtn.addEventListener(

    "click",

    () => {

        if (tasks.length === 0) {

            showToast("No tasks available.");

            return;

        }

        const pendingTasks = tasks.filter(

            task => !task.completed

        );

        if (pendingTasks.length === 0) {

            showToast(

                "All tasks are already completed."

            );

            return;

        }

        const confirmComplete = confirm(

            "Mark all pending tasks as completed?"

        );

        if (!confirmComplete) return;

        tasks.forEach(task => {

            task.completed = true;

        });

        showToast(

            "✅ All tasks marked as completed."

        );

        sync();

    }

);

// ------------------------------
// Filter Buttons
// ------------------------------

filterButtons.forEach(button => {

    button.addEventListener(

        "click",

        (e) => {

            filterButtons.forEach(btn =>

                btn.classList.remove(

                    "active"

                )

            );

            e.target.classList.add(

                "active"

            );

            filter =

                e.target.dataset.filter;

            render();

        }

    );

});

// ==============================
// Continue with Part 3
// ==============================
// ==============================
// Part 3
// Render Tasks
// Drag & Drop
// Touch Support
// ==============================

function render() {

    list.innerHTML = "";

    let filteredTasks = tasks.filter(task => {

        if (filter === "pending")
            return !task.completed;

        if (filter === "completed")
            return task.completed;

        return true;

    });

    filteredTasks.forEach(task => {

        const row = document.createElement("div");

        row.className = `task-item ${task.completed ? "completed" : ""}`;

        row.draggable = true;

        row.dataset.id = task.id;

        row.innerHTML = `

            <div class="task-left">

                <input
                    type="checkbox"
                    ${task.completed ? "checked" : ""}
                >

                <span>${task.title}</span>

            </div>

            <button class="delete-btn">

                Delete

            </button>

        `;

        // -------------------------
        // Checkbox
        // -------------------------

        const checkbox =
            row.querySelector("input");

        checkbox.addEventListener(

            "click",

            () => {

                if (task.completed) {

                    const confirmUndo = confirm(

                        "This task is already completed.\n\nDo you want to mark it as pending?"

                    );

                    if (!confirmUndo) {

                        checkbox.checked = true;

                        return;

                    }

                    task.completed = false;

                    showToast(

                        "Task marked as pending."

                    );

                }

                else {

                    task.completed = true;

                    showToast(

                        "Task completed."

                    );

                }

                sync();

            }

        );

        // -------------------------
        // Delete
        // -------------------------

        row.querySelector(".delete-btn")

            .addEventListener(

                "click",

                () => {

                    const confirmDelete = confirm(

                        "Delete this task?"

                    );

                    if (!confirmDelete)

                        return;

                    tasks = tasks.filter(

                        t => t.id !== task.id

                    );

                    showToast(

                        "Task deleted."

                    );

                    sync();

                }

            );

        // ==========================
        // DRAG START
        // ==========================

        row.addEventListener(

            "dragstart",

            () => {

                draggedTaskId = task.id;

                row.classList.add(

                    "dragging"

                );

            }

        );

        // ==========================
        // DRAG END
        // ==========================

        row.addEventListener(

            "dragend",

            () => {

                row.classList.remove(

                    "dragging"

                );

            }

        );

        // ==========================
        // DRAG OVER
        // ==========================

        row.addEventListener(

            "dragover",

            (e) => {

                e.preventDefault();

                row.classList.add(

                    "drag-over"

                );

            }

        );

        row.addEventListener(

            "dragleave",

            () => {

                row.classList.remove(

                    "drag-over"

                );

            }

        );

        // ==========================
        // DROP
        // ==========================

        row.addEventListener(

            "drop",

            (e) => {

                e.preventDefault();

                row.classList.remove(

                    "drag-over"

                );

                if (

                    draggedTaskId === task.id

                )

                    return;

                const sourceIndex =

                    tasks.findIndex(

                        t =>

                        t.id ===

                        draggedTaskId

                    );

                const targetIndex =

                    tasks.findIndex(

                        t =>

                        t.id ===

                        task.id

                    );

                const movedTask =

                    tasks.splice(

                        sourceIndex,

                        1

                    )[0];

                tasks.splice(

                    targetIndex,

                    0,

                    movedTask

                );

                showToast(

                    "Task reordered."

                );

                sync();

            }

        );

        // ==========================
        // TOUCH SUPPORT
        // ==========================

        row.addEventListener(

            "touchstart",

            () => {

                touchDraggedId =

                    task.id;

            }

        );

        row.addEventListener(

            "touchend",

            (e) => {

                const touch =

                    e.changedTouches[0];

                const target =

                    document.elementFromPoint(

                        touch.clientX,

                        touch.clientY

                    );

                const targetRow =

                    target?.closest(

                        ".task-item"

                    );

                if (

                    !targetRow ||

                    !touchDraggedId

                )

                    return;

                const sourceIndex =

                    tasks.findIndex(

                        t =>

                        t.id ===

                        touchDraggedId

                    );

                const targetIndex =

                    tasks.findIndex(

                        t =>

                        t.id ===

                        targetRow.dataset.id

                    );

                if (

                    sourceIndex ===

                    targetIndex

                )

                    return;

                const movedTask =

                    tasks.splice(

                        sourceIndex,

                        1

                    )[0];

                tasks.splice(

                    targetIndex,

                    0,

                    movedTask

                );

                touchDraggedId =

                    null;

                showToast(

                    "Task reordered."

                );

                sync();

            }

        );

        list.appendChild(row);

    });

}
// ==============================
// Part 4
// Application Initialization
// ==============================

// Update Action Buttons
function updateActionButtons() {

    deleteAllBtn.disabled = tasks.length === 0;

    const allCompleted =
        tasks.length > 0 &&
        tasks.every(task => task.completed);

    completeAllBtn.disabled =
        tasks.length === 0 || allCompleted;

}

// Override Sync
function sync() {

    saveTasks();

    updateCounter();

    updateEmptyState();

    updateActionButtons();

    render();

}

// Initialize Application
function initializeApp() {

    updateCounter();

    updateEmptyState();

    updateActionButtons();

    render();

}

// Keyboard Shortcut
input.addEventListener("keydown", (e) => {

    if (e.key === "Enter") {

        form.requestSubmit();

    }

});

// Window Load
window.addEventListener("load", () => {

    initializeApp();

});

// Initial Render
initializeApp();
