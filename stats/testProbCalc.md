# Stats Calculator

<style>
.objectcards {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
}

.objectcard {
    width: 350px;
    height: 200px;
    margin: 0px;
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
    <h3 class="maintitle" id="mainSampleSize"></h3>
    <h3 class="maintitle" id="mainRecSDM"></h3>
    <hr class="cardhr">
    <h3 class="maintitle"> Calculate SDM </h3>
    <div style="white-space: nowrap;">
        <input placeholder="Standard Error (Sx)" style="width:65%; display: inline-block;" type="text" id="se-input" name="StandardError">
        <button id="calcSDMbutton" style="width:33%; display: inline-block;" class="objectcardbutton"> Calculate </button>
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

<div class="objectcards">
<div class="createcard">
    <h1 class="maintitle">Create an object</h1>
    <div style="white-space: nowrap;">
        <input placeholder="Sample Size (n)" style="width:65%; display: inline-block;" type="text" id="N-input" name="Object Sample Size">
        <button id="createbutton" style="width:33%; display: inline-block;" class="objectcardbutton" onclick="createObj();"> Create </button>
    </div>
</div>
</div>

<script>
    const cardholder = document.getElementById("cardholder");
    const mTitle = document.getElementById("mainTitle");
    const mN = document.getElementById("mainSampleSize");
    const mRecSDM = document.getElementById("mainRecSDM");
    const calcsDMbutton = document.getElementById("calcSDMbutton");
    const historybutton = document.getElementById("historybutton");
    const history = document.getElementById("history");
    const histable = document.getElementById("histable");

    // var url = "https://frq.dtsivkovski.tk/api/stats/get/";

    // Uncomment next line for localhost testing
    url = "http://localhost:8679/api/stats/get/";

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
    const optionsPOST = {
        method: 'POST', // *GET, POST, PUT, DELETE, etc.
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
                    const n = document.createElement("p");
                    n.innerHTML = "n: " + row.n;
                    const recSDM = document.createElement("p");
                    recSDM.innerHTML = "Recent SDM Calc: " + row.recentSDM;
                    const updateN = document.createElement("input");
                    updateN.setAttribute("placeholder", "Update n");
                    const breakElement = document.createElement("br");

                    card.appendChild(h3);
                    card.appendChild(n);
                    card.appendChild(recSDM);
                    card.appendChild(updateN);
                    card.appendChild(breakElement);
                    card.appendChild(breakElement);
  
                    const buttonholder = document.createElement("div");
                    buttonholder.style.whiteSpace = "nowrap";

                    // create button and give classlist, add to card
                    const button = document.createElement("button");
                    button.classList.add("objectcardbutton");
                    deletebutton.style.backgroundColor = "#8a8787";
                    deletebutton.style.border = "1px solid #8a8787";
                    button.style.width = "20%";
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
                    deletebutton.style.width = "20%";
                    deletebutton.style.display = "inline-block";
                    deletebutton.addEventListener("click", function() {
                        deleteObj(row.id);
                    });
                    card.appendChild(deletebutton);

                    const updatebutton = document.createElement("button");
                    updatebutton.classList.add("objectcardbutton");
                    updatebutton.innerHTML = "update";
                    updatebutton.style.backgroundColor = "green";
                    updatebutton.style.border = "1px solid green";
                    updatebutton.style.width = "20%";
                    updatebutton.style.display = "inline-block";
                    // updatebutton.addEventListener("click", function() {
                    //     deleteObj(row.id);
                    // });
                    card.appendChild(updatebutton);
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
                mN.innerHTML = "Sample Size: " + row.n;
                mRecSDM.innerHTML = "Recent SDM Calc: " + row.recentSDM;

                var tempOB = document.getElementById("objbutton" + row.id);
                tempOB.innerHTML = "Selected";
                tempOB.classList.add("selectedobjectcardbutton");
                tempOB.classList.remove("objectcardbutton");
                selectedObj = row.id;

                // remove old event listener and add new one
                calcSDMbutton.onclick = function() {
                    calcSDM(row.id);
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

    function calcSDM(id) {
        console.log("Calculating SDM for Object - Id: " + id);

        // build url for fetch
        // var calcSDMurl = "https://frq.dtsivkovski.tk/api/stats/calculateSDM/" + id + "/" + document.getElementById("se-input").value;
        var calcSDMurl = "http://localhost:8679/api/stats/calculateSDM/" + id + "/" + document.getElementById("se-input").value;

        fetch(calcSDMurl, options)
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
                mRecSDM.innerHTML = "Recent SDM Calc: " + data.recentSDM;
                getAllObjects();

                // add new row to history table
                var tr = document.createElement("tr");
                var tdkey = document.createElement("td");
                var tdvalue = document.createElement("td");

                tdkey.innerHTML = "SDM (Sx = " + document.getElementById("se-input").value + ")";
                tdvalue.innerHTML = data.recentSDM;

                tr.appendChild(tdkey);
                tr.appendChild(tdvalue);
                histable.appendChild(tr);
            });
        })
        .catch(error => {
            // Handle the error here
            alert('Invalid Input! Please try again.');
            console.error('There was a problem with the fetch operation:', error);
        });
    }

    function createObj() {
        console.log("Creating Object");

        // build url for fetch
        // var createObjurl = "https://frq.dtsivkovski.tk/api/stats/create/" + document.getElementById("N-input").value;
        var createObjurl = "http://localhost:8679/api/stats/create?sampleSize=" + document.getElementById("N-input").value;

        fetch(createObjurl, optionsPOST)
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
        })
        .catch(error => {
            // Handle the error here
            alert('Invalid Input! Please try again.');
            console.error('There was a problem with the fetch operation:', error);
        });
    }

    function deleteObj(id) {

        if (confirm("Are you sure you want to delete this object?") == false)
            return;

        console.log("Deleting Object - Id: " + id);

        // build url for fetch
        // var deleteObjurl = "https://frq.dtsivkovski.tk/api/stats/delete/" + id;
        var deleteObjurl = "http://localhost:8679/api/stats/delete/" + id;

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
        // var scrubHistoryurl = "https://frq.dtsivkovski.tk/api/stats/scrub/" + selectedObj;
        var scrubHistoryurl = "http://localhost:8679/api/stats/scrub/" + selectedObj;

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

                mRecSDM.innerHTML = "Recent SDM Calc: 0";

                });
        });
    }

</script>