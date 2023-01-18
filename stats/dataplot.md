# Stats Data Modeler

<script src="https://cdn.jsdelivr.net/npm/chart.js@2.9.3/dist/Chart.min.js"></script>

<form>
    <label for="data">List of values (comma separated):</label>
    <input type="text" id="values" name="data"><br>
    <button type="button" onclick="calculate(); createDotPlot()">Calculate</button>
</form>

<br><br>

<table id="output-table">
    <tr>
        <th> n </th>
        <th> Mean </th>
        <th> Median </th>
        <th> Mode </th>
        <th> Range </th>
        <th> Standard Deviation </th>
    </tr>
    <tr>
        <td id="numTerms">-</td>
        <td id="mean">-</td>
        <td id="median">-</td>
        <td id="mode">-</td>
        <td id="range">-</td>
        <td id="standardDeviation">-</td>
    </tr>
</table>

<br><br>

<canvas id="dotPlot"></canvas>

<script>
    function calculate() {
        var data = document.getElementById("values").value;
        data = data.split(",");
        var nums = data.map(function(x) { return parseFloat(x); });
        var mean = getMean(nums);
        var median = getMedian(nums);
        var mode = getMode(nums);
        var range = getRange(nums);
        var standardDeviation = getStandardDeviation(nums);
        var n = nums.length;
        document.getElementById("mean").innerHTML = mean;
        document.getElementById("median").innerHTML = median;
        document.getElementById("mode").innerHTML = mode;
        document.getElementById("range").innerHTML = range;
        document.getElementById("standardDeviation").innerHTML = standardDeviation;
        document.getElementById("numTerms").innerHTML = n;

        // var results = "Mean: " + mean + "<br>" +
        //             "Median: " + median + "<br>" +
        //             "Mode: " + mode + "<br>" +
        //             "Range: " + range + "<br>" +
        //             "Standard Deviation: " + standardDeviation + "<br>" +
        //             "Number of terms: " + n;
        // document.getElementById("results").innerHTML = results;
    }
  
    function getMean(nums) {
        var sum = nums.reduce(function(a, b) { return a + b; });
        return (sum / nums.length).toFixed(2);
    }
  
    function getMedian(nums) {
        nums.sort(function(a, b) { return a - b; });
        var middle = Math.floor(nums.length / 2);
        if (nums.length % 2 === 0) {
            return (nums[middle - 1] + nums[middle]) / 2;
        } else {
            return nums[middle];
        }
    }
  
    function getMode(nums) {
        var mode = {};
        var max = 0;
        var result;
        for (var i = 0; i < nums.length; i++) {
            if (!mode[nums[i]]) {
            mode[nums[i]] = 0;
            }
            mode[nums[i]]++;
            if (mode[nums[i]] > max) {
            max = mode[nums[i]];
            result = nums[i];
            }
        }
        return result;
    }

    function getRange(nums) {
        return Math.max.apply(null, nums) - Math.min.apply(null, nums);
    }
  
    function getStandardDeviation(nums) {
        var mean = getMean(nums);
        var squareDiffs = nums.map(function(value) {
            var diff = value - mean;
            var sqrDiff = diff * diff;
            return sqrDiff;
        });
        var avgSquareDiff = getMean(squareDiffs);
        var stdDev = Math.sqrt(avgSquareDiff);
        return stdDev.toFixed(2);
    }

    function createDotPlot() {
        var values = document.getElementById("values").value.split(",");
        var ctx = document.getElementById("dotPlot").getContext("2d");
        var data = values.reduce(function(acc, curr) {
            acc[curr] = acc[curr] ? acc[curr] + 1 : 1;
            return acc;
        }, {});
        var dataPoints = Object.keys(data).map(function(value) {
            return {x: value, y: data[value]};
        });
        var dotPlot = new Chart(ctx, {
            type: "scatter",
            data: {
                datasets: [{
                    label: "Values",
                    data: dataPoints,
                    borderColor: "red",
                    backgroundColor: "red",
                    pointRadius: 3
                }]
            },
            options: {
                scales: {
                    x: {
                        type: "linear",
                        position: "bottom"
                    },
                    y: {
                        type: "linear",
                        position: "left"
                    }
                }
            }
        });
    }
</script>