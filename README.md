<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >

    <title>Task Tracker</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

<div class="app-container">

    <header>
        <h1>📋 Task Tracker</h1>
        <p>Organize your daily tasks efficiently.</p>
    </header>

    <!-- Add Task -->
    <form id="task-form">

        <input
            id="task-title"
            type="text"
            placeholder="Enter a task..."
            maxlength="100"
            autocomplete="off"
        >

        <button
            id="add-btn"
            type="submit"
        >
            ➕ Add Task
        </button>

    </form>

    <!-- Action Buttons -->
    <div class="action-bar">

        <button
            id="complete-all-btn"
            class="action-btn success"
            type="button"
        >
            ✓ Mark All Completed
        </button>

        <button
            id="delete-all-btn"
            class="action-btn danger"
            type="button"
        >
            🗑 Delete All
        </button>

    </div>

    <!-- Counter -->
    <section class="task-counter">

        <div class="counter-box">
            <span>Total</span>
            <strong id="total-count">0</strong>
        </div>

        <div class="counter-box">
            <span>Pending</span>
            <strong id="pending-count">0</strong>
        </div>

        <div class="counter-box">
            <span>Completed</span>
            <strong id="completed-count">0</strong>
        </div>

    </section>

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

        <div class="empty-icon">
            📭
        </div>

        <h3>No Tasks Available</h3>

        <p>
            Add your first task to get started.
        </p>

    </div>

    <!-- Task List -->
    <div id="task-list"></div>

</div>

<!-- Toast -->
<div
    id="toast"
    class="toast"
></div>

<script src="script.js"></script>

</body>
</html>



/* ===========================
   Global
=========================== */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
}

body{
    background:#eef2f7;
    color:#222;
    display:flex;
    justify-content:center;
    padding:40px 18px;
}

.app-container{
    width:100%;
    max-width:700px;
    display:flex;
    flex-direction:column;
    gap:20px;
}

/* ===========================
   Header
=========================== */

header{
    text-align:center;
}

header h1{
    font-size:34px;
    margin-bottom:8px;
}

header p{
    color:#666;
    font-size:15px;
}

/* ===========================
   Form
=========================== */

form{
    display:flex;
    gap:12px;
}

#task-title{
    flex:1;
    padding:14px;
    border:1px solid #d8d8d8;
    border-radius:10px;
    outline:none;
    font-size:15px;
    transition:.25s;
    background:white;
}

#task-title:focus{
    border-color:#1976d2;
    box-shadow:0 0 0 4px rgba(25,118,210,.12);
}

#add-btn{
    border:none;
    cursor:pointer;
    color:white;
    font-weight:600;
    border-radius:10px;
    padding:0 24px;
    background:#1976d2;
    transition:.25s;
}

#add-btn:hover{
    background:#1565c0;
    transform:translateY(-2px);
    box-shadow:0 10px 20px rgba(25,118,210,.22);
}

#add-btn:active{
    transform:scale(.95);
}

/* ===========================
   Action Buttons
=========================== */

.action-bar{
    display:flex;
    gap:12px;
}

.action-btn{
    flex:1;
    border:none;
    border-radius:10px;
    padding:13px;
    cursor:pointer;
    color:white;
    font-weight:600;
    transition:.25s;
}

.action-btn:hover{
    transform:translateY(-2px);
}

.action-btn:active{
    transform:scale(.97);
}

.success{
    background:#2e7d32;
}

.success:hover{
    background:#256428;
}

.danger{
    background:#d32f2f;
}

.danger:hover{
    background:#b71c1c;
}

/* ===========================
   Counter
=========================== */

.task-counter{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:14px;
}

.counter-box{
    background:white;
    padding:18px;
    text-align:center;
    border-radius:14px;
    box-shadow:0 8px 20px rgba(0,0,0,.07);
}

.counter-box span{
    display:block;
    color:#666;
    margin-bottom:6px;
    font-size:13px;
}

.counter-box strong{
    font-size:28px;
}

/* ===========================
   Filters
=========================== */

.filter-bar{
    display:flex;
    gap:10px;
}

.filter-btn{
    flex:1;
    border:none;
    background:white;
    padding:12px;
    cursor:pointer;
    border-radius:30px;
    transition:.25s;
    font-weight:600;
}

.filter-btn:hover{
    background:#dceeff;
}

.filter-btn.active{
    background:#1976d2;
    color:white;
}

/* ===========================
   Task List
=========================== */

