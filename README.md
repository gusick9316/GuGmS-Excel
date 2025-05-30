<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>엑셀 함수 연습</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Malgun Gothic', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* 인트로 화면 */
        #intro {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .intro-text {
            font-size: 5rem;
            font-weight: bold;
            color: #fff;
            animation: fadeInOut 3s ease-in-out;
        }

        @keyframes fadeInOut {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1.2); }
            100% { opacity: 0; transform: scale(1); }
        }

        /* 메인 화면 */
        #mainScreen {
            display: none;
            flex: 1;
            padding: 20px;
            text-align: center;
        }

        .main-container {
            background: white;
            border-radius: 20px;
            padding: 50px;
            max-width: 600px;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .developer-info {
            position: absolute;
            top: 20px;
            right: 20px;
            color: white;
            font-size: 14px;
        }

        h1 {
            color: #5a67d8;
            font-size: 3rem;
            margin-bottom: 40px;
        }

        .main-button {
            display: block;
            width: 100%;
            padding: 20px;
            margin: 20px 0;
            background: #5a67d8;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.3s;
        }

        .main-button:hover {
            background: #4c51bf;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        /* 함수 정리 화면 */
        #functionList {
            display: none;
            flex: 1;
            padding: 20px;
            background: white;
            overflow-y: auto;
        }

        .function-container {
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }

        .back-button {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 10px 20px;
            background: #5a67d8;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            z-index: 100;
        }

        .function-category {
            margin: 30px 0;
            background: #f7fafc;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .category-title {
            color: #5a67d8;
            font-size: 1.5rem;
            margin-bottom: 20px;
            text-align: left;
            border-bottom: 2px solid #5a67d8;
            padding-bottom: 10px;
        }

        .function-item {
            background: white;
            margin: 10px 0;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            text-align: left;
        }

        .function-name {
            color: #e53e3e;
            font-weight: bold;
            font-size: 1.2rem;
            margin-bottom: 10px;
        }

        .function-desc {
            color: #4a5568;
            margin-bottom: 10px;
        }

        .function-example {
            background: #edf2f7;
            padding: 10px;
            border-radius: 5px;
            font-family: monospace;
            color: #2d3748;
        }

        /* 실습 화면 */
        #practiceScreen {
            display: none;
            flex: 1;
            padding: 20px;
        }

        .practice-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            max-width: 800px;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .progress {
            font-size: 1.5rem;
            color: #5a67d8;
            margin-bottom: 20px;
        }

        .question-area {
            margin: 20px 0;
            text-align: left;
        }

        .excel-table {
            border-collapse: collapse;
            margin: 20px auto;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .excel-table td {
            border: 1px solid #ccc;
            padding: 8px 15px;
            text-align: center;
            background: white;
        }

        .excel-table .header-row {
            background: #e2e8f0;
            font-weight: bold;
        }

        .excel-table .row-header {
            background: #e2e8f0;
            font-weight: bold;
            width: 30px;
        }

        .function-wizard {
            background: #f7fafc;
            border: 1px solid #cbd5e0;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .wizard-title {
            background: #4a5568;
            color: white;
            padding: 10px;
            margin: -20px -20px 20px -20px;
            border-radius: 10px 10px 0 0;
            font-weight: bold;
        }

        .wizard-input {
            display: flex;
            align-items: center;
            margin: 10px 0;
        }

        .wizard-label {
            width: 150px;
            font-weight: bold;
        }

        .wizard-field {
            flex: 1;
            padding: 8px;
            border: 1px solid #cbd5e0;
            border-radius: 5px;
            font-size: 16px;
        }

        .submit-button {
            background: #48bb78;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 5px;
            font-size: 1.1rem;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s;
        }

        .submit-button:hover {
            background: #38a169;
        }

        .feedback {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 5rem;
            font-weight: bold;
            display: none;
            z-index: 1000;
        }

        .feedback.correct {
            color: #48bb78;
        }

        .feedback.incorrect {
            color: #e53e3e;
        }

        .warning {
            color: #e53e3e;
            margin-top: 10px;
            font-weight: bold;
        }

        /* 결과 화면 */
        #resultScreen {
            display: none;
            flex: 1;
            padding: 20px;
            overflow-y: auto;
        }

        .result-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            max-width: 800px;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .result-title {
            color: #5a67d8;
            font-size: 2.5rem;
            margin-bottom: 30px;
        }

        .result-item {
            background: #f7fafc;
            margin: 10px 0;
            padding: 15px;
            border-radius: 8px;
            text-align: left;
            border-left: 5px solid #cbd5e0;
        }

        .result-item.correct {
            border-left-color: #48bb78;
        }

        .result-item.incorrect {
            border-left-color: #e53e3e;
        }

        .score {
            font-size: 3rem;
            color: #5a67d8;
            margin: 30px 0;
        }

        .score-star {
            font-size: 2rem;
            color: #f6e05e;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: white;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <!-- 인트로 화면 -->
    <div id="intro">
        <div class="intro-text">구겜스</div>
    </div>

    <!-- 메인 화면 -->
    <div id="mainScreen">
        <div class="developer-info">개발: 김구식</div>
        <div class="main-container">
            <h1>엑셀함수연습!</h1>
            <button class="main-button" onclick="showPractice()">엑셀 실습하기</button>
            <button class="main-button" onclick="showFunctions()">함수 정리</button>
        </div>
    </div>

    <!-- 함수 정리 화면 -->
    <div id="functionList">
        <button class="back-button" onclick="showMain()">메인으로</button>
        <div class="function-container">
            <h1 style="color: #5a67d8; margin-bottom: 30px;">엑셀 함수 정리</h1>
            
            <!-- 날짜/텍스트 함수 -->
            <div class="function-category">
                <h2 class="category-title">날짜/텍스트 함수</h2>
                <div class="function-item">
                    <div class="function-name">DATE</div>
                    <div class="function-desc">년, 월, 일을 입력하여 날짜를 생성합니다.</div>
                    <div class="function-example">=DATE(2024, 12, 25) → 2024-12-25</div>
                </div>
                <div class="function-item">
                    <div class="function-name">WEEKDAY</div>
                    <div class="function-desc">날짜의 요일을 숫자로 반환합니다 (1=일요일, 7=토요일).</div>
                    <div class="function-example">=WEEKDAY("2024-12-25") → 4 (수요일)</div>
                </div>
                <div class="function-item">
                    <div class="function-name">YEAR</div>
                    <div class="function-desc">날짜에서 연도를 추출합니다.</div>
                    <div class="function-example">=YEAR("2024-12-25") → 2024</div>
                </div>
                <div class="function-item">
                    <div class="function-name">TODAY</div>
                    <div class="function-desc">오늘 날짜를 반환합니다.</div>
                    <div class="function-example">=TODAY() → 2024-12-25</div>
                </div>
                <div class="function-item">
                    <div class="function-name">LEFT</div>
                    <div class="function-desc">텍스트의 왼쪽에서 지정한 수만큼 문자를 추출합니다.</div>
                    <div class="function-example">=LEFT("엑셀함수", 2) → "엑셀"</div>
                </div>
                <div class="function-item">
                    <div class="function-name">MID</div>
                    <div class="function-desc">텍스트의 중간에서 지정한 위치부터 문자를 추출합니다.</div>
                    <div class="function-example">=MID("엑셀함수연습", 3, 2) → "함수"</div>
                </div>
                <div class="function-item">
                    <div class="function-name">RIGHT</div>
                    <div class="function-desc">텍스트의 오른쪽에서 지정한 수만큼 문자를 추출합니다.</div>
                    <div class="function-example">=RIGHT("엑셀함수", 2) → "함수"</div>
                </div>
                <div class="function-item">
                    <div class="function-name">REPT</div>
                    <div class="function-desc">텍스트를 지정한 횟수만큼 반복합니다.</div>
                    <div class="function-example">=REPT("★", 5) → "★★★★★"</div>
                </div>
            </div>

            <!-- 수학 함수 -->
            <div class="function-category">
                <h2 class="category-title">수학 함수</h2>
                <div class="function-item">
                    <div class="function-name">SUM</div>
                    <div class="function-desc">선택한 셀들의 합계를 구합니다.</div>
                    <div class="function-example">=SUM(A1:A5) → 셀 A1부터 A5까지의 합</div>
                </div>
                <div class="function-item">
                    <div class="function-name">SUMIF</div>
                    <div class="function-desc">조건을 만족하는 셀들의 합계를 구합니다.</div>
                    <div class="function-example">=SUMIF(A1:A10, ">50") → 50보다 큰 값들의 합</div>
                </div>
                <div class="function-item">
                    <div class="function-name">ROUND</div>
                    <div class="function-desc">숫자를 지정한 자릿수로 반올림합니다.</div>
                    <div class="function-example">=ROUND(3.14159, 2) → 3.14</div>
                </div>
                <div class="function-item">
                    <div class="function-name">ROUNDUP</div>
                    <div class="function-desc">숫자를 지정한 자릿수로 올림합니다.</div>
                    <div class="function-example">=ROUNDUP(3.14159, 2) → 3.15</div>
                </div>
                <div class="function-item">
                    <div class="function-name">ROUNDDOWN</div>
                    <div class="function-desc">숫자를 지정한 자릿수로 내림합니다.</div>
                    <div class="function-example">=ROUNDDOWN(3.14159, 2) → 3.14</div>
                </div>
                <div class="function-item">
                    <div class="function-name">SUMPRODUCT</div>
                    <div class="function-desc">배열의 대응하는 구성요소를 곱한 다음 그 곱의 합을 반환합니다.</div>
                    <div class="function-example">=SUMPRODUCT(A1:A3, B1:B3) → (A1×B1)+(A2×B2)+(A3×B3)</div>
                </div>
                <div class="function-item">
                    <div class="function-name">MOD</div>
                    <div class="function-desc">나눗셈의 나머지를 반환합니다.</div>
                    <div class="function-example">=MOD(10, 3) → 1</div>
                </div>
            </div>

            <!-- 데이터베이스 함수 -->
            <div class="function-category">
                <h2 class="category-title">데이터베이스 함수</h2>
                <div class="function-item">
                    <div class="function-name">DSUM</div>
                    <div class="function-desc">데이터베이스에서 조건을 만족하는 레코드의 합계를 구합니다.</div>
                    <div class="function-example">=DSUM(데이터범위, "금액", 조건범위)</div>
                </div>
                <div class="function-item">
                    <div class="function-name">DAVERAGE</div>
                    <div class="function-desc">데이터베이스에서 조건을 만족하는 레코드의 평균을 구합니다.</div>
                    <div class="function-example">=DAVERAGE(데이터범위, "점수", 조건범위)</div>
                </div>
                <div class="function-item">
                    <div class="function-name">DCOUNTA</div>
                    <div class="function-desc">데이터베이스에서 조건을 만족하는 비어있지 않은 셀의 개수를 구합니다.</div>
                    <div class="function-example">=DCOUNTA(데이터범위, "이름", 조건범위)</div>
                </div>
                <div class="function-item">
                    <div class="function-name">DCOUNT</div>
                    <div class="function-desc">데이터베이스에서 조건을 만족하는 숫자 셀의 개수를 구합니다.</div>
                    <div class="function-example">=DCOUNT(데이터범위, "수량", 조건범위)</div>
                </div>
            </div>

            <!-- 통계 함수 -->
            <div class="function-category">
                <h2 class="category-title">통계 함수</h2>
                <div class="function-item">
                    <div class="function-name">MAX</div>
                    <div class="function-desc">선택한 범위에서 가장 큰 값을 반환합니다.</div>
                    <div class="function-example">=MAX(A1:A10) → 범위 내 최대값</div>
                </div>
                <div class="function-item">
                    <div class="function-name">RANK.EQ</div>
                    <div class="function-desc">선택한 범위에서 값의 순위를 반환합니다.</div>
                    <div class="function-example">=RANK.EQ(85, A1:A10) → 85의 순위</div>
                </div>
                <div class="function-item">
                    <div class="function-name">AVERAGE</div>
                    <div class="function-desc">선택한 범위의 평균을 구합니다.</div>
                    <div class="function-example">=AVERAGE(A1:A10) → 범위의 평균값</div>
                </div>
                <div class="function-item">
                    <div class="function-name">COUNTIF</div>
                    <div class="function-desc">조건을 만족하는 셀의 개수를 구합니다.</div>
                    <div class="function-example">=COUNTIF(A1:A10, ">80") → 80보다 큰 셀 개수</div>
                </div>
                <div class="function-item">
                    <div class="function-name">COUNTA</div>
                    <div class="function-desc">비어있지 않은 셀의 개수를 구합니다.</div>
                    <div class="function-example">=COUNTA(A1:A10) → 비어있지 않은 셀 개수</div>
                </div>
                <div class="function-item">
                    <div class="function-name">COUNT</div>
                    <div class="function-desc">숫자가 있는 셀의 개수를 구합니다.</div>
                    <div class="function-example">=COUNT(A1:A10) → 숫자 셀 개수</div>
                </div>
                <div class="function-item">
                    <div class="function-name">COUNTBLANK</div>
                    <div class="function-desc">비어있는 셀의 개수를 구합니다.</div>
                    <div class="function-example">=COUNTBLANK(A1:A10) → 빈 셀 개수</div>
                </div>
                <div class="function-item">
                    <div class="function-name">MIN</div>
                    <div class="function-desc">선택한 범위에서 가장 작은 값을 반환합니다.</div>
                    <div class="function-example">=MIN(A1:A10) → 범위 내 최소값</div>
                </div>
                <div class="function-item">
                    <div class="function-name">MEDIAN</div>
                    <div class="function-desc">선택한 범위의 중앙값을 반환합니다.</div>
                    <div class="function-example">=MEDIAN(A1:A10) → 범위의 중앙값</div>
                </div>
                <div class="function-item">
                    <div class="function-name">LARGE</div>
                    <div class="function-desc">선택한 범위에서 k번째로 큰 값을 반환합니다.</div>
                    <div class="function-example">=LARGE(A1:A10, 2) → 두 번째로 큰 값</div>
                </div>
            </div>

            <!-- 찾기/참조 함수 -->
            <div class="function-category">
                <h2 class="category-title">찾기/참조 함수</h2>
                <div class="function-item">
                    <div class="function-name">INDEX</div>
                    <div class="function-desc">배열에서 행과 열 번호로 값을 찾습니다.</div>
                    <div class="function-example">=INDEX(A1:C10, 5, 2) → 5행 2열의 값</div>
                </div>
                <div class="function-item">
                    <div class="function-name">MATCH</div>
                    <div class="function-desc">범위에서 특정 값의 위치를 찾습니다.</div>
                    <div class="function-example">=MATCH("김철수", A1:A10, 0) → "김철수"의 위치</div>
                </div>
                <div class="function-item">
                    <div class="function-name">CHOOSE</div>
                    <div class="function-desc">인덱스 번호에 따라 목록에서 값을 선택합니다.</div>
                    <div class="function-example">=CHOOSE(2, "사과", "바나나", "오렌지") → "바나나"</div>
                </div>
                <div class="function-item">
                    <div class="function-name">VLOOKUP</div>
                    <div class="function-desc">표의 첫 번째 열에서 값을 찾아 같은 행의 다른 열 값을 반환합니다.</div>
                    <div class="function-example">=VLOOKUP("김철수", A1:D10, 3, FALSE) → 김철수 행의 3번째 열 값</div>
                </div>
            </div>

            <!-- 논리 함수 -->
            <div class="function-category">
                <h2 class="category-title">논리 함수</h2>
                <div class="function-item">
                    <div class="function-name">IF</div>
                    <div class="function-desc">조건이 참이면 첫 번째 값을, 거짓이면 두 번째 값을 반환합니다.</div>
                    <div class="function-example">=IF(A1>80, "합격", "불합격") → A1이 80보다 크면 "합격"</div>
                </div>
                <div class="function-item">
                    <div class="function-name">AND</div>
                    <div class="function-desc">모든 조건이 참일 때 TRUE를 반환합니다.</div>
                    <div class="function-example">=AND(A1>50, B1<100) → 두 조건 모두 참이면 TRUE</div>
                </div>
                <div class="function-item">
                    <div class="function-name">OR</div>
                    <div class="function-desc">조건 중 하나라도 참이면 TRUE를 반환합니다.</div>
                    <div class="function-example">=OR(A1="합격", B1="합격") → 하나라도 "합격"이면 TRUE</div>
                </div>
            </div>
        </div>
    </div>

    <!-- 실습 화면 -->
    <div id="practiceScreen">
        <button class="back-button" onclick="showMain()">메인으로</button>
        <div class="practice-container">
            <div class="progress" id="progress">1/10</div>
            <div id="questionArea"></div>
            <div id="warningMessage" class="warning"></div>
        </div>
    </div>

    <!-- 결과 화면 -->
    <div id="resultScreen">
        <div class="result-container">
            <h1 class="result-title">결과</h1>
            <div id="resultList"></div>
            <div class="score" id="scoreDisplay"></div>
            <div id="starDisplay"></div>
            <button class="main-button" onclick="showMain()">메인으로 돌아가기</button>
        </div>
    </div>

    <!-- 피드백 표시 -->
    <div id="feedback" class="feedback"></div>

    <footer>
        <div id="copyright" style="display: none;">ⓒ2025 구겜스</div>
    </footer>

    <script>
        // 전역 변수
        let currentQuestion = 0;
        let questions = [];
        let answers = [];
        let userAnswers = [];
        let correctCount = 0;

        // 함수 문제 생성기
        const questionGenerators = {
            DATE: () => ({
                question: "2024년 12월 25일의 날짜를 만들어주세요.",
                data: {},
                answer: "=DATE(2024,12,25)",
                params: [
                    { label: "Year", value: "2024" },
                    { label: "Month", value: "12" },
                    { label: "Day", value: "25" }
                ]
            }),
            WEEKDAY: () => ({
                question: "2024년 12월 25일의 요일 번호를 구하세요.",
                 { A1: "2024-12-25" },
                answer: "=WEEKDAY(A1)",
                params: [
                    { label: "Serial_number", value: "A1" }
                ]
            }),
            YEAR: () => ({
                question: "A1 셀의 날짜에서 연도를 추출하세요.",
                 { A1: "2024-12-25" },
                answer: "=YEAR(A1)",
                params: [
                    { label: "Serial_number", value: "A1" }
                ]
            }),
            TODAY: () => ({
                question: "오늘 날짜를 표시하는 함수를 입력하세요.",
                data: {},
                answer: "=TODAY()",
                params: []
            }),
            LEFT: () => ({
                question: 'A1 셀의 텍스트에서 왼쪽 3글자를 추출하세요.',
                data: { A1: "엑셀함수연습" },
                answer: "=LEFT(A1,3)",
                params: [
                    { label: "Text", value: "A1" },
                    { label: "Num_chars", value: "3" }
                ]
            }),
            MID: () => ({
                question: 'A1 셀의 텍스트에서 3번째 위치부터 2글자를 추출하세요.',
                 { A1: "엑셀함수연습" },
                answer: "=MID(A1,3,2)",
                params: "excel_function_practice","old_str":" MID: () => ({\n question: 'A1 셀의 텍스트에서 3번째 위치부터 2글자를 추출하세요.',\n { A1: "엑셀함수연습" },
answer: "=MID(A1,3,2)",\n params: [","new_str":" MID: () => ({
question: 'A1 셀의 텍스트에서 3번째 위치부터 2글자를 추출하세요.',\n { A1: "엑셀함수연습" },\n answer: "=MID(A1,3,2)",\n params: [\n { label: "Text", value: "A1" },\n { label: "Start_num", value: "3" },\n { label: "Num_chars", value: "2" }"}[{"type": "text", "text": "OK", "uuid": "336398e6-5cf3-4d24-8c38-382c5c891b4c"}]{"version_uuid":"75021bd5-8c47-4da6-b845-c7488510fd01","command":"update","id":"excel_function_practice","old_str":" params: [\n { label: "Text", value: "A1" },\n { label: "Start_num", value: "3" },\n { label: "Num_chars", value: "2" }","new_str":" params: [\n { label: "Text", value: "A1" },\n { label: "Start_num", value: "3" },\n { label: "Num_chars", value: "2" }\n ]\n }),\n RIGHT: () => ({\n question: 'A1 셀의 텍스트에서 오른쪽 2글자를 추출하세요.',
{ A1: "엑셀함수" },\n answer: "=RIGHT(A1,2)",\n params: [\n { label: "Text", value: "A1" },\n { label: "Num_chars", value: "2" }\n ]\n }),\n REPT: () => ({\n question: 'A1 셀의 문자를 5번 반복하세요.',\n { A1: "★" },
answer: "=REPT(A1,5)",\n params: [\n { label: "Text", value: "A1" },\n { label: "Number_times", value: "5" }\n ]\n }),\n SUM: () => ({\n question: 'A1부터 A5까지의 합계를 구하세요.',
{ A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=SUM(A1:A5)",\n params: [\n { label: "Number1", value: "A1:A5" }\n ]\n }),\n SUMIF: () => ({\n question: 'A1:A5 범위에서 30 이상인 값들의 합계를 구하세요.',
{ A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=SUMIF(A1:A5,\">=30\")",\n params: [\n { label: "Range", value: "A1:A5" },\n { label: "Criteria", value: "\">=30\"" }\n ]\n }),\n ROUND: () => ({
question: 'A1 셀의 값을 소수점 첫째 자리로 반올림하세요.',
{ A1: "3.456" },\n answer: "=ROUND(A1,1)",\n params: [\n { label: "Number", value: "A1" },\n { label: "Num_digits", value: "1" }\n ]\n }),\n ROUNDUP: () => ({\n question: 'A1 셀의 값을 소수점 첫째 자리로 올림하세요.',\n { A1: "3.123" },\n answer: "=ROUNDUP(A1,1)",\n params: [\n { label: "Number", value: "A1" },\n { label: "Num_digits", value: "1" }\n ]\n }),\n ROUNDDOWN: () => ({\n question: 'A1 셀의 값을 소수점 첫째 자리로 내림하세요.',\n { A1: "3.789" },\n answer: "=ROUNDDOWN(A1,1)",\n params: [\n { label: "Number", value: "A1" },\n { label: "Num_digits", value: "1" }\n ]\n }),\n SUMPRODUCT: () => ({\n question: 'A1:A3와 B1:B3의 곱의 합을 구하세요.',
{ A1: "2", A2: "3", A3: "4", B1: "5", B2: "6", B3: "7" },\n answer: "=SUMPRODUCT(A1:A3,B1:B3)",\n params: [\n { label: "Array1", value: "A1:A3" },\n { label: "Array2", value: "B1:B3" }\n ]\n }),\n MOD: () => ({\n question: 'A1을 B1로 나눈 나머지를 구하세요.',\n { A1: "10", B1: "3" },\n answer: "=MOD(A1,B1)",\n params: [\n { label: "Number", value: "A1" },\n { label: "Divisor", value: "B1" }\n ]\n }),\n MAX: () => ({\n question: 'A1:A5 범위에서 최대값을 구하세요.',
data: { A1: "10", A2: "50", A3: "30", A4: "40", A5: "20" },\n answer: "=MAX(A1:A5)",\n params: [\n { label: "Number1", value: "A1:A5" }\n ]\n }),\n MIN: () => ({\n question: 'A1:A5 범위에서 최소값을 구하세요.',
{ A1: "10", A2: "50", A3: "30", A4: "40", A5: "20" },\n answer: "=MIN(A1:A5)",\n params: [\n { label: "Number1", value: "A1:A5" }\n ]\n }),\n AVERAGE: () => ({\n question: 'A1:A5 범위의 평균을 구하세요.',\n { A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=AVERAGE(A1:A5)",\n params: [\n { label: "Number1", value: "A1:A5" }\n ]\n }),\n COUNT: () => ({\n question: 'A1:A5 범위에서 숫자 개수를 구하세요.',\n { A1: "10", A2: "20", A3: "텍스트", A4: "40", A5: "50" },\n answer: "=COUNT(A1:A5)",\n params: [\n { label: "Value1", value: "A1:A5" }\n ]\n }),\n COUNTA: () => ({\n question: 'A1:A5 범위에서 비어있지 않은 셀 개수를 구하세요.',
{ A1: "10", A2: "텍스트", A3: "", A4: "40", A5: "50" },\n answer: "=COUNTA(A1:A5)",\n params: [\n { label: "Value1", value: "A1:A5" }\n ]\n }),\n COUNTIF: () => ({\n question: 'A1:A5 범위에서 30보다 큰 값의 개수를 구하세요.',\n { A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=COUNTIF(A1:A5,\">30\")",\n params: [\n { label: "Range", value: "A1:A5" },\n { label: "Criteria", value: "\">30\"" }\n ]\n }),\n COUNTBLANK: () => ({\n question: 'A1:A5 범위에서 빈 셀의 개수를 구하세요.',\n { A1: "10", A2: "", A3: "30", A4: "", A5: "50" },\n answer: "=COUNTBLANK(A1:A5)",\n params: [\n { label: "Range", value: "A1:A5" }\n ]\n }),\n MEDIAN: () => ({\n question: 'A1:A5 범위의 중앙값을 구하세요.',\n { A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=MEDIAN(A1:A5)",\n params: [\n { label: "Number1", value: "A1:A5" }\n ]\n }),\n LARGE: () => ({\n question: 'A1:A5 범위에서 2번째로 큰 값을 구하세요.',\n { A1: "10", A2: "50", A3: "30", A4: "40", A5: "20" },\n answer: "=LARGE(A1:A5,2)",\n params: [\n { label: "Array", value: "A1:A5" },\n { label: "K", value: "2" }\n ]\n }),\n RANK.EQ: () => ({\n question: 'A1 값의 A1:A5 범위에서의 순위를 구하세요.',\n { A1: "40", A2: "50", A3: "30", A4: "40", A5: "20" },\n answer: "=RANK.EQ(A1,A1:A5)",\n params: [\n { label: "Number", value: "A1" },\n { label: "Ref", value: "A1:A5" }\n ]\n }),\n INDEX: () => ({\n question: 'A1:C3 범위에서 2행 3열의 값을 구하세요.',
data: { \n A1: "1", B1: "2", C1: "3",\n A2: "4", B2: "5", C2: "6",\n A3: "7", B3: "8", C3: "9"\n },\n answer: "=INDEX(A1:C3,2,3)",\n params: [\n { label: "Array", value: "A1:C3" },\n { label: "Row_num", value: "2" },\n { label: "Column_num", value: "3" }\n ]\n }),\n MATCH: () => ({\n question: 'A1:A5 범위에서 "30"의 위치를 찾으세요.',
{ A1: "10", A2: "20", A3: "30", A4: "40", A5: "50" },\n answer: "=MATCH(30,A1:A5,0)",\n params: [\n { label: "Lookup_value", value: "30" },\n { label: "Lookup_array", value: "A1:A5" },\n { label: "Match_type", value: "0" }\n ]\n }),\n CHOOSE: () => ({\n question: '2번째 선택지를 선택하세요. (선택지: "사과", "바나나", "오렌지")',\n {},\n answer: "=CHOOSE(2,"사과","바나나","오렌지")",
params: [\n { label: "Index_num", value: "2" },\n { label: "Value1", value: ""사과"" },\n { label: "Value2", value: ""바나나"" },\n { label: "Value3", value: ""오렌지"" }
]\n }),\n VLOOKUP: () => ({\n question: 'A열에서 "김철수"를 찾아 B열의 값을 반환하세요.',\n { \n A1: "이름", B1: "점수",
A2: "김철수", B2: "85",\n A3: "이영희", B3: "92"\n },\n answer: "=VLOOKUP("김철수\",A2:B3,2,FALSE)",\n params: [\n { label: "Lookup_value", value: ""김철수"" },
{ label: "Table_array", value: "A2:B3" },\n { label: "Col_index_num", value: "2" },\n { label: "Range_lookup", value: "FALSE" }\n ]\n }),\n IF: () => ({
question: 'A1이 80 이상이면 "합격", 아니면 "불합격"을 표시하세요.',\n { A1: "85" },\n answer: "=IF(A1>=80,"합격","불합격")",
params: [\n { label: "Logical_test", value: "A1>=80" },\n { label: "Value_if_true", value: ""합격"" },\n { label: "Value_if_false", value: ""불합격"" }\n ]\n }),\n AND: () => ({\n question: 'A1이 50 이상이고 B1이 100 이하인지 확인하세요.',
{ A1: "75", B1: "90" },\n answer: "=AND(A1>=50,B1<=100)",\n params: [\n { label: "Logical1", value: "A1>=50" },\n { label: "Logical2", value: "B1<=100" }\n ]\n }),\n OR: () => ({\n question: 'A1이 "합격"이거나 B1이 "합격"인지 확인하세요.',
data: { A1: "불합격", B1: "합격" },
answer: "=OR(A1="합격",B1="합격")",
params: [\n { label: "Logical1", value: "A1="합격"" },
{ label: "Logical2", value: "B1="합격"" }\n ]\n })\n };\n\n // 페이지 로드 시 실행
window.onload = function() {\n setTimeout(() => {\n document.getElementById('intro').style.display = 'none';\n document.getElementById('mainScreen').style.display = 'flex';\n document.getElementById('copyright').style.display = 'block';\n }, 3000);\n };

// 메인 화면 표시
function showMain() {
document.getElementById('mainScreen').style.display = 'flex';\n document.getElementById('functionList').style.display = 'none';\n document.getElementById('practiceScreen').style.display = 'none';\n document.getElementById('resultScreen').style.display = 'none';\n // 변수 초기화
currentQuestion = 0;\n questions = [];\n answers = [];\n userAnswers = [];\n correctCount = 0;\n }\n\n // 함수 정리 화면 표시
function showFunctions() {\n document.getElementById('mainScreen').style.display = 'none';\n document.getElementById('functionList').style.display = 'block';
}

// 실습 화면 표시\n function showPractice() {\n document.getElementById('mainScreen').style.display = 'none';\n document.getElementById('practiceScreen').style.display = 'flex';\n generateQuestions();\n displayQuestion();\n }

// 문제 생성\n function generateQuestions() {\n const functionNames = Object.keys(questionGenerators);\n const selectedFunctions = [];\n \n // 랜덤으로 10개 함수 선택
for (let i = 0; i < 10; i++) {\n const randomIndex = Math.floor(Math.random() * functionNames.length);\n selectedFunctions.push(functionNames[randomIndex]);\n }

// 선택된 함수들로 문제 생성
questions = selectedFunctions.map(funcName => {\n const generator = questionGenerators[funcName];\n const questionData = generator();\n return {\n functionName: funcName,\n ...questionData\n };\n });\n }

// 문제 표시
function displayQuestion() {\n const question = questions[currentQuestion];\n document.getElementById('progress').textContent = `${currentQuestion + 1}/10`;\n \n let tableHTML = '';\n if (Object.keys(question.data).length > 0) {\n tableHTML = '<table class=\"excel-table\">';\n tableHTML += '<tr><td class=\"header-row\"></td><td class=\"header-row\">A</td><td class=\"header-row\">B</td><td class=\"header-row\">C</td></tr>';\n \n for (let i = 1; i <= 5; i++) {\n tableHTML += `<tr><td class=\"row-header\">${i}</td>`;\n ['A', 'B', 'C'].forEach(col => {\n const cellKey = col + i;\n const cellValue = question.data[cellKey] || '';\n tableHTML += `<td>${cellValue}</td>`;\n });\n tableHTML += '</tr>';\n }\n tableHTML += '</table>';\n }\n \n let wizardHTML = '<div class=\"function-wizard\">';\n wizardHTML += `<div class=\"wizard-title">함수 인수 - ${question.functionName}</div>`;\n \n question.params.forEach((param, index) => {\n wizardHTML += `\n <div class=\"wizard-input\">\n <span class=\"wizard-label\">${param.label}:</span>\n <input type=\"text\" class=\"wizard-field\" id=\"param${index}\" placeholder=\"${param.label}\">\n </div>\n `;\n });\n \n wizardHTML += '<button class=\"submit-button" onclick="checkAnswer()">확인</button>';
wizardHTML += '</div>';\n \n document.getElementById('questionArea').innerHTML = `\n <div class=\"question-area\">\n <h2>문제 ${currentQuestion + 1}</h2>\n <p>${question.question}</p>\n ${tableHTML}\n ${wizardHTML}\n </div>\n `;\n \n document.getElementById('warningMessage').textContent = '';\n }

// 답 확인
function checkAnswer() {\n const question = questions[currentQuestion];\n let userAnswer = '=' + question.functionName + '(';\n \n const paramValues = [];\n question.params.forEach((param, index) => {\n const value = document.getElementById(`param${index}`).value;\n if (value.includes(' ')) {\n document.getElementById('warningMessage').textContent = '띄어쓰기를 지워주세요';\n return;\n }\n paramValues.push(value);\n });\n \n if (document.getElementById('warningMessage').textContent) {\n return;\n }\n \n userAnswer += paramValues.join(',') + ')';\n userAnswers.push(userAnswer);\n \n const isCorrect = userAnswer.toUpperCase() === question.answer.toUpperCase();\n if (isCorrect) {\n correctCount++;\n showFeedback('O', true);\n } else {\n showFeedback('X', false);\n }\n answers.push(isCorrect);\n \n setTimeout(() => {\n currentQuestion++;\n if (currentQuestion < 10) {\n displayQuestion();\n } else {\n showResults();\n }\n }, 3000);\n }

// 피드백 표시
function showFeedback(text, isCorrect) {\n const feedback = document.getElementById('feedback');\n feedback.textContent = text;\n feedback.className = 'feedback ' + (isCorrect ? 'correct' : 'incorrect');\n feedback.style.display = 'block';\n \n setTimeout(() => {\n feedback.style.display = 'none';\n }, 3000);\n }\n\n // 결과 표시
function showResults() {
document.getElementById('practiceScreen').style.display = 'none';\n document.getElementById('resultScreen').style.display = 'flex';\n \n let resultHTML = '';\n questions.forEach((question, index) => {\n const isCorrect = answers[index];\n resultHTML += `\n <div class=\"result-item ${isCorrect ? 'correct' : 'incorrect'}\">\n <h3>문제 ${index + 1}: ${question.functionName}</h3>\n <p><strong>문제:</strong> ${question.question}</p>\n <p><strong>당신의 답:</strong> ${userAnswers[index]}</p>
<p><strong>정답:</strong> ${question.answer}</p>\n <p><strong>결과:</strong> ${isCorrect ? 'O' : 'X'}</p>\n </div>\n `;\n });\n \n document.getElementById('resultList').innerHTML = resultHTML;\n \n const score = (correctCount / 10) * 100;\n document.getElementById('scoreDisplay').innerHTML = `점수: ${score}점`;

// 별 표시
let stars = '';\n const starCount = Math.floor(score / 20);\n for (let i = 0; i < 5; i++) {\n stars += i < starCount ? '★' : '☆';
}
document.getElementById('starDisplay').innerHTML = `<div class=\"score-star\">${stars}</div>`;\n }\n </script>\n</body>\n</html>"}[{"type": "text", "text": "OK", "uuid": "84a588cc-d1c8-4e9b-8828-59ae27e01912"}]
