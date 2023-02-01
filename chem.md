# This is the Chemistry page

<!DOCTYPE html>
<html>
  <head>
    <title>Density Calculator</title>
  </head>
  <body>
    <h1>Density Calculator</h1>
    <form>
    <label for="obj">Object name (g):</label>
      <input type="obj" id="obj" name="obj"><br><br>
      <label for="mass">Mass (g):</label>
      <input type="number" id="mass" name="mass"><br><br>
      <label for="volume">Volume (mL):</label>
      <input type="number" id="volume" name="volume"><br><br>
      <button type="button" onclick="calculateDensity()">Calculate Density</button>
    </form>
    <br><br>
    <p id="result"></p>

    <script>
      function calculateDensity() {
        var mass = document.getElementById("mass").value;
        var volume = document.getElementById("volume").value;
        var density = mass / (volume / 1000);
        document.getElementById("result").innerHTML = "Density: " + density + " g/cm^3";
      }
    </script>
  </body>
</html>
