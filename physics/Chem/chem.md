# Chem

<!DOCTYPE html>
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

    <!-- <script>
      function calculateDensity() {
        var mass = document.getElementById("mass").value;
        var volume = document.getElementById("volume").value;
        var density = mass / (volume / 1000);
        document.getElementById("result").innerHTML = "Density: " + density + " g/cm^3";
      }
    </script>  --!>

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

