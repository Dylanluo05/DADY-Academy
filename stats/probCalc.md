# Z-Score to Probability Calculator

<script src="https://cdnjs.cloudflare.com/ajax/libs/jstat/1.8.1/jstat.min.js"></script>


<form>
    <label for="z-score">Enter Z-Score:</label>
    <input type="text" id="z-score" name="z-score">
    <button type="button" onclick="calculateProbability()">Calculate Probability</button>
</form>
<p>Probability: <span id="result"></span></p>

<script>
    function calculateProbability() {
        var z = document.getElementById("z-score").value;
        var p = jStat.normal.cdf(z, 0, 1);
        document.getElementById("result").innerHTML = p.toFixed(4);
    }
</script>

<br>

# T-Score Calculator

<form>
    <label for="df">Enter degrees of freedom:</label>
    <input type="text" id="df"><br>
    <label for="tp">Enter tail probability:</label>
    <input type="text" id="prob"><br>
    <button type="button" onclick="calculateTScore()">Calculate T-Score</button>
</form>

<p>T-Score: <span id="tScore"></span></p>

<script>
    function calculateTScore() {
        var df = document.getElementById("df").value;
        var prob = document.getElementById("prob").value;
        var tScore = jStat.studentt.inv(prob, df);
        document.getElementById("tScore").innerHTML = tScore;
    }
</script>


# Standard Deviation of the Sampling Distribution (Population Proportion)

<form>
    <label for="proportion">Population Proportion:</label>
    <input type="text" id="proportion" name="proportion"><br>
    <label for="sampleSize">Sample Size:</label>
    <input type="text" id="ssSD" name="sampleSize"><br>
    <button type="button" onclick="calculateSD()">Calculate</button>
</form>
<p id="result1"></p>
<script>
    function calculateSD() {
        var proportion = document.getElementById("proportion").value;
        var ssSD = document.getElementById("ssSD").value;
        var stddev = Math.sqrt((proportion*(1-proportion))/ssSD);
        document.getElementById("result1").innerHTML = "Standard deviation of the sampling distribution: " + stddev;
    }
</script>


# Standard Deviation of the Sampling Distribution (Population Mean)

<form>
    <label for="standardError">Standard Error:</label>
    <input type="text" id="standardError" name="standardError"><br>
    <label for="sampleSize">Sample Size:</label>
    <input type="text" id="ssSE" name="sampleSize"><br>
    <button type="button" onclick="calculateSE()">Calculate</button>
</form>
<p id="result2"></p>
<script>
    function calculateSE() {
        var standardError = document.getElementById("standardError").value;
        var ssSE = document.getElementById("ssSE").value;
        var standarddev = standardError / Math.sqrt(ssSE);
        document.getElementById("result2").innerHTML = "Standard deviation of the sampling distribution: " + standarddev;
    }
</script>
