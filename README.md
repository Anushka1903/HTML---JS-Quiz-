# HTML---JS-Quiz-
This my mini [ kuchh zyada hi choti h ik] quiz webpage<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Interactive Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .quiz-container {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      width: 400px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }
    h2 {
      margin-bottom: 15px;
    }
    .btn {
      display: block;
      width: 100%;
      margin: 5px 0;
      padding: 10px;
      border: none;
      border-radius: 8px;
      background: #3498db;
      color: #fff;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s;
    }
    .btn:hover {
      background: #2980b9;
    }
    #next-btn {
      background: #2ecc71;
      display: none;
    }
    #result {
      font-size: 18px;
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h2 id="question">Question text</h2>
    <div id="answer-buttons"></div>
    <button id="next-btn" class="btn">Next</button>
    <div id="result"></div>
  </div>

  <script>
    const questions = [
      {
        question: "What is the capital of France?",
        answers: [
          { text: "Berlin", correct: false },
          { text: "Madrid", correct: false },
          { text: "Paris", correct: true },
          { text: "Rome", correct: false }
        ]
      },
      {
        question: "Which language runs in a web browser?",
        answers: [
          { text: "Java", correct: false },
          { text: "C", correct: false },
          { text: "Python", correct: false },
          { text: "JavaScript", correct: true }
        ]
      },
      {
        question: "What does CSS stand for?",
        answers: [
          { text: "Computer Style Sheets", correct: false },
          { text: "Cascading Style Sheets", correct: true },
          { text: "Creative Style System", correct: false },
          { text: "Colorful Style Sheets", correct: false }
        ]
      }
    ];

    const questionElement = document.getElementById("question");
    const answerButtons = document.getElementById("answer-buttons");
    const nextButton = document.getElementById("next-btn");
    const result = document.getElementById("result");

    let currentQuestionIndex = 0;
    let score = 0;

    function startQuiz() {
      currentQuestionIndex = 0;
      score = 0;
      nextButton.innerHTML = "Next";
      showQuestion();
    }

    function showQuestion() {
      resetState();
      let currentQuestion = questions[currentQuestionIndex];
      questionElement.innerHTML = currentQuestion.question;

      currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.text;
        button.classList.add("btn");
        button.addEventListener("click", () => selectAnswer(answer));
        answerButtons.appendChild(button);
      });
    }

    function resetState() {
      nextButton.style.display = "none";
      result.innerHTML = "";
      while (answerButtons.firstChild) {
        answerButtons.removeChild(answerButtons.firstChild);
      }
    }

    function selectAnswer(answer) {
      if (answer.correct) {
        score++;
      }
      nextButton.style.display = "block";
    }

    function showResult() {
      resetState();
      questionElement.innerHTML = `Quiz Completed! 🎉`;
      result.innerHTML = `Your Score: ${score} / ${questions.length}`;
      nextButton.innerHTML = "Play Again";
      nextButton.style.display = "block";
    }

    function handleNextButton() {
      currentQuestionIndex++;
      if (currentQuestionIndex < questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    }

    nextButton.addEventListener("click", () => {
      if (currentQuestionIndex < questions.length) {
        handleNextButton();
      } else {
        startQuiz();
      }
    });

    startQuiz();
  </script>
</body>
</html>
