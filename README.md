# BLPF-Clocking-System
Baybay Leyte Pigeon Federation - A web-based clocking system for tracking Pigeon race results and rankings. 
<!DOCTYPE html>
<html>
<head>
  <title>Pigeon Clocking System</title>
  <style>
    body { font-family: Arial; text-align: center; }
    input, button { margin: 5px; padding: 8px; }
    table { margin: auto; border-collapse: collapse; }
    th, td { border: 1px solid black; padding: 8px; }
  </style>
</head>

<body>

<h2>🐦 Pigeon Clocking System</h2>

<input type="text" id="ring" placeholder="Ring Number">
<input type="time" id="time">
<button onclick="addData()">Add</button>

<h3>Results</h3>

<table>
  <tr>
    <th>Ring</th>
    <th>Time</th>
  </tr>
  <tbody id="table"></tbody>
</table>

<script>
function addData() {
  let ring = document.getElementById("ring").value;
  let time = document.getElementById("time").value;

  let table = document.getElementById("table");
  let row = table.insertRow();

  row.insertCell(0).innerText = ring;
  row.insertCell(1).innerText = time;
}
</script>

</body>
</html>
