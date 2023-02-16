# Chem


<html>
  <head>
    <title>Density and Moles Calculator</title>
  </head>
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
</html>

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
  <tbody id = "Chemid"></tbody>
</table>  

<script>
function calculate() {
const mass = document.getElementById("mass").value;
const volume = document.getElementById("volume").value;
const mw = document.getElementById("molecularWeight").value;

const resultChemData = document.getElementbyId("Chemid");

var url = "https://frq.dtsivkovski.tk/api/Chem/create/";

const body = {
  mass: mass,
  volume: volume,
  molecularWeight: molecularWeight
};

fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(body)
})
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

    resultChemData.appendChild(tr);
  }
})
.catch(error => {
  console.error(error);
});

}
</script>


<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
  }
  
  input[type="number"] {
    width: 150px;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 4px;
  }
  
  button {
    width: 150px;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 4px;
    background-color: #4CAF50;
    color: white;
  }
  
  button:hover {
    background-color: #45a049;
  }
</style>


<table id="periodic-table">
  <tr>
    <td class="element" id="H"></td>
    <td class="element" id="He"></td>
  </tr>
  <tr>
    <td class="element" id="Li"></td>
    <td class="element" id="Be"></td>
  </tr>
</table>

 <title>Chemical Calculations Cheat Sheet</title>
</head>
<body>
  <h1>Chemical Calculations Cheat Sheet</h1>
  
  <h2>Molar mass</h2>
  <p>The molar mass of a substance is the mass of one mole of that substance.</p>
  
  <h2>Molar volume</h2>
  <p>The molar volume of a gas is the volume occupied by one mole of that gas at standard temperature and pressure (STP).</p>
  
  <h2>Ideal gas law</h2>
  
<p>The ideal gas law states that the pressure, volume, and temperature of a gas are related by the equation:</p>
  
  <p>PV = nRT</p>
  
  <p>Where:</p>
  <ul>
    <li>P = pressure (in atm)</li>
    <li>V = volume (in L)</li>
    <li>n = number of moles of gas</li>
    <li>R = ideal gas constant (0.0821 L atm/mol K)</li>
    <li>T = temperature (in K)</li>
  </ul>
  
  <h2>Density</h2>
  <p>Density is the mass per unit volume of a substance. It can be calculated using the equation:</p>
  
  <p>density = mass/volume</p>
  
  <p>The SI unit of density is kg/m<sup>3</sup>.</p>
  
</body>
</html>

