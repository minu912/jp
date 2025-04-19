<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>일본어 퀴즈</title>
  <style>
    body { background: #2c2c2c; color: white; font-family: 'Arial'; text-align: center; padding: 40px; }
    .card { background: #444; padding: 30px; border-radius: 20px; max-width: 500px; margin: auto; box-shadow: 0 0 10px #000; }
    h1 { font-size: 2em; margin-bottom: 20px; }
    #question { font-size: 1.8em; margin-bottom: 20px; }
    input { font-size: 1.5em; padding: 10px; width: 80%; border-radius: 10px; border: none; text-align: center; }
    .result { margin-top: 20px; font-size: 1.2em; }
    #score { margin-top: 10px; font-size: 1em; }
    button { margin-top: 30px; padding: 10px 20px; font-size: 1em; border: none; border-radius: 10px; background: #008cba; color: white; }
  </style>
</head>
<body>
  <div class="card">
    <h1>일본어 퀴즈</h1>
    <div id="question">문제 준비 중...</div>
    <input id="answer" type="text" placeholder="일본어로 입력" autocomplete="off" />
    <div class="result" id="result"></div>
    <div id="score"></div>
    <button onclick="startQuiz()">다시 시작</button>
  </div>

  <script>
    const words = {
      "가다": "이쿠", "하다": "스루", "오다": "쿠루", "보다": "미루", "말하다": "이우",
      "듣다": "키쿠", "쓰다": "카쿠", "읽다": "요무", "먹다": "타베루", "마시다": "노무",
      "만나다": "아우", "이야기하다": "하나스", "걷다": "아루쿠", "뛰다": "하시루", "자다": "네루",
      "일어나다": "오키루", "만들다": "츠쿠루", "기다리다": "마츠", "서다": "타츠", "앉다": "스와루",
      "사다": "카우", "팔다": "우루", "알려주다": "오시에루", "타다": "노루", "내리다": "오리루",
      "일하다": "하타라쿠", "돌아가다": "카에루", "찍다": "토루", "시작하다": "하지메루", "끝나다": "오와루",
      "빌려주다": "카스", "빌리다": "카리루", "배우다": "나라우", "웃다": "와라우", "울다": "나쿠",
      "화내다": "오코루", "버리다": "스테루", "사용하다": "츠카우", "열다": "아케루", "닫다": "시메루",
      "자르다": "키루", "보여주다": "미세루", "노래하다": "우타우", "이기다": "카츠", "지다": "마케루",
      "놀다": "아소부", "들다": "모츠", "쉬다": "야스무", "부르다": "요부", "움직이다": "우고쿠",
      "보내다": "오쿠루", "생각해내다": "오모이다스", "정하다": "키메루", "입다": "키루", "벗다": "누구",
      "신다": "하쿠", "대답하다": "코타에루", "돕다": "테츠다우", "찾다": "사가스", "고치다": "나오스",
    };

    let keys = Object.keys(words);
    let index = 0;
    let score = 0;

    const questionEl = document.getElementById("question");
    const answerEl = document.getElementById("answer");
    const resultEl = document.getElementById("result");
    const scoreEl = document.getElementById("score");

    function startQuiz() {
      index = 0;
      score = 0;
      keys = Object.keys(words);
      answerEl.disabled = false;
      resultEl.textContent = "";
      scoreEl.textContent = "";
      nextQuestion();
    }

    function nextQuestion() {
      if (index >= keys.length) {
        questionEl.textContent = "🎉 퀴즈 완료!";
        answerEl.disabled = true;
        resultEl.textContent = `총 ${keys.length}문제 중 ${score}개 정답!`;
        return;
      }
      questionEl.textContent = keys[index];
      answerEl.value = "";
      answerEl.focus();
      resultEl.textContent = "";
    }

    answerEl.addEventListener("keydown", function (e) {
      if (e.key === "Enter") {
        const userAnswer = answerEl.value.trim();
        const correct = words[keys[index]];
        if (userAnswer === correct) {
          resultEl.textContent = "✅ 정답입니다!";
          resultEl.style.color = "lightgreen";
          score++;
        } else {
          resultEl.textContent = `❌ 오답입니다. 정답: ${correct}`;
          resultEl.style.color = "red";
        }
        scoreEl.textContent = `현재 점수: ${score} / ${keys.length}`;
        index++;
        setTimeout(nextQuestion, 1000);
      }
    });

    startQuiz();
  </script>
</body>
</html>
