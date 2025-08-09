<html>
<head>
    <title>POS MDR Savings Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .calculator {
            background: #fff;
            padding: 20px 25px;
            border-radius: 10px;
            box-shadow: 0px 4px 12px rgba(0,0,0,0.1);
            width: 500px; /* Increased width */
        }
        h2 {
            text-align: center;
            margin-bottom: 15px;
            color: #800000; /* Maroonish red */
        }
        label {
            margin-top: 10px;
            display: block;
            font-weight: bold;
            color: #800000;
        }
        input, select, button {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 14px;
        }
        button {
            background: #800000; /* Maroonish red */
            color: white;
            font-size: 16px;
            margin-top: 15px;
            cursor: pointer;
        }
        button:hover {
            background: #a52a2a;
        }
        .result {
            margin-top: 20px;
            background: #ffe6e6; /* Light red shade */
            padding: 10px;
            border-radius: 5px;
            font-weight: bold;
            color: #800000;
        }
        .line {
            white-space: nowrap; /* Prevent wrapping */
            overflow-x: auto; /* Scroll if too long */
        }
    </style>
</head>
<body>

<div class="calculator">
    <h2>SAVINGS WITH IDFC CURRENT ACCOUNT</h2>

    <label>Account Variant</label>
    <select id="variant">
        <option value="10">₹50K Variant (10%)</option>
        <option value="12">₹1Lac Variant (12%)</option>
        <option value="15">₹2Lac Variant (15%)</option>
    </select>

    <label>Last Month UPI Collection (₹)</label>
    <input type="number" id="upi" placeholder="Enter UPI amount">

    <label>This Month POS Collection (₹)</label>
    <input type="number" id="pos" placeholder="Enter POS amount">

    <button onclick="calculate()">Calculate Savings</button>

    <div class="result" id="result"></div>
</div>

<script>
function calculate() {
    let variantPercent = parseFloat(document.getElementById("variant").value);
    let upi = parseFloat(document.getElementById("upi").value);
    let pos = parseFloat(document.getElementById("pos").value);

    if (isNaN(upi) || isNaN(pos) || upi <= 0 || pos <= 0) {
        document.getElementById("result").innerHTML = "Please enter valid amounts.";
        return;
    }

    let freeLimit = (upi * variantPercent) / 100;
    let chargeableAmount = pos - freeLimit;
    if (chargeableAmount < 0) chargeableAmount = 0;

    let withoutProgram = pos * 0.015;
    let withProgram = chargeableAmount * 0.015;
    let savings = withoutProgram - withProgram;

    document.getElementById("result").innerHTML = `
        <div class="line">Free POS Limit: ₹${freeLimit.toFixed(2)}</div>
        <div class="line">POS Charges Without Program: ₹${withoutProgram.toFixed(2)}</div>
        <div class="line">POS Charges With Program: ₹${withProgram.toFixed(2)}</div>
        <div class="line">💰 Possible Savings: ₹${savings.toFixed(2)}</div>
    `;
}
</script>

</body>
</html>
