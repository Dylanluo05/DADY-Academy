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

<table>
  <thead>
    <tr>
      <th>"id"</th>
      <th>"User"</th>
      <th>"mass"</th>
      <th>"volume"</th>
      <th>"Molecular Weight"</th>
      <th>"Density"</th>
      <th>"Moles"</th>
    </tr>
  </thead>
  <tbody id = "ChemId"></tbody>
</table>  

<br><br>

<script>
  function calculate() {

    const resultChemData = document.createElement("ChemId");

    var url = "http://localhost:8679/api/Chem/create?mass=" + document.getElementById("mass").value + "&volume=" + document.getElementById("volume").value + "&molecularWeight=" + document.getElementById("molecularWeight").value;
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

        id.innerHTML = rs.id;
        user.innerHTML = rs.owner;
        mass.innerHTML = rs.mass;
        vol.innerHTML = rs.volume;
        mw.innerHTML = rs.molecularWeight;
        den.innerHTML = rs.density;
        mole.innerHTML = rs.mole;

        tr.appendChild(id);
        tr.appendChild(user);
        tr.appendChild(mass);
        tr.appendChild(vol);
        tr.appendChild(mw);
        tr.appendChild(den);
        tr.appendChild(mole);

      }
        resultChemData.appendChild(tr);
    })
    .catch(error => {
      console.log(error);
    });

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
    border: 1px solid #dddddd;
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


