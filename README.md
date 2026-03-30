# al-harithiya-calculator
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Al-Harithiya Calculator</title>

<style>
body {
  background: black;
  color: white;
  text-align: center;
  font-family: Arial;
  padding: 30px;
}

input {
  padding: 12px;
  width: 280px;
  font-size: 18px;
}

button {
  padding: 10px 20px;
  margin-top: 10px;
  font-size: 16px;
}

#explain {
  text-align: left;
  margin: 10px auto;
  width: 80%;
  background: #111;
  padding: 15px;
  border-radius: 10px;
}
</style>
</head>

<body>

<h1>Al-Harithiya Calculator</h1>

<input id="input" placeholder="اكتب العملية...">
<br>
<button onclick="calculate()">Confirm</button>

<h3>Result:</h3>
<p id="result"></p>

<h3>Step by Step:</h3>
<p id="explain"></p>

<br><br>

<p style="font-size:10px;">
Made by Ali Saif Ali Mustafa Ahmed Shaheed Amir Ghaith Shawqi<br>
with the assistance of Mustafa Ahmed Khurshid<br>
First Grade A
</p>

<script>
function calculate() {
  let input = document.getElementById("input").value;

  input = input.replace(/×/g, "*").replace(/÷/g, "/").replace(/\^/g, "**");

  let explanation = "";

  try {
    let result;

    if (input.includes("%")) {
      let parts = input.split("من");
      if (parts.length === 2) {
        let percent = parseFloat(parts[0].replace("%",""));
        let number = parseFloat(parts[1]);
        result = (percent/100)*number;
        explanation += `1. أخذ النسبة: ${percent}%\n`;
        explanation += `2. ضربها في العدد: ${percent/100} × ${number} = ${result}\n`;
      } else {
        result = "صيغة النسبة غير صحيحة";
      }
    } 
    else if (input.match(/[\d\+\-\*\/\(\)\.]/) || input.includes("**")) {
      explanation += "1. تحليل العملية الحسابية\n";
      explanation += "2. استخدام ترتيب العمليات (PEMDAS)\n";
      result = eval(input);
      explanation += `3. النتيجة = ${result}\n`;
    } 
    else if (input.includes("إذا عندي")) {
      let numbers = input.match(/\d+/g);
      if (numbers && numbers.length === 2) {
        result = numbers[0] - numbers[1];
        explanation += `1. لديك ${numbers[0]} وصرفت ${numbers[1]}\n`;
        explanation += `2. الطرح: ${numbers[0]} - ${numbers[1]} = ${result}\n`;
      }
    } 
    else {
      result = "لا أعرف كيف أحسب هذا";
    }

    document.getElementById("result").innerText = result;
    document.getElementById("explain").innerText = explanation;

  } catch (err) {
    document.getElementById("result").innerText = "Error: " + err;
    document.getElementById("explain").innerText = "";
  }
}
</script>

</body>
</html>
