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

        <h1>Task Tracker</h1>

        <form id="task-form">
            <input
                type="text"
                id="task-title"
                placeholder="New task..."
                required
            >
            <button type="submit">Add</button>
        </form>

        <div class="filter-bar">
            <button
                class="filter-btn active"
                data-filter="all"
            >
                All
            </button>

            <button
                class="filter-btn"
                data-filter="pending"
            >
                Pending
            </button>

            <button
                class="filter-btn"
                data-filter="completed"
            >
                Completed
            </button>
        </div>

        <div id="task-list"></div>

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
    color: #111111;
    padding: 40px 20px;
    display: flex;
    justify-content: center;
}

.app-container {
    width: 100%;
    max-width: 500px;
    display: flex;
    flex-direction: column;
    gap: 20px;
}

h1 {
    text-align: center;
}

form {
    display: flex;
    gap: 8px;
}

input[type="text"] {
    flex: 1;
    padding: 10px;
    border: 1px solid #e5e5e5;
    border-radius: 4px;
    outline: none;
}

button {
    padding: 8px 16px;
    background: #000000;
    color: #ffffff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.filter-bar {
    display: flex;
    gap: 12px;
}

.filter-btn {
    background: none;
    border: none;
    color: #666666;
    font-size: 14px;
    cursor: pointer;
}

.filter-btn.active {
    color: #000000;
    font-weight: bold;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    border-bottom: 1px solid #e5e5e5;
    cursor: grab;
    user-select: none;
    transition: all 0.2s ease;
}

.task-item:hover {
    background-color: #f8f8f8;
}

.task-item.dragging {
    opacity: 0.5;
    background-color: #dddddd;
}

.task-item.drag-over {
    border-top: 3px solid #000;
}

.task-item.completed {
    opacity: 0.5;
}

.task-item.completed span {
    text-decoration: line-through;
}

.delete-btn {
    background: none;
    border: none;
    color: #df2020;
    cursor: pointer;
    font-weight: bold;
}

.task-left {
    display: flex;
    align-items: center;
    gap: 10px;
}



let tasks = JSON.parse(
    localStorage.getItem("tasks")
) || [];

let filter = "all";

let draggedTaskId = null;
let touchDraggedId = null;

const form =
    document.getElementById("task-form");

const input =
    document.getElementById("task-title");

const list =
    document.getElementById("task-list");

form.addEventListener("submit", (e) => {

    e.preventDefault();

    if (!input.value.trim()) return;

    tasks.push({
        id: Date.now().toString(),
        title: input.value.trim(),
        completed: false
    });

    input.value = "";

    sync();
});

function sync() {

    localStorage.setItem(
        "tasks",
        JSON.stringify(tasks)
    );

    render();
}

function render() {

    list.innerHTML = "";

    const filteredTasks = tasks.filter(task => {

        if (filter === "pending") {
            return !task.completed;
        }

        if (filter === "completed") {
            return task.completed;
        }

        return true;
    });

    filteredTasks.forEach(task => {

        const row =
            document.createElement("div");

        row.className =
            `task-item ${task.completed ? "completed" : ""}`;

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

        const checkbox =
            row.querySelector("input");

        checkbox.onclick = () => {

            task.completed =
                !task.completed;

            sync();
        };

        const deleteBtn =
            row.querySelector(".delete-btn");

        deleteBtn.onclick = () => {

            tasks = tasks.filter(
                t => t.id !== task.id
            );

            sync();
        };

        row.addEventListener(
            "dragstart",
            () => {

                draggedTaskId =
                    task.id;

                row.classList.add(
                    "dragging"
                );
            }
        );

        row.addEventListener(
            "dragend",
            () => {

                row.classList.remove(
                    "dragging"
                );
            }
        );

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

        row.addEventListener(
            "drop",
            (e) => {

                e.preventDefault();

                row.classList.remove(
                    "drag-over"
                );

                if (
                    draggedTaskId === null ||
                    draggedTaskId === task.id
                ) {
                    return;
                }

                const draggedIndex =
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
                        draggedIndex,
                        1
                    )[0];

                tasks.splice(
                    targetIndex,
                    0,
                    movedTask
                );

                sync();
            }
        );

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
                ) {
                    return;
                }

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
                ) {
                    return;
                }

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

                sync();

                touchDraggedId =
                    null;
            }
        );

        list.appendChild(row);
    });
}

document
    .querySelectorAll(".filter-btn")
    .forEach(btn => {

        btn.onclick = (e) => {

            document
                .querySelectorAll(
                    ".filter-btn"
                )
                .forEach(button => {

                    button.classList.remove(
                        "active"
                    );
                });

            e.target.classList.add(
                "active"
            );

            filter =
                e.target.dataset.filter;

            render();
        };
    });

render();
