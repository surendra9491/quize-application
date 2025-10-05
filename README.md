<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quiz Application</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-900 text-gray-100 flex flex-col min-h-screen">

  <div class="flex-grow flex flex-col items-center justify-center px-4 py-10">
    <div class="w-full max-w-2xl bg-gray-800 p-6 rounded-2xl shadow-lg">
      <h1 class="text-3xl font-bold text-center mb-6 text-blue-400">Java & Web Quiz</h1>

      <!-- Quiz Container -->
      <div id="quiz-container"></div>

      <!-- Show Report Button -->
      <div class="mt-6 text-center">
        <button id="showReportBtn"
          class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-6 rounded-lg transition-all">
          Show Report
        </button>
      </div>
    </div>
  </div>

  <!-- Result Modal -->
  <div id="resultModal"
       class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center hidden">
    <div class="bg-gray-800 text-gray-100 rounded-xl p-6 w-11/12 md:w-1/2 shadow-2xl max-h-[90vh] overflow-y-auto">
      <h2 class="text-2xl font-bold text-center text-green-400 mb-4">Quiz Report</h2>
      <p id="score" class="text-center text-lg mb-4"></p>
      <div id="answers" class="space-y-3 text-sm md:text-base"></div>
      <div class="text-center mt-6">
        <button id="closeModal"
          class="bg-red-500 hover:bg-red-600 text-white font-semibold py-2 px-6 rounded-lg">
          Close
        </button>
      </div>
    </div>
  </div>

  <script>
    // ===== QUIZ DATA =====
    const questions = [
      {
        question: "Which language is used for structuring web pages?",
        options: ["Python", "HTML", "C++", "Java"],
        answer: "HTML",
      },
      {
        question: "What does CSS stand for?",
        options: [
          "Cascading Style Sheets",
          "Creative Style Syntax",
          "Computer Styled System",
          "Custom Style Sheet",
        ],
        answer: "Cascading Style Sheets",
      },
      {
        question: "Which language is used for client-side scripting in browsers?",
        options: ["C#", "Python", "JavaScript", "Java"],
        answer: "JavaScript",
      },
      {
        question: "Which company originally developed Java?",
        options: ["Sun Microsystems", "Microsoft", "Google", "IBM"],
        answer: "Sun Microsystems",
      },
      {
        question: "What is the default value of a boolean variable in Java?",
        options: ["true", "false", "0", "null"],
        answer: "false",
      },
      {
        question: "Which keyword is used to inherit a class in Java?",
        options: ["implements", "extends", "inherits", "super"],
        answer: "extends",
      },
      {
        question: "Which method is the entry point for a Java program?",
        options: ["start()", "execute()", "run()", "main()"],
        answer: "main()",
      },
      {
        question: "Which of the following is not a Java data type?",
        options: ["int", "float", "boolean", "real"],
        answer: "real",
      },
      {
        question: "Which tool is used to compile Java programs?",
        options: ["javac", "java", "javadoc", "jar"],
        answer: "javac",
      },
      {
        question: "Which of these is used to handle exceptions in Java?",
        options: ["goto", "break", "try-catch", "stop"],
        answer: "try-catch",
      },
    ];

    const quizContainer = document.getElementById("quiz-container");
    const showReportBtn = document.getElementById("showReportBtn");
    const resultModal = document.getElementById("resultModal");
    const scoreDisplay = document.getElementById("score");
    const answersContainer = document.getElementById("answers");
    const closeModal = document.getElementById("closeModal");

    const marksPerQuestion = 2; // Each question = 2 marks
    const totalMarks = questions.length * marksPerQuestion;

    // ===== DISPLAY QUESTIONS =====
    function loadQuiz() {
      quizContainer.innerHTML = questions
        .map((q, i) => {
          return `
          <div class="mb-6">
            <h2 class="text-lg font-semibold mb-2">${i + 1}. ${q.question}</h2>
            ${q.options
              .map(
                (opt) => `
                <label class="block bg-gray-700 hover:bg-gray-600 p-2 rounded cursor-pointer">
                  <input type="radio" name="q${i}" value="${opt}" class="mr-2">
                  ${opt}
                </label>`
              )
              .join("")}
          </div>`;
        })
        .join("");
    }

    // ===== SHOW REPORT =====
    function showReport() {
      let correctCount = 0;
      let reportHTML = "";

      questions.forEach((q, i) => {
        const selected = document.querySelector(input[name="q${i}"]:checked);
        const answer = selected ? selected.value : "Not answered";

        if (answer === q.answer) correctCount++;

        reportHTML += `
          <div class="bg-gray-700 p-3 rounded-lg">
            <p><b>Q${i + 1}:</b> ${q.question}</p>
            <p>Your Answer: <span class="${
              answer === q.answer ? "text-green-400" : "text-red-400"
            }">${answer}</span></p>
            <p>Correct Answer: <span class="text-green-400">${q.answer}</span></p>
          </div>`;
      });

      const totalScore = correctCount * marksPerQuestion;
      scoreDisplay.innerHTML = `You got <b>${totalScore}</b> marks out of <b>${totalMarks}</b> 
      (<b>${correctCount}</b> correct out of ${questions.length})`;
      answersContainer.innerHTML = reportHTML;
      resultModal.classList.remove("hidden");
    }

    // ===== EVENT LISTENERS =====
    showReportBtn.addEventListener("click", showReport);
    closeModal.addEventListener("click", () => resultModal.classList.add("hidden"));

    // ===== INITIAL LOAD =====
    loadQuiz();
  </script>
</body>
</html>
