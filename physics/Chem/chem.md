# Chem

<body>
<h1>Density and Moles Calculator</h1>
    <form>
      <label for="mass">Mass (g):</label>
      <input type="number" id="mass" name="mass"><br><br>
      <label for="volume">Volume (m^3):</label>
      <input type="number" id="volume" name="volume"><br><br>
      <label for="mw">Molecular weight (g):</label>
      <input type="number" id="molecularWeight" name="mw"><br><br>
      <button type="button" onclick="calculate()">Calculate Density and Moles</button>
    </form>
    <br><br>
    <p id="result"></p>
</body>

<table id="ChemData">
  <thead>
    <tr>
      <th>id</th>
      <th>User</th>
      <th>mass</th>
      <th>volume</th>
      <th>Molecular Weight</th>
      <th>Density</th>
      <th>Moles</th>
      <th>Delete</th>
    </tr>
  </thead>
  <tbody id = "ChemId"></tbody>
</table>  

<br><br>

<script>
  
  const mass = document.getElementById("mass").value;
  const volume = document.getElementById("volume").value;
  const mw = document.getElementById("molecularWeight").value;
  const resultChemData = document.getElementById("ChemId");
//  const chemTable = document.getElementById("ChemData");

  function calculate() {
    
    var url = "https://frq.dtsivkovski.tk/api/Chem/create?mass=" + document.getElementById("mass").value + "&volume=" + document.getElementById("volume").value + "&molecularWeight=" + document.getElementById("molecularWeight").value;
    //var url = "http://localhost:8679/api/Chem/create?mass=" + document.getElementById("mass").value + "&volume=" + document.getElementById("volume").value + "&molecularWeight=" + document.getElementById("molecularWeight").value;

    // const body = {
    //   mass: mass,
    //   volume: volume,
    //   molecularWeight: molecularWeight
    // };

    const optionsPOST = {
        method: 'POST', // *GET, POST, PUT, DELETE, etc.
        mode: 'cors', // no-cors, *cors, same-origin
        cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'include', // include, *same-origin, omit
        headers: {
            'Content-Type': 'application/json',
        },
        // body: JSON.stringify(body)
    };

    var i = 0;

    fetch(url, optionsPOST)
      .then(response => {
      if (response.ok) {
        return response.json();
      } else {
        throw new Error('Error calculating density');
      }
    })
    .then(data => {
      for(const rs of data) {
        const tr = document.createElement("tr");
        const id = document.createElement("td");
        const user = document.createElement("td");
        const mass = document.createElement("td");
        const vol = document.createElement("td");
        const mw = document.createElement("td");
        const den = document.createElement("td");
        const mole = document.createElement("td");
        const del = document.createElement("td");

        id.innerHTML = rs.id;
        user.innerHTML = rs.owner;
        mass.innerHTML = rs.mass;
        vol.innerHTML = rs.volume;
        mw.innerHTML = rs.molecularWeight;
        den.innerHTML = rs.density;
        mole.innerHTML = rs.mole;
        const button = document.createElement("button");
          button.innerHTML = "Delete";
          button.id = "delButton-"+i;
          button.addEventListener("click", function() {
              event.preventDefault();
              deleteChem(this,rs.id);
          });
        del.appendChild(button);
        //del.innerHTML = <button onclick="deleteTable()">Delete</button>;

        tr.appendChild(id);
        tr.appendChild(user);
        tr.appendChild(mass);
        tr.appendChild(vol);
        tr.appendChild(mw);
        tr.appendChild(den);
        tr.appendChild(mole);
        tr.appendChild(del);

        resultChemData.appendChild(tr);

        i++;
      }
    })
    .catch(error => {
      console.log(error);
    });

  }

  function deleteChem(r,id) {
    var url = "https://frq.dtsivkovski.tk/api/Chem/delete/" + id;
    alert(url);

    var i = r.parentNode.parentNode.rowIndex;
    alert(i);
    document.getElementById("ChemData").deleteRow(i);
    /*
    const optionsDEL = {
        method: 'DELETE', // *GET, POST, PUT, DELETE, etc.
        credentials: 'same-origin',
        headers: {
        'Content-type': 'application/json; charset=UTF-8' // Indicates the content 
        },
    };

    fetch(url, optionsDEL)
      .then(res => {
      if (res.ok) {
        alert("deleted the id");
        //return res.json();
      } else {
        throw new Error('Error deleting id');
      }});
    //}).catch(error => {
      //console.log(error);
    //});
    */

   (async () => {
      await fetch(url, {method: 'DELETE'});
      alert("Deleted");

   })();
    

  }
</script>




<style>
  /* Existing styles */
  h1 {
    color: blue;
    text-align: center;
  }
  form {
    margin: auto;
    width: 30%;
    padding: 10px;
    border: 1px solid black;
  }
  label {
    margin-right: 10px;
  }
  #result {
    text-align: center;
  }
  
  /* Additional styles */
  input[type="obj"],
  input[type="number"],
  button {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 3px;
    font-size: 16px;
    margin-bottom: 10px;
  }
  
  button {
    background-color: blue;
    color: white;
    cursor: pointer;
  }

  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  td, th {
    border: 1px solid #000000;
    text-align: left;
    padding: 8px;
  } 

  tr {
    background-color: #000000;
  }
</style>

  <body>
    <table>
      <tr>
        <th>Element</th>
        <th>Symbol</th>
        <th>Atomic Number</th>
      </tr>
      <tr>
        <td>Hydrogen</td>
        <td>H</td>
        <td>1</td>
      </tr>
      <tr>
        <td>Helium</td>
        <td>He</td>
        <td>2</td>
      </tr>
      <tr>
        <td>Lithium</td>
        <td>Li</td>
        <td>3</td>
      </tr>
      <tr>
        <td>Beryllium</td>
        <td>Be</td>
        <td>4</td>
      </tr>
      <!-- Add more rows for the rest of the elements in the periodic table -->
    </table>