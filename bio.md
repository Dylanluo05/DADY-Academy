# Biology Overview

<br>

** Biology is the study of living organisms, divided into many specialized fields that cover their morphology, physiology, anatomy, behavior, origin, and distribution. **
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
</head>

<style>
    table {
        border-collapse: collapse;
    }

    td {
        padding: 50px;
        font-size: 20px;
        border: 2px solid black
    }

    .input-container {
        padding: 10px;
    }

    .punnett-input {
        height: 20px;
        width: 70px; 
        border: none;
        background-color: slategray;
        color: white;
        display: block;
        margin: auto;
    }

    .button-1 {
        height: 30px;
        width: 250px;
        border: 2px solid #EA3546;
        color: #EA3546;
        background-color: white;
        transition-duration: 0.4s;
        display: block;
        margin-top: 15px;
        margin-left: 25px;
        transition-duration: 0.4s;
    }

    .button-1:hover {
        color: white;
        background-color: #EA3546;
    }

    .punnett-results-container {
        border: 2px solid black;
        padding: 10px;
        width: 200px;
        margin-top: 30px;
    }

    #hardy-weinberg-form {
        height: 300px;
        width: 300px;
        padding: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: lightgray;
        margin-top: 20px;
    }

    .button-2 {
        height: 30px;
        width: 200px;
        background-color: royalblue;
        border: none;
        color: white;
        display: block;
        margin: auto;
        transition-duration: 0.4s;
    }

    .button-2:hover {
        background-color: dodgerblue;
    }
</style>

