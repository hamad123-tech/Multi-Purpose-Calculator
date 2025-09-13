# Multi-Purpose-Calculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Multi-Purpose Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f3f4f6;
      margin: 0;
      padding: 0;
    }
    h1 {
      background: #2563eb;
      color: white;
      padding: 15px;
      margin: 0;
    }
    .nav {
      margin: 15px 0;
    }
    .nav button {
      margin: 5px;
      padding: 10px 15px;
      border: none;
      border-radius: 6px;
      background: #3b82f6;
      color: white;
      cursor: pointer;
    }
    .nav button:hover {
      background: #1d4ed8;
    }
    .section {
      display: none;
      padding: 20px;
      background: white;
      margin: 20px auto;
      width: 90%;
      max-width: 600px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }
    input {
      margin: 5px;
      padding: 8px;
      width: 80%;
      max-width: 250px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button.calc-btn {
      background: #10b981;
      margin: 8px;
    }
    button.calc-btn:hover {
      background: #059669;
    }
    .sci-buttons button {
      margin: 4px;
      padding: 10px 14px;
      border: none;
      border-radius: 5px;
      background: #6b7280;
      color: white;
      cursor: pointer;
    }
    .sci-buttons button:hover {
      background: #374151;
    }
    footer {
      margin-top: 40px;
      padding: 15px;
      background: #111827;
      color: #f9fafb;
      font-size: 14px;
      font-style: italic;
      letter-spacing: 1px;
      text-align: center;
      font-family: "Georgia", serif;
    }
  </style>
</head>
<body>
  <h1>Multi-Purpose Calculator</h1>

  <!-- Navigation -->
  <div class="nav">
    <button onclick="showSection('gpa')">GPA</button>
    <button onclick="showSection('bmi')">BMI</button>
    <button onclick="showSection('scientific')">Scientific</button>
  </div>

  <!-- GPA Section -->
  <div id="gpa" class="section">
    <h2>GPA Calculator</h2>
    <div id="gpa-inputs"></div>
    <button onclick="addSubject()">Add Subject</button>
    <button class="calc-btn" onclick="calculateGPA()">Calculate GPA</button>
    <p id="gpa-result"></p>
  </div>

  <!-- BMI Section -->
  <div id="bmi" class="section">
    <h2>BMI Calculator</h2>
    <input type="number" id="weight" placeholder="Weight (kg)"><br>
    <input type="number" id="height" placeholder="Height (m)"><br>
    <button class="calc-btn" onclick="calculateBMI()">Calculate BMI</button>
    <p id="bmi-result"></p>
  </div>

  <!-- Scientific Section -->
  <div id="scientific" class="section">
    <h2>Scientific Calculator</h2>
    <input type="text" id="sci-input" placeholder="Enter expression">
    <div class="sci-buttons">
      <!-- Basic -->
      <button onclick="appendVal('+')">+</button>
      <button onclick="appendVal('-')">−</button>
      <button onclick="appendVal('*')">×</button>
      <button onclick="appendVal('/')">÷</button>
      <button onclick="appendVal('%')">%</button>
      <button onclick="appendVal('**')">^</button>
      <!-- Advanced -->
      <button onclick="appendVal('Math.sqrt(')">√</button>
      <button onclick="appendVal('Math.pow(')">pow</button>
      <button onclick="appendVal('Math.exp(')">exp</button>
      <button onclick="appendVal('Math.sin(')">sin</button>
      <button onclick="appendVal('Math.cos(')">cos</button>
      <button onclick="appendVal('Math.tan(')">tan</button>
      <button onclick="appendVal('Math.log(')">log</button>
      <button onclick="appendVal('Math.PI')">π</button>
      <button onclick="appendVal('Math.E')">e</button>
    </div>
    <button class="calc-btn" onclick="calculateSci()">=</button>
    <button class="calc-btn" onclick="clearSci()">C</button>
    <p id="sci-result"></p>
  </div>

  <footer>
    CREATED BY HAMMAD KHATTAK — FOUNDER OF INNOVACORE
  </footer>

  <script>
    // Navigation
    function showSection(id) {
      document.querySelectorAll('.section').forEach(sec => sec.style.display = 'none');
      document.getElementById(id).style.display = 'block';
    }

    // GPA Calculator
    function addSubject() {
      const container = document.getElementById("gpa-inputs");
      const div = document.createElement("div");
      div.innerHTML = `
        <input type="text" placeholder="Grade (A,B,C...)" class="grade">
        <input type="number" placeholder="Credit Hours" class="credits">
      `;
      container.appendChild(div);
    }

    function calculateGPA() {
      const grades = document.querySelectorAll(".grade");
      const credits = document.querySelectorAll(".credits");

      let totalPoints = 0;
      let totalCredits = 0;

      for (let i = 0; i < grades.length; i++) {
        let grade = grades[i].value.toUpperCase();
        let credit = parseFloat(credits[i].value);

        let point = 0;
        if (grade === "A") point = 4.0;
        else if (grade === "B") point = 3.0;
        else if (grade === "C") point = 2.0;
        else if (grade === "D") point = 1.0;
        else if (grade === "F") point = 0;

        if (!isNaN(credit)) {
          totalPoints += point * credit;
          totalCredits += credit;
        }
      }

      let gpa = (totalPoints / totalCredits).toFixed(2);
      document.getElementById("gpa-result").innerText = "Your GPA is: " + (isNaN(gpa) ? "0.00" : gpa);
    }

    // BMI Calculator
    function calculateBMI() {
      let weight = parseFloat(document.getElementById("weight").value);
      let height = parseFloat(document.getElementById("height").value);

      if (weight > 0 && height > 0) {
        let bmi = (weight / (height * height)).toFixed(2);
        let category = "";

        if (bmi < 18.5) category = "Underweight";
        else if (bmi < 24.9) category = "Normal";
        else if (bmi < 29.9) category = "Overweight";
        else category = "Obese";

        document.getElementById("bmi-result").innerText = `Your BMI is: ${bmi} (${category})`;
      } else {
        document.getElementById("bmi-result").innerText = "Please enter valid weight and height!";
      }
    }

    // Scientific Calculator
    function appendVal(val) {
      document.getElementById("sci-input").value += val;
    }

    function calculateSci() {
      try {
        let expr = document.getElementById("sci-input").value;
        let result = eval(expr);
        document.getElementById("sci-result").innerText = "Result: " + result;
      } catch {
        document.getElementById("sci-result").innerText = "Invalid Expression!";
      }
    }

    function clearSci() {
      document.getElementById("sci-input").value = "";
      document.getElementById("sci-result").innerText = "";
    }
  </script>
</body>
</html>
