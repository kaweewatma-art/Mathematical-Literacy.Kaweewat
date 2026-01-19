<html lang="th" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>คณิตศาสตร์ ป.5</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Prompt', sans-serif;
    }
    
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
    
    @keyframes pulse-glow {
      0%, 100% { box-shadow: 0 0 20px rgba(99, 102, 241, 0.4); }
      50% { box-shadow: 0 0 40px rgba(99, 102, 241, 0.6); }
    }
    
    @keyframes celebrate {
      0% { transform: scale(1); }
      50% { transform: scale(1.1); }
      100% { transform: scale(1); }
    }
    
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      75% { transform: translateX(5px); }
    }
    
    .float-animation {
      animation: float 3s ease-in-out infinite;
    }
    
    .pulse-glow {
      animation: pulse-glow 2s ease-in-out infinite;
    }
    
    .celebrate {
      animation: celebrate 0.5s ease-in-out;
    }
    
    .shake {
      animation: shake 0.5s ease-in-out;
    }
    
    .category-card {
      transition: all 0.3s ease;
    }
    
    .category-card:hover {
      transform: translateY(-5px) scale(1.02);
    }
    
    .option-btn {
      transition: all 0.2s ease;
    }
    
    .option-btn:hover:not(:disabled) {
      transform: scale(1.05);
    }
    
    .progress-fill {
      transition: width 0.5s ease;
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body class="h-full">
  <div id="app" class="h-full w-full overflow-auto" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);"><!-- หน้าหลัก -->
   <div id="home-screen" class="min-h-full p-4 md:p-8">
    <div class="max-w-4xl mx-auto"><!-- Header -->
     <div class="text-center mb-8">
      <div class="inline-block float-animation"><span class="text-6xl md:text-8xl">🧮</span>
      </div>
      <h1 id="app-title" class="text-3xl md:text-5xl font-bold text-white mt-4 drop-shadow-lg">คณิตศาสตร์ ป.5</h1>
      <p id="welcome-msg" class="text-lg md:text-xl text-white/90 mt-2">เลือกหมวดที่ต้องการฝึกฝน</p>
     </div><!-- Stats Bar -->
     <div id="stats-bar" class="bg-white/20 backdrop-blur-sm rounded-2xl p-4 mb-8 flex justify-around text-white">
      <div class="text-center">
       <p class="text-2xl md:text-3xl font-bold" id="total-score">0</p>
       <p class="text-sm opacity-80">คะแนนรวม</p>
      </div>
      <div class="text-center">
       <p class="text-2xl md:text-3xl font-bold" id="total-played">0</p>
       <p class="text-sm opacity-80">ข้อที่ทำ</p>
      </div>
      <div class="text-center">
       <p class="text-2xl md:text-3xl font-bold" id="accuracy">0%</p>
       <p class="text-sm opacity-80">ความแม่นยำ</p>
      </div>
     </div><!-- Categories Grid -->
     <div class="grid grid-cols-2 md:grid-cols-3 gap-4"><button onclick="startQuiz('addition')" class="category-card bg-gradient-to-br from-emerald-400 to-emerald-600 rounded-2xl p-6 text-white shadow-xl pulse-glow"> <span class="text-4xl md:text-5xl block mb-2">➕</span> <p class="font-bold text-lg">การบวก</p><p class="text-sm opacity-80">บวกจำนวนหลายหลัก</p></button> <button onclick="startQuiz('subtraction')" class="category-card bg-gradient-to-br from-rose-400 to-rose-600 rounded-2xl p-6 text-white shadow-xl"> <span class="text-4xl md:text-5xl block mb-2">➖</span> <p class="font-bold text-lg">การลบ</p><p class="text-sm opacity-80">ลบจำนวนหลายหลัก</p></button> <button onclick="startQuiz('multiplication')" class="category-card bg-gradient-to-br from-amber-400 to-amber-600 rounded-2xl p-6 text-white shadow-xl"> <span class="text-4xl md:text-5xl block mb-2">✖️</span> <p class="font-bold text-lg">การคูณ</p><p class="text-sm opacity-80">สูตรคูณและประยุกต์</p></button> <button onclick="startQuiz('division')" class="category-card bg-gradient-to-br from-sky-400 to-sky-600 rounded-2xl p-6 text-white shadow-xl"> <span class="text-4xl md:text-5xl block mb-2">➗</span> <p class="font-bold text-lg">การหาร</p><p class="text-sm opacity-80">หารลงตัวและเศษ</p></button> <button onclick="startQuiz('fraction')" class="category-card bg-gradient-to-br from-violet-400 to-violet-600 rounded-2xl p-6 text-white shadow-xl"> <span class="text-4xl md:text-5xl block mb-2">🍕</span> <p class="font-bold text-lg">เศษส่วน</p><p class="text-sm opacity-80">บวก ลบ เศษส่วน</p></button> <button onclick="startQuiz('decimal')" class="category-card bg-gradient-to-br from-pink-400 to-pink-600 rounded-2xl p-6 text-white shadow-xl"> <span class="text-4xl md:text-5xl block mb-2">🔢</span> <p class="font-bold text-lg">ทศนิยม</p><p class="text-sm opacity-80">บวก ลบ ทศนิยม</p></button>
     </div><!-- History Button -->
     <div class="mt-8 text-center"><button onclick="showHistory()" class="bg-white/20 backdrop-blur-sm text-white px-6 py-3 rounded-full font-medium hover:bg-white/30 transition"> 📊 ดูประวัติการเล่น </button>
     </div><!-- Creator Info -->
     <div class="mt-8 bg-white/20 backdrop-blur-sm rounded-2xl p-6 text-center text-white">
      <p class="text-sm opacity-80 mb-2">ผู้สร้างเกม</p>
      <p class="font-bold text-lg">👨‍🎓 เด็กชาย กวีวัธน์ แมดมิ่งเหง้า</p>
      <p class="text-sm opacity-90 mt-1">ชั้นประถมศึกษาปีที่ 5/5 ชายชั้น MEP</p>
     </div>
    </div>
   </div><!-- หน้าทำข้อสอบ -->
   <div id="quiz-screen" class="min-h-full p-4 md:p-8 hidden">
    <div class="max-w-2xl mx-auto"><!-- Quiz Header -->
     <div class="flex justify-between items-center mb-6"><button onclick="goHome()" class="bg-white/20 backdrop-blur-sm text-white px-4 py-2 rounded-full hover:bg-white/30 transition"> ← กลับ </button>
      <div class="bg-white/20 backdrop-blur-sm text-white px-4 py-2 rounded-full"><span id="current-question">1</span>/10
      </div>
     </div><!-- Progress Bar -->
     <div class="bg-white/30 rounded-full h-4 mb-8">
      <div id="progress-bar" class="progress-fill bg-white rounded-full h-4" style="width: 10%"></div>
     </div><!-- Question Card -->
     <div id="question-card" class="bg-white rounded-3xl shadow-2xl p-6 md:p-10">
      <div class="text-center mb-8"><span id="category-emoji" class="text-5xl md:text-6xl block mb-4">➕</span>
       <h2 id="category-title" class="text-xl md:text-2xl font-bold text-gray-700 mb-2">การบวก</h2>
      </div><!-- Question -->
      <div id="question-display" class="text-center mb-8">
       <p id="question-text" class="text-3xl md:text-5xl font-bold text-indigo-600">123 + 456 = ?</p>
      </div><!-- Options -->
      <div id="options-container" class="grid grid-cols-2 gap-4"><!-- Options will be inserted here -->
      </div><!-- Feedback -->
      <div id="feedback" class="hidden mt-6 text-center p-4 rounded-xl">
       <p id="feedback-text" class="text-xl font-bold"></p>
       <p id="feedback-explanation" class="text-gray-600 mt-2"></p>
      </div><!-- Next Button --> <button id="next-btn" onclick="nextQuestion()" class="hidden w-full mt-6 bg-gradient-to-r from-indigo-500 to-purple-600 text-white py-4 rounded-2xl font-bold text-lg hover:from-indigo-600 hover:to-purple-700 transition"> ข้อถัดไป ➡️ </button>
     </div><!-- Score Display -->
     <div class="mt-6 text-center text-white">
      <p class="text-lg">คะแนน: <span id="quiz-score" class="font-bold text-2xl">0</span> / <span id="quiz-total">10</span></p>
     </div>
    </div>
   </div><!-- หน้าผลลัพธ์ -->
   <div id="result-screen" class="min-h-full p-4 md:p-8 hidden flex items-center justify-center">
    <div class="max-w-lg w-full bg-white rounded-3xl shadow-2xl p-8 text-center">
     <div class="text-6xl md:text-8xl mb-4" id="result-emoji">
      🎉
     </div>
     <h2 id="result-title" class="text-2xl md:text-3xl font-bold text-gray-800 mb-2">เยี่ยมมาก!</h2>
     <p id="result-message" class="text-gray-600 mb-6">คุณทำได้ดีมากเลย!</p>
     <div class="bg-gradient-to-r from-indigo-100 to-purple-100 rounded-2xl p-6 mb-6">
      <p class="text-5xl md:text-6xl font-bold text-indigo-600" id="final-score">8/10</p>
      <p class="text-gray-500 mt-2">คะแนนที่ได้</p>
     </div>
     <div class="flex gap-4"><button onclick="startQuiz(currentCategory)" class="flex-1 bg-gradient-to-r from-emerald-500 to-teal-600 text-white py-3 rounded-xl font-bold hover:from-emerald-600 hover:to-teal-700 transition"> 🔄 เล่นอีก </button> <button onclick="goHome()" class="flex-1 bg-gradient-to-r from-indigo-500 to-purple-600 text-white py-3 rounded-xl font-bold hover:from-indigo-600 hover:to-purple-700 transition"> 🏠 หน้าหลัก </button>
     </div>
    </div>
   </div><!-- หน้าประวัติ -->
   <div id="history-screen" class="min-h-full p-4 md:p-8 hidden">
    <div class="max-w-2xl mx-auto">
     <div class="flex items-center justify-between mb-6"><button onclick="goHome()" class="bg-white/20 backdrop-blur-sm text-white px-4 py-2 rounded-full hover:bg-white/30 transition"> ← กลับ </button>
      <h2 class="text-2xl font-bold text-white">📊 ประวัติการเล่น</h2>
      <div class="w-20"></div>
     </div>
     <div id="history-list" class="space-y-3"><!-- History items will be inserted here -->
     </div>
     <div id="no-history" class="hidden bg-white/20 backdrop-blur-sm rounded-2xl p-8 text-center text-white"><span class="text-5xl block mb-4">📝</span>
      <p class="text-lg">ยังไม่มีประวัติการเล่น</p>
      <p class="opacity-80">เริ่มทำแบบฝึกหัดเพื่อบันทึกคะแนน!</p>
     </div>
    </div>
   </div>
  </div>
  <script>
    // Default config
    const defaultConfig = {
      app_title: 'คณิตศาสตร์ ป.5',
      welcome_message: 'เลือกหมวดที่ต้องการฝึกฝน',
      primary_color: '#667eea',
      secondary_color: '#764ba2',
      accent_color: '#f093fb'
    };
    
    let config = { ...defaultConfig };
    let historyData = [];
    
    // Quiz state
    let currentCategory = '';
    let currentQuestionIndex = 0;
    let score = 0;
    let questions = [];
    let answered = false;
    
    const categoryInfo = {
      addition: { emoji: '➕', title: 'การบวก' },
      subtraction: { emoji: '➖', title: 'การลบ' },
      multiplication: { emoji: '✖️', title: 'การคูณ' },
      division: { emoji: '➗', title: 'การหาร' },
      fraction: { emoji: '🍕', title: 'เศษส่วน' },
      decimal: { emoji: '🔢', title: 'ทศนิยม' }
    };
    
    // Question generators
    function generateAddition() {
      const a = Math.floor(Math.random() * 9000) + 1000;
      const b = Math.floor(Math.random() * 9000) + 1000;
      const answer = a + b;
      return {
        question: `${a.toLocaleString()} + ${b.toLocaleString()} = ?`,
        answer: answer,
        explanation: `${a.toLocaleString()} + ${b.toLocaleString()} = ${answer.toLocaleString()}`
      };
    }
    
    function generateSubtraction() {
      const a = Math.floor(Math.random() * 9000) + 5000;
      const b = Math.floor(Math.random() * 4000) + 1000;
      const answer = a - b;
      return {
        question: `${a.toLocaleString()} - ${b.toLocaleString()} = ?`,
        answer: answer,
        explanation: `${a.toLocaleString()} - ${b.toLocaleString()} = ${answer.toLocaleString()}`
      };
    }
    
    function generateMultiplication() {
      const a = Math.floor(Math.random() * 90) + 10;
      const b = Math.floor(Math.random() * 9) + 2;
      const answer = a * b;
      return {
        question: `${a} × ${b} = ?`,
        answer: answer,
        explanation: `${a} × ${b} = ${answer}`
      };
    }
    
    function generateDivision() {
      const b = Math.floor(Math.random() * 9) + 2;
      const answer = Math.floor(Math.random() * 50) + 10;
      const a = b * answer;
      return {
        question: `${a} ÷ ${b} = ?`,
        answer: answer,
        explanation: `${a} ÷ ${b} = ${answer}`
      };
    }
    
    function generateFraction() {
      const denom = [2, 3, 4, 5, 6][Math.floor(Math.random() * 5)];
      const num1 = Math.floor(Math.random() * (denom - 1)) + 1;
      const num2 = Math.floor(Math.random() * (denom - 1)) + 1;
      const isAdd = Math.random() > 0.5;
      
      if (isAdd) {
        const answer = num1 + num2;
        return {
          question: `${num1}/${denom} + ${num2}/${denom} = ?/${denom}`,
          answer: answer,
          explanation: `${num1}/${denom} + ${num2}/${denom} = ${answer}/${denom}`
        };
      } else {
        const larger = Math.max(num1, num2);
        const smaller = Math.min(num1, num2);
        const answer = larger - smaller;
        return {
          question: `${larger}/${denom} - ${smaller}/${denom} = ?/${denom}`,
          answer: answer,
          explanation: `${larger}/${denom} - ${smaller}/${denom} = ${answer}/${denom}`
        };
      }
    }
    
    function generateDecimal() {
      const a = (Math.floor(Math.random() * 900) + 100) / 10;
      const b = (Math.floor(Math.random() * 90) + 10) / 10;
      const isAdd = Math.random() > 0.5;
      
      if (isAdd) {
        const answer = Math.round((a + b) * 10) / 10;
        return {
          question: `${a.toFixed(1)} + ${b.toFixed(1)} = ?`,
          answer: answer,
          explanation: `${a.toFixed(1)} + ${b.toFixed(1)} = ${answer.toFixed(1)}`
        };
      } else {
        const larger = Math.max(a, b);
        const smaller = Math.min(a, b);
        const answer = Math.round((larger - smaller) * 10) / 10;
        return {
          question: `${larger.toFixed(1)} - ${smaller.toFixed(1)} = ?`,
          answer: answer,
          explanation: `${larger.toFixed(1)} - ${smaller.toFixed(1)} = ${answer.toFixed(1)}`
        };
      }
    }
    
    function generateQuestion(category) {
      const generators = {
        addition: generateAddition,
        subtraction: generateSubtraction,
        multiplication: generateMultiplication,
        division: generateDivision,
        fraction: generateFraction,
        decimal: generateDecimal
      };
      
      const q = generators[category]();
      const options = generateOptions(q.answer, category);
      return { ...q, options };
    }
    
    function generateOptions(correctAnswer, category) {
      const options = [correctAnswer];
      const range = category === 'fraction' ? 5 : (category === 'decimal' ? 10 : Math.max(50, Math.abs(correctAnswer) * 0.2));
      
      while (options.length < 4) {
        let wrong;
        if (category === 'decimal') {
          wrong = Math.round((correctAnswer + (Math.random() - 0.5) * range) * 10) / 10;
        } else {
          wrong = Math.round(correctAnswer + (Math.random() - 0.5) * range * 2);
        }
        if (wrong !== correctAnswer && wrong > 0 && !options.includes(wrong)) {
          options.push(wrong);
        }
      }
      
      return options.sort(() => Math.random() - 0.5);
    }
    
    function startQuiz(category) {
      currentCategory = category;
      currentQuestionIndex = 0;
      score = 0;
      questions = [];
      
      for (let i = 0; i < 10; i++) {
        questions.push(generateQuestion(category));
      }
      
      document.getElementById('home-screen').classList.add('hidden');
      document.getElementById('result-screen').classList.add('hidden');
      document.getElementById('history-screen').classList.add('hidden');
      document.getElementById('quiz-screen').classList.remove('hidden');
      
      showQuestion();
    }
    
    function showQuestion() {
      answered = false;
      const q = questions[currentQuestionIndex];
      const info = categoryInfo[currentCategory];
      
      document.getElementById('category-emoji').textContent = info.emoji;
      document.getElementById('category-title').textContent = info.title;
      document.getElementById('question-text').textContent = q.question;
      document.getElementById('current-question').textContent = currentQuestionIndex + 1;
      document.getElementById('progress-bar').style.width = `${((currentQuestionIndex + 1) / 10) * 100}%`;
      document.getElementById('quiz-score').textContent = score;
      
      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';
      
      q.options.forEach((option, index) => {
        const btn = document.createElement('button');
        btn.className = 'option-btn bg-gradient-to-r from-indigo-100 to-purple-100 text-indigo-700 font-bold text-xl md:text-2xl py-4 px-6 rounded-xl hover:from-indigo-200 hover:to-purple-200 transition';
        btn.textContent = currentCategory === 'decimal' ? option.toFixed(1) : option.toLocaleString();
        btn.onclick = () => checkAnswer(option, btn);
        optionsContainer.appendChild(btn);
      });
      
      document.getElementById('feedback').classList.add('hidden');
      document.getElementById('next-btn').classList.add('hidden');
    }
    
    function checkAnswer(selected, btn) {
      if (answered) return;
      answered = true;
      
      const q = questions[currentQuestionIndex];
      const isCorrect = selected === q.answer;
      
      const allBtns = document.querySelectorAll('.option-btn');
      allBtns.forEach(b => {
        b.disabled = true;
        const val = currentCategory === 'decimal' 
          ? parseFloat(b.textContent) 
          : parseInt(b.textContent.replace(/,/g, ''));
        if (val === q.answer) {
          b.className = 'option-btn bg-gradient-to-r from-emerald-400 to-emerald-600 text-white font-bold text-xl md:text-2xl py-4 px-6 rounded-xl';
        } else if (b === btn && !isCorrect) {
          b.className = 'option-btn bg-gradient-to-r from-rose-400 to-rose-600 text-white font-bold text-xl md:text-2xl py-4 px-6 rounded-xl shake';
        }
      });
      
      if (isCorrect) {
        score++;
        document.getElementById('quiz-score').textContent = score;
        document.getElementById('question-card').classList.add('celebrate');
        setTimeout(() => document.getElementById('question-card').classList.remove('celebrate'), 500);
      }
      
      const feedback = document.getElementById('feedback');
      const feedbackText = document.getElementById('feedback-text');
      const feedbackExplanation = document.getElementById('feedback-explanation');
      
      feedback.classList.remove('hidden');
      feedback.className = `mt-6 text-center p-4 rounded-xl ${isCorrect ? 'bg-emerald-100' : 'bg-rose-100'}`;
      feedbackText.textContent = isCorrect ? '✅ ถูกต้อง!' : '❌ ไม่ถูกต้อง';
      feedbackText.className = `text-xl font-bold ${isCorrect ? 'text-emerald-600' : 'text-rose-600'}`;
      feedbackExplanation.textContent = q.explanation;
      
      const nextBtn = document.getElementById('next-btn');
      nextBtn.classList.remove('hidden');
      nextBtn.textContent = currentQuestionIndex < 9 ? 'ข้อถัดไป ➡️' : 'ดูผลลัพธ์ 🎯';
    }
    
    async function nextQuestion() {
      if (currentQuestionIndex < 9) {
        currentQuestionIndex++;
        showQuestion();
      } else {
        await showResult();
      }
    }
    
    async function showResult() {
      document.getElementById('quiz-screen').classList.add('hidden');
      document.getElementById('result-screen').classList.remove('hidden');
      
      const percentage = (score / 10) * 100;
      let emoji, title, message;
      
      if (percentage >= 90) {
        emoji = '🏆'; title = 'ยอดเยี่ยม!'; message = 'คุณเก่งมากๆ เลย!';
      } else if (percentage >= 70) {
        emoji = '🎉'; title = 'เก่งมาก!'; message = 'ทำได้ดีมากเลย!';
      } else if (percentage >= 50) {
        emoji = '👍'; title = 'ดีใช้ได้!'; message = 'ฝึกต่อไปนะ!';
      } else {
        emoji = '💪'; title = 'พยายามต่อไป!'; message = 'ลองฝึกอีกครั้งนะ!';
      }
      
      document.getElementById('result-emoji').textContent = emoji;
      document.getElementById('result-title').textContent = title;
      document.getElementById('result-message').textContent = message;
      document.getElementById('final-score').textContent = `${score}/10`;
      
      // Save to data SDK
      if (window.dataSdk) {
        const saveResult = await window.dataSdk.create({
          category: currentCategory,
          correct_answers: score,
          total_questions: 10,
          date: new Date().toISOString()
        });
        
        if (!saveResult.isOk) {
          console.error('Failed to save result');
        }
      }
    }
    
    function goHome() {
      document.getElementById('quiz-screen').classList.add('hidden');
      document.getElementById('result-screen').classList.add('hidden');
      document.getElementById('history-screen').classList.add('hidden');
      document.getElementById('home-screen').classList.remove('hidden');
      updateStats();
    }
    
    function showHistory() {
      document.getElementById('home-screen').classList.add('hidden');
      document.getElementById('history-screen').classList.remove('hidden');
      renderHistory();
    }
    
    function renderHistory() {
      const historyList = document.getElementById('history-list');
      const noHistory = document.getElementById('no-history');
      
      if (historyData.length === 0) {
        historyList.innerHTML = '';
        noHistory.classList.remove('hidden');
        return;
      }
      
      noHistory.classList.add('hidden');
      historyList.innerHTML = '';
      
      const sortedHistory = [...historyData].sort((a, b) => new Date(b.date) - new Date(a.date));
      
      sortedHistory.slice(0, 20).forEach(record => {
        const info = categoryInfo[record.category] || { emoji: '📝', title: record.category };
        const date = new Date(record.date);
        const dateStr = date.toLocaleDateString('th-TH', { day: 'numeric', month: 'short', year: 'numeric' });
        const timeStr = date.toLocaleTimeString('th-TH', { hour: '2-digit', minute: '2-digit' });
        const percentage = Math.round((record.correct_answers / record.total_questions) * 100);
        
        const item = document.createElement('div');
        item.className = 'bg-white/20 backdrop-blur-sm rounded-xl p-4 flex items-center gap-4';
        item.innerHTML = `
          <span class="text-3xl">${info.emoji}</span>
          <div class="flex-1">
            <p class="font-bold text-white">${info.title}</p>
            <p class="text-sm text-white/70">${dateStr} ${timeStr}</p>
          </div>
          <div class="text-right">
            <p class="text-2xl font-bold text-white">${record.correct_answers}/${record.total_questions}</p>
            <p class="text-sm ${percentage >= 70 ? 'text-emerald-300' : 'text-rose-300'}">${percentage}%</p>
          </div>
        `;
        historyList.appendChild(item);
      });
    }
    
    function updateStats() {
      if (historyData.length === 0) {
        document.getElementById('total-score').textContent = '0';
        document.getElementById('total-played').textContent = '0';
        document.getElementById('accuracy').textContent = '0%';
        return;
      }
      
      const totalCorrect = historyData.reduce((sum, r) => sum + r.correct_answers, 0);
      const totalQuestions = historyData.reduce((sum, r) => sum + r.total_questions, 0);
      const accuracy = totalQuestions > 0 ? Math.round((totalCorrect / totalQuestions) * 100) : 0;
      
      document.getElementById('total-score').textContent = totalCorrect;
      document.getElementById('total-played').textContent = totalQuestions;
      document.getElementById('accuracy').textContent = `${accuracy}%`;
    }
    
    function applyConfig(cfg) {
      document.getElementById('app-title').textContent = cfg.app_title || defaultConfig.app_title;
      document.getElementById('welcome-msg').textContent = cfg.welcome_message || defaultConfig.welcome_message;
    }
    
    // Data handler
    const dataHandler = {
      onDataChanged(data) {
        historyData = data;
        updateStats();
        if (!document.getElementById('history-screen').classList.contains('hidden')) {
          renderHistory();
        }
      }
    };
    
    // Initialize
    async function init() {
      // Initialize Element SDK
      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (cfg) => {
            config = cfg;
            applyConfig(cfg);
          },
          mapToCapabilities: (cfg) => ({
            recolorables: [],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (cfg) => new Map([
            ['app_title', cfg.app_title || defaultConfig.app_title],
            ['welcome_message', cfg.welcome_message || defaultConfig.welcome_message]
          ])
        });
      }
      
      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init(dataHandler);
        if (!result.isOk) {
          console.error('Failed to initialize Data SDK');
        }
      }
      
      applyConfig(config);
    }
    
    init();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9c03269b51837336',t:'MTc2ODc5MjM1MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
