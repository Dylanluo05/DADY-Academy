# Calendar
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
</head>

<style>
    .button-1 {
        height: 40px;
        width: 500px;
        background-color: white;
        color: #f2ba92;
        border: 2px solid #f2ba92;
        transition-duration: 0.4s;
        display: block;
        margin: auto;
    }

    .button-1:hover {
        background-color: #f2ba92;
        color: white;
    }

    .label-1 {
        display: block; 
        text-align: center;
    }

    .input-1 {
        height: 25px;
        width: 350px;
        border: none;
        background-color: lightgray;
        display: block;
        margin: auto;
    }
</style>

<form id = "person-form"> 
    <label for = "email" class = "label-1">Enter email address</label><br>
    <input type = "email" id = "year-1" name = "year-1" class = "input-1"><br>
    <label for = "name" class = "label-1">Enter name</label><br>
    <input type = "name" id = "year-2" name = "year-2" class = "input-1"><br>
    <label for = "psswd" class = "label-1">Enter Password:</label><br>
    <input type = "psswd" id = "year-2" name = "year-2" class = "input-1"><br>
    <label for = "date" class = "label-1">Enter Date of Birth:</label><br>
    <input type = "date" id = "month" name = "month" class = "input-1"><br>
    <label for = "weight" class = "label-1">Enter Weight (lbs)</label><br>
    <input type = "weight" id = "day" name = "day" class = "input-1"><br>
    <label for = "height" class = "label-1">Enter Height (inches)</label><br>
    <input type = "height" id = "day" name = "day" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br><br>

<table id="results-table">
    <tr>
        <th>Expression</th>
        <th>Tokens</th> 
        <th>RPN</th>
        <th> <strong> Result </strong> </th>
    </tr>
</table>

<script>
    // Deployed API URL
    const API_URL = 'https://frq.dtsivkovski.tk/api/person';

    // Fetching API when called by button
    document.getElementById('person-form').addEventListener('submit', (event) => {
    event.preventDefault();
    let expression = document.getElementById('expression-input').value;
    // Combine API URL with expression.
    fetch(`${API_URL}/${expression}`)
      .then(response => response.json())
      .then(data => 
      {
        // Output data to table
        const table = document.getElementById('results-table');
        const row = table.insertRow(-1);
        const expressionCell = row.insertCell(0);
        const tokensCell = row.insertCell(1);
        const rpnCell = row.insertCell(2);
        const resultCell = row.insertCell(3);
        expressionCell.innerHTML = data.Expression;
        tokensCell.innerHTML = data.Tokens;
        rpnCell.innerHTML = data.RPN;
        resultCell.innerHTML = `<strong>${data.Result}</strong>`;
      });
  });
</script>

