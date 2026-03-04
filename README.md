<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Varis Premium BCA Dashboard</title>
    <style>
        /* Animated Liquid Gradient Background */
        body { margin: 0; padding: 20px; font-family: 'Segoe UI', sans-serif; color: #fff; min-height: 100vh; background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab); background-size: 400% 400%; animation: gradientBG 15s ease infinite; overflow-x: hidden; }
        @keyframes gradientBG { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }
        
        .container { max-width: 450px; margin: 0 auto; }
        
        /* Glassmorphism Core CSS */
        .glass-card { background: rgba(255, 255, 255, 0.15); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.3); box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.2); border-radius: 20px; padding: 20px; margin-bottom: 25px; text-align: center; }
        h2 { font-size: 20px; border-bottom: 1px solid rgba(255,255,255,0.3); padding-bottom: 10px; margin-top: 0; text-shadow: 1px 1px 2px rgba(0,0,0,0.2); }

        /* 3D Holographic Cube */
        .scene { width: 80px; height: 80px; perspective: 400px; margin: 20px auto; }
        .cube { width: 100%; height: 100%; position: relative; transform-style: preserve-3d; animation: spinCube 8s infinite linear; }
        .cube__face { position: absolute; width: 80px; height: 80px; background: rgba(255, 255, 255, 0.2); border: 2px solid rgba(255, 255, 255, 0.5); display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 18px; backdrop-filter: blur(5px); }
        .cube__face--front  { transform: rotateY(  0deg) translateZ(40px); }
        .cube__face--right  { transform: rotateY( 90deg) translateZ(40px); }
        .cube__face--back   { transform: rotateY(180deg) translateZ(40px); }
        .cube__face--left   { transform: rotateY(-90deg) translateZ(40px); }
        .cube__face--top    { transform: rotateX( 90deg) translateZ(40px); }
        .cube__face--bottom { transform: rotateX(-90deg) translateZ(40px); }
        @keyframes spinCube { 0% { transform: translateZ(-40px) rotateX(0deg) rotateY(0deg); } 100% { transform: translateZ(-40px) rotateX(360deg) rotateY(360deg); } }

        /* 3D Flip ID Card */
        .flip-card { background-color: transparent; width: 100%; height: 180px; perspective: 1000px; margin-bottom: 20px; }
        .flip-card-inner { position: relative; width: 100%; height: 100%; transition: transform 0.8s; transform-style: preserve-3d; cursor: pointer; }
        .flip-card:active .flip-card-inner { transform: rotateY(180deg); }
        .flip-card-front, .flip-card-back { position: absolute; width: 100%; height: 100%; backface-visibility: hidden; border-radius: 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 15px; box-sizing: border-box; }
        .flip-card-front { background: rgba(255, 255, 255, 0.25); backdrop-filter: blur(10px); border: 1px solid rgba(255,255,255,0.4); }
        .flip-card-back { background: rgba(0, 0, 0, 0.4); backdrop-filter: blur(10px); transform: rotateY(180deg); border: 1px solid rgba(255,255,255,0.2); }
        .id-title { font-size: 22px; font-weight: bold; margin: 5px 0; }
        .id-subtitle { font-size: 14px; opacity: 0.9; }

        /* Animated XP Attendance Circle */
        .xp-container { position: relative; width: 120px; height: 120px; margin: 0 auto 15px; }
        .xp-circle { transform: rotate(-90deg); width: 100%; height: 100%; }
        .xp-bg { fill: none; stroke: rgba(255,255,255,0.2); stroke-width: 10; }
        .xp-progress { fill: none; stroke: #4ade80; stroke-width: 10; stroke-linecap: round; stroke-dasharray: 314; stroke-dashoffset: 314; animation: fillXP 2s ease-out forwards; }
        @keyframes fillXP { to { stroke-dashoffset: 49.6; } } /* 84.2% of 314 */
        .xp-text { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); font-size: 22px; font-weight: bold; }
        
        /* Bunk Meter */
        .bunk-meter { background: rgba(0, 255, 100, 0.2); border-left: 5px solid #4ade80; padding: 10px; border-radius: 8px; font-weight: bold; margin-top: 15px; }

        /* Interactive Task Board */
        .task-list { text-align: left; padding: 0; list-style: none; margin: 0; }
        .task-item { background: rgba(255, 255, 255, 0.1); padding: 12px; margin-bottom: 8px; border-radius: 8px; display: flex; justify-content: space-between; align-items: center; cursor: pointer; transition: 0.3s; border: 1px solid rgba(255,255,255,0.1); }
        .task-item:active { background: rgba(255, 255, 255, 0.3); }
        .task-item.done { text-decoration: line-through; opacity: 0.5; background: rgba(0,0,0,0.2); }
    </style>
</head>
<body>

<div class="container">

    <div class="scene">
        <div class="cube">
            <div class="cube__face cube__face--front">Day 4</div>
            <div class="cube__face cube__face--back">🧥</div>
            <div class="cube__face cube__face--right">BCA</div>
            <div class="cube__face cube__face--left">Day 4</div>
            <div class="cube__face cube__face--top">🧥</div>
            <div class="cube__face cube__face--bottom">BCA</div>
        </div>
    </div>

    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <div class="id-subtitle">Nilgiri College</div>
                <div class="id-title">Abdul Varis</div>
                <div class="id-subtitle">BCA - 1st Year</div>
                <div style="font-size: 10px; margin-top: 15px; opacity: 0.7;">Tap to flip</div>
            </div>
            <div class="flip-card-back">
                <div class="id-title">Student Details</div>
                <div class="id-subtitle">Semester: 2</div>
                <div class="id-subtitle">Blood Group: O+</div>
            </div>
        </div>
    </div>

    <div class="glass-card">
        <h2>🎮 Player XP & Attendance</h2>
        
        <div class="xp-container">
            <svg class="xp-circle" viewBox="0 0 120 120">
                <circle class="xp-bg" cx="60" cy="60" r="50"></circle>
                <circle class="xp-progress" cx="60" cy="60" r="50"></circle>
            </svg>
            <div class="xp-text">84%</div>
        </div>
        
        <div style="font-size: 14px; font-weight: bold;">Level 1 BCA Developer</div>
        
        <div class="bunk-meter">
            🛡️ Safe Zone: You can bunk 7 more classes and stay above 75%.
        </div>
    </div>

    <div class="glass-card">
        <h2>📝 Live Task Board</h2>
        <ul class="task-list" id="taskList">
            <li class="task-item" onclick="this.classList.toggle('done')"><span>1. Print Lab Records</span> <span>🔄</span></li>
            <li class="task-item" onclick="this.classList.toggle('done')"><span>2. Prepare Seminar PPT</span> <span>🔄</span></li>
            <li class="task-item" onclick="this.classList.toggle('done')"><span>3. Study for Practical Exam</span> <span>🔄</span></li>
        </ul>
        <p style="font-size: 11px; opacity: 0.8; margin-top: 10px;">Tap a task to mark it as completed.</p>
    </div>

</div>

</body>
</html>
        .progress-inner { width: 80px; height: 80px; border-radius: 50%; background: #fff; display: flex; align-items: center; justify-content: center; font-size: 18px; font-weight: bold; color: #111a2c; }
        
        /* Calendar Controls */
        .calendar-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
        .nav-btn { background: #eff6ff; border: 1px solid #bfdbfe; font-size: 18px; color: #3b82f6; cursor: pointer; font-weight: bold; padding: 8px 15px; border-radius: 8px; }
        .month-title { font-size: 18px; font-weight: bold; color: #111a2c; }
        
        /* Grid Layout */
        .weekdays { display: grid; grid-template-columns: repeat(7, 1fr); font-weight: bold; color: #64748b; font-size: 13px; margin-bottom: 10px; }
        .days-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 6px; font-size: 14px; }
        
        /* Interactive Cells */
        .date-cell { min-height: 65px; display: flex; flex-direction: column; align-items: center; justify-content: flex-start; padding-top: 5px; border-radius: 8px; cursor: pointer; background: #fafafa; border: 1px solid #e2e8f0; position: relative; }
        .date-num { font-weight: bold; font-size: 15px; color: #0f172a; }
        .today { border: 2px solid #3b82f6; background: #eff6ff; }
        
        /* Dynamic Indicators */
        .day-order-badge { font-size: 11px; font-weight: bold; color: #3b82f6; margin-top: 2px; }
        .holiday-badge { font-size: 10px; color: #ef4444; font-weight: bold; margin-top: 2px; text-align: center; line-height: 1.1; }
        .coat-emoji { font-size: 13px; position: absolute; bottom: 2px; right: 4px; }
        .empty { background: transparent; border: none; cursor: default; }
    </style>
</head>
<body>

<div class="container">

    <div class="card">
        <h2>📊 Semester 2 Attendance</h2>
        <div class="progress-circle">
            <div class="progress-inner">84.2%</div>
        </div>
        <p style="font-size: 13px; color: #64748b; font-weight: bold;">01-12-2025 To 31-05-2026</p>
    </div>

    <div class="card">
        <div class="calendar-header">
            <button class="nav-btn" onclick="changeMonth(-1)">&#10094; Prev</button>
            <div class="month-title" id="month-display">March 2026</div>
            <button class="nav-btn" onclick="changeMonth(1)">Next &#10095;</button>
        </div>
        
        <div class="weekdays">
            <div>Sun</div><div>Mon</div><div>Tue</div><div>Wed</div><div>Thu</div><div>Fri</div><div>Sat</div>
        </div>
        
        <div class="days-grid" id="calendar-grid">
            </div>
    </div>

</div>

<script>
    const grid = document.getElementById('calendar-grid');
    const monthDisplay = document.getElementById('month-display');
    const today = new Date();
    
    let currentMonth = 2; // Default to March (Index 2)
    let currentYear = 2026;
    const monthNames = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];

    // Explicit Holiday Display List
    const collegeHolidays = {
        "2025-12-24": "Holiday", "2025-12-25": "Christmas", "2025-12-26": "Spl Leave", "2025-12-27": "Spl Leave",
        "2026-1-1": "New Year", "2026-1-14": "Pongal", "2026-1-26": "Republic Day",
        "2026-2-4": "Cancer Day", "2026-2-11": "CIA-II", "2026-2-21": "Mother Lang",
        "2026-3-8": "Women's Day", "2026-3-12": "Practical", "2026-3-19": "Spl Leave", "2026-3-20": "Eid-ul-Fitr", "2026-3-21": "Spl Leave", "2026-3-25": "Model Exam",
        "2026-4-3": "Good Friday", "2026-4-5": "Easter", "2026-4-6": "Study Leave", "2026-4-13": "Sem Exam", "2026-4-14": "Tamil NY",
        "2026-5-1": "Annual Lv"
    };

    // Days to pause the Day Order Counter (Weekends & Holidays)
    const skipDays = [
        // Dec
        "2025-12-7", "2025-12-13", "2025-12-14", "2025-12-21", "2025-12-24", "2025-12-25", "2025-12-26", "2025-12-27", "2025-12-28",
        // Jan
        "2026-1-1", "2026-1-4", "2026-1-10", "2026-1-11", "2026-1-14", "2026-1-15", "2026-1-16", "2026-1-17", "2026-1-18", "2026-1-25", "2026-1-26",
        // Feb
        "2026-2-1", "2026-2-8", "2026-2-14", "2026-2-15", "2026-2-22", "2026-2-28",
        // Mar
        "2026-3-1", "2026-3-8", "2026-3-14", "2026-3-15", "2026-3-19", "2026-3-20", "2026-3-21", "2026-3-22", "2026-3-28", "2026-3-29",
        // Apr 
        "2026-4-3", "2026-4-4", "2026-4-5", "2026-4-11", "2026-4-12", "2026-4-14", "2026-4-18", "2026-4-19", "2026-4-25", "2026-4-26",
        // May
        "2026-5-1", "2026-5-2", "2026-5-3", "2026-5-9", "2026-5-10", "2026-5-16", "2026-5-17", "2026-5-23", "2026-5-24", "2026-5-30", "2026-5-31"
    ];

    // The Ultimate Anchor Logic
    function calculateExactDayOrders() {
        let dayMap = {};
        
        // ANCHOR: March 4, 2026 is permanently Day 4
        dayMap["2026-3-4"] = 4;

        // Backward calculation to Dec 1
        let currOrder = 4;
        let tempDate = new Date(2026, 2, 3); // Mar 3
        while(tempDate >= new Date(2025, 11, 1)) {
            let dStr = `${tempDate.getFullYear()}-${tempDate.getMonth()+1}-${tempDate.getDate()}`;
            if(tempDate.getDay() !== 0 && !skipDays.includes(dStr)) {
                currOrder = currOrder - 1;
                if(currOrder < 1) currOrder = 5;
                dayMap[dStr] = currOrder;
            }
            tempDate.setDate(tempDate.getDate() - 1);
        }

        // Forward calculation to May 31
        currOrder = 4;
        tempDate = new Date(2026, 2, 5); // Mar 5
        while(tempDate <= new Date(2026, 4, 31)) {
            let dStr = `${tempDate.getFullYear()}-${tempDate.getMonth()+1}-${tempDate.getDate()}`;
            if(tempDate.getDay() !== 0 && !skipDays.includes(dStr)) {
                currOrder = currOrder + 1;
                if(currOrder > 5) currOrder = 1;
                dayMap[dStr] = currOrder;
            }
            tempDate.setDate(tempDate.getDate() + 1);
        }

        return dayMap;
    }

    const calculatedDayOrders = calculateExactDayOrders();

    function renderCalendar(month, year) {
        grid.innerHTML = "";
        monthDisplay.innerText = `${monthNames[month]} ${year}`;
        
        let firstDay = new Date(year, month, 1).getDay();
        let daysInMonth = new Date(year, month + 1, 0).getDate();
        
        for (let i = 0; i < firstDay; i++) {
            let emptyDiv = document.createElement('div');
            emptyDiv.className = 'date-cell empty';
            grid.appendChild(emptyDiv);
        }

        for (let i = 1; i <= daysInMonth; i++) {
            let cell = document.createElement('div');
            cell.className = 'date-cell';
            
            let dateString = `${year}-${month + 1}-${i}`;
            let dayOfWeek = new Date(year, month, i).getDay();
            
            if (today.getMonth() === month && today.getFullYear() === year && i === today.getDate()) {
                cell.classList.add('today');
            }

            let html = `<div class="date-num">${i}</div>`;
            
            // Rendering Priorities: Holidays first, then Day Orders
            if (collegeHolidays[dateString]) {
                html += `<div class="holiday-badge">${collegeHolidays[dateString]}</div>`;
                cell.style.borderColor = "#fca5a5"; 
            } else if (skipDays.includes(dateString) || dayOfWeek === 0) {
                html += `<div class="holiday-badge">Holiday</div>`;
                cell.style.borderColor = "#fca5a5";
            } else if (calculatedDayOrders[dateString]) {
                html += `<div class="day-order-badge">Day ${calculatedDayOrders[dateString]}</div>`;
            }

            // Injecting the Coat Emoji securely
            if (dayOfWeek === 3 && calculatedDayOrders[dateString]) {
                html += `<div class="coat-emoji">🧥</div>`;
            }

            cell.innerHTML = html;
            
            cell.onclick = function() {
                let task = prompt(`Set a reminder for ${monthNames[month]} ${i}:`);
                if (task) alert(`🔔 Reminder saved: "${task}"`);
            };

            grid.appendChild(cell);
        }
    }

    function changeMonth(step) {
        currentMonth += step;
        if (currentMonth < 0) { currentMonth = 11; currentYear--; }
        if (currentMonth > 11) { currentMonth = 0; currentYear++; }
        
        // Strict boundary lock: Dec 2025 to May 2026
        if (currentYear === 2025 && currentMonth < 11) { currentMonth = 11; }
        if (currentYear === 2026 && currentMonth > 4) { currentMonth = 4; }
        
        renderCalendar(currentMonth, currentYear);
    }

    // Initialize display
    renderCalendar(currentMonth, currentYear);
</script>

</body>
</html>
