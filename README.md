
<html lang="en">
<head>
<meta charset="UTF-8">
<title>DSHS School System</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  body { 
    margin: 0; 
    min-height: 70vh; 
    background: url(https://i.ibb.co/XxJDdGth/your-image.png) center center / cover no-repeat fixed; 
    font-family: Arial, sans-serif;
  }
  .signup-link { color: blue; font-weight: bold; cursor: pointer; }
  .signup-link:hover { text-decoration: underline; }
  input, button, textarea, select { 
    width: 100%; 
    padding: 10px; 
    margin-top: 8px; 
    box-sizing: border-box; 
    font-size: 14px;
  }
  button { cursor: pointer; border-radius: 5px; }
  
  .toggle-btn { 
    background: #003366; 
    color: white; 
    font-size: 18px; 
    border: none; 
    position: fixed; 
    top: 12px; 
    left: 12px; 
    z-index: 1000; 
    padding: 10px 15px; 
    border-radius: 6px;
    cursor: pointer;
  }
  .toggle-btn:hover { background: #002244; }
  
  .login { 
    height: 100vh; 
    display: flex; 
    justify-content: center; 
    align-items: center; 
    padding: 20px;
  }
  .box { 
    background: rgba(255,255,255,0.95); 
    padding: 30px; 
    width: 100%; 
    max-width: 400px; 
    border-radius: 10px; 
    box-shadow: 0 10px 30px rgba(0,0,0,0.3); 
    text-align: center; 
  }
  .pass-wrapper { position: relative; }
  .pass-wrapper span { 
    position: absolute; 
    right: 15px; 
    top: 15px; 
    cursor: pointer; 
    font-size: 18px;
  }
  
  .dashboard { display: none; min-height: 100vh; }
  .header { 
    background: rgba(0,51,102,0.95); 
    color: white; 
    padding: 15px; 
    text-align: center; 
    font-size: 16px; 
    position: relative; 
    z-index: 1;
  }
  .container { 
    display: flex; 
    min-height: calc(100vh - 60px); 
    position: relative; 
  }
  
  .menu {
    width: 250px;
    background: rgba(255,255,255,0.98);
    padding: 15px;
    box-shadow: 2px 0 15px rgba(0,0,0,0.2);
    display: flex;
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    z-index: 999;
    transition: transform 0.3s ease;
    transform: translateX(-100%);
    overflow-y: auto;
    padding-top: 60px;
  }
  .menu.show { transform: translateX(0); }
  .menu button {
    background: #f0f0f0;
    color: #333;
    margin-top: 8px;
    font-size: 14px;
    border: 1px solid #ddd;
    border-radius: 6px;
    padding: 12px 10px;
    transition: all 0.2s;
  }
  .menu button:hover { background: #003366; color: white; }
  .logout { 
    margin-top: auto; 
    background: #d9534f !important; 
    color: white !important; 
  }
  
  .content { 
    flex: 1; 
    padding: 20px; 
    display: flex; 
    flex-direction: column; 
    align-items: center; 
    overflow-y: auto; 
  }
  .section { 
    background: rgba(255,255,255,0.95); 
    padding: 20px; 
    border-radius: 8px; 
    width: 100%; 
    max-width: 800px; 
    margin-top: 15px; 
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  }
  
  table { 
    border-collapse: collapse; 
    width: 100%; 
    margin-top: 15px; 
    overflow-x: auto;
  }
  table, th, td { 
    border: 1px solid #ddd; 
    text-align: center; 
    padding: 10px; 
  }
  th { background: #003366; color: white; }
  
  .schedule-box { 
    display: flex; 
    flex-wrap: wrap; 
    gap: 10px; 
    margin-top: 15px; 
  }
  .schedule-box div { 
    flex: 1 1 150px; 
    background: #f5f5f5; 
    border: 1px solid #ddd; 
    padding: 15px; 
    border-radius: 8px; 
    text-align: center; 
  }
  
  .chatbox { 
    border: 1px solid #ddd; 
    padding: 15px; 
    height: 250px; 
    width: 100%; 
    overflow-y: auto; 
    margin-top: 10px; 
    border-radius: 5px; 
    background: white;
  }
  
  .id-card { 
    background: white; 
    border: 2px solid #003366; 
    border-radius: 10px; 
    padding: 15px; 
    width: 100%; 
    max-width: 320px; 
    margin: 10px; 
    display: inline-block; 
    vertical-align: top; 
  }
  .id-card-header { 
    background: #003366; 
    color: white; 
    padding: 12px; 
    text-align: center; 
    border-radius: 8px 8px 0 0; 
    margin: -15px -15px 15px -15px; 
  }
  .id-card-photo { 
    width: 100px; 
    height: 100px; 
    background: #eee; 
    border-radius: 50%; 
    margin: 10px auto; 
    display: flex; 
    align-items: center; 
    justify-content: center; 
    overflow: hidden; 
    border: 3px solid #003366;
  }
  .id-card-photo img { width: 100%; height: 100%; object-fit: cover; }
  .id-card-info { text-align: left; font-size: 13px; }
  
  .attendance-calendar { 
    display: grid; 
    grid-template-columns: repeat(7, 1fr); 
    gap: 5px; 
    margin-top: 15px; 
    overflow-x: auto;
  }
  .attendance-day { 
    padding: 12px 8px; 
    text-align: center; 
    border: 1px solid #ddd; 
    border-radius: 5px; 
    min-width: 40px;
  }
  .attendance-day.present { background: #d4edda; }
  .attendance-day.absent { background: #f8d7da; }
  .attendance-day.header { 
    background: #003366; 
    color: white; 
    font-weight: bold; 
    padding: 10px;
  }
  
  .subject-item { 
    display: flex; 
    align-items: center; 
    padding: 10px; 
    border: 1px solid #ddd; 
    margin: 8px 0; 
    border-radius: 5px; 
    flex-wrap: wrap;
    gap: 10px;
  }
  .subject-item input[type="text"] { 
    flex: 1; 
    min-width: 120px; 
    margin: 0; 
  }
  
  .planner-container { 
    max-height: 400px; 
    overflow-y: auto; 
    padding: 15px; 
    border: 1px solid #ddd; 
    border-radius: 8px; 
    background: #f9f9f9; 
  }
  .planner-section { margin-bottom: 20px; }
  .planner-section h4 { 
    background: #003366; 
    color: white; 
    padding: 10px; 
    margin: 0 0 10px 0; 
    border-radius: 5px 5px 0 0; 
  }
  .planner-item { 
    display: flex; 
    align-items: center; 
    padding: 10px; 
    border: 1px solid #ddd; 
    margin: 5px 0; 
    border-radius: 5px; 
    background: white; 
    flex-wrap: wrap;
    gap: 10px;
  }
  .planner-item input[type="checkbox"] { width: auto; margin: 0; }
  .planner-item.completed { text-decoration: line-through; opacity: 0.6; }
  .planner-item .goal-text { flex: 1; min-width: 150px; }
  .planner-item .goal-time { font-size: 12px; color: #666; }
  .planner-item .alarm-btn { 
    width: auto; 
    padding: 6px 12px; 
    font-size: 12px; 
    background: #003366; 
    color: white; 
  }
  
  .attendance-legend { 
    position: fixed; 
    bottom: 20px; 
    right: 20px; 
    background: white; 
    padding: 15px; 
    border-radius: 8px; 
    box-shadow: 0 2px 15px rgba(0,0,0,0.2); 
    z-index: 100;
    border: 2px solid #003366;
  }
  
  .performance-box {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 20px;
    border-radius: 10px;
    margin: 15px 0;
    text-align: center;
  }
  .performance-stats { display: flex; justify-content: space-around; margin-top: 15px; }
  .stat-item { text-align: center; }
  .stat-number { font-size: 28px; font-weight: bold; }
  .stat-label { font-size: 12px; opacity: 0.9; }
  
  @media (max-width: 768px) {
    .menu { width: 85%; max-width: 300px; }
    .section { padding: 15px; margin-top: 10px; }
    .attendance-legend { position: relative; bottom: auto; right: auto; margin-top: 15px; width: 100%; }
    .schedule-box div { flex: 1 1 100%; }
    table { display: block; overflow-x: auto; white-space: nowrap; }
  }
  
  @media print {
    .menu, .toggle-btn, .header { display: none !important; }
    .id-card { break-inside: avoid; page-break-inside: avoid; border: 2px solid #000; }
  }
</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://unpkg.com/html5-qrcode/html5-qrcode.min.js"></script>
</head>
<body>
  
  <div class="login-wrapper">
  <img src="https://i.ibb.co/F4DpWS4d/logo.png" alt="DSHS Logo" style="display:block; margin: 40px auto 5px; width:180px;">
</div>

<div class="login" id="login">
  <div class="box">
    <h2>Login</h2>
    <input type="text" id="loginUsername" placeholder="Username">
    <div class="pass-wrapper">
      <input type="password" id="loginPassword" placeholder="Password">
      <span onclick="togglePassword()">👁️</span>
    </div>
    <button onclick="login()">Login</button>
    <p id="msg"></p>
    <p style="font-size:13px; margin-top:10px;">Don't have an account yet? <span class="signup-link" onclick="showSignup()">Sign up!</span></p>
  </div>
</div>

<div class="login" id="signup" style="display:none;">
  <div class="box">
    <h2>Student Sign Up</h2>
    <input type="text" id="signupName" placeholder="Full Name">
    <input type="text" id="signupID" placeholder="Student I.D">
    <input type="text" id="signupSection" placeholder="Section">
    <input type="text" id="signupTrack" placeholder="Track">
    <input type="text" id="signupStrand" placeholder="Strand">
    <input type="text" id="signupGradeLevel" placeholder="Grade Level">
    <input type="text" id="signupUsername" placeholder="Username">
    <input type="password" id="signupPass" placeholder="Password">
    <button onclick="submitSignup()">Create Account</button>
    <button onclick="clearSignup()">Clear</button>
    <p style="font-size:13px; margin-top:10px;">Already have an account? <span class="signup-link" onclick="showLogin()">Login</span></p>
  </div>
</div>

<div class="dashboard" id="dashboard">
  <div class="header" id="roleTitle"></div>
  <div class="container">
    <div class="menu" id="menu"></div>
    <div class="content" id="content">
      <img src="https://source.unsplash.com/800x400/?school" alt="School" class="school" style="max-width:100%;border-radius:10px;margin-bottom:20px;">
      <div class="section"><h3>Welcome</h3><p>Select an option from the menu.</p></div>
    </div>
  </div>
</div>

<script>
  //------ HASH PASSWORD ------
function simpleHash(str){
  let hash = 0;
  for(let i=0;i<str.length;i++){
    const char = str.charCodeAt(i);
    hash = ((hash<<5)-hash)+char;
    hash = hash & hash;
  }
  return hash.toString();
}

//------ DATA ------
let role="", currentUser="";
let students = JSON.parse(localStorage.getItem('students')) || [
  {name:"Jibdel",id:"ST001",section:"12-A",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jibdel",password:simpleHash("1234"),approved:true,pic:""},
  {name:"Viennes",id:"ST002",section:"12-B",track:"Academic",strand:"ABM",gradeLevel:"12",username:"viennes",password:simpleHash("5678"),approved:true,pic:""},
  {name:"Jurl",id:"ST003",section:"12-C",track:"Academic",strand:"STEM",gradeLevel:"12",username:"jurl",password:simpleHash("abcd"),approved:true,pic:""}
];
let teachers = JSON.parse(localStorage.getItem('teachers')) || [
  {name:"Mr. Smith",id:"TE001",position:"Teacher III",sectionHandled:"12-A",username:"teacher1",password:simpleHash("teach123")}
];
let parents = JSON.parse(localStorage.getItem('parents')) || [
  {name:"Parent of Jibdel",child:"Jibdel",username:"parentSt001",password:simpleHash("par123")}
];
let subjects = JSON.parse(localStorage.getItem('subjects')) || ["3I's","Genchem 2","P6 2","Perdev","CPAR","Entrepreneurship"];
let scheduleTimes = JSON.parse(localStorage.getItem('scheduleTimes')) || {"3I's":"8:00-9:00","Genchem 2":"9:00-10:00","P6 2":"10:00-11:00","Perdev":"11:45-12:30","CPAR":"12:30-1:00","Entrepreneurship":"1:00-2:00"};
let gradesData = JSON.parse(localStorage.getItem('gradesData')) || {};
if(Object.keys(gradesData).length===0){
  students.forEach(function(s){
    gradesData[s.name]={};
    subjects.forEach(function(sub){ gradesData[s.name][sub]=Math.floor(Math.random()*21)+80; });
  });
}
let attendanceData = JSON.parse(localStorage.getItem('attendanceData')) || {};
if(Object.keys(attendanceData).length===0){
  students.forEach(function(s){ attendanceData[s.name]={}; });
}
let bulletinBoard = JSON.parse(localStorage.getItem('bulletinBoard')) || ["Welcome to the DSHS School System!"];
let plannerData = JSON.parse(localStorage.getItem('plannerData')) || {};
let adminAccount = {name:"Administrator", username:"admin", password:simpleHash("admin123")};

//------ SAVE ------
function saveData(){
  try{
    localStorage.setItem('students', JSON.stringify(students));
    localStorage.setItem('teachers', JSON.stringify(teachers));
    localStorage.setItem('parents', JSON.stringify(parents));
    localStorage.setItem('subjects', JSON.stringify(subjects));
    localStorage.setItem('scheduleTimes', JSON.stringify(scheduleTimes));
    localStorage.setItem('gradesData', JSON.stringify(gradesData));
    localStorage.setItem('attendanceData', JSON.stringify(attendanceData));
    localStorage.setItem('bulletinBoard', JSON.stringify(bulletinBoard));
    localStorage.setItem('plannerData', JSON.stringify(plannerData));
  } catch(e){ alert("Storage error."); }
}

//------ PASSWORD TOGGLE ------
function togglePassword(){
  const p=document.getElementById("loginPassword");
  p.type=(p.type==="password")?"text":"password";
}

//------ LOGIN ------
function login(){
  const username=document.getElementById("loginUsername").value.trim();
  const pass=simpleHash(document.getElementById("loginPassword").value);
  let found=false;

  if(username===adminAccount.username && pass===adminAccount.password){ role="admin"; currentUser=adminAccount.name; found=true; }
  teachers.forEach(function(t){ if(username===t.username && pass===t.password){ role="teacher"; currentUser=t.name; found=true; }});
  students.forEach(function(s){ if(username===s.username && pass===s.password){ if(s.approved){ role="student"; currentUser=s.name; found=true; } else { document.getElementById("msg").innerText="Account not approved yet"; return; } }});
  parents.forEach(function(p){ if(username===p.username && pass===p.password){ role="parent"; currentUser=p.child; found=true; }});

  if(!found){ document.getElementById("msg").innerText="Invalid login or not approved yet"; return; }
  document.getElementById("login").style.display="none";
  document.getElementById("signup").style.display="none";
  document.getElementById("dashboard").style.display="block";
  loadDashboard();
}

//------ DASHBOARD ------
function loadDashboard(){
  document.getElementById("roleTitle").innerText = role.toUpperCase()+" DASHBOARD";
  const menu=document.getElementById("menu"); menu.innerHTML="";
  
  let toggleBtn = document.querySelector(".toggle-btn");
  if(!toggleBtn){
    toggleBtn = document.createElement("button");
    toggleBtn.className = "toggle-btn";
    toggleBtn.innerText = "☰ Menu";
    document.body.appendChild(toggleBtn);
  }
  toggleBtn.onclick = function() {
    document.getElementById("menu").classList.toggle("show");
  };

  let items = ["Attendance","Subject Schedule","My Info","Bulletin Board","School Map"];
  if(role==="teacher") items = ["Attendance","Subject Schedule","My Info","Bulletin Board","Grades","Parent Chat","My Planner","Emergency Numbers","School Map"];
  else if(role==="student") items = ["Attendance","Subject Schedule","My Info","Bulletin Board","Grades","QR Code","Emergency Numbers","School Map"];
  else if(role==="parent") items = ["Child Attendance","Child Grades","Child Schedule","My Info","Bulletin Board","Teacher Chat","Emergency Numbers","School Map"];
  else if(role==="admin") items = ["Student Approval","Create Teacher","All Students","Manage Users","Bulletin Board","Emergency Numbers","School Map"];

  createMenu(items);
  const logoutBtn=document.createElement("button"); logoutBtn.innerText="⬅ Logout"; logoutBtn.className="logout"; logoutBtn.onclick=logout; menu.appendChild(logoutBtn);
}

//------ CREATE MENU ------
function createMenu(items){
  const menu=document.getElementById("menu");
  items.forEach(function(item){
    const btn=document.createElement("button");
    btn.innerText=item;
    btn.onclick=function() {
      document.getElementById("menu").classList.remove("show");
      loadSection(item);
    };
    menu.appendChild(btn);
  });
}

//------ LOGOUT ------
function logout(){
  role=""; currentUser="";
  document.getElementById("dashboard").style.display="none";
  document.getElementById("login").style.display="flex";
  let toggleBtn = document.querySelector(".toggle-btn");
  if(toggleBtn) toggleBtn.remove();
}

//------ SHOW SIGNUP/LOGIN ------
function showSignup(){ document.getElementById("login").style.display="none"; document.getElementById("signup").style.display="flex"; }
function showLogin(){ document.getElementById("signup").style.display="none"; document.getElementById("login").style.display="flex"; }
function clearSignup(){ ["signupName","signupID","signupSection","signupTrack","signupStrand","signupGradeLevel","signupUsername","signupPass"].forEach(function(id){ document.getElementById(id).value=""; }); }

//------ SUBMIT SIGNUP ------
function submitSignup(){
  let name=document.getElementById("signupName").value.trim();
  let id=document.getElementById("signupID").value.trim();
  let section=document.getElementById("signupSection").value.trim();
  let track=document.getElementById("signupTrack").value.trim();
  let strand=document.getElementById("signupStrand").value.trim();
  let gradeLevel=document.getElementById("signupGradeLevel").value.trim();
  let username=document.getElementById("signupUsername").value.trim();
  let password=document.getElementById("signupPass").value.trim();
  if(!name||!id||!section||!track||!strand||!gradeLevel||!username||!password){ alert("All fields required!"); return; }
  if(password.length<6){ alert("Password must be at least 6 characters!"); return; }
  if(students.find(function(s){ return s.username===username; }) || students.find(function(s){ return s.id===id; })){ alert("Username or ID already exists!"); return; }

  students.push({name,id,section,track,strand,gradeLevel,username,password:simpleHash(password),approved:false,pic:""});
  gradesData[name]={}; subjects.forEach(function(sub){ gradesData[name][sub]=0; });
  attendanceData[name]={}; saveData();
  alert("Signup successful! Wait for admin approval.");
  clearSignup(); showLogin();
}

//------ LOAD SECTION ------
function loadSection(tab){
  const content=document.getElementById("content");
  content.innerHTML="";
  const section=document.createElement("div"); section.className="section";

  //------ ATTENDANCE ------
  if(tab==="Attendance" || tab==="Child Attendance"){
    section.innerHTML="<h3>Attendance</h3>";
    
    let studentName = currentUser;
    if(role === "teacher") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "attendanceStudentSelect";
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
        const opt = document.createElement("option");
        opt.value = s.name;
        opt.innerText = s.name;
        selectStudent.appendChild(opt);
      });
      section.appendChild(selectStudent);
      studentName = selectStudent.value;
      
      selectStudent.onchange = function() {
        studentName = this.value;
        renderAttendanceCalendar(section, studentName);
      };
    } else if(role === "parent") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "attendanceStudentSelect";
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) {
          const opt = document.createElement("option");
          opt.value = child.name;
          opt.innerText = child.name;
          selectStudent.appendChild(opt);
          studentName = child.name;
        }
      }
      section.appendChild(selectStudent);
    }
    
    const dateInput = document.createElement("input");
    dateInput.type = "month";
    dateInput.value = new Date().toISOString().split("T")[0].substring(0, 7);
    section.appendChild(dateInput);
    
    const qrDiv = document.createElement("div");
    qrDiv.id = "scanner-container";
    section.appendChild(qrDiv);
    
    const resultDiv = document.createElement("div");
    resultDiv.id = "scanner-result";
    section.appendChild(resultDiv);
    
    content.appendChild(section);
    
    renderAttendanceCalendar(section, studentName);
    
    //------ QR SCANNER FOR TEACHERS ------
    if(role === "teacher") {
      const scannerDiv = document.createElement("div");
      scannerDiv.id = "qr-scanner";
      scannerDiv.style.marginTop = "20px";
      section.appendChild(scannerDiv);
      
      setTimeout(function(){
        try {
          const html5QrCode = new Html5Qrcode("qr-scanner");
          html5QrCode.start(
            { facingMode: "environment" },
            { fps: 10, qrbox: 250 },
            function(decodedText){
              const parts = decodedText.split("-");
              const scannedStudent = parts[0];
              const today = new Date().toISOString().split("T")[0];
              
              if(attendanceData[scannedStudent]) {
                attendanceData[scannedStudent][today] = "P";
                saveData();
                resultDiv.innerHTML = "<span style='color:green;'>Marked " + scannedStudent + " present on " + today + "</span>";
                renderAttendanceCalendar(section, studentName);
              }
              html5QrCode.stop();
            },
            function(errorMessage){}
          ).catch(function(err){
            console.log("Scanner error:", err);
          });
        } catch(e) {
          console.log("Scanner initialization error:", e);
        }
      }, 500);
    }
  }
  
    //------ GRADES ------
  if(tab === "Grades" || tab === "Child Grades"){
    section.innerHTML = "<h3>Grades</h3>";
    
    let studentName = currentUser;
    if(role === "teacher") {
      const selectStudent = document.createElement("select");
      selectStudent.id = "gradesStudentSelect";
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
        const opt = document.createElement("option");
        opt.value = s.name;
        opt.innerText = s.name;
        selectStudent.appendChild(opt);
      });
      section.appendChild(selectStudent);
      studentName = selectStudent.value;
      
      selectStudent.onchange = function() {
        studentName = this.value;
        renderGradesTable(section, studentName);
      };
    } else if(role === "parent") {
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) studentName = child.name;
      }
    }
    
    content.appendChild(section);
    renderGradesTable(section, studentName);
  }
  
  //------ SUBJECT SCHEDULE ------
  if(tab === "Subject Schedule" || tab === "Child Schedule"){
    section.innerHTML = "<h3>Subject Schedule</h3>";
    
    let studentName = currentUser;
    if(role === "parent") {
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) studentName = child.name;
      }
    }
    
    const scheduleBox = document.createElement("div");
    scheduleBox.className = "schedule-box";
    
    subjects.forEach(function(sub){
      const div = document.createElement("div");
      const time = scheduleTimes[sub] || "TBA";
      div.innerHTML = "<strong>" + sub + "</strong><br>" + time;
      scheduleBox.appendChild(div);
    });
    section.appendChild(scheduleBox);
    
    if(role === "teacher" || role === "admin") {
      section.innerHTML += "<h4>Manage Subjects</h4>";
      subjects.forEach(function(sub, index){
        const item = document.createElement("div");
        item.className = "subject-item";
        item.innerHTML = '<input type="text" value="' + sub + '" onchange="updateSubject(' + index + ', this.value)">' +
          '<input type="text" value="' + (scheduleTimes[sub] || '') + '" placeholder="Time" onchange="updateScheduleTime(\'' + sub + '\', this.value)">' +
          '<button onclick="deleteSubject(' + index + ')" style="width:auto;background:#dc3545;color:white;">Delete</button>';
        section.appendChild(item);
      });
      
      const addDiv = document.createElement("div");
      addDiv.className = "subject-item";
      addDiv.innerHTML = '<input type="text" id="newSubjectName" placeholder="New Subject">' +
        '<input type="text" id="newSubjectTime" placeholder="Time">' +
        '<button onclick="addSubject()" style="width:auto;background:#28a745;color:white;">Add</button>';
      section.appendChild(addDiv);
    }
  }

  //------ QR CODE ------
  if(tab === "QR Code" && role === "student"){
    section.innerHTML = "<h3>Your QR Code</h3>";
    const qrDiv = document.createElement("div");
    qrDiv.id = "qr-code";
    section.appendChild(qrDiv);
    new QRCode(qrDiv, {
      text: currentUser + "-" + new Date().toISOString().split("T")[0],
      width: 200,
      height: 200
    });
    section.innerHTML += "<p>Scan this QR code for attendance</p>";
    
    //------ PERFORMANCE BOX ------
    const perfBox = document.createElement("div");
    perfBox.className = "performance-box";
    const totalDays = Object.keys(attendanceData[currentUser] || {}).length;
    const presentDays = Object.values(attendanceData[currentUser] || {}).filter(function(s){ return s === "P"; }).length;
    const absentDays = totalDays - presentDays;
    const percentage = totalDays > 0 ? Math.round((presentDays / totalDays) * 100) : 0;
    
    perfBox.innerHTML = "<h3>Your Attendance Performance</h3>" +
      "<div class='performance-stats'>" +
      "<div class='stat-item'><div class='stat-number'>" + presentDays + "</div><div class='stat-label'>Present</div></div>" +
      "<div class='stat-item'><div class='stat-number'>" + absentDays + "</div><div class='stat-label'>Absent</div></div>" +
      "<div class='stat-item'><div class='stat-number'>" + percentage + "%</div><div class='stat-label'>Rate</div></div>" +
      "</div>";
    section.appendChild(perfBox);
  }

  //------ CHAT ------
  if(tab === "Parent Chat" || tab === "Teacher Chat" || tab === "E-Motion"){
    section.innerHTML = "<h3>" + tab + "</h3>";
    
    if(tab === "Parent Chat" && role === "teacher") {
      section.innerHTML += "<label>Select Parent:</label>";
      const parentSelect = document.createElement("select");
      parentSelect.id = "chatParentSelect";
      
      const teacher = teachers.find(function(t){ return t.name === currentUser; });
      if(teacher) {
        students.filter(function(s){ return s.section === teacher.sectionHandled; }).forEach(function(s){
          const parent = parents.find(function(p){ return p.child === s.name; });
          if(parent) {
            const opt = document.createElement("option");
            opt.value = parent.username;
            opt.innerText = parent.name;
            parentSelect.appendChild(opt);
          }
        });
      }
      section.appendChild(parentSelect);
    }
    
    if(tab === "Teacher Chat" && role === "parent") {
      section.innerHTML += "<label>Select Teacher:</label>";
      const teacherSelect = document.createElement("select");
      teacherSelect.id = "chatTeacherSelect";
      
      const parent = parents.find(function(p){ return p.child === currentUser; });
      if(parent) {
        const child = students.find(function(s){ return s.name === parent.child; });
        if(child) {
          teachers.filter(function(t){ return t.sectionHandled === child.section; }).forEach(function(t){
            const opt = document.createElement("option");
            opt.value = t.username;
            opt.innerText = t.name;
            teacherSelect.appendChild(opt);
          });
        }
      }
      section.appendChild(teacherSelect);
    }
    
    const chatbox = document.createElement("div");
    chatbox.id = "chatbox";
    chatbox.className = "chatbox";
    chatbox.innerHTML = "<p>Chat messages will appear here...</p>";
    section.appendChild(chatbox);
    
    const input = document.createElement("input");
    input.type = "text";
    input.id = "chatInput";
    input.placeholder = "Type your message...";
    section.appendChild(input);
    
    const sendBtn = document.createElement("button");
    sendBtn.innerText = "Send";
    sendBtn.onclick = function() { sendChatMessage(tab); };
    section.appendChild(sendBtn);
  }

  //------ MY INFO ------
  if(tab === "My Info"){
    section.innerHTML = "<h3>My Information</h3>";
    
    let user = null;
    
    if(role === "student") {
      user = students.find(function(s){ return s.name === currentUser; });
    } else if(role === "teacher") {
      user = teachers.find(function(t){ return t.name === currentUser; });
    } else if(role === "parent") {
      user = parents.find(function(p){ return p.child === currentUser; });
    } else if(role === "admin") {
      user = adminAccount;
    }
    
    if(user) {
      section.innerHTML += '<div style="text-align:center;margin-bottom:15px;">' +
        '<div class="id-card-photo" style="width:100px;height:100px;margin:0 auto 10px;">' +
        '<img id="profilePic" src="' + (user.pic || '') + '" alt="Profile Photo" onerror="this.src=\'https://via.placeholder.com/100\'">' +
        '</div>' +
        '<input type="file" id="uploadPic" accept="image/*" style="width:auto;">' +
        '<button onclick="uploadProfilePhoto()" style="width:auto;background:#003366;color:white;">Upload Photo</button>' +
        '</div>' +
        '<div class="id-card-info">' +
        '<p><strong>Name:</strong> ' + user.name + '</p>' +
        '<p><strong>ID:</strong> ' + (user.id || '-') + '</p>' +
        '<p><strong>Username:</strong> ' + (user.username || '-') + '</p>' +
        '<p><strong>Section:</strong> ' + (user.section || user.sectionHandled || '-') + '</p>' +
        '<p><strong>Track:</strong> ' + (user.track || '-') + '</p>' +
        '<p><strong>Strand:</strong> ' + (user.strand || '-') + '</p>' +
        '<p><strong>Grade Level:</strong> ' + (user.gradeLevel || '-') + '</p>' +
        '<p><strong>Position:</strong> ' + (user.position || '-') + '</p>' +
        '</div>';
    } else {
      section.innerHTML += "<p>User information not found.</p>";
    }
  }

  //------ BULLETIN BOARD ------
  if(tab === "Bulletin Board"){
    section.innerHTML = "<h3>Bulletin Board</h3>";
    
    const board = document.createElement("div");
    bulletinBoard.forEach(function(msg, index){
      const msgDiv = document.createElement("div");
      msgDiv.style.padding = "15px";
      msgDiv.style.borderBottom = "1px solid #ddd";
      msgDiv.style.marginBottom = "10px";
      msgDiv.innerHTML = "<p>" + msg + "</p>";
      
      if(role === "teacher" || role === "admin") {
        const deleteBtn = document.createElement("button");
        deleteBtn.innerText = "Delete";
        deleteBtn.style.width = "auto";
        deleteBtn.style.background = "#dc3545";
        deleteBtn.style.color = "white";
        deleteBtn.style.padding = "6px 12px";
        deleteBtn.onclick = function() {
          bulletinBoard.splice(index, 1);
          saveData();
          loadSection("Bulletin Board");
        };
        msgDiv.appendChild(deleteBtn);
      }
      
      board.appendChild(msgDiv);
    });
    section.appendChild(board);
    
    if(role === "teacher" || role === "admin") {
      const newMsg = document.createElement("input");
      newMsg.id = "newAnnouncement";
      newMsg.placeholder = "Type new announcement...";
      section.appendChild(newMsg);
      
      const addBtn = document.createElement("button");
      addBtn.innerText = "Add Announcement";
      addBtn.style.background = "#003366";
      addBtn.style.color = "white";
      addBtn.onclick = function() {
        if(newMsg.value.trim()) {
          bulletinBoard.push(newMsg.value.trim());
          saveData();
          loadSection("Bulletin Board");
        }
      };
      section.appendChild(addBtn);
    }
  }
  
  //------ ADMIN FUNCTIONS ------
  if(role === "admin"){
    if(tab === "Student Approval"){
      section.innerHTML = "<h3>Approve Students</h3>";
      const pendingStudents = students.filter(function(s){ return !s.approved; });
      
      if(pendingStudents.length === 0) {
        section.innerHTML += "<p>No pending approvals.</p>";
      } else {
        pendingStudents.forEach(function(s){
          const div = document.createElement("div");
          div.style.padding = "15px";
          div.style.border = "1px solid #ddd";
          div.style.marginBottom = "10px";
          div.style.borderRadius = "8px";
          div.innerHTML = '<p><strong>Name:</strong> ' + s.name + '</p>' +
            '<p><strong>ID:</strong> ' + s.id + '</p>' +
            '<p><strong>Section:</strong> ' + s.section + '</p>' +
            '<button onclick="approveStudent(\'' + s.id + '\')" style="background:#28a745;color:white;width:auto;padding:10px 20px;margin-right:10px;">Approve</button>' +
            '<button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:10px 20px;">Delete</button>';
          section.appendChild(div);
        });
      }
    }
    
    if(tab === "Create Teacher"){
      section.innerHTML = "<h3>Create Teacher Account</h3>";
      section.innerHTML += '<input type="text" id="newTeacherName" placeholder="Full Name">' +
        '<input type="text" id="newTeacherID" placeholder="Teacher ID">' +
        '<input type="text" id="newTeacherPosition" placeholder="Position">' +
        '<input type="text" id="newTeacherSection" placeholder="Section Handled">' +
        '<input type="text" id="newTeacherUsername" placeholder="Username">' +
        '<input type="password" id="newTeacherPassword" placeholder="Password">' +
        '<button onclick="createTeacher()" style="background:#003366;color:white;">Create Teacher</button>';
    }
    
    if(tab === "All Students"){
      section.innerHTML = "<h3>All Students</h3>";
      
      const filterSection = document.createElement("select");
      filterSection.id = "filterSection";
      filterSection.innerHTML = "<option value='all'>All Sections</option>";
      const sections = [...new Set(students.map(function(s){ return s.section; }))];
      sections.forEach(function(sec){
        const opt = document.createElement("option");
        opt.value = sec;
        opt.innerText = sec;
        filterSection.appendChild(opt);
      });
      section.appendChild(filterSection);
      
      const printBtn = document.createElement("button");
      printBtn.innerText = "Print ID Cards";
      printBtn.style.background = "#28a745";
      printBtn.style.color = "white";
      printBtn.style.margin = "10px 5px";
      printBtn.style.padding = "12px 20px";
      printBtn.onclick = function(){ window.print(); };
      section.appendChild(printBtn);
      
      const studentsContainer = document.createElement("div");
      studentsContainer.id = "studentsContainer";
      section.appendChild(studentsContainer);
      
      filterSection.onchange = function(){
        renderStudentsBySection(studentsContainer, this.value);
      };
      
      renderStudentsBySection(studentsContainer, "all");
    }
    
    if(tab === "Manage Users"){
      section.innerHTML = "<h3>Manage Users</h3>";
      
      //------ STUDENTS MANAGEMENT ------
      section.innerHTML += "<h4>Students</h4>";
      const studentsTable = document.createElement("table");
      studentsTable.innerHTML = "<tr><th>Name</th><th>ID</th><th>Section</th><th>Action</th></tr>";
      students.forEach(function(s){
        const tr = document.createElement("tr");
        tr.innerHTML = '<td>' + s.name + '</td><td>' + s.id + '</td><td>' + s.section + '</td>' +
          '<td><button onclick="deleteStudent(\'' + s.id + '\')" style="background:#dc3545;color:white;width:auto;padding:5px 10px;">Delete</button></td>';
        studentsTable.appendChild(tr);
      });
      section.appendChild(studentsTable);
      
      //------ TEACHERS MANAGEMENT ------
      section.innerHTML += "<h4 style='margin-top:20px;'>Teachers</h4>";
      const teachersTable = document.createElement("table");
      teachersTable.innerHTML = "<tr><th>Name</th><th>ID</th><th>Section</th><th>Action</th></tr>";
      teachers.forEach(function(t){
        const tr = document.createElement("tr");
        tr.innerHTML = '<td>' + t.name + '</td><td>' + t.id + '</td><td>' + t.sectionHandled + '</td>' +
          '<td><button onclick="deleteTeacher(\'' + t.id + '\')" style="background:#dc3545;color:white;width:auto;padding:5px 10px;">Delete</button></td>';
        teachersTable.appendChild(tr);
      });
      section.appendChild(teachersTable);
    }
  }
  
    //------ MY PLANNER (TEACHER ONLY) ------
  if(tab === "My Planner" && role === "teacher"){
    section.innerHTML = "<h3>My Planner</h3>";
    
    if(!plannerData[currentUser]) {
      plannerData[currentUser] = { daily: [], weekly: [], monthly: [] };
    }
    
    const plannerContainer = document.createElement("div");
    plannerContainer.className = "planner-container";
    
    //------ DAILY GOALS ------
    const dailySection = document.createElement("div");
    dailySection.className = "planner-section";
    dailySection.innerHTML = "<h4>Daily Goals</h4>";
    plannerData[currentUser].daily.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'daily\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button class="alarm-btn" onclick="setAlarm(\'' + goal.time + '\')">⏰</button>' +
        '<button onclick="deletePlannerGoal(\'daily\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:4px 8px;">×</button>';
      dailySection.appendChild(item);
    });
    const dailyInput = document.createElement("div");
    dailyInput.innerHTML = '<input type="text" id="dailyGoalInput" placeholder="Add daily goal...">' +
      '<input type="time" id="dailyGoalTime">' +
      '<button onclick="addPlannerGoal(\'daily\')" style="width:auto;background:#28a745;color:white;">Add</button>';
    dailySection.appendChild(dailyInput);
    plannerContainer.appendChild(dailySection);
    
    //------ WEEKLY GOALS ------
    const weeklySection = document.createElement("div");
    weeklySection.className = "planner-section";
    weeklySection.innerHTML = "<h4>Weekly Goals</h4>";
    plannerData[currentUser].weekly.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'weekly\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button class="alarm-btn" onclick="setAlarm(\'' + goal.time + '\')">⏰</button>' +
        '<button onclick="deletePlannerGoal(\'weekly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:4px 8px;">×</button>';
      weeklySection.appendChild(item);
    });
    const weeklyInput = document.createElement("div");
    weeklyInput.innerHTML = '<input type="text" id="weeklyGoalInput" placeholder="Add weekly goal...">' +
      '<input type="date" id="weeklyGoalDate">' +
      '<button onclick="addPlannerGoal(\'weekly\')" style="width:auto;background:#28a745;color:white;">Add</button>';
    weeklySection.appendChild(weeklyInput);
    plannerContainer.appendChild(weeklySection);
    
    //------ MONTHLY GOALS ------
    const monthlySection = document.createElement("div");
    monthlySection.className = "planner-section";
    monthlySection.innerHTML = "<h4>Monthly Goals</h4>";
    plannerData[currentUser].monthly.forEach(function(goal, index){
      const item = document.createElement("div");
      item.className = "planner-item" + (goal.completed ? " completed" : "");
      item.innerHTML = '<input type="checkbox"' + (goal.completed ? " checked" : "") + ' onchange="togglePlannerGoal(\'monthly\', ' + index + ')">' +
        '<span class="goal-text">' + goal.text + '</span>' +
        '<span class="goal-time">' + (goal.time || "") + '</span>' +
        '<button class="alarm-btn" onclick="setAlarm(\'' + goal.time + '\')">⏰</button>' +
        '<button onclick="deletePlannerGoal(\'monthly\', ' + index + ')" style="width:auto;background:#dc3545;color:white;padding:4px 8px;">×</button>';
      monthlySection.appendChild(item);
    });
    const monthlyInput = document.createElement("div");
    monthlyInput.innerHTML = '<input type="text" id="monthlyGoalInput" placeholder="Add monthly goal...">' +
      '<input type="date" id="monthlyGoalDate">' +
      '<button onclick="addPlannerGoal(\'monthly\')" style="width:auto;background:#28a745;color:white;">Add</button>';
    monthlySection.appendChild(monthlyInput);
    plannerContainer.appendChild(monthlySection);
    
    section.appendChild(plannerContainer);
  }
  
  //------ EMERGENCY NUMBERS ------
  if(tab === "Emergency Numbers"){
    section.innerHTML = "<h3>Emergency Numbers</h3>";
    const numbers = [
      {name:"PNP DUMINGAG", num:"099859558677"},
      {name:"BFP DUMINGAG", num:"09300459871"},
      {name:"LGU DUMINGAG", num:"09482121024"},
      {name:"MDRRMO DUMINGAG", num:"09098046609"}
    ];
    numbers.forEach(function(n){
      const div = document.createElement("div");
      div.style.margin = "10px 0";
      div.innerHTML = '<a href="tel:' + n.num + '">' + n.name + ' - ' + n.num + '</a>';
      section.appendChild(div);
    });
  }
  
  //------ SCHOOL MAP ------
  if(tab === "School Map"){
    section.innerHTML = "<h3>School Map</h3>";
    section.innerHTML += '<div style="background:#f5f5f5;padding:20px;border-radius:10px;text-align:center;">' +
      '<h4>DSHS Campus Layout</h4>' +
      '<p><strong>Building A</strong> - Main Entrance & Administration</p>' +
      '<p><strong>Building B</strong> - Classrooms 12-A, 12-B, 12-C</p>' +
      '<p><strong>Building C</strong> - Science Laboratory</p>' +
      '<p><strong>Building D</strong> - Library & Computer Room</p>' +
      '<p><strong>Building E</strong> - Faculty Room</p>' +
      '<p><strong>Gymnasium</strong> - Physical Education Activities</p>' +
      '<p><strong>Cafeteria</strong> - Student Lounge</p>' +
      '<p><strong>Guidance Office</strong> - Counseling Services</p>' +
      '</div>';
  }
  
  content.appendChild(section);
}

