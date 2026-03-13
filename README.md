# Daily-Tracker
Just first I made.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Morning Tracker - Daily Activity Tracker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --color-primary: #f97316;
            --color-accent: #ec4899;
            --color-success: #10b981;
            --color-info: #3b82f6;
            --color-warning: #f59e0b;
            --color-danger: #ef4444;
            --color-bg-light: #fafafa;
            --color-text-dark: #1f2937;
            --color-text-light: #6b7280;
            --color-border: #e5e7eb;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        html, body {
            font-family: 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', sans-serif;
            background: linear-gradient(135deg, #fef3c7 0%, #dbeafe 50%, #f3e8ff 100%);
            min-height: 100vh;
            color: var(--color-text-dark);
        }

        body {
            padding-bottom: 32px;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #fb923c 0%, #ec4899 100%);
            color: white;
            padding: 32px 24px;
            border-radius: 0 0 24px 24px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            margin-bottom: 32px;
        }

        .header-top {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 24px;
        }

        .header-title {
            font-size: 28px;
            font-weight: 900;
            letter-spacing: -0.5px;
        }

        .sun-icon {
            animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .date-text {
            font-size: 14px;
            opacity: 0.9;
            font-weight: 500;
            margin-bottom: 24px;
        }

        /* Progress Section */
        .progress-container {
            display: flex;
            align-items: center;
            gap: 24px;
        }

        .progress-ring-container {
            position: relative;
            width: 96px;
            height: 96px;
            flex-shrink: 0;
        }

        .progress-ring-svg {
            width: 100%;
            height: 100%;
            transform: rotate(-90deg);
        }

        .progress-ring-bg {
            fill: none;
            stroke: rgba(255, 255, 255, 0.3);
            stroke-width: 6;
        }

        .progress-ring-fill {
            fill: none;
            stroke: white;
            stroke-width: 6;
            stroke-linecap: round;
            transition: stroke-dasharray 0.5s ease-in-out;
        }

        .progress-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }

        .progress-count {
            font-size: 20px;
            font-weight: 900;
        }

        .progress-label {
            font-size: 12px;
            opacity: 0.9;
        }

        .progress-info h3 {
            font-size: 12px;
            opacity: 0.9;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .progress-percentage {
            font-size: 24px;
            font-weight: 900;
        }

        .progress-subtext {
            font-size: 12px;
            opacity: 0.75;
            margin-top: 4px;
        }

        /* Activities Container */
        .activities-container {
            max-width: 448px;
            margin: 0 auto;
            padding: 0 16px;
        }

        .activity-grid {
            display: grid;
            gap: 16px;
        }

        /* Activity Card */
        .activity-card {
            border-radius: 16px;
            padding: 20px;
            transition: var(--transition);
            border: 2px solid var(--color-border);
            background: white;
        }

        .activity-card.completed {
            background: linear-gradient(135deg, #f0fdf4 0%, #dbeafe 100%);
            border-color: #86efac;
            box-shadow: 0 4px 20px rgba(16, 185, 129, 0.2);
        }

        .activity-card:hover:not(.completed) {
            border-color: #d1d5db;
        }

        .activity-header {
            display: flex;
            align-items: flex-start;
            justify-content: space-between;
            margin-bottom: 16px;
        }

        .activity-info {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
        }

        .activity-icon {
            width: 48px;
            height: 48px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            flex-shrink: 0;
        }

        .activity-icon.running { background: linear-gradient(135deg, #60a5fa 0%, #06b6d4 100%); }
        .activity-icon.steps { background: linear-gradient(135deg, #a855f7 0%, #ec4899 100%); }
        .activity-icon.meditation { background: linear-gradient(135deg, #4ade80 0%, #10b981 100%); }
        .activity-icon.stretching { background: linear-gradient(135deg, #facc15 0%, #f97316 100%); }
        .activity-icon.hydration { background: linear-gradient(135deg, #3b82f6 0%, #1e40af 100%); }
        .activity-icon.breakfast { background: linear-gradient(135deg, #f87171 0%, #ec4899 100%); }

        .activity-title {
            font-size: 18px;
            font-weight: 700;
            color: var(--color-text-dark);
        }

        .activity-progress-text {
            font-size: 12px;
            color: var(--color-text-light);
            margin-top: 2px;
        }

        .activity-checkbox {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 28px;
            transition: transform 0.2s;
            padding: 0;
        }

        .activity-checkbox:hover {
            transform: scale(1.1);
        }

        .activity-checkbox:active {
            transform: scale(0.95);
        }

        /* Progress Bar */
        .progress-bar-container {
            margin-bottom: 12px;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e5e7eb;
            border-radius: 9999px;
            overflow: hidden;
        }

        .progress-bar-fill {
            height: 100%;
            background: linear-gradient(90deg, #60a5fa 0%, #06b6d4 100%);
            border-radius: 9999px;
            transition: width 0.3s ease-in-out;
        }

        .progress-bar-fill.success {
            background: linear-gradient(90deg, #4ade80 0%, #10b981 100%);
        }

        /* Counter Controls */
        .counter-container {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .counter-btn {
            padding: 8px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            transition: var(--transition);
            font-weight: 600;
        }

        .counter-btn.minus {
            background: #fee2e2;
            color: #dc2626;
        }

        .counter-btn.minus:hover {
            background: #fecaca;
        }

        .counter-btn.minus:active {
            background: #fca5a5;
        }

        .counter-btn.plus {
            background: #dcfce7;
            color: #16a34a;
        }

        .counter-btn.plus:hover {
            background: #bbf7d0;
        }

        .counter-btn.plus:active {
            background: #86efac;
        }

        .counter-input {
            flex: 1;
            text-align: center;
            font-size: 18px;
            font-weight: 700;
            background: #f3f4f6;
            border-radius: 8px;
            padding: 8px;
            border: none;
            outline: none;
        }

        .counter-input:focus {
            outline: 2px solid var(--color-info);
            outline-offset: 0;
        }

        /* Breakfast Button */
        .breakfast-btn {
            width: 100%;
            padding: 12px;
            border-radius: 12px;
            border: none;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
        }

        .breakfast-btn.inactive {
            background: #e5e7eb;
            color: #4b5563;
        }

        .breakfast-btn.inactive:hover {
            background: #d1d5db;
        }

        .breakfast-btn.active {
            background: #22c55e;
            color: white;
            box-shadow: 0 4px 12px rgba(34, 197, 94, 0.4);
        }

        /* Celebration Banner */
        .celebration-banner {
            margin: 32px 16px 0 16px;
            background: linear-gradient(135deg, #22c55e 0%, #10b981 100%);
            color: white;
            border-radius: 16px;
            padding: 24px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(34, 197, 94, 0.3);
            animation: bounce 1s ease-in-out infinite;
        }

        .celebration-banner h3 {
            font-size: 20px;
            font-weight: 900;
            margin-bottom: 8px;
        }

        .celebration-banner p {
            font-size: 12px;
            opacity: 0.9;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        /* Responsive */
        @media (max-width: 480px) {
            .header {
                padding: 24px 16px;
            }

            .header-title {
                font-size: 24px;
            }

            .progress-container {
                gap: 16px;
            }

            .activity-card {
                padding: 16px;
            }
        }

        /* Scrollbar styling */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: transparent;
        }

        ::-webkit-scrollbar-thumb {
            background: rgba(107, 114, 128, 0.3);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: rgba(107, 114, 128, 0.5);
        }
    </style>
</head>
<body>
    <div id="app"></div>

    <script>
        // Application State
        class MorningTrackerApp {
            constructor() {
                this.currentDate = new Date().toDateString();
                this.activities = this.loadActivities();
                this.init();
            }

            loadActivities() {
                const saved = localStorage.getItem('morningActivities');
                const today = new Date().toDateString();
                const savedDate = localStorage.getItem('trackerDate');

                if (saved && savedDate === today) {
                    return JSON.parse(saved);
                }

                localStorage.setItem('trackerDate', today);
                return {
                    running: { completed: false, miles: 0, target: 5 },
                    steps: { completed: false, count: 0, target: 10000 },
                    meditation: { completed: false, minutes: 0, target: 10 },
                    stretching: { completed: false, minutes: 0, target: 15 },
                    hydration: { completed: false, cups: 0, target: 3 },
                    breakfast: { completed: false, healthy: false }
                };
            }

            saveActivities() {
                localStorage.setItem('morningActivities', JSON.stringify(this.activities));
            }

            toggleCompleted(key) {
                this.activities[key].completed = !this.activities[key].completed;
                this.saveActivities();
                this.render();
            }

            updateValue(key, field, value) {
                this.activities[key][field] = value;
                this.saveActivities();
                this.render();
            }

            increment(key, field) {
                this.activities[key][field]++;
                this.saveActivities();
                this.render();
            }

            decrement(key, field) {
                if (this.activities[key][field] > 0) {
                    this.activities[key][field]--;
                    this.saveActivities();
                    this.render();
                }
            }

            getCompletedCount() {
                return Object.values(this.activities).filter(a => a.completed).length;
            }

            getTotalActivities() {
                return Object.keys(this.activities).length;
            }

            getProgressPercent() {
                return (this.getCompletedCount() / this.getTotalActivities()) * 100;
            }

            isGoalMet(key) {
                const activity = this.activities[key];
                if (activity.target) {
                    const value = activity.miles || activity.count || activity.minutes || activity.cups || 0;
                    return value >= activity.target;
                }
                return activity.healthy;
            }

            renderProgressRing() {
                const percent = this.getProgressPercent();
                const radius = 45;
                const circumference = 2 * Math.PI * radius;
                const offset = circumference - (percent / 100) * circumference;

                return `
                    <svg class="progress-ring-svg" viewBox="0 0 100 100">
                        <circle class="progress-ring-bg" cx="50" cy="50" r="45"></circle>
                        <circle
                            class="progress-ring-fill"
                            cx="50"
                            cy="50"
                            r="45"
                            stroke-dasharray="${circumference}"
                            stroke-dashoffset="${offset}"
                        ></circle>
                    </svg>
                    <div class="progress-text">
                        <div class="progress-count">${this.getCompletedCount()}</div>
                        <div class="progress-label">of ${this.getTotalActivities()}</div>
                    </div>
                `;
            }

            renderActivityCard(key, config) {
                const activity = this.activities[key];
                const isGoalMet = this.isGoalMet(key);
                const completed = activity.completed ? 'completed' : '';

                if (!activity.target) {
                    return `
                        <div class="activity-card ${completed}">
                            <div class="activity-header">
                                <div class="activity-info">
                                    <div class="activity-icon ${key}">
                                        ${config.icon}
                                    </div>
                                    <div>
                                        <div class="activity-title">${config.title}</div>
                                    </div>
                                </div>
                                <button class="activity-checkbox" onclick="app.toggleCompleted('${key}')">
                                    ${activity.completed ? '✅' : '⭕'}
                                </button>
                            </div>
                            <button
                                class="breakfast-btn ${activity.healthy ? 'active' : 'inactive'}"
                                onclick="app.updateValue('${key}', 'healthy', ${!activity.healthy})"
                            >
                                ${activity.healthy ? '✓ Healthy Breakfast' : 'Log Breakfast'}
                            </button>
                        </div>
                    `;
                }

                const value = activity.miles || activity.count || activity.minutes || activity.cups || 0;
                const fieldName = activity.miles !== undefined ? 'miles' : 
                                 activity.count !== undefined ? 'count' : 
                                 activity.minutes !== undefined ? 'minutes' : 'cups';
                const progressPercent = Math.min((value / activity.target) * 100, 100);
                const barClass = isGoalMet ? 'success' : '';

                return `
                    <div class="activity-card ${completed}">
                        <div class="activity-header">
                            <div class="activity-info">
                                <div class="activity-icon ${key}">
                                    ${config.icon}
                                </div>
                                <div>
                                    <div class="activity-title">${config.title}</div>
                                    <div class="activity-progress-text">${value} / ${activity.target}</div>
                                </div>
                            </div>
                            <button class="activity-checkbox" onclick="app.toggleCompleted('${key}')">
                                ${activity.completed ? '✅' : '⭕'}
                            </button>
                        </div>
                        <div class="progress-bar-container">
                            <div class="progress-bar">
                                <div class="progress-bar-fill ${barClass}" style="width: ${progressPercent}%"></div>
                            </div>
                        </div>
                        <div class="counter-container">
                            <button class="counter-btn minus" onclick="app.decrement('${key}', '${fieldName}')">−</button>
                            <input type="number" class="counter-input" value="${value}" onchange="app.updateValue('${key}', '${fieldName}', parseInt(this.value) || 0)">
                            <button class="counter-btn plus" onclick="app.increment('${key}', '${fieldName}')">+</button>
                        </div>
                    </div>
                `;
            }

            render() {
                const completedCount = this.getCompletedCount();
                const totalActivities = this.getTotalActivities();
                const progressPercent = this.getProgressPercent();

                const html = `
                    <div class="header">
                        <div class="header-top">
                            <span class="sun-icon">☀️</span>
                            <h1 class="header-title">Morning Tracker</h1>
                        </div>
                        <div class="date-text">${new Date().toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric' })}</div>
                        <div class="progress-container">
                            <div class="progress-ring-container">
                                ${this.renderProgressRing()}
                            </div>
                            <div class="progress-info">
                                <h3>Morning Goal</h3>
                                <div class="progress-percentage">${Math.round(progressPercent)}%</div>
                                <p class="progress-subtext">Complete activities to level up!</p>
                            </div>
                        </div>
                    </div>

                    <div class="activities-container">
                        <div class="activity-grid">
                            ${this.renderActivityCard('running', { title: 'Running', icon: '🏃' })}
                            ${this.renderActivityCard('steps', { title: 'Steps', icon: '📈' })}
                            ${this.renderActivityCard('meditation', { title: 'Meditation', icon: '❤️' })}
                            ${this.renderActivityCard('stretching', { title: 'Stretching', icon: '⚡' })}
                            ${this.renderActivityCard('hydration', { title: 'Hydration', icon: '☕' })}
                            ${this.renderActivityCard('breakfast', { title: 'Breakfast', icon: '🍎' })}
                        </div>
                    </div>

                    ${completedCount === totalActivities ? `
                        <div class="celebration-banner">
                            <h3>🎉 Awesome! All activities completed!</h3>
                            <p>Keep up the great morning routine!</p>
                        </div>
                    ` : ''}
                `;

                document.getElementById('app').innerHTML = html;
            }

            init() {
                this.render();
                // Check for new day
                setInterval(() => {
                    const now = new Date().toDateString();
                    if (now !== this.currentDate) {
                        this.currentDate = now;
                        this.activities = this.loadActivities();
                        this.render();
                    }
                }, 60000); // Check every minute
            }
        }

        // Initialize app
        const app = new MorningTrackerApp();
    </script>
</body>
</html>
