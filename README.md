<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Scientific Notation Scanner</title>

  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    *{
      box-sizing:border-box;
    }

    body{
      margin:0;
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      background:linear-gradient(135deg,#ffd6e7,#ffeaf4,#ffdff0);
      font-family:'Quicksand', sans-serif;
      overflow:hidden;
    }

    .bg-bubble{
      position:fixed;
      border-radius:50%;
      background:rgba(255,255,255,0.35);
      animation:float 6s ease-in-out infinite;
      z-index:0;
    }

    .b1{
      width:90px;
      height:90px;
      top:8%;
      left:8%;
    }

    .b2{
      width:140px;
      height:140px;
      bottom:10%;
      right:8%;
      animation-delay:1s;
    }

    .b3{
      width:65px;
      height:65px;
      top:20%;
      right:18%;
      animation-delay:2s;
    }

    @keyframes float{
      0%,100%{transform:translateY(0);}
      50%{transform:translateY(-12px);}
    }

    .container{
      position:relative;
      z-index:1;
      width:90%;
      max-width:620px;
      background:rgba(255,255,255,0.92);
      padding:30px;
      border-radius:28px;
      box-shadow:0 12px 30px rgba(255,105,180,0.18);
      text-align:center;
      animation:popIn .7s ease;
    }

    @keyframes popIn{
      from{
        opacity:0;
        transform:scale(0.94) translateY(12px);
      }
      to{
        opacity:1;
        transform:scale(1) translateY(0);
      }
    }

    h1{
      margin-top:0;
      margin-bottom:10px;
      color:#ff4f9a;
      font-size:30px;
    }

    .sub{
      color:#9c5f7b;
      margin-bottom:20px;
      font-size:15px;
    }

    .input-box{
      display:flex;
      gap:10px;
      justify-content:center;
      flex-wrap:wrap;
      margin-bottom:14px;
    }

    input{
      width:100%;
      max-width:340px;
      padding:14px 16px;
      border:2px solid #ffc1da;
      border-radius:14px;
      font-size:17px;
      outline:none;
      transition:.25s;
      background:#fff8fc;
      font-family:'Quicksand', sans-serif;
    }

    input:focus{
      border-color:#ff70ad;
      box-shadow:0 0 0 4px rgba(255,112,173,0.15);
      transform:scale(1.01);
    }

    .main-btn{
      color:#7a3e57;
      border:none;
      border-radius:14px;
      padding:13px 20px;
      cursor:pointer;
      font-size:16px;
      font-weight:700;
      transition:.2s;
      font-family:'Quicksand', sans-serif;
      box-shadow:0 4px 10px rgba(255,182,193,0.25);
    }

    .check-btn{
      background:#ffd6e8;
    }

    .clear-btn{
      background:#ffe7c7;
    }

    .main-btn:hover{
      transform:translateY(-2px) scale(1.03);
    }

    .pad, .examples{
      margin-top:18px;
    }

    .section-title{
      font-size:16px;
      color:#d94d8a;
      margin-bottom:10px;
      font-weight:700;
    }

    .btn-group{
      display:flex;
      flex-wrap:wrap;
      justify-content:center;
      gap:8px;
    }

    .small-btn{
      border:none;
      border-radius:14px;
      padding:10px 14px;
      cursor:pointer;
      font-size:14px;
      font-weight:700;
      transition:.2s;
      font-family:'Quicksand', sans-serif;
      box-shadow:0 4px 10px rgba(255,182,193,0.25);
    }

    .small-btn:hover{
      transform:scale(1.06);
    }

    .pink{
      background:#ffd9ea;
      color:#9e4b72;
    }

    .lavender{
      background:#eee0ff;
      color:#7f5aa6;
    }

    .mint{
      background:#dff7ea;
      color:#3d8b68;
    }

    .peach{
      background:#ffe5dc;
      color:#b56b63;
    }

    .butter{
      background:#fff2bf;
      color:#9d7a16;
    }

    .result{
      margin-top:22px;
      padding:16px;
      border-radius:18px;
      font-size:18px;
      font-weight:700;
      display:none;
      animation:bounceIn .4s ease;
    }

    @keyframes bounceIn{
      0%{
        opacity:0;
        transform:scale(0.85);
      }
      60%{
        transform:scale(1.05);
      }
      100%{
        opacity:1;
        transform:scale(1);
      }
    }

    .success{
      display:block;
      background:#e8fff0;
      color:#2e9b63;
      border:2px solid #b8efca;
    }

    .fail{
      display:block;
      background:#fff0f3;
      color:#d14f79;
      border:2px solid #ffc0d2;
    }

    .note{
      margin-top:10px;
      font-size:14px;
      color:#8f6a7d;
      line-height:1.6;
    }

    .mini{
      margin-top:8px;
      font-size:13px;
      color:#aa7a90;
    }
  </style>
</head>
<body>

  <div class="bg-bubble b1"></div>
  <div class="bg-bubble b2"></div>
  <div class="bg-bubble b3"></div>

  <div class="container">
    <h1>💗 Scientific Notation Scanner 💗</h1>
    <div class="sub">This scanner accepts both computer notation using <b>e</b> and mathematical notation using <b>×10^</b>.</div>

    <div class="input-box">
      <input type="text" id="numberInput" placeholder="Example: 3.5e4 or 3.5×10^4">
      <button class="main-btn check-btn" onclick="checkInput()">Check</button>
      <button class="main-btn clear-btn" onclick="clearInput()">Clear</button>
    </div>

    <div class="pad">
      <div class="section-title">Input Helper Buttons</div>
      <div class="btn-group">
        <button class="small-btn pink" onclick="addText('0')">0</button>
        <button class="small-btn pink" onclick="addText('1')">1</button>
        <button class="small-btn pink" onclick="addText('2')">2</button>
        <button class="small-btn pink" onclick="addText('3')">3</button>
        <button class="small-btn pink" onclick="addText('4')">4</button>
        <button class="small-btn pink" onclick="addText('5')">5</button>
        <button class="small-btn pink" onclick="addText('6')">6</button>
        <button class="small-btn pink" onclick="addText('7')">7</button>
        <button class="small-btn pink" onclick="addText('8')">8</button>
        <button class="small-btn pink" onclick="addText('9')">9</button>
        <button class="small-btn butter" onclick="addText('.')">.</button>
        <button class="small-btn lavender" onclick="addText('e')">e</button>
        <button class="small-btn lavender" onclick="addText('×10^')">×10^</button>
        <button class="small-btn peach" onclick="addText('-')">-</button>
        <button class="small-btn peach" onclick="addText('+')">+</button>
      </div>
      <div class="mini">Use these buttons to build scientific notation more easily.</div>
    </div>

    <div class="examples">
      <div class="section-title">Valid Examples</div>
      <div class="btn-group">
        <button class="small-btn mint" onclick="setExample('1.2e3')">1.2e3</button>
        <button class="small-btn mint" onclick="setExample('6.5e7')">6.5e7</button>
        <button class="small-btn mint" onclick="setExample('8.01e-4')">8.01e-4</button>
        <button class="small-btn mint" onclick="setExample('3.2×10^5')">3.2×10^5</button>
        <button class="small-btn mint" onclick="setExample('-4.7×10^-3')">-4.7×10^-3</button>
      </div>
    </div>

    <div class="examples">
      <div class="section-title">Invalid Examples</div>
      <div class="btn-group">
        <button class="small-btn peach" onclick="setExample('1500')">1500</button>
        <button class="small-btn peach" onclick="setExample('0.75')">0.75</button>
        <button class="small-btn peach" onclick="setExample('5ee3')">5ee3</button>
        <button class="small-btn peach" onclick="setExample('12e')">12e</button>
        <button class="small-btn peach" onclick="setExample('2×10')">2×10</button>
      </div>
    </div>

    <div id="result" class="result"></div>
    <div id="note" class="note"></div>
  </div>

  <script>
    function addText(text){
      document.getElementById("numberInput").value += text;
    }

    function setExample(example){
      document.getElementById("numberInput").value = example;
      checkInput();
    }

    function clearInput(){
      document.getElementById("numberInput").value = "";
      document.getElementById("result").className = "result";
      document.getElementById("result").innerHTML = "";
      document.getElementById("note").innerHTML = "";
    }

    function checkInput(){
      let input = document.getElementById("numberInput").value.trim();

      let computerPattern = /^-?[1-9](\.\d+)?[eE][+-]?\d+$/;
      let mathPattern = /^-?[1-9](\.\d+)?×10\^[+-]?\d+$/;

      let result = document.getElementById("result");
      let note = document.getElementById("note");

      if(computerPattern.test(input)){
        result.className = "result success";
        result.innerHTML = "✔ Valid scientific notation in computer format";
        note.innerHTML = "Accepted format: <b>a e n</b>, for example <b>3.5e4</b>.";
      }
      else if(mathPattern.test(input)){
        result.className = "result success";
        result.innerHTML = "✔ Valid scientific notation in mathematical format";
        note.innerHTML = "Accepted format: <b>a × 10^n</b>, for example <b>3.5×10^4</b>.";
      }
      else{
        result.className = "result fail";
        result.innerHTML = "✖ Invalid scientific notation";
        note.innerHTML = "Try a format like <b>2.3e5</b> or <b>2.3×10^5</b>.";
      }
    }

    document.getElementById("numberInput").addEventListener("keydown", function(event){
      if(event.key === "Enter"){
        checkInput();
      }
    });
  </script>

</body>
</html>

