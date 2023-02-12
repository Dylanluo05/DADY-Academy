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
    margin: 0.5em;
    padding: 0.75em;
    
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

.createcard {
    width: 95%;
    margin: 10px;
    padding: 2em;
    border: 1px solid white;
    border-radius: 10px;
    background-image: linear-gradient(to right, red, purple);
}

.maintitle{
    color: white;
}

input[type=text] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 1px solid white;
  border-radius: 4px;
  background-color: black;
  color: white;
}
input[type=text]:focus {
  border: 1px solid white;
}

hr.cardhr {
    height:2px;
    border-width:0;
    color:white;
    background-color:white
}

</style>

<div class="objectcards">
<div class="maincard">
    <h1 class="maintitle" id="mainTitle">No Currently Selected Object</h1>
    <h3 class="maintitle" id="mainMass"></h3>
    <h3 class="maintitle" id="mainRecKE"></h3>
    <h3 class="maintitle" id="mainRecPE"></h3>
    <hr class="cardhr">
    <h3 class="maintitle"> Calculate KE </h3>
    <div style="white-space: nowrap;">
        <input placeholder="Velocity (v) value" style="width:65%; display: inline-block;" type="text" id="velocity-input" name="Velocity">
        <button id="calcKEbutton" style="width:33%; display: inline-block;" class="objectcardbutton"> Calculate KE </button>
    </div>
    <br>
    <h3 class="maintitle"> Calculate PE </h3>
    <div style="white-space: nowrap;">
        <input placeholder="Gravity (g) value" style="width:32%; display: inline-block;" type="text" id="gravity-input" name="Gravity">
        <input placeholder="Height (h) value" style="width:32%; display: inline-block;" type="text" id="height-input" name="Height">
        <button id="calcPEbutton" style="width:33%; display: inline-block;" class="objectcardbutton"> Calculate PE </button>
    </div>
</div>
</div>
<br>

## Your objects

<div class="objectcards" id="cardholder">
</div>
<br>


<div class="objectcards">
<div class="createcard">
    <h1 class="maintitle">Create an object</h1>
    <div style="white-space: nowrap;">
        <input placeholder="Mass (m) value" style="width:65%; display: inline-block;" type="text" id="mass-input" name="Object Mass">
        <button id="createbutton" style="width:33%; display: inline-block;" class="objectcardbutton" onclick="createObj();"> Create Object </button>
    </div>
</div>
</div>

<script>
    const cardholder = document.getElementById("cardholder");
    const mTitle = document.getElementById("mainTitle");
    const mMass = document.getElementById("mainMass");
    const mRecKE = document.getElementById("mainRecKE");
    const mRecPE = document.getElementById("mainRecPE");
    const calcKEbutton = document.getElementById("calcKEbutton");
    const calcPEbutton = document.getElementById("calcPEbutton");

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

    function getAllObjects() {
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

                //remove existing cardholder
                while(cardholder.firstChild) {
                    cardholder.removeChild(cardholder.firstChild);
                }

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
    }

    getAllObjects();


    function selectObj(id) {
        console.log("Selected Object - Id: " + id);

        // set innerHTML to selected object values using storedinfo
        for (const row of storedinfo) {
            if (row.id == id) {
                mTitle.innerHTML = "Object #" + row.id;
                mMass.innerHTML = "Mass: " + row.mass + "kg";
                mRecKE.innerHTML = "Recent KE Calc: " + row.recentKE;
                mRecPE.innerHTML = "Recent PE Calc: " + row.recentPE;

                // remove old event listener and add new one
                calcKEbutton.onclick = function() {
                    calcKE(row.id);
                };

                calcPEbutton.onclick = function() {
                    calcPE(row.id);
                };


            }
        }
    }

    function calcKE(id) {
        console.log("Calculating KE for Object - Id: " + id);

        // build url for fetch
        var calcKEurl = "https://frq.dtsivkovski.tk/api/physics/calculateKE/" + id + "/" + document.getElementById("velocity-input").value;

        fetch(calcKEurl, options)
        // response is a RESTful "promise" on any successful fetch
        .then(response => {
            // check for response errors and display
            if (response.status !== 200) {
                const errorMsg = 'Database response error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // valid response will contain json data
            response.json().then(data => {
                console.log(data);
                mRecKE.innerHTML = "Recent KE Calc: " + data.recentKE;
                getAllObjects();
                });
        });
    }

    function calcPE(id) {
        console.log("Calculating PE for Object - Id: " + id);

        // build url for fetch
        var calcPEurl = "https://frq.dtsivkovski.tk/api/physics/calculatePE/" + id + "/" + document.getElementById("gravity-input").value + "/" + document.getElementById("height-input").value;

        fetch(calcPEurl, options)
        // response is a RESTful "promise" on any successful fetch
        .then(response => {
            // check for response errors and display
            if (response.status !== 200) {
                const errorMsg = 'Database response error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // valid response will contain json data
            response.json().then(data => {
                console.log(data);
                mRecPE.innerHTML = "Recent PE Calc: " + data.recentPE;
                getAllObjects();
                });
        });
    }

    function createObj() {
        console.log("Creating Object");

        // build url for fetch
        var createObjurl = "https://frq.dtsivkovski.tk/api/physics/create/" + document.getElementById("mass-input").value;

        fetch(createObjurl, options)
        // response is a RESTful "promise" on any successful fetch
        .then(response => {
            // check for response errors and display
            if (response.status !== 200) {
                const errorMsg = 'Database response error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // valid response will contain json data
            response.json().then(data => {
                console.log(data);

                var tempId = data.id;

                getAllObjects();
                selectObj(tempId);
                });
        });
    }

</script>


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