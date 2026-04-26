<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List with Calendar</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 50%, #558b2f 100%);
            background-attachment: fixed;
            min-height: 100vh;
            padding: 20px;
            position: relative;
            font-weight: 300;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                radial-gradient(circle at 20% 50%, rgba(46, 125, 50, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(85, 139, 47, 0.3) 0%, transparent 50%),
                linear-gradient(180deg, rgba(27, 94, 32, 0.4) 0%, rgba(46, 125, 50, 0.3) 50%, rgba(85, 139, 47, 0.4) 100%);
            pointer-events: none;
            z-index: -1;
        }

        body::after {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(76, 175, 80, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 10%, rgba(139, 195, 74, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 50% 100%, rgba(27, 94, 32, 0.2) 0%, transparent 30%);
            pointer-events: none;
            z-index: -1;
        }

        .main-container {
            max-width: 1400px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 20px;
            position: relative;
            z-index: 1;
        }

        .container {
            background: rgba(255, 255, 255, 0.96);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(102, 187, 106, 0.2);
        }

        h1 {
            color: #1b5e20;
            margin-bottom: 20px;
            text-align: center;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.05);
            font-size: 2.2em;
            font-weight: 300;
            letter-spacing: 0.5px;
        }

        h2 {
            color: #2e7d32;
            font-size: 1.4em;
            margin-bottom: 15px;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.05);
            font-weight: 300;
            letter-spacing: 0.3px;
        }

        /* Task Input Section */
        .input-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 20px;
        }

        #taskInput {
            padding: 12px 15px;
            border: 2px solid #a5d6a7;
            border-radius: 8px;
            font-size: 15px;
            background: #f1f8e9;
            color: #1b5e20;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
            font-weight: 300;
        }

        #taskInput::placeholder {
            color: #a5d6a7;
            font-weight: 300;
        }

        #taskInput:focus {
            outline: none;
            border-color: #2e7d32;
            box-shadow: 0 0 12px rgba(46, 125, 50, 0.4);
            background: #e8f5e9;
        }

        #dueDate {
            padding: 12px 15px;
            border: 2px solid #a5d6a7;
            border-radius: 8px;
            font-size: 15px;
            background: #f1f8e9;
            color: #1b5e20;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
            font-weight: 300;
        }

        #dueDate:focus {
            outline: none;
            border-color: #2e7d32;
            box-shadow: 0 0 12px rgba(46, 125, 50, 0.4);
            background: #e8f5e9;
        }

        /* Reminder Input Section */
        #reminderInput {
            padding: 12px 15px;
            border: 2px solid #ffc107;
            border-radius: 8px;
            font-size: 15px;
            background: #fffef0;
            color: #1b5e20;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
            font-weight: 300;
        }

        #reminderInput::placeholder {
            color: #ffc107;
            font-weight: 300;
        }

        #reminderInput:focus {
            outline: none;
            border-color: #ff9800;
            box-shadow: 0 0 12px rgba(255, 193, 7, 0.4);
            background: #fff9e6;
        }

        #reminderDate {
            padding: 12px 15px;
            border: 2px solid #ffc107;
            border-radius: 8px;
            font-size: 15px;
            background: #fffef0;
            color: #1b5e20;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
            font-weight: 300;
        }

        #reminderDate:focus {
            outline: none;
            border-color: #ff9800;
            box-shadow: 0 0 12px rgba(255, 193, 7, 0.4);
            background: #fff9e6;
        }

        #reminderType {
            padding: 12px 15px;
            border: 2px solid #ffc107;
            border-radius: 8px;
            font-size: 15px;
            background: #fffef0;
            color: #1b5e20;
            transition: all 0.3s;
            font-family: 'Poppins', sans-serif;
            font-weight: 300;
        }

        #reminderType:focus {
            outline: none;
            border-color: #ff9800;
            box-shadow: 0 0 12px rgba(255, 193, 7, 0.4);
        }

        .button-group {
            display: flex;
            gap: 10px;
        }

        #addBtn {
            flex: 1;
            padding: 12px 20px;
            background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 400;
            font-size: 15px;
            transition: all 0.3s;
            box-shadow: 0 6px 16px rgba(27, 94, 32, 0.4);
            font-family: 'Poppins', sans-serif;
            letter-spacing: 0.5px;
        }

        #addBtn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(27, 94, 32, 0.6);
            background: linear-gradient(135deg, #1b5e20 0%, #0d3818 100%);
        }

        #addBtn:active {
            transform: translateY(0);
        }

        #addReminderBtn {
            flex: 1;
            padding: 12px 20px;
            background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 400;
            font-size: 15px;
            transition: all 0.3s;
            box-shadow: 0 6px 16px rgba(255, 152, 0, 0.4);
            font-family: 'Poppins', sans-serif;
            letter-spacing: 0.5px;
        }

        #addReminderBtn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(255, 152, 0, 0.6);
            background: linear-gradient(135deg, #f57c00 0%, #e65100 100%);
        }

        #addReminderBtn:active {
            transform: translateY(0);
        }

        /* Task List */
        ul {
            list-style: none;
            max-height: 500px;
            overflow-y: auto;
            padding-right: 8px;
        }

        ul::-webkit-scrollbar {
            width: 8px;
        }

        ul::-webkit-scrollbar-track {
            background: #f1f8e9;
            border-radius: 10px;
        }

        ul::-webkit-scrollbar-thumb {
            background: #2e7d32;
            border-radius: 10px;
        }

        ul::-webkit-scrollbar-thumb:hover {
            background: #1b5e20;
        }

        #reminderList::-webkit-scrollbar {
            width: 8px;
        }

        #reminderList::-webkit-scrollbar-track {
            background: #fff9e6;
            border-radius: 10px;
        }

        #reminderList::-webkit-scrollbar-thumb {
            background: #ff9800;
            border-radius: 10px;
        }

        #reminderList::-webkit-scrollbar-thumb:hover {
            background: #f57c00;
        }

        li {
            background: linear-gradient(135deg, #f1f8e9 0%, #e8f5e9 100%);
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            display: flex;
            gap: 10px;
            align-items: center;
            border-left: 4px solid #2e7d32;
            transition: all 0.3s;
            box-shadow: 0 3px 10px rgba(27, 94, 32, 0.15);
        }

        li:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 16px rgba(27, 94, 32, 0.25);
            background: linear-gradient(135deg, #e8f5e9 0%, #dcedc1 100%);
        }

        li.completed {
            opacity: 0.6;
            border-left-color: #558b2f;
            background: linear-gradient(135deg, #dcedc1 0%, #c5e1a5 100%);
        }

        li.completed span {
            text-decoration: line-through;
            color: #999;
        }

        .reminder-item {
            background: linear-gradient(135deg, #fff9e6 0%, #fffef0 100%);
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            display: flex;
            gap: 10px;
            align-items: center;
            border-left: 4px solid #ff9800;
            transition: all 0.3s;
            box-shadow: 0 3px 10px rgba(255, 152, 0, 0.15);
        }

        .reminder-item:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 16px rgba(255, 152, 0, 0.25);
            background: linear-gradient(135deg, #fffef0 0%, #fff3e0 100%);
        }

        .task-content {
            flex: 1;
        }

        .reminder-content {
            flex: 1;
        }

        .task-text {
            font-weight: 400;
            display: block;
            margin-bottom: 3px;
            color: #1b5e20;
            font-size: 15px;
            letter-spacing: 0.3px;
        }

        .reminder-text {
            font-weight: 400;
            display: block;
            margin-bottom: 3px;
            color: #e65100;
            font-size: 15px;
            letter-spacing: 0.3px;
        }

        .reminder-type-badge {
            display: inline-block;
            background: #ff9800;
            color: white;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 500;
            margin-top: 3px;
        }

        .task-date {
            font-size: 12px;
            color: #999;
            font-weight: 300;
        }

        .reminder-date {
            font-size: 12px;
            color: #f57c00;
            font-weight: 300;
        }

        input[type="checkbox"] {
            width: 18px;
            height: 18px;
            cursor: pointer;
            accent-color: #2e7d32;
        }

        .delete-btn {
            background: linear-gradient(135deg, #d32f2f 0%, #c62828 100%);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.2s;
            font-family: 'Poppins', sans-serif;
            font-weight: 400;
        }

        .delete-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(198, 40, 40, 0.4);
        }

        #emptyMsg {
            text-align: center;
            color: #999;
            padding: 40px 20px;
            font-style: italic;
            font-size: 1em;
            font-weight: 300;
            letter-spacing: 0.3px;
        }

        #emptyReminder {
            text-align: center;
            color: #999;
            padding: 40px 20px;
            font-style: italic;
            font-size: 1em;
            font-weight: 300;
            letter-spacing: 0.3px;
        }

        /* Calendar Styles */
        .calendar-container {
            text-align: center;
        }

        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            gap: 10px;
        }

        .calendar-header button {
            background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 400;
            transition: all 0.3s;
            box-shadow: 0 4px 12px rgba(27, 94, 32, 0.4);
            font-family: 'Poppins', sans-serif;
            font-size: 14px;
            letter-spacing: 0.3px;
        }

        .calendar-header button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(27, 94, 32, 0.6);
        }

        .calendar-month {
            font-size: 1.3em;
            font-weight: 300;
            color: #1b5e20;
            flex: 1;
            letter-spacing: 0.5px;
        }

        .calendar {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(27, 94, 32, 0.2);
        }

        .calendar th {
            background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
            color: white;
            padding: 12px;
            font-weight: 400;
            font-size: 13px;
            letter-spacing: 0.5px;
        }

        .calendar td {
            border: 1px solid #c8e6c9;
            padding: 10px;
            height: 80px;
            vertical-align: top;
            position: relative;
            cursor: pointer;
            transition: all 0.2s;
            background: white;
            font-weight: 300;
        }

        .calendar td:hover {
            background: #f1f8e9;
            box-shadow: inset 0 0 8px rgba(46, 125, 50, 0.2);
        }

        .calendar td.other-month {
            background: #fafafa;
            color: #ccc;
        }

        .calendar td.today {
            background: linear-gradient(135deg, #a5d6a7 0%, #81c784 100%);
            font-weight: 400;
            box-shadow: inset 0 0 12px rgba(27, 94, 32, 0.3);
            color: white;
        }

        .calendar td.today .day-number {
            color: white;
        }

        .calendar td.has-tasks {
            background: linear-gradient(135deg, #e8f5e9 0%, #f1f8e9 100%);
        }

        .calendar td.has-reminder {
            background: linear-gradient(135deg, #fff9e6 0%, #fffef0 100%);
            border: 2px solid #ff9800;
        }

        .day-number {
            font-weight: 400;
            margin-bottom: 3px;
            color: #1b5e20;
            font-size: 14px;
        }

        .day-tasks {
            font-size: 10px;
            color: #2e7d32;
            max-height: 60px;
            overflow: hidden;
            font-weight: 300;
        }

        .day-task-item {
            background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%);
            color: white;
            padding: 2px 6px;
            border-radius: 3px;
            margin: 2px 0;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            font-size: 10px;
            box-shadow: 0 2px 4px rgba(27, 94, 32, 0.3);
            font-weight: 300;
        }

        .day-task-item.completed {
            background: #558b2f;
            text-decoration: line-through;
            opacity: 0.8;
        }

        .day-reminder-item {
            background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);
            color: white;
            padding: 2px 6px;
            border-radius: 3px;
            margin: 2px 0;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            font-size: 10px;
            box-shadow: 0 2px 4px rgba(255, 152, 0, 0.3);
            font-weight: 300;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background-color: rgba(255, 255, 255, 0.99);
            margin: 10% auto;
            padding: 30px;
            border-radius: 15px;
            width: 80%;
            max-width: 400px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
            border-top: 5px solid #2e7d32;
            animation: slideDown 0.3s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .modal-close {
            color: #2e7d32;
            float: right;
            font-size: 28px;
            font-weight: 300;
            cursor: pointer;
            transition: color 0.2s;
        }

        .modal-close:hover {
            color: #1b5e20;
        }

        .modal-tasks {
            margin-top: 20px;
            text-align: left;
        }

        .modal-task-item {
            background: #f1f8e9;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            display: flex;
            gap: 10px;
            align-items: center;
            border-left: 3px solid #2e7d32;
            transition: all 0.2s;
            font-weight: 300;
        }

        .modal-task-item:hover {
            background: #e8f5e9;
            transform: translateX(5px);
        }

        .modal-task-item.completed {
            opacity: 0.6;
            border-left-color: #558b2f;
        }

        .modal-task-item.completed span {
            text-decoration: line-through;
            color: #999;
        }

        /* Responsive */
        @media (max-width: 1024px) {
            .main-container {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (max-width: 768px) {
            .main-container {
                grid-template-columns: 1fr;
            }

            .calendar td {
                padding: 5px;
                height: 60px;
                font-size: 12px;
            }

            .day-tasks {
                font-size: 10px;
            }

            .container {
                padding: 20px;
            }

            h1 {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Left: Task List -->
        <div class="container">
            <h1>🌿 My To-Do List</h1>
            
            <div class="input-group">
                <input type="text" id="taskInput" placeholder="Add a new task...">
                <input type="date" id="dueDate">
                <div class="button-group">
                    <button id="addBtn">Add Task</button>
                </div>
            </div>

            <div id="emptyMsg">No tasks yet!</div>
            <ul id="taskList"></ul>
        </div>

        <!-- Middle: Reminders -->
        <div class="container">
            <h2>✨ Reminders & Events</h2>
            
            <div class="input-group">
                <input type="text" id="reminderInput" placeholder="Birthday, Anniversary...">
                <input type="date" id="reminderDate">
                <select id="reminderType">
                    <option value="birthday">🎂 Birthday</option>
                    <option value="anniversary">💍 Anniversary</option>
                    <option value="holiday">🎄 Holiday</option>
                    <option value="event">🎊 Event</option>
                    <option value="other">⭐ Other</option>
                </select>
                <div class="button-group">
                    <button id="addReminderBtn">Add Reminder</button>
                </div>
            </div>

            <div id="emptyReminder">No reminders yet!</div>
            <ul id="reminderList"></ul>
        </div>

        <!-- Right: Calendar -->
        <div class="container calendar-container">
            <h2>💚 Calendar</h2>
            
            <div class="calendar-header">
                <button id="prevBtn">← Prev</button>
                <div class="calendar-month" id="monthYear"></div>
                <button id="nextBtn">Next →</button>
            </div>

            <table class="calendar" id="calendarTable"></table>

            <div style="font-size: 12px; color: #1b5e20; margin-top: 15px; font-weight: 300; letter-spacing: 0.3px;">
                <p>🟢 Light green = Has tasks</p>
                <p>🟡 Yellow = Has reminders</p>
                <p>🟢 Green = Today</p>
            </div>
        </div>
    </div>

    <!-- Modal for day tasks -->
    <div id="dayModal" class="modal">
        <div class="modal-content">
            <span class="modal-close">&times;</span>
            <h2 id="modalDate" style="color: #1b5e20; font-weight: 300; letter-spacing: 0.3px;"></h2>
            <div id="modalTasksList" class="modal-tasks"></div>
        </div>
    </div>

    <script>
        const taskInput = document.getElementById('taskInput');
        const dueDate = document.getElementById('dueDate');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');
        const emptyMsg = document.getElementById('emptyMsg');

        const reminderInput = document.getElementById('reminderInput');
        const reminderDate = document.getElementById('reminderDate');
        const reminderType = document.getElementById('reminderType');
        const addReminderBtn = document.getElementById('addReminderBtn');
        const reminderList = document.getElementById('reminderList');
        const emptyReminder = document.getElementById('emptyReminder');

        const calendarTable = document.getElementById('calendarTable');
        const monthYear = document.getElementById('monthYear');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const dayModal = document.getElementById('dayModal');
        const modalClose = document.querySelector('.modal-close');
        const modalDate = document.getElementById('modalDate');
        const modalTasksList = document.getElementById('modalTasksList');

        let currentDate = new Date();

        const reminderEmojis = {
            birthday: '🎂',
            anniversary: '💍',
            holiday: '🎄',
            event: '🎊',
            other: '⭐'
        };

        // Initialize
        window.addEventListener('load', () => {
            loadTasks();
            loadReminders();
            renderCalendar();
            setTodayAsDefault();
        });

        // Event listeners - Tasks
        addBtn.addEventListener('click', addTask);
        taskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTask();
        });

        // Event listeners - Reminders
        addReminderBtn.addEventListener('click', addReminder);
        reminderInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addReminder();
        });

        // Event listeners - Calendar
        prevBtn.addEventListener('click', () => {
            currentDate.setMonth(currentDate.getMonth() - 1);
            renderCalendar();
        });
        nextBtn.addEventListener('click', () => {
            currentDate.setMonth(currentDate.getMonth() + 1);
            renderCalendar();
        });
        modalClose.addEventListener('click', () => {
            dayModal.style.display = 'none';
        });
        window.addEventListener('click', (e) => {
            if (e.target === dayModal) {
                dayModal.style.display = 'none';
            }
        });

        function setTodayAsDefault() {
            const today = new Date().toISOString().split('T')[0];
            dueDate.value = today;
            reminderDate.value = today;
        }

        // ===== TASKS =====
        function addTask() {
            const taskText = taskInput.value.trim();
            const taskDueDate = dueDate.value;
            
            if (taskText === '') {
                alert('Please enter a task!');
                return;
            }

            const tasks = getTasks();
            const newTask = {
                id: Date.now(),
                text: taskText,
                completed: false,
                dueDate: taskDueDate || new Date().toISOString().split('T')[0]
            };

            tasks.push(newTask);
            localStorage.setItem('tasks', JSON.stringify(tasks));
            taskInput.value = '';
            setTodayAsDefault();
            loadTasks();
            renderCalendar();
        }

        function deleteTask(id) {
            const tasks = getTasks();
            const updatedTasks = tasks.filter(task => task.id !== id);
            localStorage.setItem('tasks', JSON.stringify(updatedTasks));
            loadTasks();
            renderCalendar();
        }

        function toggleTask(id) {
            const tasks = getTasks();
            const task = tasks.find(t => t.id === id);
            if (task) {
                task.completed = !task.completed;
                localStorage.setItem('tasks', JSON.stringify(tasks));
                loadTasks();
                renderCalendar();
            }
        }

        function getTasks() {
            const tasks = localStorage.getItem('tasks');
            return tasks ? JSON.parse(tasks) : [];
        }

        function loadTasks() {
            const tasks = getTasks();
            taskList.innerHTML = '';

            if (tasks.length === 0) {
                emptyMsg.style.display = 'block';
                return;
            }

            emptyMsg.style.display = 'none';
            tasks.sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate));

            tasks.forEach(task => {
                const li = document.createElement('li');
                li.className = task.completed ? 'completed' : '';
                const dueDate = new Date(task.dueDate).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
                li.innerHTML = `
                    <input type="checkbox" ${task.completed ? 'checked' : ''} onchange="toggleTask(${task.id})">
                    <div class="task-content">
                        <span class="task-text">${task.text}</span>
                        <span class="task-date">Due: ${dueDate}</span>
                    </div>
                    <button class="delete-btn" onclick="deleteTask(${task.id})">Delete</button>
                `;
                taskList.appendChild(li);
            });
        }

        // ===== REMINDERS =====
        function addReminder() {
            const reminderText = reminderInput.value.trim();
            const reminderDateValue = reminderDate.value;
            const type = reminderType.value;
            
            if (reminderText === '') {
                alert('Please enter a reminder!');
                return;
            }

            const reminders = getReminders();
            const newReminder = {
                id: Date.now(),
                text: reminderText,
                date: reminderDateValue || new Date().toISOString().split('T')[0],
                type: type
            };

            reminders.push(newReminder);
            localStorage.setItem('reminders', JSON.stringify(reminders));
            reminderInput.value = '';
            setTodayAsDefault();
            loadReminders();
            renderCalendar();
        }

        function deleteReminder(id) {
            const reminders = getReminders();
            const updatedReminders = reminders.filter(r => r.id !== id);
            localStorage.setItem('reminders', JSON.stringify(updatedReminders));
            loadReminders();
            renderCalendar();
        }

        function getReminders() {
            const reminders = localStorage.getItem('reminders');
            return reminders ? JSON.parse(reminders) : [];
        }

        function loadReminders() {
            const reminders = getReminders();
            reminderList.innerHTML = '';

            if (reminders.length === 0) {
                emptyReminder.style.display = 'block';
                return;
            }

            emptyReminder.style.display = 'none';
            reminders.sort((a, b) => new Date(a.date) - new Date(b.date));

            reminders.forEach(reminder => {
                const li = document.createElement('li');
                li.className = 'reminder-item';
                const reminderDateObj = new Date(reminder.date).toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
                const emoji = reminderEmojis[reminder.type] || '⭐';
                li.innerHTML = `
                    <div class="reminder-content">
                        <span class="reminder-text">${emoji} ${reminder.text}</span>
                        <span class="reminder-type-badge">${reminder.type.toUpperCase()}</span>
                        <span class="reminder-date">Date: ${reminderDateObj}</span>
                    </div>
                    <button class="delete-btn" onclick="deleteReminder(${reminder.id})">Delete</button>
                `;
                reminderList.appendChild(li);
            });
        }

        // ===== CALENDAR =====
        function renderCalendar() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();

            monthYear.textContent = currentDate.toLocaleDateString('en-US', { month: 'long', year: 'numeric' });
            calendarTable.innerHTML = '';

            const headerRow = document.createElement('tr');
            const days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
            days.forEach(day => {
                const th = document.createElement('th');
                th.textContent = day;
                headerRow.appendChild(th);
            });
            calendarTable.appendChild(headerRow);

            const firstDay = new Date(year, month, 1).getDay();
            const daysInMonth = new Date(year, month + 1, 0).getDate();
            const daysInPrevMonth = new Date(year, month, 0).getDate();

            const tasks = getTasks();
            const reminders = getReminders();
            const tasksByDate = {};
            const remindersByDate = {};

            tasks.forEach(task => {
                if (!tasksByDate[task.dueDate]) tasksByDate[task.dueDate] = [];
                tasksByDate[task.dueDate].push(task);
            });

            reminders.forEach(reminder => {
                if (!remindersByDate[reminder.date]) remindersByDate[reminder.date] = [];
                remindersByDate[reminder.date].push(reminder);
            });

            const today = new Date();
            const todayStr = today.toISOString().split('T')[0];

            let date = 1;
            let prevDate = daysInPrevMonth - firstDay + 1;

            for (let row = 0; row < 6; row++) {
                const tr = document.createElement('tr');

                for (let col = 0; col < 7; col++) {
                    const td = document.createElement('td');
                    let cellDate;
                    let displayDate;

                    if (row === 0 && col < firstDay) {
                        displayDate = prevDate;
                        td.className = 'other-month';
                        cellDate = new Date(year, month - 1, prevDate).toISOString().split('T')[0];
                        prevDate++;
                    } else if (date <= daysInMonth) {
                        displayDate = date;
                        cellDate = new Date(year, month, date).toISOString().split('T')[0];
                        date++;
                    } else {
                        displayDate = date - daysInMonth;
                        td.className = 'other-month';
                        cellDate = new Date(year, month + 1, displayDate).toISOString().split('T')[0];
                        date++;
                    }

                    td.innerHTML = `<div class="day-number">${displayDate}</div>`;

                    if (tasksByDate[cellDate]) {
                        td.classList.add('has-tasks');
                        const dayTasksDiv = document.createElement('div');
                        dayTasksDiv.className = 'day-tasks';
                        tasksByDate[cellDate].slice(0, 1).forEach(task => {
                            const taskDiv = document.createElement('div');
                            taskDiv.className = `day-task-item ${task.completed ? 'completed' : ''}`;
                            taskDiv.textContent = task.text.substring(0, 12);
                            dayTasksDiv.appendChild(taskDiv);
                        });
                        td.appendChild(dayTasksDiv);
                    }

                    if (remindersByDate[cellDate]) {
                        td.classList.add('has-reminder');
                        const dayRemindersDiv = document.createElement('div');
                        dayRemindersDiv.className = 'day-tasks';
                        remindersByDate[cellDate].slice(0, 1).forEach(reminder => {
                            const reminderDiv = document.createElement('div');
                            reminderDiv.className = 'day-reminder-item';
                            reminderDiv.textContent = `${reminderEmojis[reminder.type]} ${reminder.text.substring(0, 10)}`;
                            dayRemindersDiv.appendChild(reminderDiv);
                        });
                        td.appendChild(dayRemindersDiv);
                    }

                    if (cellDate === todayStr) {
                        td.classList.add('today');
                    }

                    td.addEventListener('click', () => {
                        if (tasksByDate[cellDate]) {
                            showDayModal(cellDate, tasksByDate[cellDate]);
                        }
                    });

                    tr.appendChild(td);
                }

                calendarTable.appendChild(tr);
                if (date > daysInMonth) break;
            }
        }

        function showDayModal(dateStr, dayTasks) {
            const date = new Date(dateStr + 'T00:00:00');
            modalDate.textContent = date.toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' });
            
            modalTasksList.innerHTML = '';
            dayTasks.forEach(task => {
                const div = document.createElement('div');
                div.className = `modal-task-item ${task.completed ? 'completed' : ''}`;
                div.innerHTML = `
                    <input type="checkbox" ${task.completed ? 'checked' : ''} onchange="toggleTask(${task.id})">
                    <span>${task.text}</span>
                `;
                modalTasksList.appendChild(div);
            });

            dayModal.style.display = 'block';
        }
    </script>
</body>
</html>