#task-list{
    display:flex;
    flex-direction:column;
    gap:16px;
}

/* ===========================
   Task Card
=========================== */

.task-item{
    display:flex;
    justify-content:space-between;
    align-items:center;
    gap:18px;

    background:white;

    padding:18px;

    border-radius:14px;

    box-shadow:0 8px 18px rgba(0,0,0,.08);

    transition:
        transform .25s,
        box-shadow .25s,
        opacity .25s;

    cursor:grab;

    position:relative;

    user-select:none;
}

.task-item:hover{
    transform:translateY(-3px);
    box-shadow:0 12px 24px rgba(0,0,0,.12);
}

.task-item:active{
    cursor:grabbing;
}

.task-item.dragging{
    cursor:grabbing;
    opacity:.9;
    transform:scale(1.03);
    z-index:100;
}

/* ===========================
   Left Section
=========================== */

.task-left{
    display:flex;
    align-items:center;
    gap:14px;
    flex:1;
}

.task-left span{
    font-size:15px;
    line-height:1.5;
    word-break:break-word;
}

/* ===========================
   Completed Task
=========================== */

.task-item.completed .task-left{
    opacity:.45;
}

.task-item.completed .task-left span{
    text-decoration:none;
}

/* ===========================
   Checkbox
=========================== */

input[type="checkbox"]{
    width:18px;
    height:18px;
    cursor:pointer;
    flex-shrink:0;
}

/* ===========================
   Delete Button
=========================== */

.delete-btn{

    border:none;

    background:#ffebee;

    color:#d32f2f;

    padding:10px 16px;

    border-radius:8px;

    cursor:pointer;

    font-weight:600;

    transition:.25s;

    opacity:1 !important;

    flex-shrink:0;
}

.delete-btn:hover{
    background:#ffd6d6;
}
/* ===========================
   Drag & Drop
=========================== */

.drag-over{
    outline:2px dashed #1976d2;
    outline-offset:4px;
}

/* ===========================
   Empty State
=========================== */

.empty-state{
    display:none;
    background:#fff;
    padding:45px 25px;
    border-radius:14px;
    text-align:center;
    box-shadow:0 8px 20px rgba(0,0,0,.08);
}

.empty-state.show{
    display:block;
}

.empty-icon{
    font-size:60px;
    margin-bottom:14px;
}

.empty-state h3{
    margin-bottom:8px;
    font-size:22px;
}

.empty-state p{
    color:#666;
    font-size:15px;
}

/* ===========================
   Toast
=========================== */

.toast{
    position:fixed;
    bottom:25px;
    right:25px;

    min-width:240px;
    max-width:320px;

    padding:14px 18px;

    border-radius:10px;

    background:#333;
    color:#fff;

    box-shadow:0 10px 24px rgba(0,0,0,.25);

    opacity:0;
    transform:translateY(30px);

    transition:
        opacity .35s ease,
        transform .35s ease;

    pointer-events:none;

    z-index:9999;
}

.toast.show{
    opacity:1;
    transform:translateY(0);
}

.toast.success{
    background:#2e7d32;
}

.toast.error{
    background:#d32f2f;
}

.toast.info{
    background:#1976d2;
}

/* ===========================
   Buttons
=========================== */

button:disabled{
    opacity:.55;
    cursor:not-allowed;
    transform:none !important;
}

/* ===========================
   Animation
=========================== */

@keyframes fadeIn{

    from{
        opacity:0;
        transform:translateY(10px);
    }

    to{
        opacity:1;
        transform:translateY(0);
    }

}

.task-item{
    animation:fadeIn .25s ease;
}

/* ===========================
   Scrollbar
=========================== */

::-webkit-scrollbar{
    width:8px;
}

::-webkit-scrollbar-track{
    background:#f2f2f2;
}

::-webkit-scrollbar-thumb{
    background:#c7c7c7;
    border-radius:20px;
}

::-webkit-scrollbar-thumb:hover{
    background:#a9a9a9;
}

/* ===========================
   Mobile
=========================== */

@media (max-width:650px){

    body{
        padding:20px 14px;
    }

    form{
        flex-direction:column;
    }

    #add-btn{
        width:100%;
        padding:14px;
    }

    .action-bar{
        flex-direction:column;
    }

    .task-counter{
        grid-template-columns:1fr;
    }

    .filter-bar{
        flex-wrap:wrap;
    }

    .filter-btn{
        min-width:95px;
    }

    .task-item{
        flex-direction:column;
        align-items:flex-start;
    }

    .task-left{
        width:100%;
    }

    .delete-btn{
        align-self:flex-end;
    }

    .toast{
        left:15px;
        right:15px;
        bottom:18px;
        max-width:none;
        min-width:auto;
    }

}