//------ RENDER ATTENDANCE CALENDAR ------
function renderAttendanceCalendar(container, studentName) {
  const existingCalendar = document.getElementById("attendanceCalendar");
  if(existingCalendar) existingCalendar.remove();
  
  const calendar = document.createElement("div");
  calendar.id = "attendanceCalendar";
  calendar.className = "attendance-calendar";
  
  const days = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
  days.forEach(function(day){
    const div = document.createElement("div");
    div.className = "attendance-day header";
    div.innerText = day;
    calendar.appendChild(div);
  });
  
  const dateInput = document.querySelector('input[type="month"]');
  const selectedDate = dateInput ? dateInput.value : new Date().toISOString().split("T")[0].substring(0, 7);
  const yearMonth = selectedDate.split("-");
  const year = yearMonth[0];
  const month = yearMonth[1];
  
  const daysInMonth = new Date(year, month, 0).getDate();
  const firstDay = new Date(year, month - 1, 1).getDay();
  
  for(let i = 0; i < firstDay; i++) {
    const div = document.createElement("div");
    div.className = "attendance-day";
    div.style.background = "#f9f9f9";
    calendar.appendChild(div);
  }
  
  for(let day = 1; day <= daysInMonth; day++) {
    const dateStr = year + "-" + month.padStart(2, '0') + "-" + day.toString().padStart(2, '0');
    const div = document.createElement("div");
    div.className = "attendance-day";
    div.innerText = day;
    
    const status = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
    if(status === "P") {
      div.classList.add("present");
      div.innerHTML += " ✓";
    } else if(status === "A") {
      div.classList.add("absent");
      div.innerHTML += " ✗";
    }
    
    div.onclick = function(){
      if(role === "teacher" || role === "admin") {
        const currentStatus = attendanceData[studentName] ? attendanceData[studentName][dateStr] : null;
        if(currentStatus === "P") {
          attendanceData[studentName][dateStr] = "A";
        } else if(currentStatus === "A") {
          delete attendanceData[studentName][dateStr];
        } else {
          attendanceData[studentName][dateStr] = "P";
        }
        saveData();
        renderAttendanceCalendar(container, studentName);
      }
    };
    
    calendar.appendChild(div);
  }
  
  container.appendChild(calendar);
  
  //------ LEGEND BOX ------
  const legend = document.createElement("div");
  legend.className = "attendance-legend";
  legend.innerHTML = "<p><strong>Legend:</strong></p>" +
    "<p style='color:green;'>✓ Present</p>" +
    "<p style='color:red;'>✗ Absent</p>" +
    "<p style='font-size:11px;color:#666;'>" + ((role === "teacher" || role === "admin") ? "Click to toggle" : "View only") + "</p>";
  container.appendChild(legend);
}

