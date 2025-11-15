<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Multi-Tool Program</title>

<style>
    /* GENERAL PAGE DESIGN */
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #4b79a1, #283e51);
        color: white;
    }

    h2 {
        text-align: center;
        margin-top: 0;
    }

    /* MENU BAR */
    .menu {
        display: flex;
        justify-content: center;
        gap: 20px;
        padding: 15px;
        background: rgba(0,0,0,0.3);
        position: sticky;
        top: 0;
    }

    .menu button {
        padding: 12px 20px;
        border: none;
        border-radius: 10px;
        background: #ffc107;
        cursor: pointer;
        font-weight: bold;
    }

    .menu button:hover {
        background: #ffb300;
    }

    /* TOOL CONTAINER */
    .container {
        width: 85%;
        margin: 20px auto;
        padding: 25px;
        background: rgba(255,255,255,0.15);
        border-radius: 20px;
        backdrop-filter: blur(8px);
        box-shadow: 0 10px 25px rgba(0,0,0,0.3);
        display: none;
    }

    input, select {
        width: 90%;
        padding: 10px;
        border: none;
        border-radius: 10px;
        font-size: 16px;
        margin-top: 10px;
    }

    button.action {
        margin-top: 15px;
        padding: 12px 25px;
        border: none;
        border-radius: 10px;
        background: #ffdd57;
        cursor: pointer;
        font-weight: bold;
        font-size: 17px;
    }

    button.action:hover {
        background: #ffca28;
    }

    /* TABLES */
    table {
        width: 100%;
        margin-top: 20px;
        border-collapse: collapse;
    }

    th, td {
        padding: 10px;
        border: 1px solid rgba(255,255,255,0.3);
        text-align: center;
    }

    th {
        background: rgba(0,0,0,0.4);
    }
</style>
</head>
<body>

<!-- ================= MENU ================= -->
<div class="menu">
    <button onclick="showTool('converter')">Unit Converter</button>
    <button onclick="showTool('tax')">Income Tax Calculator</button>
    <button onclick="showTool('loops')">Loop Calculator</button>
    <button onclick="showTool('payroll')">Payroll System</button>
</div>

<!-- ======================================================
          1. UNIT CONVERTER
====================================================== -->
<div id="converter" class="container">
    <h2>Unit Converter</h2>

    <input type="number" id="convValue" placeholder="Enter value">

    <select id="convOption">
        <option value="f-c">Fahrenheit → Celsius</option>
        <option value="c-f">Celsius → Fahrenheit</option>
        <option value="m-ft">Meters → Feet</option>
        <option value="ft-m">Feet → Meters</option>
    </select>

    <button class="action" onclick="convert()">Convert</button>

    <div id="convResult"></div>
</div>

<!-- ======================================================
          2. INCOME TAX CALCULATOR
====================================================== -->
<div id="tax" class="container">
    <h2>Income Tax Calculator</h2>

    <input type="number" id="income" placeholder="Enter Taxable Income">

    <button class="action" onclick="computeTax()">Compute Tax</button>

    <div id="taxResult"></div>
</div>

<!-- ======================================================
          3. LOOP CALCULATOR
====================================================== -->
<div id="loops" class="container">
    <h2>Loop Calculator</h2>

    <input type="number" id="num" placeholder="Enter an integer value">

    <button class="action" onclick="computeLoops()">Compute</button>

    <div id="loopOutput"></div>
</div>

<!-- ======================================================
          4. PAYROLL SYSTEM
====================================================== -->
<div id="payroll" class="container">
    <h2>Payroll Management System</h2>

    <input type="text" id="empName" placeholder="Employee Name">
    <input type="number" id="daysWorked" placeholder="Days Worked">
    <input type="number" id="dailyRate" placeholder="Daily Rate">
    <input type="number" id="deduction" placeholder="Deduction">

    <button class="action" onclick="addEmployee()">Add Employee</button>

    <table id="payTable">
        <thead>
            <tr>
                <th>No.</th>
                <th>Name</th>
                <th>Days</th>
                <th>Rate</th>
                <th>Gross Pay</th>
                <th>Deduction</th>
                <th>Net Pay</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <input type="number" id="deleteLine" placeholder="Line to delete">
    <button class="action" onclick="deleteEmployee()">Delete</button>
