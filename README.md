<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SEMESTER 2 Calendar</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background-color: #f4f5f7; color: #1a1a1a; padding: 15px; margin: 0; }
        .container { max-width: 450px; margin: 0 auto; }
        .card { background: #ffffff; padding: 20px; border-radius: 15px; margin-bottom: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.08); text-align: center; }
        h2 { color: #111a2c; font-size: 20px; margin-top: 0; border-bottom: 2px solid #eee; padding-bottom: 10px; font-weight: 800; }
        
        /* Attendance Visuals */
        .progress-circle { position: relative; width: 110px; height: 110px; border-radius: 50%; background: conic-gradient(#22c55e 84.2%, #e5e7eb 0); margin: 15px auto; display: flex; align-items: center; justify-content: center; }
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