//------ RENDER GRADES TABLE ------
function renderGradesTable(container, studentName) {
  const existingTable = document.getElementById("gradesTable");
  if(existingTable) existingTable.remove();
  
  const table = document.createElement("table");
  table.id = "gradesTable";
  table.innerHTML = "<tr><th>Subject</th><th>Grade</th><th>Status</th></tr>";
  
  let total = 0;
  let count = 0;
  
  subjects.forEach(function(sub){
    const tr = document.createElement("tr");
    const grade = gradesData[studentName] ? gradesData[studentName][sub] : 0;
    total += grade;
    count++;
    
    let status = "Passing";
    if(grade < 75) status = "Needs Improvement";
    
    const editable = (role === "teacher" || role === "admin") ? "contenteditable" : "";
    const onblur = (role === "teacher" || role === "admin") ? " onblur=\"updateGrade('" + studentName + "', '" + sub + "', this.innerText)\"" : "";
    
    tr.innerHTML = "<td>" + sub + "</td><td " + editable + onblur + ">" + grade + "</td><td style='color:" + (grade >= 75 ? 'green' : 'red') + "'>" + status + "</td>";
    table.appendChild(tr);
  });
  
  const avgRow = document.createElement("tr");
  avgRow.innerHTML = "<td><strong>Average</strong></td><td><strong>" + (count > 0 ? (total / count).toFixed(2) : 0) + "</strong></td><td></td>";
  table.appendChild(avgRow);
  
  container.appendChild(table);
}