</div>

<!-- ======================= JAVASCRIPT ======================= -->
<script>
function showTool(id) {
    document.querySelectorAll('.container')
            .forEach(div => div.style.display = 'none');
    document.getElementById(id).style.display = 'block';
}

/* ---------- 1. UNIT CONVERTER ---------- */
function convert() {
    let val = parseFloat(document.getElementById("convValue").value);
    let opt = document.getElementById("convOption").value;
    let res = "";

    if (isNaN(val)) { res = "Enter a valid number."; }
    else {
        switch(opt) {
            case "f-c": res = ((val - 32) * 5/9).toFixed(2) + " °C"; break;
            case "c-f": res = ((val * 9/5) + 32).toFixed(2) + " °F"; break;
            case "m-ft": res = (val * 3.28084).toFixed(2) + " ft"; break;
            case "ft-m": res = (val / 3.28084).toFixed(2) + " m"; break;
        }
    }
    document.getElementById("convResult").innerHTML = res;
}

/* ---------- 2. INCOME TAX ---------- */
function computeTax() {
    let inc = parseFloat(document.getElementById("income").value);
    let t = 0;

    if (inc <= 250000) t = 0;
    else if (inc <= 400000) t = (inc - 250000) * 0.20;
    else if (inc <= 800000) t = 30000 + (inc - 400000) * 0.25;
    else if (inc <= 2000000) t = 130000 + (inc - 800000) * 0.30;
    else if (inc <= 8000000) t = 490000 + (inc - 2000000) * 0.32;
    else t = 2410000 + (inc - 8000000) * 0.35;

    document.getElementById("taxResult").innerHTML =
        "Income Tax: ₱" + t.toLocaleString(undefined, {minimumFractionDigits: 2});
}

/* ---------- 3. LOOPS ---------- */
function computeLoops() {
    let n = parseInt(document.getElementById("num").value);
    if (isNaN(n) || n < 1) {
        document.getElementById("loopOutput").innerHTML = "Enter valid number.";
        return;
    }

    // Factorial using while
    let fact = 1, i = 1;
    while (i <= n) { fact *= i; i++; }

    // Sum using do-while
    let sum = 0, j = 1;
    do { sum += j; j++; } while (j <= n);

    // Average using for
    let avg = 0;
    for (let k=1; k<=n; k++) avg += k;
    avg /= n;

    document.getElementById("loopOutput").innerHTML =
        `Factorial: ${fact}<br>
         Sum: ${sum}<br>
         Average: ${avg.toFixed(2)}`;
}

/* ---------- 4. PAYROLL ---------- */
let payroll = [];

function addEmployee() {
    let name = empName.value;
    let d = parseInt(daysWorked.value);
    let r = parseFloat(dailyRate.value);
    let ded = parseFloat(deduction.value);

    if (!name || isNaN(d) || isNaN(r) || isNaN(ded)) {
        alert("Complete all fields!");
        return;
    }

    payroll.push({
        name: name,
        days: d,
        rate: r,
        gross: d * r,
        ded: ded,
        net: (d * r) - ded
    });

    updatePayroll();
}

function updatePayroll() {
    let body = document.querySelector("#payTable tbody");
    body.innerHTML = "";

    payroll.forEach((p, idx) => {
        body.innerHTML += `
            <tr>
                <td>${idx+1}</td>
                <td>${p.name}</td>
                <td>${p.days}</td>
                <td>${p.rate.toFixed(2)}</td>
                <td>${p.gross.toFixed(2)}</td>
                <td>${p.ded.toFixed(2)}</td>
                <td>${p.net.toFixed(2)}</td>
            </tr>`;
    });
}

function deleteEmployee() {
    let idx = parseInt(deleteLine.value);
    if (idx < 1 || idx > payroll.length) {
        alert("Invalid line number.");
        return;
    }
    payroll.splice(idx-1, 1);
    updatePayroll();
}
</script>

</body>
</html>

