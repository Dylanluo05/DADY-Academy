# Physics Energy Calculator

## Not logged in? - [Login Now](/DADY-Academy/security/login)

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
    color: black;
    border: 1px solid white;
    margin: 0.5em;
    padding: 0.75em;
    background-image: none;
}
.objectcardbutton:hover {
    border: 1px solid white;
    background-color: #e5e5e5;
}

.selectedobjectcardbutton {
    border: 1px solid white;
    margin: 0.5em;
    padding: 0.75em;
    background-image: none;
    background-color: #778899;
    color: white;
    cursor: default;
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
        <button id="calcKEbutton" style="width:33%; display: inline-block;" class="objectcardbutton"> Calculate </button>
    </div>
    <br>
    <h3 class="maintitle"> Calculate PE </h3>
    <div style="white-space: nowrap;">
        <input placeholder="Gravity (g) value" style="width:32%; display: inline-block;" type="text" id="gravity-input" name="Gravity">
        <input placeholder="Height (h) value" style="width:32%; display: inline-block;" type="text" id="height-input" name="Height">
        <button id="calcPEbutton" style="width:33%; display: inline-block;" class="objectcardbutton"> Calculate </button>
    </div>
    <br>
    <button id="historybutton" class="objectcardbutton" onclick="toggleHistory()"> Show History </button>
    <div id="history" style="display: none;">
        <table id="histable">
        </table>
        <button style="border: 1px solid red; background-color: red; display: none;" id="clearhistorybutton" class="objectcardbutton" onclick="scrubHistory()"> Clear History </button>
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
        <button id="createbutton" style="width:33%; display: inline-block;" class="objectcardbutton" onclick="createObj();"> Create  </button>
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
    const historybutton = document.getElementById("historybutton");
    const history = document.getElementById("history");
    const histable = document.getElementById("histable");

    var url = "https://frq.dtsivkovski.tk/api/physics/energy/get/";
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
                    
                    const buttonholder = document.createElement("div");
                    buttonholder.style.whiteSpace = "nowrap";

                    // create button and give classlist, add to card
                    const button = document.createElement("button");
                    button.classList.add("objectcardbutton");
                    button.style.width = "40%";
                    button.style.display = "inline-block";
                    button.innerHTML = "Select";
                    button.id = "objbutton" + row.id;
                    button.addEventListener("click", function() {
                        selectObj(row.id);
                    });
                    card.appendChild(button);

                    // add deletebutton and give classlist
                    const deletebutton = document.createElement("button");
                    deletebutton.classList.add("objectcardbutton");
                    deletebutton.innerHTML = "Delete";
                    deletebutton.style.backgroundColor = "red";
                    deletebutton.style.border = "1px solid red";
                    deletebutton.style.width = "40%";
                    deletebutton.style.display = "inline-block";
                    deletebutton.addEventListener("click", function() {
                        deleteObj(row.id);
                    });
                    card.appendChild(deletebutton);
                }

                storedinfo = data;
            });
        })
    }

    getAllObjects();

    var selectedObj;

    function selectObj(id) {
        console.log("Selected Object - Id: " + id);

        // turn on history delete button when selected obj for first time
        document.getElementById("clearhistorybutton").style.display = "block";

        // remove selected class from button with selectedObj id
        if (selectedObj != null) {
            var tempOB = document.getElementById("objbutton" + selectedObj);
            tempOB.innerHTML = "Select";
            tempOB.classList.remove("selectedobjectcardbutton");
            tempOB.classList.add("objectcardbutton");
        }

        // set innerHTML to selected object values using storedinfo
        for (const row of storedinfo) {
            if (row.id == id) {
                mTitle.innerHTML = "Object #" + row.id;
                mMass.innerHTML = "Mass: " + row.mass + "kg";
                mRecKE.innerHTML = "Recent KE Calc: " + row.recentKE;
                mRecPE.innerHTML = "Recent PE Calc: " + row.recentPE;

                var tempOB = document.getElementById("objbutton" + row.id);
                tempOB.innerHTML = "Selected";
                tempOB.classList.add("selectedobjectcardbutton");
                tempOB.classList.remove("objectcardbutton");
                selectedObj = row.id;

                // remove old event listener and add new one
                calcKEbutton.onclick = function() {
                    calcKE(row.id);
                };

                calcPEbutton.onclick = function() {
                    calcPE(row.id);
                };

                while (histable.firstChild) {
                    histable.removeChild(histable.firstChild);
                }
                const th1 = document.createElement("th");
                const th2 = document.createElement("th");
                th1.innerHTML = "Calculation";
                th2.innerHTML = "Result";
                histable.appendChild(th1);
                histable.appendChild(th2);

                for (const [key,value] of Object.entries(row.history)) {
                    // console.log(key + " : " + value);

                    var tr = document.createElement("tr");
                    var tdkey = document.createElement("td");
                    var tdvalue = document.createElement("td");

                    tdkey.innerHTML = key;
                    tdvalue.innerHTML = value;
                    tr.appendChild(tdkey);
                    tr.appendChild(tdvalue);
                    histable.appendChild(tr);
                }



            }
        }
    }

    function calcKE(id) {
        console.log("Calculating KE for Object - Id: " + id);

        // build url for fetch
        var calcKEurl = "https://frq.dtsivkovski.tk/api/physics/energy/calculateKE/" + id + "/" + document.getElementById("velocity-input").value;

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

                // add new row to history table
                var tr = document.createElement("tr");
                var tdkey = document.createElement("td");
                var tdvalue = document.createElement("td");

                tdkey.innerHTML = "KE (v = " + document.getElementById("velocity-input").value + ")";
                tdvalue.innerHTML = data.recentKE;

                tr.appendChild(tdkey);
                tr.appendChild(tdvalue);
                histable.appendChild(tr);


                });
        });
    }

    function calcPE(id) {
        console.log("Calculating PE for Object - Id: " + id);

        // build url for fetch
        var calcPEurl = "https://frq.dtsivkovski.tk/api/physics/energy/calculatePE/" + id + "/" + document.getElementById("gravity-input").value + "/" + document.getElementById("height-input").value;

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

                var tr = document.createElement("tr");
                var tdkey = document.createElement("td");
                var tdvalue = document.createElement("td");

                tdkey.innerHTML = "PE (g = " + document.getElementById("gravity-input").value + ", h = " + document.getElementById("height-input").value + ")";
                tdvalue.innerHTML = data.recentPE;

                tr.appendChild(tdkey);
                tr.appendChild(tdvalue);
                histable.appendChild(tr);


                });
        });
    }

    function createObj() {
        console.log("Creating Object");

        // build url for fetch
        var createObjurl = "https://frq.dtsivkovski.tk/api/physics/energy/create/" + document.getElementById("mass-input").value;

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

                getAllObjects();
                selectObj(data.id);
                });
        });
    }

    function deleteObj(id) {

        if (confirm("Are you sure you want to delete this object?") == false)
            return;

        console.log("Deleting Object - Id: " + id);

        // build url for fetch
        var deleteObjurl = "https://frq.dtsivkovski.tk/api/physics/energy/delete/" + id;

        fetch(deleteObjurl, options)
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

                getAllObjects();
                selectObj(data[0].id);
                });
        });
    }

    function toggleHistory() {
        if (history.style.display == "none") {
            history.style.display = "block";
            historybutton.innerHTML = "Hide History";
        } else {
            history.style.display = "none";
            historybutton.innerHTML = "Show History";
        }
    }

    function scrubHistory() {
        if (confirm("Are you sure you want to delete all of this object's history?") == false)
            return;

        console.log("Deleting History - Id: " + selectedObj);

        // build url for fetch
        var scrubHistoryurl = "https://frq.dtsivkovski.tk/api/physics/energy/scrub/" + selectedObj;

        fetch(scrubHistoryurl, options)
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

                getAllObjects();
                selectObj(data.id);

                while (histable.firstChild) {
                    histable.removeChild(histable.firstChild);
                }

                mRecKE.innerHTML = "Recent KE Calc: 0";
                mRecPE.innerHTML = "Recent PE Calc: 0";

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