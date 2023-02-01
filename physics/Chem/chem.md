# Chem


<html>
  <head>
    <title>Density Calculator</title>
  </head>
  <body>
    <h1>Density Calculator</h1>
    <form>
      <label for="mass">Mass (g):</label>
      <input type="number" id="mass" name="mass"><br><br>
      <label for="volume">Volume (mL):</label>
      <input type="number" id="volume" name="volume"><br><br>
      <button type="button" onclick="calculateDensity()">Calculate Density</button>
    </form>
    <br><br>
    <p id="result"></p>

   

  </body>
</html>


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
  


<script>
var elements = document.getElementsByClassName("element");

for (var i = 0; i < elements.length; i++) {
  elements[i].onclick = function() {
    this.innerHTML = "Clicked!";
  }
}
</script>

