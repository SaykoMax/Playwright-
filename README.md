BUG-029: Website redirects to Home page after browser refresh

Overview

Refreshing the browser on any page redirects the user to the Home page instead of retaining the current page.

Module

Navigation

Preconditions

ShopEasy application is open.

User has navigated to any page other than the Home page (e.g., Products, Cart, Wishlist, About).


Steps to Reproduce

1. Open the ShopEasy application.


2. Navigate to the Products, Cart, or Wishlist page.


3. Press F5 or click the browser's Refresh button.



Expected Result

The application should remain on the current page after refreshing.

Actual Result

The application always redirects the user to the Home page after refresh.


---

BUG-030: Wishlist items do not provide an "Add to Cart" option

Overview

Products added to the Wishlist cannot be directly added to the Cart because the Wishlist page does not provide an Add to Cart button.

Module

Wishlist

Preconditions

User has added at least one product to the Wishlist.


Steps to Reproduce

1. Open the ShopEasy application.


2. Add a product to the Wishlist.


3. Navigate to the Wishlist page.


4. Observe the available actions for the product.



Expected Result

Each wishlist item should have an Add to Cart option so users can easily move products to the shopping cart.

Actual Result

No Add to Cart option is available for wishlist items.


---

BUG-031: Product offers or discounts are not displayed

Overview

The application does not display any offers, discounts, or promotional information on product listings.

Module

Products

Preconditions

ShopEasy application is open.

User is on the Products page.


Steps to Reproduce

1. Open the ShopEasy application.


2. Navigate to the Products page.


3. Browse through the available products.



Expected Result

Products with applicable offers or discounts should display promotional information such as discount percentage, sale price, or offer badge.

Actual Result

No offers or discount information are displayed for any products.


---

BUG-032: Product filtering options are not functional

Overview

The application does not allow users to filter products based on Fashion Category, Size, Gender, Brand, or Color.

Module

Products / Filters

Preconditions

ShopEasy application is open.

User is on the Products page.


Steps to Reproduce

1. Open the ShopEasy application.


2. Navigate to the Products page.


3. Attempt to filter products by Fashion Category, Size, Gender, Brand, or Color.



Expected Result

Products should be filtered based on the selected criteria.

Actual Result

No filtering options are available, or selecting filter criteria does not affect the displayed products.ght:15px;
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