/* ===========================
   Small Phones
=========================== */

@media (max-width:400px){

    header h1{
        font-size:28px;
    }

    .counter-box strong{
        font-size:24px;
    }

    .task-left span{
        font-size:14px;
    }

    .filter-btn{
        font-size:13px;
        padding:10px;
    }

}




// ==============================
// Task Tracker
// ==============================

const taskForm = document.getElementById("task-form");
const taskInput = document.getElementById("task-title");
const taskList = document.getElementById("task-list");

const emptyState = document.getElementById("empty-state");
const toast = document.getElementById("toast");

const totalCount = document.getElementById("total-count");
const pendingCount = document.getElementById("pending-count");
const completedCount = document.getElementById("completed-count");

const deleteAllBtn = document.getElementById("delete-all-btn");
const completeAllBtn = document.getElementById("complete-all-btn");

const filterButtons = document.querySelectorAll(".filter-btn");

let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
let currentFilter = "all";

let draggedIndex = null;
let dragElement = null;
let startY = 0;
let offsetY = 0;

// ==============================
// Local Storage
// ==============================

function saveTasks() {
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

// ==============================
// Toast
// ==============================

function showToast(message, type = "success") {

    toast.textContent = message;

    toast.className = "toast";

    toast.classList.add(type);

    toast.classList.add("show");

    setTimeout(() => {
        toast.classList.remove("show");
    }, 2200);
}

// ==============================
// Counter
// ==============================

function updateCounter() {

    totalCount.textContent = tasks.length;

    pendingCount.textContent =
        tasks.filter(task => !task.completed).length;

    completedCount.textContent =
        tasks.filter(task => task.completed).length;

}

// ==============================
// Empty State
// ==============================

function updateEmptyState() {

    if (tasks.length === 0) {
        emptyState.classList.add("show");
    } else {
        emptyState.classList.remove("show");
    }

}

// ==============================
// Render
// ==============================

function renderTasks() {

    taskList.innerHTML = "";

    let filtered = tasks;

    if (currentFilter === "pending") {
        filtered = tasks.filter(task => !task.completed);
    }

    if (currentFilter === "completed") {
        filtered = tasks.filter(task => task.completed);
    }

    filtered.forEach(task => {

        const originalIndex = tasks.indexOf(task);

        const card = document.createElement("div");

        card.className =
            "task-item" +
            (task.completed ? " completed" : "");

        card.dataset.index = originalIndex;

        card.innerHTML = `
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

        // Checkbox

        const checkbox =
            card.querySelector("input");

        checkbox.addEventListener("change", () => {

            if (
                task.completed &&
                !confirm(
                    "Move this completed task back to Pending?"
                )
            ) {

                checkbox.checked = true;
                return;
            }

            task.completed = checkbox.checked;

            saveTasks();

            renderTasks();

            showToast(
                task.completed
                    ? "Task Completed"
                    : "Task Moved To Pending",
                "info"
            );

        });

        // Delete

        card
            .querySelector(".delete-btn")
            .addEventListener("click", () => {

                tasks.splice(originalIndex, 1);

                saveTasks();

                renderTasks();

                showToast(
                    "Task Deleted",
                    "error"
                );

            });

        taskList.appendChild(card);

    });

    updateCounter();

    updateEmptyState();

    attachDragEvents();

}

// ==============================
// Add Task
// ==============================

taskForm.addEventListener("submit", e => {

    e.preventDefault();

    const title =
        taskInput.value.trim();

    if (!title) {

        showToast(
            "Task cannot be empty",
            "error"
        );

        return;
    }

    const duplicate =
        tasks.some(task =>
            task.title.toLowerCase() ===
            title.toLowerCase()
        );

    if (duplicate) {

        showToast(
            "Task already exists",
            "error"
        );

        return;
    }

    tasks.push({

        title,

        completed: false

    });

    saveTasks();

    renderTasks();

    taskInput.value = "";

    taskInput.focus();

    showToast(
        "Task Added Successfully"
    );

});

// ==============================
// Filters
// ==============================

filterButtons.forEach(button => {

    button.addEventListener("click", () => {

        filterButtons.forEach(btn =>
            btn.classList.remove("active")
        );

        button.classList.add("active");

        currentFilter =
            button.dataset.filter;

        renderTasks();

    });

});
// ==============================
// Custom Drag & Drop
// (No HTML5 Drag API)
// ==============================

function attachDragEvents() {

    const cards = document.querySelectorAll(".task-item");

    cards.forEach(card => {

        card.addEventListener("mousedown", startDrag);

    });

}

function startDrag(event) {

    // Ignore checkbox and delete button
    if (
        event.target.tagName === "INPUT" ||
        event.target.classList.contains("delete-btn")
    ) {
        return;
    }

    dragElement = event.currentTarget;

    draggedIndex = Number(dragElement.dataset.index);

    startY = event.clientY;

    const rect = dragElement.getBoundingClientRect();

    offsetY = event.clientY - rect.top;

    dragElement.classList.add("dragging");

    dragElement.style.width = rect.width + "px";
    dragElement.style.position = "fixed";
    dragElement.style.left = rect.left + "px";
    dragElement.style.top = rect.top + "px";
    dragElement.style.pointerEvents = "none";
    dragElement.style.zIndex = "9999";

    document.addEventListener("mousemove", dragMove);
    document.addEventListener("mouseup", stopDrag);

}

function dragMove(event) {

    if (!dragElement) return;

    dragElement.style.top =
        event.clientY - offsetY + "px";

    const cards =
        [...document.querySelectorAll(".task-item")];

    cards.forEach(card =>
        card.classList.remove("drag-over")
    );

    for (const card of cards) {

        if (card === dragElement) continue;

        const rect =
            card.getBoundingClientRect();

        if (
            event.clientY >
                rect.top &&
            event.clientY <
                rect.bottom
        ) {

            card.classList.add("drag-over");

            break;

        }

    }

}

function stopDrag(event) {

    if (!dragElement) return;

    const cards =
        [...document.querySelectorAll(".task-item")];

    let targetIndex = draggedIndex;

    cards.forEach(card => {

        const rect =
            card.getBoundingClientRect();

        if (
            event.clientY >
                rect.top &&
            event.clientY <
                rect.bottom
        ) {

            targetIndex =
                Number(card.dataset.index);

        }

        card.classList.remove("drag-over");

    });

    dragElement.classList.remove("dragging");

    dragElement.style.position = "";
    dragElement.style.left = "";
    dragElement.style.top = "";
    dragElement.style.width = "";
    dragElement.style.pointerEvents = "";
    dragElement.style.zIndex = "";

    if (
        targetIndex !== draggedIndex &&
        targetIndex >= 0
    ) {

        const movedTask =
            tasks.splice(draggedIndex, 1)[0];

        tasks.splice(
            targetIndex,
            0,
            movedTask
        );

        saveTasks();

        showToast(
            "Task Order Updated",
            "info"
        );

    }

    dragElement = null;
    draggedIndex = null;

    document.removeEventListener(
        "mousemove",
        dragMove
    );

    document.removeEventListener(
        "mouseup",
        stopDrag
    );

    renderTasks();

}
// ==============================
// Delete All
// ==============================

deleteAllBtn.addEventListener("click", () => {

    if (tasks.length === 0) {

        showToast(
            "No tasks to delete",
            "error"
        );

        return;

    }

    if (!confirm("Delete all tasks?")) {
        return;
    }

    tasks = [];

    saveTasks();

    renderTasks();

    showToast(
        "All Tasks Deleted",
        "error"
    );

});

// ==============================
// Mark All Completed
// ==============================

completeAllBtn.addEventListener("click", () => {

    if (tasks.length === 0) {

        showToast(
            "No tasks available",
            "error"
        );

        return;

    }

    const pending =
        tasks.some(task => !task.completed);

    if (!pending) {

        showToast(
            "All tasks are already completed",
            "info"
        );

        return;

    }

    if (!confirm("Mark all pending tasks as completed?")) {
        return;
    }

    tasks.forEach(task => {
        task.completed = true;
    });

    saveTasks();

    renderTasks();

    showToast(
        "All Tasks Completed",
        "success"
    );

});

// ==============================
// Keyboard Shortcut
// ==============================

taskInput.addEventListener("keydown", event => {

    if (
        event.key === "Enter" &&
        taskInput.value.trim() === ""
    ) {

        event.preventDefault();

        showToast(
            "Task cannot be empty",
            "error"
        );

    }

});

// ==============================
// Initialize
// ==============================

renderTasks();