//------ RENDER STUDENTS BY SECTION ------
function renderStudentsBySection(container, sectionFilter) {
  container.innerHTML = "";
  
  let filteredStudents = students;
  if(sectionFilter !== "all") {
    filteredStudents = students.filter(function(s){ return s.section === sectionFilter; });
  }
  
  filteredStudents.forEach(function(s){
    const idCard = document.createElement("div");
    idCard.className = "id-card";
    idCard.innerHTML = '<div class="id-card-header"><h3 style="margin:0;">DSHS</h3><p style="margin:0;font-size:12px;">Student ID Card</p></div>' +
      '<div class="id-card-photo"><img src="' + (s.pic || 'https://via.placeholder.com/80') + '" alt="Photo" onerror="this.src=\'https://via.placeholder.com/80\'"></div>' +
      '<div class="id-card-info"><p><strong>Name:</strong> ' + s.name + '</p><p><strong>ID No:</strong> ' + s.id + '</p>' +
      '<p><strong>Section:</strong> ' + s.section + '</p><p><strong>Track:</strong> ' + s.track + '</p>' +
      '<p><strong>Strand:</strong> ' + s.strand + '</p><p><strong>Grade:</strong> ' + s.gradeLevel + '</p></div>' +
      '<div id="qr-' + s.id + '" style="text-align:center;margin-top:10px;"></div>';
    
    container.appendChild(idCard);
    
    setTimeout(function(){
      new QRCode(document.getElementById("qr-" + s.id), {
        text: s.name + "-" + s.id,
        width: 60,
        height: 60
      });
    }, 100);
  });
}

