<!DOCTYPE html>
<html lang="en">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>World Challenge 3.0</title>


<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}


body{

background:#030303;
color:white;
min-height:100vh;
display:flex;
justify-content:center;
align-items:center;

}


.app{

width:92%;
max-width:450px;

}


.box{

background:#101010;
border:1px solid #d4af37;
border-radius:28px;
padding:25px;
text-align:center;
box-shadow:0 0 45px rgba(212,175,55,.25);

}



h1{

font-size:36px;
color:#d4af37;

}


.gold{

color:#d4af37;

}


.card{

background:#181818;
border-radius:18px;
padding:18px;
margin-top:15px;

}


.title{

color:#d4af37;
font-size:18px;

}


.timer{

font-size:40px;
color:#00ff99;
margin:20px;

}


button{

width:100%;
padding:16px;
margin-top:15px;
background:#d4af37;
border:0;
border-radius:15px;
font-size:18px;
font-weight:bold;

}


input,select,textarea{

width:100%;
padding:13px;
margin-top:12px;
border-radius:10px;
border:0;

}


textarea{

height:100px;

}


.hidden{

display:none;

}


.badge{

font-size:30px;

}


</style>

</head>


<body>


<div class="app">





<div class="box" id="home">


<h1>
🌍 World Challenge
</h1>


<p>
The World's Biggest Daily Challenge
</p>




<div class="card">


<div class="title">
💰 Today's Reward
</div>


<br>


<h2>
$10,000
</h2>


</div>





<div class="card">


<div class="title">
⏳ Time Left
</div>


<div class="timer" id="timer">

24:00:00

</div>


</div>






<div class="card">


<div class="title">
🎯 Challenge Today
</div>


<br>


Create something amazing from your city.


</div>






<button onclick="showRegister()">

🚀 CREATE ACCOUNT

</button>



<button onclick="showLogin()">

🔐 LOGIN

</button>



</div>









<div class="box hidden" id="register">


<h1>
👤 Register
</h1>



<div class="card">


<input id="regName" placeholder="Full Name">


<select id="regCountry">


<option value="">
Choose Country
</option>


<option>
🇬🇪 Georgia
</option>


<option>
🇺🇸 United States
</option>


<option>
🇬🇧 United Kingdom
</option>


<option>
🇩🇪 Germany
</option>


<option>
🇯🇵 Japan
</option>


<option>
🇫🇷 France
</option>


</select>




<input id="regEmail" placeholder="Email">


<input id="regPass" placeholder="Password" type="password">



<button onclick="register()">

CREATE ACCOUNT

</button>


<p id="regError"></p>


</div>


</div>

<div class="box hidden" id="login">


<h1>
🔐 Login
</h1>


<div class="card">


<input id="loginEmail" placeholder="Email">


<input id="loginPass" placeholder="Password" type="password">



<button onclick="login()">

LOGIN

</button>


<p id="loginError"></p>


</div>


</div>







<div class="box hidden" id="profile">


<h1>
👤 Profile
</h1>



<div class="card">


<div class="badge">
🏅
</div>


<h2 id="profileName">
Player
</h2>


<p id="profileCountry">
🌍 Country
</p>



<br>



<p>
⭐ Level:
<b id="level">1</b>
</p>



<p>
⭐ Points:
<b id="profilePoints">0</b>
</p>



<p>
🎯 Completed:
<b id="completed">0</b>
</p>



</div>



<button onclick="openChallenge()">

🎯 DAILY CHALLENGE

</button>


<button onclick="showRanking()">

🏆 RANKING

</button>


</div>







<div class="box hidden" id="challenge">


<h1>
🎯 Challenge
</h1>



<div class="card">


<div class="title">
Today's Mission
</div>


<br>


Show the world your creativity.


</div>




<div class="card">


<input type="file">


<textarea placeholder="Your description"></textarea>




<button onclick="finishChallenge()">

SUBMIT

</button>


<p id="challengeMessage"></p>


</div>


</div>







<div class="box hidden" id="ranking">


<h1>
🏆 Global Ranking
</h1>



<div class="card">


🥇 Maria 🇺🇸
<br>
⭐ 5000


<br><br>


🥈 Luka 🇬🇪
<br>
⭐ 4200


<br><br>


🥉 Ken 🇯🇵
<br>
⭐ 3900


</div>


</div>





</div>

<script>


let end = new Date();

end.setHours(end.getHours()+24);



function updateTimer(){


let now = new Date();

let diff = end-now;


let h=Math.floor(diff/(1000*60*60));

let m=Math.floor((diff%(1000*60*60))/(1000*60));

let s=Math.floor((diff%(1000*60))/1000);



document.getElementById("timer").innerHTML =

String(h).padStart(2,"0")+":"+
String(m).padStart(2,"0")+":"+
String(s).padStart(2,"0");


}



setInterval(updateTimer,1000);

updateTimer();






function hideAll(){


document.getElementById("home").classList.add("hidden");

document.getElementById("register").classList.add("hidden");

document.getElementById("login").classList.add("hidden");

document.getElementById("profile").classList.add("hidden");

document.getElementById("challenge").classList.add("hidden");

document.getElementById("ranking").classList.add("hidden");


}







function showRegister(){

hideAll();

document.getElementById("register").classList.remove("hidden");

}



function showLogin(){

hideAll();

document.getElementById("login").classList.remove("hidden");

}







function register(){


let user={

name:document.getElementById("regName").value,

country:document.getElementById("regCountry").value,

email:document.getElementById("regEmail").value,

password:document.getElementById("regPass").value,

points:0,

completed:0

};



if(!user.name || !user.email || !user.password){

document.getElementById("regError").innerHTML=
"❌ Fill all fields";

return;

}



localStorage.setItem(

"WC30USER",

JSON.stringify(user)

);



loadProfile();


hideAll();

document.getElementById("profile").classList.remove("hidden");


}








function login(){



let saved=localStorage.getItem("WC30USER");



if(saved){


let user=JSON.parse(saved);



if(user.email==document.getElementById("loginEmail").value &&

user.password==document.getElementById("loginPass").value){



loadProfile();


hideAll();

document.getElementById("profile").classList.remove("hidden");


}

else{


document.getElementById("loginError").innerHTML=

"❌ Wrong login";


}



}


}








function loadProfile(){



let saved=localStorage.getItem("WC30USER");



if(saved){


let user=JSON.parse(saved);



document.getElementById("profileName").innerHTML=
user.name;



document.getElementById("profileCountry").innerHTML=
user.country;



document.getElementById("profilePoints").innerHTML=
user.points;



document.getElementById("completed").innerHTML=
user.completed;



document.getElementById("level").innerHTML=

Math.floor(user.points/100)+1;


}



}








function openChallenge(){


hideAll();


document.getElementById("challenge").classList.remove("hidden");


}







function finishChallenge(){


let saved=localStorage.getItem("WC30USER");



if(saved){


let user=JSON.parse(saved);


user.points+=50;

user.completed+=1;



localStorage.setItem(

"WC30USER",

JSON.stringify(user)

);



loadProfile();


}



document.getElementById("challengeMessage").innerHTML=

"✅ Completed! +50 Points";


}








function showRanking(){


hideAll();


document.getElementById("ranking").classList.remove("hidden");


}






loadProfile();


</script>


</body>

</html>