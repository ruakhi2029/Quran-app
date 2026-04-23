<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Reminder Light 🌙</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: white;
}

.app {
    max-width: 420px;
    margin: auto;
    padding: 20px;
}

.header {
    text-align: center;
    padding: 15px;
    font-size: 26px;
    font-weight: bold;
}

.card {
    background: rgba(255,255,255,0.1);
    padding: 15px;
    border-radius: 15px;
    margin: 15px 0;
    backdrop-filter: blur(6px);
}

button {
    width: 100%;
    padding: 12px;
    margin-top: 10px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    font-size: 15px;
}

.mood { background: #feca57; }
.pray { background: #1dd1a1; }
.reset { background: #ff6b6b; color: white; }

.output {
    margin-top: 10px;
    font-size: 15px;
    line-height: 1.5;
}

.streak {
    font-size: 18px;
    text-align: center;
}
</style>
</head>

<body>

<div class="app">

<div class="header">🌙 Reminder Light</div>

<div class="card streak">
🔥 Daily Streak: <span id="streak">0</span> days
</div>

<div class="card">
<h3>How are you feeling?</h3>

<button class="mood" onclick="mood('calm')">😊 Calm</button>
<button class="mood" onclick="mood('sad')">😔 Sad</button>
<button class="mood" onclick="mood('stress')">😣 Stressed</button>
<button class="mood" onclick="mood('grateful')">🤍 Grateful</button>

<div class="output" id="moodOutput"></div>
</div>

<div class="card">
<h3>Prayer Reminder</h3>
<button class="pray" onclick="startReminder()">⏰ Start Reminder (every 1 min demo)</button>
<div class="output" id="prayOutput"></div>
</div>

<div class="card">
<h3>Random Reflection</h3>
<button onclick="randomAyah()">📖 Inspire Me</button>
<div class="output" id="ayah"></div>
</div>

<div class="card">
<button class="reset" onclick="resetAll()">Reset App</button>
</div>

</div>

<script>

// --- Streak system (saved in browser) ---
let streak = localStorage.getItem("streak") || 0;
document.getElementById("streak").innerText = streak;

function addStreak() {
    streak++;
    localStorage.setItem("streak", streak);
    document.getElementById("streak").innerText = streak;
}

// --- Mood system ---
function mood(type) {
    let msg = "";

    if (type === "calm") {
        msg = "🌿 'In the remembrance of Allah do hearts find rest.' (13:28)";
    }
    if (type === "sad") {
        msg = "🌧️ 'Do not lose hope in the mercy of Allah.' (39:53)";
    }
    if (type === "stress") {
        msg = "⚡ 'Indeed, with hardship comes ease.' (94:6)";
    }
    if (type === "grateful") {
        msg = "✨ 'If you are grateful, I will increase you.' (14:7)";
    }

    document.getElementById("moodOutput").innerText = msg;
}

// --- Prayer reminder (demo timer) ---
let reminder;

function startReminder() {
    clearInterval(reminder);

    document.getElementById("prayOutput").innerText =
        "⏰ Reminder started (demo: every 60 seconds)";

    reminder = setInterval(() => {
        alert("⏰ Time to pause and remember your prayer");
        addStreak();
    }, 60000);
}

// --- Random ayah inspiration ---
function randomAyah() {
    const ayahs = [
        "🌙 Allah is with those who are patient (2:153)",
        "🌿 Do not despair of Allah's mercy (39:53)",
        "✨ Remember Me, I will remember you (2:152)",
        "🌧️ Indeed with hardship comes ease (94:6)",
        "🤍 Allah does not burden a soul beyond what it can bear (2:286)"
    ];

    let pick = ayahs[Math.floor(Math.random() * ayahs.length)];
    document.getElementById("ayah").innerText = pick;
}

// --- reset ---
function resetAll() {
    localStorage.removeItem("streak");
    streak = 0;
    document.getElementById("streak").innerText = streak;
    document.getElementById("moodOutput").innerText = "";
    document.getElementById("ayah").innerText = "";
    document.getElementById("prayOutput").innerText = "";
}

</script>

</body>
</html>
