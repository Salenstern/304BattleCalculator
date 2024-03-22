# 304BattleCalculator
304 RP Calculators
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice and Stats Calculator</title>
    <script>
        function calculateDice() {
            var numDice = document.getElementById("num_dice").value;
            var typeDice = document.getElementById("type_dice").value;
            var additiveModifier = parseInt(document.getElementById("additive_modifier").value);
            var multiplicativeModifier = parseFloat(document.getElementById("multiplicative_modifier").value);
            var total = 0;
            for (var i = 0; i < numDice; i++) {
                total += Math.floor(Math.random() * typeDice) + 1;
            }
            total = (total + additiveModifier) * multiplicativeModifier;
            document.getElementById("diceResult").innerText = "Dice Total: " + total.toFixed(2);
        }

        function generateStats() {
            let pool = [1,1,1,1,2,2,2,3,3,3,4,4,4,4,4,4,4,5,5,5,6,6,6,7,7,8,8,9,9,10];
            let numbers = [];
            for (let i = 0; i < 3; i++) {
                numbers.push(pool[Math.floor(Math.random() * pool.length)]);
            }

            // Check for hero bonus
            if (Math.floor(Math.random() * 100) + 1 === 1) {
                numbers = numbers.map(num => num + 5); // Apply Hero bonus
                document.getElementById("statsResult").innerText = "Generated Stats: " + numbers.join(", ") + " - Hero";
            } else {
                document.getElementById("statsResult").innerText = "Generated Stats: " + numbers.join(", ");
            }
        }
    </script>
</head>
<body>
    <h1>304 Calculator</h1>
    <form onsubmit="calculateDice(); return false;">
        <label for="num_dice">Number of Troop Type:</label>
        <input type="number" id="num_dice" name="num_dice" required><br><br>
        
        <label for="type_dice">Troop Type:</label>
        <select id="type_dice" name="type_dice">
            <option value="2">D2</option>
            <option value="3">D3</option>
            <option value="4">D4</option>
            <option value="5">D5</option>
            <option value="6">D6</option>
            <option value="7">D7</option>
            <option value="8">D8</option>
            <option value="10">D10</option>
            <option value="12">D12</option>
            <option value="20">D20</option>
            <option value="100">D100</option>
        </select><br><br>
        
        <label for="additive_modifier">Additive Modifier:</label>
        <input type="number" id="additive_modifier" name="additive_modifier" required><br><br>
        
        <label for="multiplicative_modifier">Multiplicative Modifier:</label>
        <input type="number" id="multiplicative_modifier" name="multiplicative_modifier" step="any" required><br><br>
        
        <input type="submit" value="Calculate">
    </form>
    <p id="diceResult"></p>

    <h1>Leader Stats Generator</h1>
    <button onclick="generateStats()">Generate Stats</button>
    <p id="statsResult"></p>
</body>
</html>
