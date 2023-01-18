# 1-prop calculations

<script src="https://cdn.jsdelivr.net/npm/chart.js@2.9.3/dist/Chart.min.js"></script>

<form>
    <label for="data">List of values (comma separated):</label>
    <input type="text" id="data" name="data"><br>
    <button type="button" onclick="calculate()">Calculate</button>
</form>
<div id="results"></div>

<script>
    function calculate() {
        var data = document.getElementById("data").value;
        data = data.split(",");
        var nums = data.map(function(x) { return parseFloat(x); });
        var mean = getMean(nums);
        var median = getMedian(nums);
        var mode = getMode(nums);
        var range = getRange(nums);
        var standardDeviation = getStandardDeviation(nums);
        var n = nums.length;
        var results = "Mean: " + mean + "<br>" +
                    "Median: " + median + "<br>" +
                    "Mode: " + mode + "<br>" +
                    "Range: " + range + "<br>" +
                    "Standard Deviation: " + standardDeviation + "<br>" +
                    "Number of terms: " + n;
        document.getElementById("results").innerHTML = results;
        createDotPlot();
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
</script>

<br><br>

<form>
    <label>Enter values separated by commas:</label>
    <input type="text" id="values" placeholder="e.g. 3, 5, 7, 2">
    <button type="button" onclick="createDotPlot()">Create Dot Plot</button>
</form>
<canvas id="dotPlot"></canvas>

<script>
    function createDotPlot() {
    var values = document.getElementById("values").value.split(",");
    var ctx = document.getElementById("dotPlot").getContext("2d");
    var dotPlot = new Chart(ctx, {
        type: "scatter",
        data: {
            datasets: [{
                label: "Values",
                data: values.map(function(value) {
                    return {
                        x: value,
                        y: 0
                    };
                }),
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
                }
            }
        }
    });
}
</script>