<body>
    <form id = "punnett-square-form">
        <table>
            <tr>
                <td style = "border: none;"></td>
                <td class = "input-container">
                    <input type = "text" class = "punnett-input" name = "square-input-1" required>
                </td>
                <td class = "input-container">
                    <input type = "text" class = "punnett-input" name = "square-input-2" required>
                </td>
            </tr>
            <tr>
                <td class = "input-container">
                    <input type = "text" class = "punnett-input" name = "square-input-3" required>
                </td>
                <td id = "square-1"></td>
                <td id = "square-2"></td>
            </tr>
            <tr>
                <td class = "input-container">
                    <input type = "text" class = "punnett-input" name = "square-input-4" required>
                </td>
                <td id = "square-3"></td>
                <td id = "square-4"></td>
            </tr>
        </table>
        <input type = "submit" class = "button-1" value = "Update Punnett Square">
    </form>
    <div class = "punnett-results-container">
        <p id = "dominant-percentage-display">Chance of inheriting dominant trait:</p>
        <p id = "recessive-percentage-display">Chance of inheriting recessive trait:</p>
    </div>
    <form id = "hardy-weinberg-form">
        <div id = "hardy-weinberg-inputs">
            <h2 style = "font-weight: lighter; text-align: center;">p^2 + 2pq + q^2 = 1</h3>
            <ul>
                <li>p = Dominant allele frequency</li>
                <li>q = Recessive allele frequency</li>
            </ul>
            <label for = "p-value" style = "display: block; text-align: center; font-size: 15px;">Enter p value:</label>
            <input type = "text" style = "display: block; margin: auto;" name = "p-value" required>
            <br>
            <label for = "q-value" style = "display: block; text-align: center; font-size: 15px;">Enter q value:</label>
            <input type = "text" style = "display: block; margin: auto;" name = "q-value" required>
            <br>
            <input type = "submit" class = "button-2" value = "Compute">
        </div>
        <div id = "hardy-weinberg-results"> 
            <h2 id = "equilibrium-status" style = "text-align: center;"></h2>
            <button id = "return-button" class = "button-2">Return to input page</button>
        </div>
    </form>
    <script>
        $("#punnett-square-form").on("submit", punnettUpdate);
        var square1 = document.getElementById("square-1");
        var square2 = document.getElementById("square-2");
        var square3 = document.getElementById("square-3");
        var square4 = document.getElementById("square-4");

        function punnettUpdate() {
            event.preventDefault();
            var formData = $("#punnett-square-form").serializeArray();
            var square1Combination = "";
            var square2Combination = "";
            var square3Combination = "";
            var square4Combination = "";
            var squareCombinations = [];
            if (formData[2].value.toLowerCase() == formData[2].value && formData[0].value.toUpperCase() == formData[0].value) {
                square1Combination += formData[0].value + formData[2].value;
            } else {
                square1Combination += formData[2].value + formData[0].value;
            }
            squareCombinations.push(square1Combination);
            if (formData[2].value.toLowerCase() == formData[2].value && formData[1].value.toUpperCase() == formData[1].value) {
                square2Combination += formData[1].value + formData[2].value;
            } else {
                square2Combination += formData[2].value + formData[1].value;
            }
            squareCombinations.push(square2Combination);
            if (formData[3].value.toLowerCase() == formData[3].value && formData[0].value.toUpperCase() == formData[0].value) {
                square3Combination += formData[0].value + formData[3].value;
            } else {
                square3Combination += formData[3].value + formData[0].value;
            }
            squareCombinations.push(square3Combination);
            if (formData[3].value.toLowerCase() == formData[3].value && formData[1].value.toUpperCase() == formData[1].value) {
                square4Combination += formData[1].value + formData[3].value;
            } else {
                square4Combination += formData[3].value + formData[1].value;
            }
            squareCombinations.push(square4Combination);
            
            square1.innerHTML = square1Combination;
            square2.innerHTML = square2Combination;
            square3.innerHTML = square3Combination;
            square4.innerHTML = square4Combination;

            var dominantCount = 0;
            
            for (var key in squareCombinations) {
                for (var j = 0; j < squareCombinations[key].length; j++) {
                    if (squareCombinations[key].substring(j, j + 1).toUpperCase() == squareCombinations[key].substring(j, j + 1)) {
                        dominantCount++;
                        break;
                    }
                }
            }

            var dominantPercentage = (dominantCount / 4) * 100;
            var recessivePercentage = 100 - dominantPercentage;
            var dominantPercentageDisplay = document.getElementById("dominant-percentage-display");
            var recessivePercentageDisplay = document.getElementById("recessive-percentage-display");
            dominantPercentageDisplay.innerHTML = "Chance of inheriting dominant trait: " + dominantPercentage + "%";
            recessivePercentageDisplay.innerHTML = "Chance of inheriting recessive trait: " + recessivePercentage + "%"; 
            document.getElementById("punnett-square-form").reset();
        }
        var hardyWeinbergInputs = document.getElementById("hardy-weinberg-inputs");
        hardyWeinbergInputs.style.display = "block";
        var hardyWeinbergResults = document.getElementById("hardy-weinberg-results");
        hardyWeinbergResults.style.display = "none";
        var equilibriumStatus = document.getElementById("equilibrium-status");
        var returnButton = document.getElementById("return-button");
        returnButton.addEventListener("click", returnHardyWeinberg);
        function returnHardyWeinberg() {
            hardyWeinbergResults.style.display = "none";
            hardyWeinbergInputs.style.display = "block";
        }
        $("#hardy-weinberg-form").on("submit", hardyWeinberg);
        function hardyWeinberg() {
            event.preventDefault();
            var hardyWeinbergFormData = $("#hardy-weinberg-form").serializeArray();
            var pValue = parseFloat(hardyWeinbergFormData[0].value);
            var qValue = parseFloat(hardyWeinbergFormData[1].value);
            var hardyWeinbergSum = (pValue ** 2) + (2 * pValue * qValue) + (qValue ** 2);
            
            document.getElementById("hardy-weinberg-form").reset();
            hardyWeinbergInputs.style.display = "none";
            hardyWeinbergResults.style.display = "block";
            
            if (hardyWeinbergSum == 1) {
                equilibriumStatus.innerHTML = "The population is at equilibrium";
            } else {
                equilibriumStatus.innerHTML = "The population is not at equilibrium";
            }
        }
    </script>
</body>

