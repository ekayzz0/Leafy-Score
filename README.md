# leafy-score

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leafy Score</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f7f7f7;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 600px;
        }
        h1 {
            color: #2d3e50;
        }
        input, button {
            padding: 10px;
            font-size: 16px;
            margin-top: 10px;
        }
        input {
            width: 80%;
            max-width: 400px;
        }
        button {
            background-color: #28a745;
            color: white;
            border: none;
            cursor: pointer;
            width: 80%;
            max-width: 400px;
        }
        button:hover {
            background-color: #218838;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Leafy Score</h1>
        <p>Enter the name of a strain you've tried and its THC content:</p>
        
        <input type="text" id="strainName" placeholder="Strain Name">
        <input type="number" id="thcContent" placeholder="THC Content (%)" min="0" max="100">
        <button onclick="addStrain()">Add Strain</button>

        <div class="result" id="result">
            <p>Your total score: <span id="totalScore">0</span></p>
            <p>Your highest THC strain: <span id="highestStrain">None</span> with <span id="highestTHC">0</span>% THC</p>
        </div>
    </div>

    <script>
        let strains = [];
        let totalScore = 0;
        let highestTHC = 0;
        let highestStrain = "None";

        function addStrain() {
            const strainName = document.getElementById("strainName").value;
            const thcContent = parseFloat(document.getElementById("thcContent").value);

            if (!strainName || isNaN(thcContent) || thcContent < 0 || thcContent > 100) {
                alert("Please enter valid strain name and THC content.");
                return;
            }

            // Add strain to array
            strains.push({ name: strainName, thc: thcContent });
            totalScore += thcContent;

            // Check if this strain has the highest THC content
            if (thcContent > highestTHC) {
                highestTHC = thcContent;
                highestStrain = strainName;
            }

            // Update the displayed score and highest strain
            document.getElementById("totalScore").textContent = totalScore;
            document.getElementById("highestStrain").textContent = highestStrain;
            document.getElementById("highestTHC").textContent = highestTHC.toFixed(2);
            
            // Reset input fields
            document.getElementById("strainName").value = '';
            document.getElementById("thcContent").value = '';
        }
    </script>
</body>
</html>
