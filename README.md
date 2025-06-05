<!DOCTYPE html>
<html lang="my">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#6c63ff">
  <link rel="manifest" href="manifest.json">
  <title>အငယ်လေးစမ်းသပ်ဂိမ်း</title>
  <style>
    body {
      font-family: 'Noto Sans Myanmar', sans-serif;
      background: linear-gradient(to right, #fbc2eb, #a18cd1);
      color: #333;
      padding: 20px;
      max-width: 600px;
      margin: auto;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
    h1, h2 {
      text-align: center;
    }
    .question {
      margin: 20px 0;
    }
    button {
      padding: 10px 20px;
      margin: 10px;
      border: none;
      background-color: #6c63ff;
      color: white;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background-color: #574b90;
    }
    .result {
      font-weight: bold;
      font-size: 1.2em;
      margin-top: 20px;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>အငယ်လေးစမ်းသပ်ဂိမ်း</h1>
  <h2>လွယ်ကူပြီး ပျော်စရာကောင်းတဲ့မေးခွန်းများ</h2>

  <div id="game"></div>
  <div class="result" id="score"></div>

  <script>
    const questions = [
      { text: "အငယ်လေးရဲ့ စိတ်ဟာ အတိတ်ကိုတမ်းတနေသူတစ်ယောက်ပါ", correct: true },
      { text: "အနာဂဏ်ကိုပဲ စိတ်ဝင်စားပြီး ပိုပြီးကောင်းအောင်ကြိုးစားနေသူတစ်ယောက်ပါ", correct: false },
      { text: "ငယ်လေးက သူ့အချစ်ကိုကြိုက်သူတစ်ယောက်", correct: true },
      { text: "ငယ်လေးဟာ ကို့အချစ်ကိုယ်သာ ဦးစားပေးပြီး ဆုံးဖျက်တက်သူတစ်ယောက်", correct: false },
      { text: "အငယ်လေးက စိတ်အေးလက်အေး သီချင်းလေးတွေကို နားထောင်ရတာကြိုက်တဲ့သူတစ်ယောက်ပါ", correct: true },
      { text: "ဒါမှမဟုတ် ခံစားချက် အပြည့်နဲ့ သီဆိုထားတဲ့ R&B သိုမဟုတ် Soul သီချင်းတွေ ကိုပိုပြီးကြိုက်တယ်။", correct: false },
      { text: "ဆက်ဆံရေးတစ်ခုကိုတည်ဆောက်နေတဲ့အချိန်မှာဆိုရင် နားလည်မှုကိုပိုယူရတာကိုကြိုက်တယ်", correct: true },
      { text: "ဆက်ဆံ‌ရေးတစ်ခုဆိုတာထက် သူ့ကိုပိုပြီးသိစိတ်ကချစ်လာတာကိုစောင့်ရတာကြိုက်တယ်။", correct: false },
      { text: "အကို့ကိုချစ်တယ် :3", correct: true },
      { text: "အကို့ကိုအချစ်ဘူး 😥", correct: false }
    ];

    let current = 0;
    let score = 0;

    const gameDiv = document.getElementById("game");
    const scoreDiv = document.getElementById("score");

    function showQuestion() {
      if (current >= questions.length) {
        scoreDiv.textContent = `အငယ်လေးရဲ့ဖြေဆိုမှုများအတွက်ဖြေဆိုနိုင်သော မေးခွန်းအရေအတွက်: ${score} / ${questions.length}`;
        return;
      }

      const q = questions[current];
      gameDiv.innerHTML = `
        <div class="question">
          <p>${q.text}</p>
          <button onclick="answer(true)">အမှန်</button>
          <button onclick="answer(false)">အမှား</button>
        </div>
      `;
    }

    function answer(choice) {
      if (choice === questions[current].correct) {
        score++;
      }
      current++;
      showQuestion();
    }

    // Register service worker for PWA
    if ('serviceWorker' in navigator) {
      window.addEventListener('load', () => {
        navigator.serviceWorker.register('service-worker.js');
      });
    }

    showQuestion();
  </script>
</body>
</html>