//------ APPROVE STUDENT ------
function approveStudent(id) {
  const student = students.find(function(s){ return s.id === id; });
  if(student) {
    student.approved = true;
    saveData();
    alert(student.name + " has been approved!");
    loadSection("Student Approval");
  }
}

//------ DELETE STUDENT ------
function deleteStudent(id) {
  const student = students.find(function(s){ return s.id === id; });
  if(student) {
    if(confirm("Are you sure you want to delete " + student.name + "?")) {
      students = students.filter(function(s){ return s.id !== id; });
      delete gradesData[student.name];
      delete attendanceData[student.name];
      saveData();
      alert(student.name + " has been deleted.");
      loadSection("Student Approval");
    }
  }
}

//------ DELETE TEACHER ------
function deleteTeacher(id) {
  const teacher = teachers.find(function(t){ return t.id === id; });
  if(teacher) {
    if(confirm("Are you sure you want to delete " + teacher.name + "?")) {
      teachers = teachers.filter(function(t){ return t.id !== id; });
      saveData();
      alert(teacher.name + " has been deleted.");
      loadSection("Manage Users");
    }
  }
}

//------ CREATE TEACHER ------
function createTeacher() {
  const name = document.getElementById("newTeacherName").value.trim();
  const id = document.getElementById("newTeacherID").value.trim();
  const position = document.getElementById("newTeacherPosition").value.trim();
  const section = document.getElementById("newTeacherSection").value.trim();
  const username = document.getElementById("newTeacherUsername").value.trim();
  const password = document.getElementById("newTeacherPassword").value.trim();
  
  if(!name || !username || !password || !section) {
    alert("Please fill in all required fields!");
    return;
  }
  
  if(teachers.find(function(t){ return t.username === username; })) {
    alert("Username already exists!");
    return;
  }
  
  teachers.push({
    name: name,
    id: id,
    position: position,
    sectionHandled: section,
    username: username,
    password: simpleHash(password)
  });
  
  saveData();
  alert("Teacher account created successfully!");
  
  document.getElementById("newTeacherName").value = "";
  document.getElementById("newTeacherID").value = "";
  document.getElementById("newTeacherPosition").value = "";
  document.getElementById("newTeacherSection").value = "";
  document.getElementById("newTeacherUsername").value = "";
  document.getElementById("newTeacherPassword").value = "";
}

