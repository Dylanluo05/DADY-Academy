<head>
  <title>Density Calculator</title>
  

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
</style>


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

  <h1>Moles Calculator</h1>

  <form>
    <label for="obj">Object name (g):</label>
    <input type="obj" id="obj" name="obj"><br><br>
    <label for="mass">Molecular weight (g):</label>
    <input type="number" id="mass" name="mass"><br><br>
    
    <button type="button" onclick="calculatemoles()">Calculate Moles</button>
  </form>

<br>
<br>
<br>


<html>
<head>
    <style>
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

      tr:nth-child(even) {
        background-color: #dddddd;
      }
    </style>
  </head>
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
  </body>
</html>

<script>




  
</body>