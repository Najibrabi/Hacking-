<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Login System Demo</title>
<style>
body {
    font-family: Arial;
    background: #f0f2f5;
    margin: 0;
    padding: 0;
}
.container {
    width: 400px;
    margin: 50px auto;
    background: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
h2 { text-align: center; margin-bottom: 20px; }
input[type="text"], input[type="email"], input[type="password"] {
    width: 100%;
    padding: 12px;
    margin: 8px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
}
button {
    width: 100%;
    padding: 12px;
    background: #1e90ff;
    border: none;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}
button:hover { background: #007acc; }
p { text-align: center; margin-top: 15px; }
a { color: #1e90ff; cursor: pointer; text-decoration: none; }
a:hover { text-decoration: underline; }
.hidden { display: none; }
</style>
</head>
<body>

<div class="container">

    <!-- Register Page -->
    <div id="registerPage">
        <h2>Register</h2>
        <input type="email" id="regEmail" placeholder="Email" required>
        <input type="password" id="regPassword" placeholder="Password" required>
        <input type="password" id="regConfirmPassword" placeholder="Confirm Password" required>
        <button onclick="registerUser()">Register</button>
        <p>Already have an account? <a onclick="showPage('loginPage')">Login</a></p>
        <p>Forgot password? <a onclick="showPage('forgetPage')">Reset</a></p>
    </div>

    <!-- Login Page -->
    <div id="loginPage" class="hidden">
        <h2>Login</h2>
        <input type="email" id="loginEmail" placeholder="Email" required>
        <input type="password" id="loginPassword" placeholder="Password" required>
        <button onclick="loginUser()">Login</button>
        <p>Don't have account? <a onclick="showPage('registerPage')">Register</a></p>
        <p>Forgot password? <a onclick="showPage('forgetPage')">Reset</a></p>
    </div>

    <!-- Forget Password Page -->
    <div id="forgetPage" class="hidden">
        <h2>Reset Password</h2>
        <input type="email" id="forgetEmail" placeholder="Email" required>
        <button onclick="resetPassword()">Reset Password</button>
        <p>Remembered? <a onclick="showPage('loginPage')">Login</a></p>
    </div>

    <!-- Dashboard Page -->
    <div id="dashboardPage" class="hidden">
        <h2>Welcome!</h2>
        <p>You are logged in.</p>
        <button onclick="logoutUser()">Logout</button>
    </div>

</div>

<script>
// Show page function
function showPage(pageId) {
    const pages = ['registerPage','loginPage','forgetPage','dashboardPage'];
    pages.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(pageId).classList.remove('hidden');
}

// Register
function registerUser() {
    const email = document.getElementById('regEmail').value;
    const pass = document.getElementById('regPassword').value;
    const confirm = document.getElementById('regConfirmPassword').value;

    if(!email || !pass || !confirm) { alert("Fill all fields"); return; }
    if(pass !== confirm) { alert("Passwords do not match"); return; }

    localStorage.setItem('userEmail', email);
    localStorage.setItem('userPassword', pass);
    alert("Registration successful!");
    showPage('loginPage');
}

// Login
function loginUser() {
    const email = document.getElementById('loginEmail').value;
    const pass = document.getElementById('loginPassword').value;

    const storedEmail = localStorage.getItem('userEmail');
    const storedPass = localStorage.getItem('userPassword');

    if(email === storedEmail && pass === storedPass){
        alert("Login successful!");
        showPage('dashboardPage');
    } else {
        alert("Incorrect email or password");
    }
}

// Reset Password
function resetPassword() {
    const email = document.getElementById('forgetEmail').value;
    const storedEmail = localStorage.getItem('userEmail');
    if(email === storedEmail){
        const newPass = prompt("Enter new password:");
        if(newPass){
            localStorage.setItem('userPassword', newPass);
            alert("Password reset successful!");
            showPage('loginPage');
        }
    } else {
        alert("Email not found!");
    }
}

// Logout
function logoutUser() {
    alert("Logged out!");
    showPage('loginPage');
}

// Initialize page
showPage('registerPage');
</script>

</body>
</html>
