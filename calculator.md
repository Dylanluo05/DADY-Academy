# Calculator


<form id="calculator-form">
  <label for="expression-input">Expression:</label><br>
  <input type="text" id="expression-input" name="expression"><br>
  <button type="submit" id="submit-button">Submit</button>
</form> 

<br/>

## History

<button id="clear-button">Clear History</button>

<table id="results-table">
  <tr>
    <th>Expression</th>
    <th>Tokens</th> 
    <th>RPN</th>
    <th> <strong> Result </strong> </th>
  </tr>
</table>

<script>
// Button to clear table if wanted
document.getElementById('clear-button').addEventListener('click', () => {
    const table = document.getElementById('results-table');
    // iterate while table rows exist (except for headers)
    while (table.rows.length > 1) {
      table.deleteRow(-1);
    }
  });

// Deployed API URL
  const API_URL = 'https://frq.dtsivkovski.tk/api/calculator';

// Fetching API when called by button
  document.getElementById('calculator-form').addEventListener('submit', (event) => {
    event.preventDefault();
    let expression = document.getElementById('expression-input').value;
    expression = expression.replace(/\^/g, 'POW');
    // Combine API URL with expression.
    fetch(`${API_URL}/${expression}`)
      .then(response => response.json())
      .then(data => {
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