//------ UPDATE SUBJECT ------
function updateSubject(index, newValue) {
  const oldValue = subjects[index];
  subjects[index] = newValue;
  
  if(scheduleTimes[oldValue]) {
    scheduleTimes[newValue] = scheduleTimes[oldValue];
    delete scheduleTimes[oldValue];
  }
  
  students.forEach(function(s){
    if(gradesData[s.name] && gradesData[s.name][oldValue] !== undefined) {
      gradesData[s.name][newValue] = gradesData[s.name][oldValue];
      delete gradesData[s.name][oldValue];
    }
  });
  
  saveData();
}

//------ UPDATE SCHEDULE TIME ------
function updateScheduleTime(subject, time) {
  scheduleTimes[subject] = time;
  saveData();
}

//------ DELETE SUBJECT ------
function deleteSubject(index) {
  const subject = subjects[index];
  subjects.splice(index, 1);
  delete scheduleTimes[subject];
  
  students.forEach(function(s){
    if(gradesData[s.name]) {
      delete gradesData[s.name][subject];
    }
  });
  
  saveData();
  loadSection("Subject Schedule");
}

//------ ADD SUBJECT ------
function addSubject() {
  const name = document.getElementById("newSubjectName").value.trim();
  const time = document.getElementById("newSubjectTime").value.trim();
  
  if(!name) {
    alert("Please enter a subject name!");
    return;
  }
  
  if(subjects.includes(name)) {
    alert("Subject already exists!");
    return;
  }
  
  subjects.push(name);
  scheduleTimes[name] = time || "TBA";
  
  students.forEach(function(s){
    if(!gradesData[s.name]) gradesData[s.name] = {};
    gradesData[s.name][name] = 0;
  });
  
  saveData();
  loadSection("Subject Schedule");
}

