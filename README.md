# Real-Time-Public-Transport-Tracking-for-Small-Cities-
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<title>Real-Time Public Transport Tracker</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f4f6f9;
text-align:center;
}

header{
background:#2c3e50;
color:white;
padding:20px;
font-size:28px;
}

.container{
width:350px;
margin:50px auto;
background:white;
padding:25px;
border-radius:10px;
box-shadow:0 0 10px rgba(0,0,0,0.2);
}

input{
width:90%;
padding:10px;
margin:10px;
}

button{
padding:10px 15px;
background:#3498db;
border:none;
color:white;
cursor:pointer;
border-radius:5px;
}

button:hover{
background:#2980b9;
}

#dashboard{
display:none;
width:80%;
margin:auto;
}

table{
width:100%;
border-collapse:collapse;
margin-top:20px;
}

th,td{
border:1px solid #ddd;
padding:10px;
}

th{
background:#3498db;
color:white;
}

.running{
color:green;
font-weight:bold;
}

.delayed{
color:red;
font-weight:bold;
}

</style>

</head>

<body>

<header>Real-Time Public Transport Tracker</header>

<div class="container" id="loginBox">

<h2>User Login</h2>

<input type="text" id="name" placeholder="Enter Name">
<input type="email" id="email" placeholder="Enter Email">
<input type="password" id="password" placeholder="Enter Password">

<br>

<button onclick="login()">Login</button>

</div>

<div id="dashboard">

<h2>Bus Tracking Dashboard</h2>

<p id="welcome"></p>

<table id="busTable">

<tr>
<th>Bus No</th>
<th>Route</th>
<th>Current Location</th>
<th>Status</th>
</tr>

</table>

</div>

<script>

const buses=[

{
busNo:"101",
route:"Central Bus Stand - Market",
location:"Central Bus Stand",
status:"Running"
},

{
busNo:"102",
route:"Railway Station - College",
location:"Railway Station",
status:"Running"
},

{
busNo:"103",
route:"Airport - City Center",
location:"Highway",
status:"Delayed"
}

];

function login(){

let name=document.getElementById("name").value;
let email=document.getElementById("email").value;
let pass=document.getElementById("password").value;

if(name==""||email==""||pass==""){
alert("Please enter all details");
return;
}

localStorage.setItem("userName",name);
localStorage.setItem("email",email);

document.getElementById("loginBox").style.display="none";
document.getElementById("dashboard").style.display="block";

document.getElementById("welcome").innerHTML="Welcome "+name;

loadBuses();
simulateTracking();

}


function loadBuses(){

let table=document.getElementById("busTable");

buses.forEach(bus=>{

let row=table.insertRow();

row.insertCell(0).innerHTML=bus.busNo;
row.insertCell(1).innerHTML=bus.route;
row.insertCell(2).innerHTML=bus.location;

let status=row.insertCell(3);
status.innerHTML=bus.status;

if(bus.status=="Running"){
status.className="running";
}else{
status.className="delayed";
}

});

}


function simulateTracking(){

const locations=[
"City Center",
"Main Road",
"Market Stop",
"Bus Stand",
"College Road",
"Hospital Stop",
"Railway Station",
"Airport Road"
];

setInterval(()=>{

let table=document.getElementById("busTable");

for(let i=1;i<table.rows.length;i++){

let randomLocation=locations[Math.floor(Math.random()*locations.length)];

table.rows[i].cells[2].innerHTML=randomLocation;

}

},5000);

}

</script>

</body>
</html>
