<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Firebase Auth</title>
  <link rel="stylesheet" href="styles.css">
  <script src="https://www.gstatic.com/firebasejs/9.6.8/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.8/firebase-auth.js"></script>
</head>
<body>
  <h2>Register</h2>
  <form id="register-form">
    <input type="name" id="register-name" placeholder="name" required>
    <input type="email" id="register-email" placeholder="Email" required>
    <input type="password" id="register-password" placeholder="Password" required>
    <button type="submit">Register</button>
  </form>

  <h2>Login</h2>
  <form id="login-form">
    <input type="email" id="login-email" placeholder="Email" required>
    <input type="password" id="login-password" placeholder="Password" required>
    <button type="submit">Login</button>
  </form>

  <script>
    // Your Firebase configuration
    const firebaseConfig = {
      apiKey: "AIzaSyCSbEa43-q5UlW2VqWGyh-De_eRZZLW0i0",
      authDomain: "mkazi-27226.firebaseapp.com",
      projectId: "mkazi-27226",
      storageBucket:  "mkazi-27226.appspot.com",
      messagingSenderId: "307670414185",
      appId: "1:307670414185:web:7d1017284e168ab87983f8"
    };

    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);

    // Register form submission
    document.getElementById('register-form').addEventListener('submit', function(event) {
      event.preventDefault();
      const email = document.getElementById('register-email').value;
      const password = document.getElementById('register-password').value;

      firebase.auth().createUserWithEmailAndPassword(email, password)
        .then((userCredential) => {
          // Registration successful
          console.log('User registered:', userCredential.user);
          alert('Registration successful!');
        })
        .catch((error) => {
          // Handle errors
          console.error('Error registering user:', error.message);
          alert('Error: ' + error.message);
        });
    });

    // Login form submission
    document.getElementById('login-form').addEventListener('submit', function(event) {
      event.preventDefault();
      const email = document.getElementById('login-email').value;
      const password = document.getElementById('login-password').value;

      firebase.auth().signInWithEmailAndPassword(email, password)
        .then((userCredential) => {
          // Login successful
          console.log('User logged in:', userCredential.user);
          alert('Login successful!');
        })
        .catch((error) => {
          // Handle errors
          console.error('Error logging in user:', error.message);
          alert('Error: ' + error.message);
        });
    });
  </script>
</body>
</html>