//------ UPDATE GRADE ------
function updateGrade(student, subject, newGrade) {
  const grade = parseInt(newGrade);
  if(isNaN(grade) || grade < 0 || grade > 100) {
    alert("Grade must be between 0 and 100.");
    loadSection("Grades");
    return;
  }
  
  if(!gradesData[student]) gradesData[student] = {};
  gradesData[student][subject] = grade;
  saveData();
}

//------ UPLOAD PROFILE PHOTO ------
function uploadProfilePhoto() {
  const fileInput = document.getElementById("uploadPic");
  if(!fileInput.files || !fileInput.files[0]) {
    alert("Please select a photo first!");
    return;
  }
  
  const reader = new FileReader();
  reader.onload = function(e){
    const photoData = e.target.result;
    
    if(role === "student") {
      const user = students.find(function(s){ return s.name === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("Photo uploaded successfully!");
      }
    } else if(role === "teacher") {
      const user = teachers.find(function(t){ return t.name === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("Photo uploaded successfully!");
      }
    } else if(role === "parent") {
      const user = parents.find(function(p){ return p.child === currentUser; });
      if(user) {
        user.pic = photoData;
        saveData();
        document.getElementById("profilePic").src = photoData;
        alert("Photo uploaded successfully!");
      }
    } else if(role === "admin") {
      adminAccount.pic = photoData;
      saveData();
      document.getElementById("profilePic").src = photoData;
      alert("Photo uploaded successfully!");
    }
  };
  reader.readAsDataURL(fileInput.files[0]);
}

//------ SEND CHAT MESSAGE ------
function sendChatMessage(tab) {
  const input = document.getElementById("chatInput");
  const chatbox = document.getElementById("chatbox");
  const message = input.value.trim();
  
  if(!message) {
    alert("Please type a message!");
    return;
  }
  
  const timestamp = new Date().toLocaleString();
  chatbox.innerHTML += "<p><strong>" + currentUser + ":</strong> " + message + " <small style='color:#888;'>(" + timestamp + ")</small></p>";
  chatbox.scrollTop = chatbox.scrollHeight;
  input.value = "";
}

//------ ADD PLANNER GOAL ------
function addPlannerGoal(type) {
  const input = document.getElementById(type + "GoalInput");
  const timeInput = document.getElementById(type + "GoalTime") || document.getElementById(type + "GoalDate");
  
  if(!input.value.trim()) {
    alert("Please enter a goal!");
    return;
  }
  
  if(!plannerData[currentUser]) {
    plannerData[currentUser] = { daily: [], weekly: [], monthly: [] };
  }
  
  plannerData[currentUser][type].push({
    text: input.value.trim(),
    time: timeInput ? timeInput.value : "",
    completed: false
  });
  
  saveData();
  loadSection("My Planner");
}

//------ TOGGLE PLANNER GOAL ------
function togglePlannerGoal(type, index) {
  plannerData[currentUser][type][index].completed = !plannerData[currentUser][type][index].completed;
  saveData();
  loadSection("My Planner");
}

//------ DELETE PLANNER GOAL ------
function deletePlannerGoal(type, index) {
  plannerData[currentUser][type].splice(index, 1);
  saveData();
  loadSection("My Planner");
}

//------ SET ALARM ------
function setAlarm(time) {
  if(!time) {
    alert("No time set for this goal!");
    return;
  }
  alert("Alarm set for " + time + "\n\nNote: Browser notifications must be enabled for actual alerts.");
}

//------ INITIALIZE ON PAGE LOAD ------
window.onload = function() {
  saveData();
};
</script>
</body>
</html>
