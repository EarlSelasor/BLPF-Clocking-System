  # BLPF-Clocking-System
Baybay Leyte Pigeon Federation - A web-based clocking system for tracking Pigeon race results and rankings. 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Baybay Leyte Pigeon Tracker</title>
<meta name="description" content="Track pigeon ring numbers, stickers, and time, synced with friends.">
<script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-database-compat.js"></script>
</head>
<body>
<h1>Baybay Leyte Pigeon Tracker</h1>

<div>
  <label>Ring Number:</label>
  <input type="text" id="ringNumber" placeholder="Enter ring number">
</div>

<div>
  <label>Sticker:</label>
  <input type="text" id="sticker" placeholder="Enter sticker info">
</div>

<div>
  <label>Time:</label>
  <input type="text" id="time" readonly>
</div>

<button onclick="submitData()">Submit</button>

<h2>Submitted Records</h2>
<ul id="records"></ul>

<script>
// Firebase config
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
  projectId: "YOUR_PROJECT_ID",
};
firebase.initializeApp(firebaseConfig);
const db = firebase.database();

// Auto-fill current time
function updateTime() {
  const now = new Date();
  document.getElementById('time').value = now.toLocaleTimeString();
}
setInterval(updateTime, 1000);
updateTime();

// Submit data to Firebase
function submitData() {
  const ring = document.getElementById('ringNumber').value;
  const sticker = document.getElementById('sticker').value;
  const time = document.getElementById('time').value;

  if (!ring || !sticker) {
    alert("Please enter ring number and sticker info!");
    return;
  }

  const record = { ring, sticker, time };
  db.ref('pigeons').push(record);

  document.getElementById('ringNumber').value = '';
  document.getElementById('sticker').value = '';
}

// Listen for changes in Firebase
db.ref('pigeons').on('value', snapshot => {
  const records = snapshot.val();
  const ul = document.getElementById('records');
  ul.innerHTML = '';
  for (let key in records) {
    const r = records[key];
    const li = document.createElement('li');
    li.textContent = `Ring: ${r.ring} | Sticker: ${r.sticker} | Time: ${r.time}`;
    ul.appendChild(li);
  }
});
</script>
</body>
</html>
