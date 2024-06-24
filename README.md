<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration and Login Form</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.bundle.min.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-firestore.js"></script>
    <style>
        body {
            background-color: #f8f9fa;
        }
        .form-container {
            max-width: 500px;
            margin: auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .navbar {
            margin-bottom: 20px;
        }
        .content {
            display: none;
        }
    </style>
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">MyApp</a>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ml-auto">
                <li class="nav-item">
                    <a class="nav-link" href="#" id="home-link">Home</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#" id="about-link">About Us</a>
                </li>
            </ul>
        </div>
    </nav>

    <div class="content" id="home-content">
        <div class="form-container">
            <h2>Register</h2>
            <form id="registration-form">
                <div class="form-group">
                    <label for="firstName">First Name</label>
                    <input type="text" class="form-control" id="firstName" required>
                </div>
                <div class="form-group">
                    <label for="lastName">Last Name</label>
                    <input type="text" class="form-control" id="lastName" required>
                </div>
                <div class="form-group">
                    <label for="registrationNumber">Registration Number</label>
                    <input type="text" class="form-control" id="registrationNumber" required>
                </div>
                <div class="form-group">
                    <label for="email">Email</label>
                    <input type="email" class="form-control" id="email" required>
                </div>
                <div class="form-group">
                    <label for="password">Password</label>
                    <input type="password" class="form-control" id="password" required>
                </div>
                <div class="form-group">
                    <label for="confirmPassword">Confirm Password</label>
                    <input type="password" class="form-control" id="confirmPassword" required>
                </div>
                <button type="submit" class="btn btn-primary">Register</button>
            </form>
        </div>

        <div class="form-container mt-4">
            <h2>Login</h2>
            <form id="login-form">
                <div class="form-group">
                    <label for="loginEmail">Email or Username</label>
                    <input type="text" class="form-control" id="loginEmail" required>
                </div>
                <div class="form-group">
                    <label for="loginPassword">Password</label>
                    <input type="password" class="form-control" id="loginPassword" required>
                </div>
                <button type="submit" class="btn btn-primary">Login</button>
            </form>
        </div>
    </div>

    <div class="content" id="about-content">
        <div class="form-container">
            <h2>About Us</h2>
            <p>Mimi Elisha, Developer</p>
        </div>
    </div>

    <script>
        // Firebase configuration
        var firebaseConfig = {
            apiKey: "AIzaSyCSbEa43-q5UlW2VqWGyh-De_eRZZLW0i0",
            authDomain: "mkazi-27226.firebaseapp.com",
            projectId: "mkazi-27226",
            storageBucket: "mkazi-27226.appspot.com",
            messagingSenderId: "307670414185",
            appId: "1:307670414185:web:7d1017284e168ab87983f8
        };
        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);

        // Show Home Content by default
        document.getElementById('home-content').style.display = 'block';

        // Navigation Links
        document.getElementById('home-link').addEventListener('click', function() {
            document.getElementById('home-content').style.display = 'block';
            document.getElementById('about-content').style.display = 'none';
        });

        document.getElementById('about-link').addEventListener('click', function() {
            document.getElementById('home-content').style.display = 'none';
            document.getElementById('about-content').style.display = 'block';
        });

        // Registration form submission
        const registrationForm = document.getElementById('registration-form');
        registrationForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const registrationNumber = document.getElementById('registrationNumber').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const confirmPassword = document.getElementById('confirmPassword').value;

            if (password !== confirmPassword) {
                alert('Passwords do not match');
                return;
            }

            firebase.auth().createUserWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    var user = userCredential.user;
                    // Save additional user info to Firestore
                    firebase.firestore().collection('users').doc(user.uid).set({
                        firstName: firstName,
                        lastName: lastName,
                        registrationNumber: registrationNumber,
                        email: email
                    }).then(() => {
                        alert('Registration successful');
                    }).catch((error) => {
                        console.error('Error writing document: ', error);
                    });
                })
                .catch((error) => {
                    var errorCode = error.code;
                    var errorMessage = error.message;
                    alert(errorMessage);
                });
        });

        // Login form submission
        const loginForm = document.getElementById('login-form');
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;

            firebase.auth().signInWithEmailAndPassword(email, password)
                .then((userCredential) => {
                    var user = userCredential.user;
                    alert('Login successful');
                })
                .catch((error) => {
                    var errorCode = error.code;
                    var errorMessage = error.message;
                    alert(errorMessage);
                });
        });
    </script>
</body>
</html>
