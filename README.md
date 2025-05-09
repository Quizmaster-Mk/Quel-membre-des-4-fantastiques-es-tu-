<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Quel membre des 4 Fantastiques êtes-vous ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #001f3f;
      color: white;
      text-align: center;
      padding: 20px;
    }

    h1 {
      color: #FFDC00;
      text-shadow: 2px 2px 5px #0074D9;
      font-size: 36px;
      margin-bottom: 20px;
    }

    .question {
      background-color: #7FDBFF;
      color: #000;
      padding: 20px;
      margin: 20px auto;
      width: 80%;
      border-radius: 10px;
      box-shadow: 0 0 10px #39CCCC;
    }

    .options button {
      background-color: #0074D9;
      color: white;
      border: none;
      padding: 10px 20px;
      margin: 10px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s ease;
    }

    .options button:hover {
      background-color: #001f3f;
    }

    .result {
      background-color: #7FDBFF;
      color: #000;
      padding: 20px;
      border-radius: 10px;
      width: 80%;
      margin: 20px auto;
      display: none;
    }

    .result h2 {
      color: #FF4136;
    }

    img.logo {
      max-width: 200px;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <!-- Logo en-tête (optionnel) -->
  <!-- <img src="https://ton-lien-de-logo.png" class="logo" alt="4 Fantastiques"> -->
  
  <h1>Quel membre des 4 Fantastiques êtes-vous ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <button onclick="startQuiz()">Recommencer</button>
  </div>

  <script>
    const questions = [
      {
        question: "Quel est votre plus grand atout ?",
        options: ["Intelligence", "Compassion", "Charisme", "Force brute"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Que faites-vous en situation de crise ?",
        options: ["Analyser la situation", "Protéger les autres", "Agir sans attendre", "Encaisser les coups"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Quel super-pouvoir vous attire le plus ?",
        options: ["Élasticité", "Invisibilité", "Vol et feu", "Peau rocheuse"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Comment vos amis vous décriraient ?",
        options: ["Cerveau du groupe", "Protecteur·rice", "Exubérant·e", "Solide et fiable"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Votre approche du travail d’équipe ?",
        options: ["Organisateur", "Médiateur", "Meneur", "Pilier silencieux"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Un défaut qui vous décrit ?",
        options: ["Trop rationnel", "Trop effacé·e", "Trop impulsif·ve", "Trop grognon·ne"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Quel lieu préférez-vous ?",
        options: ["Un labo", "Un endroit paisible", "Un volcan en éruption", "Une carrière de pierre"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Quel type de films préférez-vous ?",
        options: ["Science-fiction", "Romance", "Action", "Drame humain"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Votre devise ?",
        options: ["La logique avant tout", "Je veille sur les miens", "Pas de temps à perdre !", "C’est l’heure de cogner !"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Si vous étiez un élément ?",
        options: ["Air (réflexion)", "Eau (fluidité)", "Feu (énergie)", "Terre (solidité)"],
        result: [0, 1, 2, 3]
      }
    ];

    const characters = [
      {
        name: "Mister Fantastic",
        description: "Génie scientifique et leader du groupe. Vous êtes réfléchi·e, méthodique et toujours à la recherche de solutions."
      },
      {
        name: "Invisible Woman",
        description: "Empathique, protectrice mais puissante. Vous avez un grand cœur et une force intérieure immense."
      },
      {
        name: "Human Torch",
        description: "Téméraire, fougueux·se, et charismatique. Vous aimez briller et foncer tête baissée."
      },
      {
        name: "The Thing",
        description: "Solide comme le roc, loyal et un peu bourru. Vous êtes le roc du groupe, toujours là quand il faut."
      }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];

      document.getElementById('result-text').innerText = `${result.name} — ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    // Lancer le quiz dès le chargement
    startQuiz();
  </script>
</body>
</html>
