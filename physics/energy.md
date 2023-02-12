# Physics Energy Calculator


<style>

.objectcards {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
}

.objectcard {
    width: 200px;
    height: 200px;
    margin: 10px;
    padding: 2em;
    border: 1px solid white;
    border-radius: 10px;
    background-image: linear-gradient(to right, purple, navy);
    text-align: center;
}

table .objectcard {
    width: 100%;
    margin: 0;
    padding: 0;
    border: 0;
    border-radius: 0;
    background-color: #f1f1f1;
    text-align: center;
}

.objectcardbutton {
    background-color: white;
    border: 1px solid white;
    
}
.objectcardbutton:hover {
    border: 1px solid white;
    background-color: #e5e5e5;
}

.maincard {
    width: 95%;
    margin: 10px;
    padding: 2em;
    border: 1px solid white;
    border-radius: 10px;
    background-image: linear-gradient(to right, purple, navy);
}

.maintitle{
    color: white;
}

</style>

<div class="objectcards">
<div class="maincard">
    <h1 class="maintitle">No Currently Selected Object</h1>
    <h3 class="maintitle" id="mainMass"></h3>
    <h3 class="maintitle" id="mainRecKE"></h3>
    <h3 class="maintitle" id="mainRecPE"></h3>
</div>
</div>

## Your objects

<div class="objectcards" id="cardholder">
    <div class="objectcard" id="obj26">
        <h3>Object #26</h3>
        <p>Mass: 25kg</p>
        <p>Recent KE Calc: 25000</p>
        <p>Recent PE Calc: 25000</p>
        <button class="objectcardbutton" >Select Object</button>
    </div>
    <div class="objectcard" id="obj26">
        <h3>Object #26</h3>
        <p>Mass: 25kg</p>
        <p>Recent KE Calc: 25000</p>
        <p>Recent PE Calc: 25000</p>
        <button class="objectcardbutton">Select Object</button>
    </div>
    <div class="objectcard" id="obj26">
        <h3>Object #26</h3>
        <p>Mass: 25kg</p>
        <p>Recent KE Calc: 25000</p>
        <p>Recent PE Calc: 25000</p>
        <button class="objectcardbutton">Select Object</button>
    </div>
</div>

<script>
    const cardholder = document.getElementById("cardholder");

    var url = "https://frq.dtsivkovski.tk/api/physics/get/";
    // Uncomment next line for localhost testing
    // url = "http://localhost:8085/api/person/";

    // set options for cross origin header request
    const options = {
    method: 'GET', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'include', // include, *same-origin, omit
    headers: {
        'Content-Type': 'application/json',
    },
    };

    var storedinfo;

    // fetch the API
    fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
        // check for response errors and display
        if (response.status !== 200) {
            const errorMsg = 'Database response error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            cardholder.appendChild(tr);
            return;
        }
        // valid response will contain json data
        response.json().then(data => {
            console.log(data);

            for (const row of data) {
                // create card and give classlist, add to cardholder
                const card = document.createElement("div");
                card.classList.add("objectcard");
                cardholder.appendChild(card);

                // create elements for card
                const h3 = document.createElement("h3");
                h3.innerHTML = "Object #" + row.id;
                const mass = document.createElement("p");
                mass.innerHTML = "Mass: " + row.mass + "kg";
                const recKE = document.createElement("p");
                recKE.innerHTML = "Recent KE Calc: " + row.recentKE;
                const recPE = document.createElement("p");
                recPE.innerHTML = "Recent PE Calc: " + row.recentPE;

                card.appendChild(h3);
                card.appendChild(mass);
                card.appendChild(recKE);
                card.appendChild(recPE);
                
                // create button and give classlist, add to card and
                const button = document.createElement("button");
                button.classList.add("objectcardbutton");
                button.innerHTML = "Select Object";
                button.addEventListener("click", function() {
                    selectObj(row.id);
                });
                card.appendChild(button);
            }

            storedinfo = data;
        });
    })


    function selectObj(id) {
        console.log(id);
    }
</script>




## Create an object

<!-- <form id="obj-create-form">
    <label for="name-input">Name of Object</label><br>
    <input type="text" id="name-input" name="Name"><br>
    <label for="mass-input">Mass of Object</label><br>
    <input type="text" id="mass-input" name="Mass"><br>
    <button id="obj-create-submit">Create Object</button>
</form>

<br>

## KE Calculator

<img src="images/phys-ke.png" height="200px">

<form id="KE-form">
    <label for="object-selector"> Select an Object </label><br>
    <select id="object-selector" name="object-selector">
        <option value="{object.ID}"> {object1.name} </option>
        <option value="{object.ID}"> {object2.name} </option>
    </select><br>
    <label for="v-input">Velocity Value</label><br>
    <input type="text" id="v-input" name="V"><br>
    <button id="KE-submit">Calculate</button>
</form> 

<br>

## PE Gravity Calculator

<img src="images/phys-pe.png" height="200px">

<form id="PEG-form">
    
    <label for="object-selector"> Select an Object </label><br>
    <select id="object-selector" name="object-selector">
        <option value="{object.ID}"> {object1.name} </option>
        <option value="{object.ID}"> {object2.name} </option>
    </select><br>
    <label for="h-input"> Height Value</label><br>
    <input type="text" id="h-input" name="H"><br>
    <label for="g-input"> G Value</label><br>
    <input type="text" id="g-input" name="G"><br>
    <button id="PEG-submit">Calculate</button>
</form> 
-->