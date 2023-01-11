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

## isLeapYear()

<form id = "calendar-form-1"> 
    <label for = "year-1" class = "label-1">Enter a year:</label><br>
    <input type = "number" id = "year-1" name = "year-1" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br>

<table id="results-table-1">
    <tr>
        <th>Year</th>
        <th>isLeapYear</th>
    </tr>
</table>

<br>

## firstDayOfYear()

<form id = "calendar-form-2"> 
    <label for = "year-2" class = "label-1">Enter a year:</label><br>
    <input type = "number" id = "year-2" name = "year-2" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br>

<table id="results-table-2">
    <tr>
        <th>Year</th>
        <th>firstDayOfYear</th>
    </tr>
</table>

<br>

## dayOfYear()

<form id = "calendar-form-3"> 
    <label for = "year-3" class = "label-1">Enter a year:</label><br>
    <input type = "number" id = "year-3" name = "year-3" class = "input-1"><br>
    <label for = "month-3" class = "label-1">Enter a month:</label><br>
    <input type = "number" id = "month-3" name = "month-3" class = "input-1"><br>
    <label for = "day-3" class = "label-1">Enter a day:</label><br>
    <input type = "number" id = "day-3" name = "day-3" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br>

<table id="results-table-3">
    <tr>
        <th>Year</th>
        <th>Month</th>
        <th>Day</th>
        <th>dayOfYear</th>
    </tr>
</table>

<br>

## dayOfWeek()

<form id = "calendar-form-4"> 
    <label for = "year-4" class = "label-1">Enter a year:</label><br>
    <input type = "number" id = "year-4" name = "year-4" class = "input-1"><br>
    <label for = "month-4" class = "label-1">Enter a month:</label><br>
    <input type = "number" id = "month-4" name = "month-4" class = "input-1"><br>
    <label for = "day-4" class = "label-1">Enter a day:</label><br>
    <input type = "number" id = "day-4" name = "day-4" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br>

<table id="results-table-4">
    <tr>
        <th>Year</th>
        <th>Month</th>
        <th>Day</th>
        <th>dayOfWeek</th>
    </tr>
</table>

<br>

## numberOfLeapYears()

<form id = "calendar-form-5"> 
    <label for = "year-pair-1" class = "label-1">Enter the first year:</label><br>
    <input type = "number" id = "year-pair-1" name = "year-pair-1" class = "input-1"><br>
    <label for = "year-pair-2" class = "label-1">Enter the second year:</label><br>
    <input type = "number" id = "year-pair-2" name = "year-pair-2" class = "input-1"><br>
    <input type = "submit" class = "button-1">
</form>

<br>

<table id="results-table-5">
    <tr>
        <th>Year 1</th>
        <th>Year 2</th>
        <th>numberOfLeapYears</th>
    </tr>
</table>

<script>
    // Deployed API URL
    const API_URL = 'https://frq.dtsivkovski.tk/api/calendar';

    // Fetching API when called by button
    document.getElementById('calendar-form-1').addEventListener('submit', (event) => {
        event.preventDefault();
        var year1 = document.getElementById('year-1').value;
        // Combine API URL with expression.
        fetch(`${API_URL}/isLeapYear/${year1}`)
        .then(response => response.json())
        .then(data => {
            // Output data to table
            const table = document.getElementById('results-table-1');
            const row = table.insertRow(-1);
            const year1Cell = row.insertCell(0);
            const isLeapYearCell = row.insertCell(1);
            year1Cell.innerHTML = data.year;
            isLeapYearCell.innerHTML = data.isLeapYear;
        });
    });

    document.getElementById('calendar-form-2').addEventListener('submit', (event) => {
        event.preventDefault();
        var year2 = document.getElementById('year-2').value;
        // Combine API URL with expression.
        fetch(`${API_URL}/firstDayOfYear/${year2}`)
        .then(response => response.json())
        .then(data => {
            // Output data to table
            const table = document.getElementById('results-table-2');
            const row = table.insertRow(-1);
            const year2Cell = row.insertCell(0);
            const firstDayOfYearCell = row.insertCell(1);
            year2Cell.innerHTML = data.year;
            firstDayOfYearCell.innerHTML = data.firstDayOfYear;
        });
    });

    document.getElementById('calendar-form-3').addEventListener('submit', (event) => {
        event.preventDefault();
        var year3 = document.getElementById('year-3').value;
        var month3 = document.getElementById('month-3').value;
        var day3 = document.getElementById('day-3').value;
        // Combine API URL with expression.
        fetch(`${API_URL}/dayOfYear/${month3}/${day3}/${year3}`)
        .then(response => response.json())
        .then(data => {
            // Output data to table
            const table = document.getElementById('results-table-3');
            const row = table.insertRow(-1);
            const year3Cell = row.insertCell(0);
            const month3Cell = row.insertCell(1);
            const day3Cell = row.insertCell(2)
            const dayOfYearCell = row.insertCell(3);
            year3Cell.innerHTML = data.year;
            month3Cell.innerHTML = data.month;
            day3Cell.innerHTML = data.day;
            dayOfYearCell.innerHTML = data.dayOfYear;
        });
    });

    document.getElementById('calendar-form-4').addEventListener('submit', (event) => {
        event.preventDefault();
        var year4 = document.getElementById('year-4').value;
        var month4 = document.getElementById('month-4').value;
        var day4 = document.getElementById('day-4').value;
        // Combine API URL with expression.
        fetch(`${API_URL}/dayOfWeek/${month4}/${day4}/${year4}`)
        .then(response => response.json())
        .then(data => {
            // Output data to table
            const table = document.getElementById('results-table-4');
            const row = table.insertRow(-1);
            const year4Cell = row.insertCell(0);
            const month4Cell = row.insertCell(1);
            const day4Cell = row.insertCell(2);
            const dayOfWeekCell = row.insertCell(3);
            year4Cell.innerHTML = data.year;
            month4Cell.innerHTML = data.month;
            day4Cell.innerHTML = data.day;
            dayOfWeekCell.innerHTML = data.dayOfWeek;
        });
    });

    document.getElementById('calendar-form-5').addEventListener('submit', (event) => {
        event.preventDefault();
        var yearPair1 = document.getElementById('year-pair-1').value;
        var yearPair2 = document.getElementById('year-pair-2').value;
        // Combine API URL with expression.
        fetch(`${API_URL}/numberOfLeapYears/${yearPair1}/${yearPair2}`)
        .then(response => response.json())
        .then(data => {
            // Output data to table
            const table = document.getElementById('results-table-5');
            const row = table.insertRow(-1);
            const yearPair1Cell = row.insertCell(0);
            const yearPair2Cell = row.insertCell(1);
            const numberOfLeapYearsCell = row.insertCell(2);
            yearPair1Cell.innerHTML = data.year1;
            yearPair2Cell.innerHTML = data.year2;
            numberOfLeapYearsCell.innerHTML = data.numberOfLeapYears;
        });
    });
</script>