# vehicle-tracking-dashboard-project
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vehicle Tracking Dashboard</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f4f4f4;
    margin:0;
    padding:20px;
}

h1{
    text-align:center;
    color:#333;
}

.dashboard{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:15px;
    margin-top:20px;
}

.card{
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 2px 5px rgba(0,0,0,0.2);
    text-align:center;
}

.card h3{
    margin-bottom:10px;
    color:#555;
}

.card p{
    font-size:22px;
    font-weight:bold;
    color:#222;
}

.status-running{
    color:green;
}

.status-stopped{
    color:red;
}

table{
    width:100%;
    margin-top:20px;
    border-collapse:collapse;
    background:white;
}

table,th,td{
    border:1px solid #ddd;
}

th,td{
    padding:10px;
    text-align:center;
}

th{
    background:#007bff;
    color:white;
}
</style>
</head>

<body>

<h1>🚗 Vehicle Tracking Dashboard</h1>

<div class="dashboard">

<div class="card">
<h3>Vehicle ID</h3>
<p>VH001</p>
</div>

<div class="card">
<h3>Speed</h3>
<p id="speed">60 km/h</p>
</div>

<div class="card">
<h3>Fuel Level</h3>
<p id="fuel">100%</p>
</div>

<div class="card">
<h3>Status</h3>
<p id="status" class="status-running">Running</p>
</div>

<div class="card">
<h3>Location</h3>
<p id="location">Coimbatore</p>
</div>

</div>

<table>
<thead>
<tr>
<th>Time</th>
<th>Location</th>
<th>Speed</th>
</tr>
</thead>
<tbody id="history">
</tbody>
</table>
<script>
let fuel = 100;
const locations = [
"Coimbatore",
"Salem",
"Erode",
"Namakkal",
"Karur",
"Trichy"
];

let index = 0;

function updateDashboard(){

let speed = Math.floor(Math.random()*80)+20;

fuel--;

if(fuel < 0){
fuel = 100;
}

let location = locations[index];

document.getElementById("speed").innerText =
speed + " km/h";

document.getElementById("fuel").innerText =
fuel + "%";

document.getElementById("location").innerText =
location;

let status =
speed > 0 ? "Running" : "Stopped";

let statusElement =
document.getElementById("status");

statusElement.innerText = status;

statusElement.className =
speed > 0 ?
"status-running" :
"status-stopped";

let time =
new Date().toLocaleTimeString();
let row =
`<tr>
<td>${time}</td>
<td>${location}</td>
<td>${speed} km/h</td>
</tr>`;

document.getElementById("history")
.innerHTML = row +
document.getElementById("history").innerHTML;

index = (index + 1) % locations.length;
}

setInterval(updateDashboard,3000);

</script>

</body>
</html>
