<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="stopwatch">
    <h1 id="display">00:00:00</h1>
    <div class="controls">
      <button onclick="startStopwatch()">Start</button>
      <button onclick="pauseStopwatch()">Pause</button>
      <button onclick="resetStopwatch()">Reset</button>
      <button onclick="lapTime()">Lap</button>
    </div>
    <ul id="lap-times"></ul>
  </div>
  
  <script src="script.js"></script>
</body>
</html>
.stopwatch {
  text-align: center;
}

#display {
  font-size: 48px;
  margin-bottom: 20px;
}

.controls button {
  margin: 5px;
  padding: 10px 20px;
  font-size: 16px;
}
let startTime;
let elapsedTime = 0;
let timerInterval;

function startStopwatch() {
  if (!startTime) {
    startTime = Date.now() - elapsedTime;
    timerInterval = setInterval(updateDisplay, 10);
  }
}

function pauseStopwatch() {
  clearInterval(timerInterval);
  timerInterval = null;
}

function resetStopwatch() {
  clearInterval(timerInterval);
  timerInterval = null;
  startTime = null;
  elapsedTime = 0;
  document.getElementById('display').innerText = '00:00:00';
  document.getElementById('lap-times').innerHTML = '';
}

function updateDisplay() {
  const currentTime = Date.now();
  elapsedTime = currentTime - startTime;
  displayTime(elapsedTime);
}

function displayTime(time) {
  const milliseconds = Math.floor((time % 1000) / 10);
  const seconds = Math.floor((time / 1000) % 60);
  const minutes = Math.floor((time / (1000 * 60)) % 60);
  const hours = Math.floor((time / (1000 * 60 * 60)) % 24);

  document.getElementById('display').innerText = 
    ${formatTime(hours)}:${formatTime(minutes)}:${formatTime(seconds)}.${formatTime(milliseconds)};
}

function formatTime(time) {
  return time < 10 ? 0${time} : time;
}

function lapTime() {
  const lapTimesElement = document.getElementById('lap-times');
  const lapTimeElement = document.createElement('li');
  lapTimeElement.innerText = document.getElementById('display').innerText;
  lapTimesElement.appendChild(lapTimeElement);
}
