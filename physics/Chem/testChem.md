# Chem

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

  tr:nth-child(even) {
    background-color: #dddddd;
  }
</style>

<body>
<h1>Density and Moles Calculator</h1>
<form id="input-form">
  <label for="mass">Mass:</label>
  <input type="number" id="mass" name="mass" required>
  <br>
  <label for="volume">Volume:</label>
  <input type="number" id="volume" name="volume" required>
  <br>
  <label for="molecular-weight">Molecular weight:</label>
  <input type="number" id="molecular-weight" name="molecular-weight" required>
  <br>
  <button type="submit">Calculate</button>
</form>

<table>
  <thead>
    <tr>
      <th>Mass</th>
      <th>Volume</th>
      <th>Molecular weight</th>
      <th>Density</th>
      <th>Moles</th>
    </tr>
  </thead>
  <tbody id="result-table-body"></tbody>
</table>


<br><br>

<script>
    const API_URL = "http://localhost:8679/api/Chem/create/"; // replace with actual API URL

// function to handle form submission
function handleFormSubmit(event) {
  event.preventDefault(); // prevent default form submission behavior

  // get input values from form
  const mass = parseFloat(document.getElementById("mass").value);
  const volume = parseFloat(document.getElementById("volume").value);
  const molecularWeight = parseFloat(document.getElementById("molecular-weight").value);

  // send input values to API and get results
  const formData = new FormData();
  formData.append("mass", mass);
  formData.append("volume", volume);
  formData.append("molecularWeight", molecularWeight);
  fetch(API_URL, {
    method: "POST",
    body: formData
  })
  .then(response => response.json())
  .then(result => {
    // display results in table
    const tableBody = document.getElementById("result-table-body");
    tableBody.innerHTML = `
      <tr>
        <td>${mass}</td>
        <td>${volume}</td>
        <td>${molecularWeight}</td>
        <td>${result.density}</td>
        <td>${result.moles}</td>
      </tr>
    `;
  })
  .catch(error => {
    console.error(error);
    alert("An error occurred. Please try again later.");
  });
}

// add event listener to form submit button
const form = document.getElementById("input-form");
form.addEventListener("submit", handleFormSubmit);

</script>

