<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Test de QI – Multi-niveaux</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f2f5;
      margin: 0;
      padding: 0;
    }

    .container {
      max-width: 800px;
      margin: 40px auto;
      background: white;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    h1 {
      text-align: center;
      color: #2c3e50;
    }

    .levels {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin: 20px 0;
    }

    button {
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      cursor: pointer;
      background-color: #3498db;
      color: white;
      transition: background 0.3s;
    }

    button:hover {
      background-color: #2c80b4;
    }

    #test-container {
      margin-top: 20px;
    }

    #test-container h2 {
      color: #34495e;
    }

    .question-block {
      margin-bottom: 20px;
    }

    .question-block input[type="text"] {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 6px;
      font-size: 16px;
    }

    .feedback {
      margin-top: 5px;
      font-weight: bold;
    }

    .correct {
      color: green;
    }

    .incorrect {
      color: red;
    }

    #result {
      margin-top: 20px;
      font-weight: bold;
      font-size: 18px;
      text-align: center;
      color: #27ae60;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Test de QI – Choisis ton niveau</h1>

    <div class="levels">
      <button onclick="showTest('debutant')">Débutant</button>
      <button onclick="showTest('intermediaire')">Intermédiaire</button>
      <button onclick="showTest('avance')">Avancé</button>
    </div>

    <form id="test-form" onsubmit="return checkAnswers()">
      <div id="test-container"></div>
      <div style="text-align: center;">
        <button type="submit" style="display:none;" id="submit-btn">Soumettre</button>
      </div>
    </form>

    <div id="result"></div>
  </div>

  <script>
    const tests = {
      debutant: [
        { q: "1. Combien font 2 + 2 ?", answer: "4" },
        { q: "2. Quel est le contraire de 'haut' ?", answer: "bas" },
        { q: "3. Complétez : Le chat ___ sur le mur.", answer: "saute" }
      ],
      intermediaire: [
        { q: "1. Quelle lettre vient après E, G, I ?", answer: "k" },
        { q: "2. Marie a 3 pommes et en donne 1. Combien lui reste-t-il ?", answer: "2" },
        { q: "3. Quel est l’intrus : cerise, banane, voiture, pomme ?", answer: "voiture" }
      ],
      avance: [
        { q: "1. Suite logique : 2 - 4 - 8 - 16 - ?", answer: "32" },
        { q: "2. TOIT = 63, PORTE = 75. Combien vaut FENÊTRE ?", answer: "84" },
        { q: "3. Un cube peint sur ses faces, découpé en 64 petits cubes. Combien ont 2 faces peintes ?", answer: "24" }
      ]
    };

    let currentLevel = "";

    function showTest(level) {
      currentLevel = level;
      const container = document.getElementById("test-container");
      const btn = document.getElementById("submit-btn");
      container.innerHTML = `<h2>Niveau : ${capitalize(level)}</h2>`;
      tests[level].forEach((item, i) => {
        container.innerHTML += `
          <div class="question-block">
            <p>${item.q}</p>
            <input type="text" name="q${i}" required>
            <div class="feedback" id="feedback${i}"></div>
          </div>
        `;
      });
      btn.style.display = "inline-block";
      document.getElementById("result").innerText = "";
    }

    function capitalize(word) {
      return word.charAt(0).toUpperCase() + word.slice(1);
    }

    function checkAnswers() {
      const inputs = document.querySelectorAll('input[type="text"]');
      let score = 0;

      inputs.forEach((input, i) => {
        const correct = tests[currentLevel][i].answer.toLowerCase().trim();
        const userAnswer = input.value.toLowerCase().trim();
        const feedback = document.getElementById("feedback" + i);

        if (userAnswer === correct) {
          score++;
          feedback.innerHTML = "✓ Bonne réponse";
          feedback.className = "feedback correct";
        } else {
          feedback.innerHTML = `✗ Mauvaise réponse. Réponse attendue : "${tests[currentLevel][i].answer}"`;
          feedback.className = "feedback incorrect";
        }
      });

      document.getElementById("result").innerText = `✅ Résultat final : ${score} / ${tests[currentLevel].length}`;
      return false;
    }
  </script>
</body>
</html>
# QI_TEST
