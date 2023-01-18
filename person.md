# Person

<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
</head>

<style>
    .button-1 {
        height: 40px;
        width: 500px;
        background-color: white;
        color: #f2ba92;
        border: 2px solid #f2ba92;
        transition-duration: 0.4s;
        display: block;
        margin: auto;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .button-1:hover {
        background-color: #f2ba92;
        color: white;
    }

    .label-1 {
        display: block;
        text-align: center;
    }

    .input-1 {
        height: 5%;
        width: 10rem;
        border: none;
        background-color: lightgray;
        display: block;
        margin: auto;
    }
</style>

<table>
    <thead>
    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
        <th>Age</th>
        <th>Date of Birth</th>
    </tr>
    </thead>
    <tbody id="result">
        <!-- javascript generated data -->
    </tbody>
</table>
<form>
    <label for = "email" class = "label-1">Enter email address</label>
    <input type = "email" name = "year-1" class = "input-1" id="inputEmail" placeholder="abc@xyz.com">
    <br>
    <label for = "name" class = "label-1">Enter name</label>
    <input type = "text" class = "input-1" id="inputName" placeholder="Name">
    <br>
    <label for = "psswd" class = "label-1">Enter Password:</label>
    <input type = "password" class = "input-1" id="inputPassword" placeholder="Password">
    <br>
    <label for = "date" class = "label-1">Enter Date of Birth:</label>
    <input type = "text" class = "input-1" id="inputDob" placeholder="YYYY-MM-DD">
    <br>
    <button onclick="createUser()" class="button-1">Create user</button>
</form>

<br><br>


<script>
    const resultContainer = document.getElementById("result");
    const API_URL = 'https://frq.dtsivkovski.tk/api/person/';
    fetch(API_URL)
        // response is a RESTful "promise" on any successful fetch
        .then(response => {
            console.log(response);
            // check for response errors
            if (response.status !== 200) {
                const errorMsg = 'API response error: ' + response.status;
                console.log(errorMsg);
                const tr = document.createElement("tr");
                const td = document.createElement("td");
                td.innerHTML = errorMsg;
                tr.appendChild(td);
                resultContainer.appendChild(tr);
                return;
            }
            // valid response will have json data
            response.json().then(data => {
                console.log(data);
                // Country data
                for (const row of data) {
                    console.log(row);
                    // tr for each row
                    const tr = document.createElement("tr");
                    // td for each column
                    const id = document.createElement("td");
                    const name = document.createElement("td");
                    const email = document.createElement("td");
                    const age = document.createElement("td");
                    const dob = document.createElement("td");
                    // data is specific to the API
                    id.innerHTML = row.id;
                    name.innerHTML = row.name;
                    email.innerHTML = row.email;
                    age.innerHTML = row.age;
                    dob.innerHTML = row.dob.substring(0,10);
                    // this build td's into tr
                    tr.appendChild(id);
                    tr.appendChild(name);
                    tr.appendChild(email);
                    tr.appendChild(age);
                    tr.appendChild(dob)
                    // add HTML to container
                    resultContainer.appendChild(tr);
                }
            });
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = err;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            });

    function createUser() {
        const API_URL = 'https://frq.dtsivkovski.tk/api/person/post?';
        const url = API_URL;
        console.log(url);
        const email = document.getElementById("inputEmail").value;
        const password = document.getElementById("inputPassword").value;
        const name = document.getElementById("inputName").value;
        const dob = document.getElementById("inputDob").value;
        options = {
            method: 'POST',
            mode: 'no-cors', // no-cors, *cors, same-origin
    // cache: 'default', //*default, no-cache, reload, force-cache, only-if-cached
            // credentials: 'same-origin', // include, same-origin, omit
            headers: {
                'Content-Type': 'application/json'
            },
        };
        const final = url +'email=' + email + '&password=' + password + '&name=' + name + '&dob=' + dob;
        console.log(final);
        console.log(options);
        fetch(final, options);
        location.reload();
    }
</script>
