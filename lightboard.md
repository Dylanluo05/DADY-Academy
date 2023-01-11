# Lightboard API

<button id="refresh-button">Generate New</button>

<div id="table-container"></div>

<script>

// API, generates a 5 by 5 board
const API_URL = 'https://frq.dtsivkovski.tk/api/lightboard/generate/5/5';

// define tablecontainer
const tableContainer = document.getElementById("table-container");

// Refresh button to refresh table
const refreshButton = document.getElementById('refresh-button');

// Refresh table 
function refreshTable() {
  fetch(API_URL)
    .then(response => response.json())
    .then(data => {

        // Remove the existing table
        while (tableContainer.firstChild) {
        tableContainer.removeChild(tableContainer.firstChild);
        }

        // Styling for table
        const table = document.createElement('table');
        table.style.width = '50%';
        table.style.margin = '0 auto';

        // Set row value based on object's row value, create row if new
        let currentRow;
        for (const { row, column, light } of data) {
        if (row !== currentRow) {
            currentRow = row;
            const tr = document.createElement('tr');
            table.appendChild(tr);
        }

        // Create box element with background color based on rgb value
        const td = document.createElement('td');
        td.style.backgroundColor = `rgb(${light.red}, ${light.green}, ${light.blue})`;

        // Set text color based on brightness
        const brightness = (light.red * 299 + light.green * 587 + light.blue * 114) / 1000;
        if (brightness < 128) {
          td.style.color = 'white';
        } else {
          td.style.color = 'black';
        }

        // Styling for the text inside the box, append to table
        td.innerText = `#${light.red.toString(16).padStart(2, '0')}${light.green.toString(16).padStart(2, '0')}${light.blue.toString(16).padStart(2, '0')}`;
        td.style.textAlign = 'center';
        td.style.verticalAlign = 'middle';
        td.style.fontFamily = 'monospace';
        table.lastElementChild.appendChild(td);
      }

    // Add the new table to the table container
    tableContainer.appendChild(table);

    });
}

refreshButton.addEventListener('click', refreshTable);

</script>
