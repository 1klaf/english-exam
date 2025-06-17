="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>اختبار استيعاب المقروء - السادس الإعدادي</title>
<style>
  body { font-family: 'Arial', sans-serif; background-color: #f4f4f4; padding: 0 20px; text-align: center; }
  .quiz-container { max-width: 600px; margin: 50px auto; background: #fff; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
  .question { font-size: 20px; margin-bottom: 15px; }
  .option { display: block; background: #eee; margin: 8px 0; padding: 10px; border-radius: 5px; cursor: pointer; text-align: right; transition: 0.3s; border: 2px solid transparent; }
  .option:hover { background: #ddd; }
  .option.correct { background-color: #c8f7c5; border-color: #2ecc71; }
  .option.incorrect { background-color: #f7c5c5; border-color: #e74c3c; }
  #nextBtn { padding: 10px 20px; margin-top: 20px; background: #3498db; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px; }
  #nextBtn:disabled { background: #ccc; cursor: not-allowed; }
  .footer { margin-top: 30px; color: #777; font-size: 14px; }
  #visits, #completed { margin-top: 10px; color: #444; font-size: 16px; display: none; }
</style>
</head>
<body>

<div class="quiz-container">
  <div id="question" class="question"></div>
  <div id="options"></div>
  <button id="nextBtn" disabled>التالي</button>
  <div id="result" style="margin-top:20px;font-size:18px;"></div>
</div>

<div id="visits">عدد الزائرين: جاري التحميل...</div>
<div id="completed">عدد الذين أكملوا الامتحان: جاري التحميل...</div>
<div class="footer">
  تم الإنشاء بواسطة <b>sad23is خلف</b><br>
  <b>دعواتكم لوالدي بالرحمة</b>
</div>

<script>
const quizData = [
  // سيتم استكمال إضافة جميع الأسئلة هنا (123 سؤالاً)
];

let currentQuestion = 0;
let correctCount = 0;
let incorrectCount = 0;
const questionEl = document.getElementById('question');
const optionsEl = document.getElementById('options');
const nextBtn = document.getElementById('nextBtn');
const resultEl = document.getElementById('result');

function loadQuestion() {
  nextBtn.disabled = true;
  questionEl.textContent = `السؤال ${currentQuestion + 1} من ${quizData.length}: ${quizData[currentQuestion].question}`;
  optionsEl.innerHTML = '';

  quizData[currentQuestion].options.forEach((option, index) => {
    const optionBtn = document.createElement('button');
    optionBtn.className = 'option';
    optionBtn.textContent = option;
    optionBtn.onclick = () => selectAnswer(optionBtn, index);
    optionsEl.appendChild(optionBtn);
  });
}

function selectAnswer(optionBtn, selectedIndex) {
  const correctIndex = quizData[currentQuestion].answer;
  Array.from(document.getElementsByClassName('option')).forEach(btn => btn.disabled = true);

  if (selectedIndex === correctIndex) {
    optionBtn.classList.add('correct');
    correctCount++;
  } else {
    optionBtn.classList.add('incorrect');
    Array.from(document.getElementsByClassName('option'))[correctIndex].classList.add('correct');
    incorrectCount++;
  }

  nextBtn.disabled = false;
}

nextBtn.onclick = () => {
  currentQuestion++;
  if (currentQuestion < quizData.length) {
    loadQuestion();
  } else {
    questionEl.textContent = 'تم الانتهاء من جميع الأسئلة!';
    optionsEl.innerHTML = '';
    nextBtn.style.display = 'none';
    resultEl.innerHTML = `✅ عدد الإجابات الصحيحة: ${correctCount} <br>❌ عدد الإجابات الخاطئة: ${incorrectCount}`;

    const completedCount = localStorage.getItem('quiz_completed') || 0;
    localStorage.setItem('quiz_completed', parseInt(completedCount) + 1);
  }
};

const PASSWORD = "S21K";
const visitsEl = document.getElementById('visits');
const completedEl = document.getElementById('completed');
const visitCounter = localStorage.getItem('quiz_visits') || 0;
const newCount = parseInt(visitCounter) + 1;
localStorage.setItem('quiz_visits', newCount);

window.addEventListener('keydown', function(e) {
  if (e.key.toLowerCase() === 's') {
    const entered = prompt("أدخل كلمة المرور لرؤية عدد الزائرين وعدد الذين أكملوا:");
    if (entered === PASSWORD) {
      visitsEl.style.display = 'block';
      visitsEl.textContent = `عدد الزائرين: ${newCount}`;
      completedEl.style.display = 'block';
      completedEl.textContent = `عدد الذين أكملوا الامتحان: ${localStorage.getItem('quiz_completed') || 0}`;
    }
  }
});

loadQuestion();
</script>

</body>
</html>
<!DOCTYPE html>
<html lang

