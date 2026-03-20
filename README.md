<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scientific Notation Scanner</title>
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            box-sizing: border-box;
        }
        body {
            margin: 0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ffd6e7, #ffe6f0, #fff0f5);
            font-family: 'Quicksand', sans-serif;
            padding: 20px;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            max-width: 600px;
            width: 100%;
        }
        h1 {
            color: #ff4f9a;
            font-size: 28px;
            margin-bottom: 15px;
            text-align: center;
        }
        p {
            color: #555;
            line-height: 1.6;
        }
        .input-box {
            margin: 20px 0;
        }
        input {
            width: 100%;
            padding: 12px;
            border: 2px solid #ffb6c1;
            border-radius: 10px;
            font-size: 16px;
            margin-bottom: 10px;
        }
        button {
            background: #ffb6c1;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            margin: 5px;
            cursor: pointer;
            font-size: 14px;
        }
        button:hover {
            background: #ff9eb5;
        }
        .btn-group {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin: 15px 0;
            justify-content: center;
        }
        .small-btn {
            background: #ffe4e9;
            color: #b34e71;
            min-width: 45px;
        }
        .example-btn {
            background: #e3f2e9;
            color: #2e7d5e;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
        }
        .valid {
            background: #d4edda;
            color: #155724;
        }
        .invalid {
            background: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔬 Scientific Notation Scanner</h1>
        <p>This scanner accepts both computer notation using <strong>e</strong> and mathematical notation using <strong>×10ⁿ</strong>.</p>
        <p><em>Example: 3.5e4 or 3.5×10⁴</em></p>

        <div class="input-box">
            <input type="text" id="inputField" placeholder="Enter scientific notation...">
            <div style="text-align: center;">
                <button onclick="checkInput()">Check</button>
                <button onclick="clearInput()">Clear</button>
            </div>
        </div>

        <div>
            <p><strong>Input Helper Buttons</strong></p>
            <div class="btn-group">
                <button class="small-btn" onclick="addText('0')">0</button>
                <button class="small-btn" onclick="addText('1')">1</button>
                <button class="small-btn" onclick="addText('2')">2</button>
                <button class="small-btn" onclick="addText('3')">3</button>
                <button class="small-btn" onclick="addText('4')">4</button>
                <button class="small-btn" onclick="addText('5')">5</button>
                <button class="small-btn" onclick="addText('6')">6</button>
                <button class="small-btn" onclick="addText('7')">7</button>
                <button class="small-btn" onclick="addText('8')">8</button>
                <button class="small-btn" onclick="addText('9')">9</button>
                <button class="small-btn" onclick="addText('.')">.</button>
                <button class="small-btn" onclick="addText('e')">e</button>
                <button class="small-btn" onclick="addText('×10^')">×10^</button>
                <button class="small-btn" onclick="addText('+')">+</button>
                <button class="small-btn" onclick="addText('-')">-</button>
            </div>
            <p><small>Use these buttons to build scientific notation more easily.</small></p>
        </div>

        <div>
            <p><strong>Valid Examples</strong></p>
            <div class="btn-group">
                <button class="example-btn" onclick="setExample('1.2e3')">1.2e3</button>
                <button class="example-btn" onclick="setExample('6.5e7')">6.5e7</button>
                <button class="example-btn" onclick="setExample('8.01e-4')">8.01e-4</button>
                <button class="example-btn" onclick="setExample('3.2×10^5')">3.2×10^5</button>
                <button class="example-btn" onclick="setExample('-4.7×10^-3')">-4.7×10^-3</button>
            </div>
        </div>

        <div>
            <p><strong>Invalid Examples</strong></p>
            <div class="btn-group">
                <button class="example-btn" style="background:#f8d7da" onclick="setExample('1500')">1500</button>
                <button class="example-btn" style="background:#f8d7da" onclick="setExample('0.75')">0.75</button>
                <button class="example-btn" style="background:#f8d7da" onclick="setExample('5ee3')">5ee3</button>
                <button class="example-btn" style="background:#f8d7da" onclick="setExample('12e')">12e</button>
                <button class="example-btn" style="background:#f8d7da" onclick="setExample('2×10')">2×10</button>
            </div>
        </div>

        <div id="result" class="result"></div>
    </div>

    <script>
        function addText(text) {
            document.getElementById('inputField').value += text;
        }

        function setExample(example) {
            document.getElementById('inputField').value = example;
            checkInput();
        }

        function checkInput() {
            let input = document.getElementById('inputField').value;
            let resultDiv = document.getElementById('result');
            
            let ePattern = /^-?\d+(\.\d+)?[eE][+-]?\d+$/;
            let xPattern = /^-?\d+(\.\d+)?×10\^[+-]?\d+$/;
            
            if (ePattern.test(input) || xPattern.test(input)) {
                resultDiv.className = 'result valid';
                resultDiv.innerHTML = '✅ Valid scientific notation!';
            } else {
                resultDiv.className = 'result invalid';
                resultDiv.innerHTML = '❌ Invalid scientific notation!';
            }
        }

        function clearInput() {
            document.getElementById('inputField').value = '';
            document.getElementById('result').className = 'result';
            document.getElementById('result').innerHTML = '';
        }
    </script>
</body>
</html>
