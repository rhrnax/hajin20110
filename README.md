<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>물리학 I 퀴즈</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f7fbff;
      margin: 0;
      padding: 30px;
      text-align: center;
    }

    h1 {
      color: #003366;
      margin-bottom: 20px;
    }

    .quiz-box {
      background-color: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      max-width: 700px;
      margin: auto;
    }

    .question {
      font-size: 20px;
      margin-bottom: 20px;
    }

    .options button {
      display: block;
      width: 90%;
      margin: 10px auto;
      padding: 12px;
      font-size: 16px;
      border: none;
      border-radius: 10px;
      background-color: #e0f0ff;
      cursor: pointer;
      transition: 0.2s;
    }

    .options button:hover {
      background-color: #aed8ff;
    }

    .result {
      margin-top: 15px;
      font-size: 18px;
      font-weight: bold;
    }

    .explanation {
      margin-top: 10px;
      font-size: 16px;
      color: #444;
    }

    .next-btn {
      margin-top: 20px;
      padding: 10px 25px;
      font-size: 16px;
      border: none;
      background-color: #0077cc;
      color: white;
      border-radius: 10px;
      cursor: pointer;
    }

    .next-btn:hover {
      background-color: #005fa3;
    }

    .summary {
      font-size: 20px;
      font-weight: bold;
      margin-top: 30px;
    }
  </style>
</head>
<body>

  <h1>⚛️ 물리학 I 퀴즈</h1>

  <div class="quiz-box" id="quizBox">
    <div class="question" id="questionText"></div>
    <div class="options" id="optionButtons"></div>
    <div class="result" id="resultText"></div>
    <div class="explanation" id="explanationText"></div>
    <button class="next-btn" id="nextButton" onclick="nextQuestion()" style="display:none;">다음 문제 ➡️</button>
    <div class="summary" id="summaryText"></div>
  </div>

  <script>
    const quizData = [
      {
        question: "정지해 있던 물체가 갑자기 움직였다면, 작용한 힘은?",
        options: ["외부에서 작용한 힘", "물체의 질량 변화", "공기의 저항"],
        answer: 0,
        explanation: "물체가 정지 상태에서 움직이기 시작했다면 외부에서 힘이 작용했기 때문입니다. 뉴턴의 제1법칙에 해당합니다."
      },
      {
        question: "등속 직선 운동을 하는 물체의 가속도는?",
        options: ["0", "9.8", "무한대"],
        answer: 0,
        explanation: "속도가 변하지 않기 때문에 가속도는 0입니다. 즉, 등속 운동은 힘이 작용하지 않는 상태입니다."
      },
      {
        question: "운동 에너지는 어떤 요인에 따라 결정될까?",
        options: ["온도", "속도와 질량", "위치 에너지"],
        answer: 1,
        explanation: "운동 에너지는 \\( \\frac{1}{2}mv^2 \\)로 질량(m)과 속도(v)의 제곱에 비례합니다."
      },
      {
        question: "작용 반작용 법칙은 어떤 힘에 관한 법칙인가?",
        options: ["중력", "전기력", "상호작용하는 두 힘"],
        answer: 2,
        explanation: "작용 반작용 법칙은 두 물체 사이에 작용하는 힘쌍에 대한 것으로, 힘은 항상 쌍으로 작용합니다."
      },
      {
        question: "질량이 같을 때 더 빠른 물체가 가지는 운동 에너지는?",
        options: ["더 크다", "더 작다", "같다"],
        answer: 0,
        explanation: "운동 에너지는 속도의 제곱에 비례하므로 더 빠를수록 더 큰 운동 에너지를 가집니다."
      },
      {
        question: "F=ma에서 'a'가 두 배가 되면 힘은?",
        options: ["절반", "두 배", "변하지 않음"],
        answer: 1,
        explanation: "F = ma에서 가속도(a)가 두 배가 되면 힘(F)도 두 배가 됩니다. 질량(m)이 일정할 때 그렇습니다."
      }
    ];

    let currentIndex = 0;
    let correctCount = 0;
    let answered = false;

    function loadQuestion() {
      const current = quizData[currentIndex];
      document.getElementById("questionText").innerText = `Q${currentIndex + 1}. ${current.question}`;
      document.getElementById("resultText").innerText = "";
      document.getElementById("explanationText").innerText = "";
      document.getElementById("summaryText").innerText = "";
      document.getElementById("nextButton").style.display = "none";
      answered = false;

      const optionsDiv = document.getElementById("optionButtons");
      optionsDiv.innerHTML = "";
      current.options.forEach((opt, idx) => {
        const btn = document.createElement("button");
        btn.innerText = opt;
        btn.onclick = () => checkAnswer(idx);
        optionsDiv.appendChild(btn);
      });
    }

    function checkAnswer(selectedIndex) {
      if (answered) return;
      answered = true;

      const current = quizData[currentIndex];
      const correct = current.answer;

      const resultText = document.getElementById("resultText");
      const explanationText = document.getElementById("explanationText");

      if (selectedIndex === correct) {
        resultText.innerText = "✅ 정답입니다!";
        resultText.style.color = "green";
        correctCount++;
      } else {
        resultText.innerText = "❌ 오답입니다.";
        resultText.style.color = "red";
      }

      explanationText.innerText = "📘 해설: " + current.explanation;
      document.getElementById("nextButton").style.display = "inline-block";
    }

    function nextQuestion() {
      currentIndex++;
      if (currentIndex < quizData.length) {
        loadQuestion();
      } else {
        showSummary();
      }
    }

    function showSummary() {
      document.getElementById("quizBox").innerHTML = `
        <h2>🎉 퀴즈 완료!</h2>
        <p class="summary">총 ${quizData.length}문제 중 ${correctCount}문제 맞췄어요!</p>
        <p>수고했어요 😊 다시 하려면 새로고침하세요.</p>
      `;
    }

    // 시작 시 첫 문제 로드
    loadQuestion();
  </script>

</body>
</html>
