<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>구식이의 함수연습</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Noto Sans KR', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            position: relative;
            animation: titleBounce 2s infinite;
        }
        
        @keyframes titleBounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        h1 {
            font-size: 3rem;
            color: #ff6b6b;
            text-shadow: 3px 3px 0 #ffe66d;
            margin-bottom: 10px;
        }
        
        .character-area {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
            height: 200px;
            position: relative;
        }
        
        .character {
            width: 150px;
            height: 150px;
            background-color: #ffe66d;
            border-radius: 50%;
            position: absolute;
            transition: all 0.3s ease;
        }
        
        .character-face {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .eyes {
            display: flex;
            gap: 20px;
            margin-bottom: 10px;
        }
        
        .eye {
            width: 20px;
            height: 20px;
            background-color: #333;
            border-radius: 50%;
        }
        
        .mouth {
            width: 40px;
            height: 20px;
            background-color: #ff6b6b;
            border-radius: 0 0 20px 20px;
        }
        
        .game-area {
            background-color: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }
        
        .question {
            font-size: 1.2rem;
            margin-bottom: 20px;
            font-weight: bold;
        }
        
        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .option {
            padding: 15px;
            background-color: #f0f0f0;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            text-align: center;
        }
        
        .option:hover {
            background-color: #e0e0e0;
            transform: translateY(-3px);
        }
        
        .option.correct {
            background-color: #a8e6cf;
        }
        
        .option.incorrect {
            background-color: #ffaaa5;
        }
        
        .progress-bar {
            height: 10px;
            background-color: #f0f0f0;
            border-radius: 5px;
            margin-bottom: 20px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: #ff6b6b;
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .coin-display {
            display: flex;
            align-items: center;
            justify-content: flex-end;
            margin-bottom: 20px;
        }
        
        .coin {
            width: 30px;
            height: 30px;
            background-color: #ffe66d;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 10px;
            font-weight: bold;
            color: #333;
        }
        
        .shop-button {
            padding: 10px 20px;
            background-color: #ff6b6b;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s ease;
            margin-left: 10px;
        }
        
        .shop-button:hover {
            background-color: #ff5252;
            transform: translateY(-2px);
        }
        
        .result-screen {
            text-align: center;
            display: none;
        }
        
        .result-message {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #ff6b6b;
        }
        
        .score {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 20px;
        }
        
        .detailed-results {
            text-align: left;
            margin-bottom: 30px;
        }
        
        .result-item {
            padding: 10px;
            border-bottom: 1px solid #f0f0f0;
            display: flex;
            justify-content: space-between;
        }
        
        .restart-button {
            padding: 15px 30px;
            background-color: #ff6b6b;
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.2rem;
            transition: all 0.2s ease;
        }
        
        .restart-button:hover {
            background-color: #ff5252;
            transform: translateY(-3px);
        }
        
        .shop-screen {
            display: none;
            background-color: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        
        .shop-items {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .shop-item {
            background-color: #f9f9f9;
            border-radius: 10px;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .shop-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .shop-item-image {
            width: 100px;
            height: 100px;
            background-color: #ffe66d;
            border-radius: 10px;
            margin: 0 auto 10px;
        }
        
        .shop-item-price {
            font-weight: bold;
            color: #ff6b6b;
        }
        
        .back-button {
            padding: 10px 20px;
            background-color: #333;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .back-button:hover {
            background-color: #555;
        }
        
        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            color: #888;
        }
        
        @keyframes happyJump {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        
        @keyframes sadShake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        @keyframes dance {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(10deg); }
            75% { transform: rotate(-10deg); }
        }
        
        /* 반응형 디자인 */
        @media (max-width: 768px) {
            .options {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .shop-items {
                grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>구식이의 함수연습</h1>
        </header>
        
        <div class="character-area">
            <div class="character">
                <div class="character-face">
                    <div class="eyes">
                        <div class="eye"></div>
                        <div class="eye"></div>
                    </div>
                    <div class="mouth"></div>
                </div>
            </div>
        </div>
        
        <div class="coin-display">
            <span>코인:</span>
            <div class="coin" id="coin-count">0</div>
            <button class="shop-button" id="shop-button">상점</button>
        </div>
        
        <div class="progress-bar">
            <div class="progress" id="progress"></div>
        </div>
        
        <div class="game-area" id="game-area">
            <div class="question" id="question"></div>
            <div class="options" id="options"></div>
        </div>
        
        <div class="result-screen" id="result-screen">
            <div class="result-message" id="result-message"></div>
            <div class="score" id="score"></div>
            <div class="detailed-results" id="detailed-results"></div>
            <button class="restart-button" id="restart-button">다시하기</button>
        </div>
        
        <div class="shop-screen" id="shop-screen">
            <h2>상점</h2>
            <div class="shop-items" id="shop-items">
                <!-- 상점 아이템들이 여기에 동적으로 추가됩니다 -->
            </div>
            <button class="back-button" id="back-button">뒤로가기</button>
        </div>
        
        <footer>
            구겜스2025 - 김구식ⓒ
        </footer>
    </div>

    <script>
        // 게임 데이터
        const functions = [
            "DATE", "WEEKDAY", "YEAR", "TODAY", "LEFT", "MID", "RIGHT", "REPT", 
            "SUM", "SUMIF", "ROUND", "ROUNDUP", "ROUNDDOWN", "SUMPRODUCT", "MOD", 
            "DSUM", "DAVERAGE", "DCOUNTA", "DCOUNT", "MAX", "RANK.EQ", "AVERAGE", 
            "COUNTIF", "COUNTA", "COUNT", "COUNTBLANK", "MIN", "MEDIAN", "LARGE", 
            "INDEX", "MATCH", "CHOOSE", "VLOOKUP", "IF", "AND", "OR"
        ];
        
        const functionDescriptions = {
            "DATE": "특정 날짜를 나타내는 일련 번호를 반환합니다.",
            "WEEKDAY": "날짜에 해당하는 요일을 숫자로 반환합니다.",
            "YEAR": "날짜의 연도를 반환합니다.",
            "TODAY": "현재 날짜를 반환합니다.",
            "LEFT": "텍스트 문자열의 첫 문자부터 지정된 수의 문자를 반환합니다.",
            "MID": "텍스트 문자열의 지정된 위치에서부터 지정된 수의 문자를 반환합니다.",
            "RIGHT": "텍스트 문자열의 마지막 문자부터 지정된 수의 문자를 반환합니다.",
            "REPT": "텍스트를 지정된 횟수만큼 반복합니다.",
            "SUM": "인수의 합계를 구합니다.",
            "SUMIF": "지정한 조건에 맞는 인수의 합계를 구합니다.",
            "ROUND": "숫자를 지정한 자릿수로 반올림합니다.",
            "ROUNDUP": "숫자를 지정한 자릿수로 올림합니다.",
            "ROUNDDOWN": "숫자를 지정한 자릿수로 내림합니다.",
            "SUMPRODUCT": "배열의 해당 요소를 곱한 후 그 곱의 합계를 반환합니다.",
            "MOD": "나눗셈의 나머지를 반환합니다.",
            "DSUM": "데이터베이스에서 조건에 맞는 레코드의 합계를 구합니다.",
            "DAVERAGE": "데이터베이스에서 조건에 맞는 레코드의 평균을 구합니다.",
            "DCOUNTA": "데이터베이스에서 조건에 맞는 비어 있지 않은 레코드를 셉니다.",
            "DCOUNT": "데이터베이스에서 조건에 맞는 숫자가 포함된 레코드를 셉니다.",
            "MAX": "인수 목록에서 최대값을 반환합니다.",
            "RANK.EQ": "숫자 목록에서 숫자의 순위를 반환합니다.",
            "AVERAGE": "인수의 평균을 반환합니다.",
            "COUNTIF": "범위에서 조건에 맞는 셀의 개수를 반환합니다.",
            "COUNTA": "범위에서 비어 있지 않은 셀의 개수를 반환합니다.",
            "COUNT": "범위에서 숫자가 포함된 셀의 개수를 반환합니다.",
            "COUNTBLANK": "범위에서 비어 있는 셀의 개수를 반환합니다.",
            "MIN": "인수 목록에서 최소값을 반환합니다.",
            "MEDIAN": "주어진 숫자의 중간값을 반환합니다.",
            "LARGE": "데이터 집합에서 k번째로 큰 값을 반환합니다.",
            "INDEX": "배열에서 지정한 행과 열의 값을 반환합니다.",
            "MATCH": "참조 또는 배열에서 지정한 값과 일치하는 항목의 상대 위치를 반환합니다.",
            "CHOOSE": "값 목록에서 특정 값을 선택합니다.",
            "VLOOKUP": "배열의 첫 열에서 값을 찾아 지정한 열의 같은 행에 있는 값을 반환합니다.",
            "IF": "조건이 참이면 하나의 값을 반환하고 거짓이면 다른 값을 반환합니다.",
            "AND": "모든 인수가 TRUE이면 TRUE를 반환합니다.",
            "OR": "인수 중 하나라도 TRUE이면 TRUE를 반환합니다."
        };
        
        const functionExamples = {
            "DATE": "=DATE(2023,5,15) → 2023년 5월 15일",
            "WEEKDAY": "=WEEKDAY(DATE(2023,5,15)) → 2 (월요일)",
            "YEAR": "=YEAR(DATE(2023,5,15)) → 2023",
            "TODAY": "=TODAY() → 현재 날짜",
            "LEFT": "=LEFT(\"엑셀함수\",2) → \"엑셀\"",
            "MID": "=MID(\"엑셀함수\",3,1) → \"함\"",
            "RIGHT": "=RIGHT(\"엑셀함수\",1) → \"수\"",
            "REPT": "=REPT(\"★\",5) → \"★★★★★\"",
            "SUM": "=SUM(1,2,3) → 6",
            "SUMIF": "=SUMIF(A1:A5,\">10\") → A1:A5에서 10보다 큰 값의 합계",
            "ROUND": "=ROUND(3.1415,2) → 3.14",
            "ROUNDUP": "=ROUNDUP(3.1415,2) → 3.15",
            "ROUNDDOWN": "=ROUNDDOWN(3.1415,2) → 3.14",
            "SUMPRODUCT": "=SUMPRODUCT(A1:A3,B1:B3) → A1*B1 + A2*B2 + A3*B3",
            "MOD": "=MOD(10,3) → 1",
            "DSUM": "=DSUM(database,field,criteria) → 조건에 맞는 합계",
            "DAVERAGE": "=DAVERAGE(database,field,criteria) → 조건에 맞는 평균",
            "DCOUNTA": "=DCOUNTA(database,field,criteria) → 조건에 맞는 비어 있지 않은 셀 수",
            "DCOUNT": "=DCOUNT(database,field,criteria) → 조건에 맞는 숫자 셀 수",
            "MAX": "=MAX(1,3,2) → 3",
            "RANK.EQ": "=RANK.EQ(A1,A1:A10) → A1의 순위",
            "AVERAGE": "=AVERAGE(1,3,2) → 2",
            "COUNTIF": "=COUNTIF(A1:A10,\">5\") → 5보다 큰 셀 수",
            "COUNTA": "=COUNTA(A1:A10) → 비어 있지 않은 셀 수",
            "COUNT": "=COUNT(A1:A10) → 숫자 셀 수",
            "COUNTBLANK": "=COUNTBLANK(A1:A10) → 빈 셀 수",
            "MIN": "=MIN(1,3,2) → 1",
            "MEDIAN": "=MEDIAN(1,3,2) → 2",
            "LARGE": "=LARGE(A1:A10,2) → 두 번째로 큰 값",
            "INDEX": "=INDEX(A1:C3,2,3) → 2행 3열의 값",
            "MATCH": "=MATCH(\"사과\",A1:A5,0) → \"사과\"의 위치",
            "CHOOSE": "=CHOOSE(2,\"빨강\",\"파랑\",\"초록\") → \"파랑\"",
            "VLOOKUP": "=VLOOKUP(\"사과\",A1:B5,2,FALSE) → \"사과\"에 해당하는 B열 값",
            "IF": "=IF(A1>10,\"큰 수\",\"작은 수\") → 조건에 따른 결과",
            "AND": "=AND(A1>10,A1<20) → 두 조건 모두 만족 여부",
            "OR": "=OR(A1>10,A1<5) → 두 조건 중 하나라도 만족 여부"
        };
        
        const shopItems = [
            { id: 1, name: "모자", price: 50, type: "hat" },
            { id: 2, name: "안경", price: 70, type: "glasses" },
            { id: 3, name: "넥타이", price: 60, type: "tie" },
            { id: 4, name: "스마트워치", price: 100, type: "watch" },
            { id: 5, name: "골드 스킨", price: 200, type: "skin", color: "#FFD700" },
            { id: 6, name: "실버 스킨", price: 150, type: "skin", color: "#C0C0C0" },
            { id: 7, name: "레드 스킨", price: 120, type: "skin", color: "#FF6B6B" },
            { id: 8, name: "블루 스킨", price: 120, type: "skin", color: "#6BB9FF" },
            { id: 9, name: "특별한 눈", price: 80, type: "eyes" },
            { id: 10, name: "웃는 입", price: 60, type: "mouth" }
        ];
        
        const encouragementMessages = [
            { min: 0, max: 30, messages: [
                "괜찮아요! 다음엔 더 잘할 수 있을 거예요.",
                "첫 단추를 꿰는 게 가장 어려운 법이에요. 계속 도전하세요!",
                "실패는 성공의 어머니랍니다. 포기하지 마세요!",
                "오늘의 실수는 내일의 지혜가 됩니다.",
                "조금씩 배워가면 언젠간 마스터할 수 있을 거예요!"
            ]},
            { min: 31, max: 60, messages: [
                "나쁘지 않아요! 조금 더 노력하면 훨씬 나아질 거예요.",
                "절반 이상 맞추셨네요! 다음엔 더 좋은 결과를 기대해봐요.",
                "꾸준히 연습하면 금방 실력이 늘 거예요.",
                "이제 기본은 잡으셨네요. 조금만 더 힘내세요!",
                "오늘의 성과가 내일의 자신감이 됩니다."
            ]},
            { min: 61, max: 80, messages: [
                "잘하고 있어요! 거의 다 왔어요.",
                "대부분 맞추셨네요. 조금만 더 집중하면 완벽해질 거예요.",
                "훌륭한 실력이에요! 마지막까지 파이팅!",
                "이 정도면 이미 함수 마스터 반은 왔어요!",
                "거의 다 왔어요. 마지막까지 힘내세요!"
            ]},
            { min: 81, max: 99, messages: [
                "와우! 거의 다 맞추셨네요!",
                "이제 완벽한 마스터까지 코앞이에요!",
                "정말 대단해요! 한 문제만 더 신경 쓰면 될 것 같아요.",
                "함수 사용법을 거의 다 알고 계시네요!",
                "이 정도면 이미 전문가 수준이에요!"
            ]},
            { min: 100, max: 100, messages: [
                "완벽해요! 진정한 함수 마스터!",
                "100점! 이보다 더 좋을 순 없어요!",
                "엑셀 함수의 달인이 되셨군요!",
                "모든 문제를 맞추다니 대단해요!",
                "함수 사용법을 완벽히 마스터하셨네요!"
            ]}
        ];
        
        // 게임 상태
        let currentQuestion = 0;
        let score = 0;
        let coins = 0;
        let correctAnswers = 0;
        let results = [];
        let equippedItems = [];
        
        // DOM 요소
        const questionElement = document.getElementById('question');
        const optionsElement = document.getElementById('options');
        const gameArea = document.getElementById('game-area');
        const resultScreen = document.getElementById('result-screen');
        const resultMessage = document.getElementById('result-message');
        const scoreElement = document.getElementById('score');
        const detailedResults = document.getElementById('detailed-results');
        const restartButton = document.getElementById('restart-button');
        const progressBar = document.getElementById('progress');
        const coinCount = document.getElementById('coin-count');
        const shopButton = document.getElementById('shop-button');
        const shopScreen = document.getElementById('shop-screen');
        const shopItemsElement = document.getElementById('shop-items');
        const backButton = document.getElementById('back-button');
        const character = document.querySelector('.character');
        
        // 애니메이션 효과
        const animations = [
            function() { character.style.animation = "happyJump 0.5s 2"; },
            function() { character.style.animation = "spin 1s 1"; },
            function() { character.style.animation = "dance 0.5s 3"; },
            function() { character.style.transform = "scale(1.2)"; setTimeout(() => { character.style.transform = "scale(1)"; }, 500); },
            function() { character.style.transform = "translateY(-20px)"; setTimeout(() => { character.style.transform = "translateY(0)"; }, 500); },
            function() { character.style.transform = "rotate(10deg)"; setTimeout(() => { character.style.transform = "rotate(-10deg)"; }, 250); setTimeout(() => { character.style.transform = "rotate(0)"; }, 500); },
            function() { 
                character.style.transform = "translateX(-20px)"; 
                setTimeout(() => { character.style.transform = "translateX(20px)"; }, 200); 
                setTimeout(() => { character.style.transform = "translateX(-20px)"; }, 400); 
                setTimeout(() => { character.style.transform = "translateX(20px)"; }, 600); 
                setTimeout(() => { character.style.transform = "translateX(0)"; }, 800); 
            },
            function() { character.style.transform = "scale(0.8)"; setTimeout(() => { character.style.transform = "scale(1.2)"; }, 300); setTimeout(() => { character.style.transform = "scale(1)"; }, 600); },
            function() { 
                const face = character.querySelector('.character-face');
                face.style.transform = "rotate(180deg)";
                setTimeout(() => { face.style.transform = "rotate(0)"; }, 1000);
            },
            function() { 
                const eyes = character.querySelectorAll('.eye');
                eyes.forEach(eye => {
                    eye.style.height = "5px";
                    setTimeout(() => { eye.style.height = "20px"; }, 300);
                });
            }
        ];
        
        // 문제 생성
        function generateQuestions() {
            const selectedFunctions = [];
            const questions = [];
            
            // 10개의 함수를 무작위로 선택 (중복 없이)
            while (selectedFunctions.length < 10) {
                const randomFunc = functions[Math.floor(Math.random() * functions.length)];
                if (!selectedFunctions.includes(randomFunc)) {
                    selectedFunctions.push(randomFunc);
                }
            }
            
            // 각 함수에 대해 2-3개의 문제 생성
            selectedFunctions.forEach(func => {
                // 설명 기반 문제
                questions.push({
                    type: "description",
                    question: `다음 중 "${func}" 함수의 설명으로 올바른 것은?`,
                    correctAnswer: functionDescriptions[func],
                    options: generateWrongDescriptions(func)
                });
                
                // 예제 기반 문제
                questions.push({
                    type: "example",
                    question: `다음 중 "${func}" 함수의 올바른 사용 예시는?`,
                    correctAnswer: functionExamples[func],
                    options: generateWrongExamples(func)
                });
                
                // 함수 이름 맞추기 문제
                if (Math.random() > 0.5) {
                    const desc = functionDescriptions[func];
                    questions.push({
                        type: "name",
                        question: `다음 설명에 해당하는 함수는?<br>"${desc}"`,
                        correctAnswer: func,
                        options: generateWrongFunctions(func)
                    });
                }
            });
            
            // 문제 순서 무작위로 섞기
            return shuffleArray(questions).slice(0, 10); // 10문제만 선택
        }
        
        function generateWrongDescriptions(correctFunc) {
            const wrongDescriptions = [];
            const allFuncs = [...functions];
            
            // 정답 함수 제거
            const index = allFuncs.indexOf(correctFunc);
            if (index > -1) {
                allFuncs.splice(index, 1);
            }
            
            // 3개의 잘못된 설명 선택
            while (wrongDescriptions.length < 3) {
                const randomFunc = allFuncs[Math.floor(Math.random() * allFuncs.length)];
                wrongDescriptions.push(functionDescriptions[randomFunc]);
                
                // 중복 방지
                const index = allFuncs.indexOf(randomFunc);
                if (index > -1) {
                    allFuncs.splice(index, 1);
                }
            }
            
            return shuffleArray([...wrongDescriptions, functionDescriptions[correctFunc]]);
        }
        
        function generateWrongExamples(correctFunc) {
            const wrongExamples = [];
            const allFuncs = [...functions];
            
            // 정답 함수 제거
            const index = allFuncs.indexOf(correctFunc);
            if (index > -1) {
                allFuncs.splice(index, 1);
            }
            
            // 3개의 잘못된 예제 선택
            while (wrongExamples.length < 3) {
                const randomFunc = allFuncs[Math.floor(Math.random() * allFuncs.length)];
                wrongExamples.push(functionExamples[randomFunc]);
                
                // 중복 방지
                const index = allFuncs.indexOf(randomFunc);
                if (index > -1) {
                    allFuncs.splice(index, 1);
                }
            }
            
            return shuffleArray([...wrongExamples, functionExamples[correctFunc]]);
        }
        
        function generateWrongFunctions(correctFunc) {
            const wrongFuncs = [];
            const allFuncs = [...functions];
            
            // 정답 함수 제거
            const index = allFuncs.indexOf(correctFunc);
            if (index > -1) {
                allFuncs.splice(index, 1);
            }
            
            // 3개의 잘못된 함수 선택
            while (wrongFuncs.length < 3) {
                const randomFunc = allFuncs[Math.floor(Math.random() * allFuncs.length)];
                wrongFuncs.push(randomFunc);
                
                // 중복 방지
                const index = allFuncs.indexOf(randomFunc);
                if (index > -1) {
                    allFuncs.splice(index, 1);
                }
            }
            
            return shuffleArray([...wrongFuncs, correctFunc]);
        }
        
        function shuffleArray(array) {
            const newArray = [...array];
            for (let i = newArray.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
            }
            return newArray;
        }
        
        // 게임 초기화
        function initGame() {
            currentQuestion = 0;
            score = 0;
            correctAnswers = 0;
            results = [];
            
            // 로컬 스토리지에서 코인 불러오기
            const savedCoins = localStorage.getItem('excelFunctionCoins');
            coins = savedCoins ? parseInt(savedCoins) : 0;
            coinCount.textContent = coins;
            
            // 로컬 스토리지에서 장착 아이템 불러오기
            const savedItems = localStorage.getItem('equippedItems');
            equippedItems = savedItems ? JSON.parse(savedItems) : [];
            applyEquippedItems();
            
            // 문제 생성
            const questions = generateQuestions();
            localStorage.setItem('currentQuestions', JSON.stringify(questions));
            
            // 첫 문제 표시
            showQuestion(questions[0]);
            
            // 게임 화면 표시
            gameArea.style.display = 'block';
            resultScreen.style.display = 'none';
            shopScreen.style.display = 'none';
        }
        
        // 문제 표시
        function showQuestion(question) {
            questionElement.innerHTML = question.question;
            optionsElement.innerHTML = '';
            
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.classList.add('option');
                optionElement.textContent = option;
                optionElement.addEventListener('click', () => selectAnswer(option, question.correctAnswer));
                optionsElement.appendChild(optionElement);
            });
            
            // 진행률 업데이트
            progressBar.style.width = `${(currentQuestion / 10) * 100}%`;
        }
        
        // 답변 선택
        function selectAnswer(selectedAnswer, correctAnswer) {
            const isCorrect = selectedAnswer === correctAnswer;
            results.push({
                question: questionElement.textContent,
                selectedAnswer,
                correctAnswer,
                isCorrect
            });
            
            if (isCorrect) {
                score += 10;
                correctAnswers++;
                coins += 5; // 맞출 때마다 5코인 지급
                coinCount.textContent = coins;
                
                // 코인 저장
                localStorage.setItem('excelFunctionCoins', coins.toString());
                
                // 캐릭터 애니메이션
                const randomAnimation = animations[Math.floor(Math.random() * animations.length)];
                randomAnimation();
                
                // 옵션 표시
                const options = document.querySelectorAll('.option');
                options.forEach(option => {
                    if (option.textContent === correctAnswer) {
                        option.classList.add('correct');
                    }
                });
            } else {
                // 캐릭터 애니메이션 (틀렸을 때)
                character.style.animation = "sadShake 0.5s 1";
                
                // 옵션 표시
                const options = document.querySelectorAll('.option');
                options.forEach(option => {
                    if (option.textContent === correctAnswer) {
                        option.classList.add('correct');
                    }
                    if (option.textContent === selectedAnswer) {
                        option.classList.add('incorrect');
                    }
                });
            }
            
            // 다음 문제 또는 결과 화면으로
            setTimeout(() => {
                currentQuestion++;
                const questions = JSON.parse(localStorage.getItem('currentQuestions'));
                
                if (currentQuestion < questions.length) {
                    showQuestion(questions[currentQuestion]);
                } else {
                    showResult();
                }
            }, 1500);
        }
        
        // 결과 화면 표시
        function showResult() {
            gameArea.style.display = 'none';
            resultScreen.style.display = 'block';
            
            // 점수 표시
            scoreElement.textContent = `최종 점수: ${score}점`;
            
            // 결과 메시지
            const encouragement = encouragementMessages.find(range => score >= range.min && score <= range.max);
            const randomMessage = encouragement.messages[Math.floor(Math.random() * encouragement.messages.length)];
            resultMessage.textContent = randomMessage;
            
            // 상세 결과
            detailedResults.innerHTML = '';
            results.forEach((result, index) => {
                const resultItem = document.createElement('div');
                resultItem.classList.add('result-item');
                
                const questionNumber = document.createElement('span');
                questionNumber.textContent = `문제 ${index + 1}`;
                
                const resultIcon = document.createElement('span');
                resultIcon.textContent = result.isCorrect ? '✓' : '✗';
                resultIcon.style.color = result.isCorrect ? 'green' : 'red';
                resultIcon.style.margin = '0 10px';
                
                const questionText = document.createElement('span');
                questionText.textContent = result.question.length > 30 ? 
                    result.question.substring(0, 30) + '...' : result.question;
                questionText.title = result.question;
                
                resultItem.appendChild(questionNumber);
                resultItem.appendChild(resultIcon);
                resultItem.appendChild(questionText);
                detailedResults.appendChild(resultItem);
            });
        }
        
        // 상점 초기화
        function initShop() {
            shopItemsElement.innerHTML = '';
            
            shopItems.forEach(item => {
                const shopItem = document.createElement('div');
                shopItem.classList.add('shop-item');
                
                const itemImage = document.createElement('div');
                itemImage.classList.add('shop-item-image');
                itemImage.style.backgroundColor = item.color || '#ddd';
                
                const itemName = document.createElement('div');
                itemName.textContent = item.name;
                
                const itemPrice = document.createElement('div');
                itemPrice.classList.add('shop-item-price');
                itemPrice.textContent = `${item.price} 코인`;
                
                const buyButton = document.createElement('button');
                buyButton.textContent = equippedItems.some(ei => ei.id === item.id) ? '장착 중' : '구매';
                buyButton.disabled = equippedItems.some(ei => ei.id === item.id) || coins < item.price;
                buyButton.addEventListener('click', () => buyItem(item));
                
                shopItem.appendChild(itemImage);
                shopItem.appendChild(itemName);
                shopItem.appendChild(itemPrice);
                shopItem.appendChild(buyButton);
                shopItemsElement.appendChild(shopItem);
            });
        }
        
        // 아이템 구매
        function buyItem(item) {
            if (coins >= item.price) {
                coins -= item.price;
                coinCount.textContent = coins;
                localStorage.setItem('excelFunctionCoins', coins.toString());
                
                // 같은 타입의 아이템이 있다면 제거
                equippedItems = equippedItems.filter(ei => ei.type !== item.type);
                equippedItems.push(item);
                localStorage.setItem('equippedItems', JSON.stringify(equippedItems));
                
                // 캐릭터에 적용
                applyEquippedItems();
                
                // 상점 새로고침
                initShop();
                
                // 애니메이션 효과
                character.style.animation = "happyJump 0.5s 2";
            }
        }
        
        // 장착 아이템 적용
        function applyEquippedItems() {
            // 기본 스타일 초기화
            character.style.backgroundColor = '#ffe66d';
            
            const face = character.querySelector('.character-face');
            const eyes = character.querySelectorAll('.eye');
            const mouth = character.querySelector('.mouth');
            
            // 기본 요소 초기화
            eyes.forEach(eye => {
                eye.style.width = '20px';
                eye.style.height = '20px';
                eye.style.backgroundColor = '#333';
            });
            
            mouth.style.width = '40px';
            mouth.style.height = '20px';
            mouth.style.backgroundColor = '#ff6b6b';
            mouth.style.borderRadius = '0 0 20px 20px';
            
            // 장착 아이템 적용
            equippedItems.forEach(item => {
                switch(item.type) {
                    case 'skin':
                        character.style.backgroundColor = item.color;
                        break;
                    case 'eyes':
                        eyes.forEach(eye => {
                            eye.style.width = '30px';
                            eye.style.height = '5px';
                        });
                        break;
                    case 'mouth':
                        mouth.style.width = '30px';
                        mouth.style.height = '30px';
                        mouth.style.borderRadius = '50%';
                        break;
                    // 다른 아이템 타입들에 대한 처리 추가 가능
                }
            });
        }
        
        // 이벤트 리스너
        restartButton.addEventListener('click', initGame);
        
        shopButton.addEventListener('click', () => {
            gameArea.style.display = 'none';
            resultScreen.style.display = 'none';
            shopScreen.style.display = 'block';
            initShop();
        });
        
        backButton.addEventListener('click', () => {
            shopScreen.style.display = 'none';
            if (results.length > 0) {
                resultScreen.style.display = 'block';
            } else {
                gameArea.style.display = 'block';
            }
        });
        
        // 게임 시작
        initGame();
    </script>
</body>
</html>
