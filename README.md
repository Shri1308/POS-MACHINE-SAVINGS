<!DOCTYPE html>
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
            width: 320px;
        }
        h2 {
            text-align: center;
            margin-bottom: 15px;
        }
        label {
            margin-top: 10px;
            display: block;
            font-weight: bold;
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
            background: #4CAF50;
            color: white;
            font-size: 16px;
            margin-top: 15px;
            cursor: pointer;
        }
        button:hover {
            background: #45a049;
        }
        .result {
            margin-top: 20px;
            background: #e8f5e9;
            padding: 10px;
            border-radius: 5px;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="calculator">
    <h2>POS MDR Savings</h2>

    <label>Account Variant</label>
    <select id="variant">
        <option value="10">₹50K Variant (10%)</option>
        <option value="12">₹1Lac Variant (12%)</option>
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

    // Free POS limit = (UPI × Variant %)
    let freeLimit = (upi * variantPercent) / 100;

    // Amount chargeable under MDR after free limit
    let chargeableAmount = pos - freeLimit;
    if (chargeableAmount < 0) chargeableAmount = 0;

    // Charges without program (1.5% of full POS)
    let withoutProgram = pos * 0.015;

    // Charges with program (1.5% of amount above free limit)
    let withProgram = chargeableAmount * 0.015;

    // Savings
    let savings = withoutProgram - withProgram;

    document.getElementById("result").innerHTML = `
        Free POS Limit: ₹${freeLimit.toFixed(2)}<br>
        POS Charges Without Program: ₹${withoutProgram.toFixed(2)}<br>
        POS Charges With Program: ₹${withProgram.toFixed(2)}<br>
        💰 Possible Savings: ₹${savings.toFixed(2)}
    `;
}
</script>

</body>
</html>
