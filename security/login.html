<!DOCTYPE html>
<html>
    <head>
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Oswald&display=swap" rel="stylesheet">
        <link href="https://fonts.googleapis.com/css2?family=Raleway:wght@300&display=swap" rel="stylesheet">
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">
    </head>
    <style>
        html, body {
            margin: 0;
            padding: 0;
            color: white;
            background-color: #160E2C;
            font-family: "Raleway", sans-serif;
            overflow-x: hidden;
        }

        h1 {
            font-family: "Oswald", sans-serif;
            font-size: 48px;
            color: white;
            transition-duration: 0.4s;
        }

        #login-background-1 {
            height: 100vh;
            width: 100%;
            background-image: linear-gradient(to right, royalblue, purple);
        }

        .login-container {
            height: 60vh;
            width: 25%;
            padding: 10px;
            background-color: whitesmoke;
            margin: 0;
            position: absolute;
            top: 55%;
            left: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 15px 15px 0 rgba(255,255,255,0.7);
        }

        .login-input {
            height: 35px;
            width: 300px;
            padding-left: 10px;
            background-color: lightgray;
            border: none;
            display: block;
            margin: auto; 
            border-radius: 50px;
        }

        .login-button {
            height: 35px;
            width: 300px;
            background-image: linear-gradient(to right,violet, dodgerblue, mediumseagreen);
            border: none;
            color: white;
            border-radius: 50px;
            display: block;
            margin: auto;
            cursor: pointer;
        }

    </style>


    <body>
        <div id = "login-background-1">
            <div id = "navbar-content"></div>
            <div class = "login-container">
                <h1 style = "text-align: center; color: black">Login</h1>
                <form id="login-form">
                    <input class = "login-input" type = "email" name = "email" id = "email" placeholder = "Email"><br><br>
                    <input class = "login-input" type = "password" name = "password" id = "password" placeholder = "Password"><br><br>
                    <button class = "login-button" onclick="submitForm()">Log In</button>
                    <button id="logout" class="login-button" onclick="logout()">Log Out</button>
                </form>
                <br>
                <p style = "color: black; text-align: center;">Need an account?</p>
                <a style = "color: blue; display: block; text-align: center; margin-top: -10px;" href = "/security/signup.html">Sign Up</a>
            </div>
        </div>
        <!-- <div>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password">
        </div> -->
        <button type="submit">Login</button>
    </body>

    <script>

        function submitForm() {
        const email = document.getElementById("email").value;
        const password = document.getElementById("password").value;

        const url = "https://frq.dtsivkovski.tk/authenticate";
        
        const options = {
            method: 'POST', 
            mode: 'cors', // no-cors, *cors, same-origin
            cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
            credentials: 'include', // include, *same-origin, omit
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                "email" : email,
                "password" : password
            })
        };

        console.log(options);

        // fetch(url, options)
        //   .then(response => console.log(response.text()))
        //   .then(result => console.log(result))
        //   .catch(error => console.log('error', error));


        // Fetch JWT
        fetch(url, options)
        .then(response => {
            // trap error response from Web API
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return; 
            }
            // Success!!!
            // Redirect to Database location
            
            sessionStorage.setItem("username", email);
            //   window.location.href = "/DADY-Academy/templates/home";


        })

        
        }

        function logout() {
        document.cookie = "jwt=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
        sessionStorage.setItem("username", null);
        sessionStorage.setItem("token", null);
        window.location.reload();

        }

        if (sessionStorage.getItem("username") == null) {
            document.getElementById("logout").innerHTML = "Logout";
        }
        else {
            document.getElementById("logout").innerHTML = "Logout - " + sessionStorage.getItem("username");
        }

    </script>

    <!-- <script>
        $(function() {
            $("#navbar-content").load("/layouts/navbar.html");
        });

        // const form = document.getElementById("login-form");
        // form.addEventListener("submit", async (event) => {
        //     event.preventDefault();
        //     const email = document.getElementById("email").value;
        //     const password = document.getElementById("password").value;
        //     const response = await fetch("https://frq.dtsivkovski.tk/api/person/authenticate/", {
        //         method: "POST",
        //         headers: { "Content-Type": "application/json" },
        //         body: JSON.stringify({ email, password }),
        //     });
        //     const data = await response.json();
        //     if (data.token) {
        //         localStorage.setItem("jwt", data.token);
        //         // Redirect to the protected area
        //         window.location.href = "/protected";
        //     } else {
        //         // Show an error message
        //         alert("Invalid credentials");
        //     }
        // });

        // const form = document.getElementById("Login-form");
        // form.addEventListener("submit", async (event) => {
        //     event.preventDefault();
        //     const email = document.getElementById("email").value;
        //     const password = document.getElementById("password").value;
        //     const loginResponse = fetch("https://frq.dtsivkovski.tk/authenticate/", {
        //         method: "POST",
        //         headers: { "Content-Type": "application/json" },
        //         body: JSON.stringify({ email, password }),
        //     });
        // });

        // const form = document.getElementById("Login-form");
        // form.addEventListener("submit", async (event) => {
        //     event.preventDefault();
        //     const email = document.getElementById("email").value;
        //     const password = document.getElementById("password").value;
        //     const loginResponse = fetch("https://frq.dtsivkovski.tk/api/person./authenticate/", {
        //         method: "POST",
        //         headers: { "Content-Type": "application/json" },
        //         body: JSON.stringify({ email, password }),
        //     });

        //     // If the login was successful, the server will return a JWT
        //     if (loginResponse.ok) { // Extract the JWT from the response
        //         const jwt = loginResponse.headers.get("Authorization").split(" ")[1];
        //         // Store the JWT in a cookie or in local storage
        //         localStorage.setItem("jwt", jwt);
        //         console.log(jwt)
        //     }
        // });

        document.getElementById("login-form").addEventListener("submit", async (event) => {
            event.preventDefault();
            const email = document.getElementById("email").value;
            const password = document.getElementById("password").value;
            await sendCredentials(email, password);
        });

        async function sendCredentials(email, password) {
            const body = {"email": "dan@mail", "password": "1234"};
            try {
                const requestOptions = await fetch("https://frq.dtsivkovski.tk/authenticate", {
                    method: "POST",
                    mode: "cors",
                    cache: "no-cache",
                    credentials: "include",
                    body: JSON.stringify(body),
                    headers: {
                        "Content-Type": "application/json"
                    }
                });

                console.log(JSON.stringify(body));
                
                fetch("https://frq.dtsivkovski.tk/authenticate", requestOptions)
                .then(response => {
                    // trap error response from Web API
                    if (!response.ok) {
                        const errorMsg = 'Login error: ' + response.status;
                        console.log(errorMsg);
                        return;
                    }
                    // Success!!!
                    // Redirect to Database location
                    window.location.href = "/APCSA/data/database";
                })

            //     // If the login was successful, the server will return a JWT
            //     if (response.ok) { // Extract the JWT from the response
            //         const jwt = loginResponse.headers.get("Authorization").split(" ")[1];
            //         // Store the JWT in a cookie or in local storage
            //         localStorage.setItem("jwt", jwt);
            //         console.log(jwt)
            //     };

            //     if (!response.ok) throw new Error(response.statusText);
            //     const setCookie = response.headers.get("Set-Cookie");
                
            //     if (!setCookie) throw new Error("No Set-Cookie header in response");
            //     document.cookie = setCookie;
                } catch (error) {
                    console.error("Incorrect email or password");
                    console.log(error);
                }

        }

    </script> -->
</html>
