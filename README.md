<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Unit Converter</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #4e54c8, #8f94fb);
        height: 100vh;
        margin: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
    }
    .container {
        background: rgba(255, 255, 255, 0.15);
        backdrop-filter: blur(10px);
        padding: 25px;
        border-radius: 20px;
        width: 350px;
        text-align: center;
        box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    }
    input, select, button {
        width: 90%;
        padding: 10px;
        margin: 10px 0;
        border-radius: 10px;
        border: none;
        font-size: 16px;
    }
    button {
        background: #ffdd57;
        cursor: pointer;
        font-weight: bold;
    }
    button:hover {
        background: #ffca2c;
    }
    #result {
        margin-top: 15px;
        font-size: 20px;
        font-weight: bold;
    }
</style>
</head>
<body>

<div class="container">
    <h2>Unit Converter</h2>

    <input type="number" id="value" placeholder="Enter value">

    <select id="option">
        <option value="f-c">Fahrenheit → Celsius</option>
        <option value="c-f">Celsius → Fahrenheit</option>
        <option value="m-ft">Meters → Feet</option>
        <option value="ft-m">Feet → Meters</option>
    </select>

    <button onclick="convert()">Convert</button>

    <div id="result"></div>
</div>

<script>
function convert() {
    let value = parseFloat(document.getElementById("value").value);
    let option = document.getElementById("option").value;
    let result = "";

    if (isNaN(value)) {
        result = "Please enter a valid number.";
    } else {
        switch(option) {
            case "f-c":
                result = ((value - 32) * 5/9).toFixed(2) + " °C";
                break;
            case "c-f":
                result = ((value * 9/5) + 32).toFixed(2) + " °F";
                break;
            case "m-ft":
                result = (value * 3.28084).toFixed(2) + " ft";
                break;
            case "ft-m":
                result = (value / 3.28084).toFixed(2) + " m";
                break;
        }
    }

    document.getElementById("result").innerHTML = result;
}
</script>

</body>
</html>
