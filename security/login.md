<body>
    <div id = "authentication-form">
        <div id = "navbar-content"></div>
        <div class = "login-container">
            <h1 style = "text-align: center; color: black">Login</h1>
            <form>
                <input class = "login-input" type = "email" name = "email" id = "email" placeholder = "Email"><br><br>
                <input class = "login-input" type = "password" name = "password" id = "password" placeholder = "Password"><br><br>
                <input type = "submit" class = "login-button" onclick="submitForm()">
            </form>
            <br>
            <p style = "color: black; text-align: center;">Need an account?</p>
            <a style = "color: blue; display: block; text-align: center; margin-top: -10px;" href = "/security/signup.html">Sign Up</a>
        </div>
    </div>
</body>

<style>
    html, body {
        margin: 0;
        padding: 0;
        color: white;
        background-color: #160E2C;
        font-family: 'Raleway', sans-serif;
        overflow-x: hidden;
    }

    h1 {
        font-family: 'Oswald', sans-serif;
        font-size: 48px;
        color: white;
        transition-duration: 0.4s;
    }

    #authentication-form {
        height: 100vh;
        width: 100%;
        background-image: linear-gradient(to right, purple, dodgerblue);
    }

    .login-container {
        height: 50vh;
        width: 30%;
        padding: 10px;
        background-color: whitesmoke;
        margin: 0;
        position: absolute;
        top: 55%;
        left: 50%;
        transform: translate(-50%, -50%);
        box-shadow: 0 15px 15px 0 rgba(255,255,255,0.7);
    }

    .login-label {
        color: silver;
        font-weight: lighter;
        position: relative;
        font-size: 15px;
        top: 20px;
    }

    .login-input {
        height: 30px;
        width: 200px;
        border-left: none;
        border-top: none;
        border-right: none;
        border-bottom: 2px solid black;
        background-color: transparent;
        color: black;
        caret-color: black;
    }

    .login-input:focus {
        outline: none;
    }

    .question {
        height: 50px;
        width: 200px;
        padding: 7px;
        background-color: transparent;
        display: block;
        margin: auto;
        margin-top: -20px;
    }

    #navigation {
        height: 30px; 
        width: 300px; 
        display: grid; 
        grid-template-columns: 70px 160px 70px; 
        margin: auto; 
        margin-top: 20px;
    }

    .next-button {
        height: 20px;
        width: 80px;
        display: flex;
        flex-direction: row;
        align-items: center;
        cursor: pointer;
    }
  
    .back-button {
        height: 20px;
        width: 80px;
        display: flex;
        flex-direction: row;
        align-items: center;
        cursor: default;
    }

    .login-submit {
        height: 30px;
        width: 200px;
        background-image: linear-gradient(to right,violet, dodgerblue, mediumseagreen);
        border: none;
        color: white;
        border-radius: 50px;
        display: none;
        opacity: 0;
        position: relative;
        right: 70px;
        top: -5px;
        cursor: pointer;
    }
</style>

<script>
    // function submitForm() {
    //     $.post('https://frq.dtsivkovski.tk/api/person/authenticate', $("#loginForm").serialize(), function(data) {
    //         console.log(data);
    //     });
    // }

    async function authenticate(email, password) {
        const apiUrl = 'https://frq.dtsivkovski.tk/api/person/authenticate';

        const requestBody = JSON.stringify({
            email: email,
            name: name,
            password: password
        });

        const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'
            },
            body: requestBody
        });

        if (!response.ok) {
            throw new Error('Authentication failed');
        }

        const data = await response.json();
        const token = data.token;

        return token;
    }

    document.getElementById('authentication-form').addEventListener('submit', async (event) => {
        event.preventDefault();
  
        const email = document.getElementById('email').value;
        const password = document.getElementById('password').value;
  
        try {
          const token = await authenticate(email, password);
          console.log('Successful authentication! Token:', token);
        } catch (error) {
          console.error('Authentication failed:', error);
        }
    });
</script>
