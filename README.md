<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Асық Ойыны</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #e3ffbf;
            background-image: url('Үй.jpg');
            overflow: hidden;
            touch-action: manipulation;
            user-select: none;
            -webkit-user-select: none;
        }

        #game-container {
            position: relative;
            width: 100vw;
            height: 100vh;
            overflow: hidden;
        }

        #bag {
            position: absolute;
            width: 500px;
            height: 500px;
            background-image: url('Q.png');
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            bottom: 5%;
            left: 50%;
            transform: translateX(-50%);
            cursor: pointer;
            z-index: 10;
            transition: transform 0.3s;
        }

        #bag:active {
            transform: translateX(-50%) scale(0.95);
        }

        .asyk {
            position: absolute;
            width: 110px;
            height: 110px;
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            cursor: pointer;
            z-index: 5;
            transition: transform 0.2s;
            filter: drop-shadow(0 0 5px gold);
        }

        .asyk:active {
            transform: scale(1.2);
        }

        #question-table {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            z-index: 100;
            display: none;
            max-width: 90%;
            width: 600px;
            text-align: center;
            border: 3px solid #5d4037;
            animation: pulse-border 2s infinite;
        }

        @keyframes pulse-border {
            0% { border-color: #5d4037; }
            50% { border-color: #ffcc00; }
            100% { border-color: #5d4037; }
        }

        #question-table h2 {
            color: #5d4037;
            margin-bottom: 20px;
            font-size: 24px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
        }

        #question-table table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
            font-size: 18px;
        }

        #question-table th, #question-table td {
            border: 2px solid #8d6e63;
            padding: 12px;
            text-align: center;
            transition: all 0.3s;
        }

        #question-table th {
            background-color: #5d4037;
            color: white;
            font-size: 20px;
        }

        #question-table tr:nth-child(even) {
            background-color: #efebe9;
        }

        #question-table tr:hover {
            background-color: #d7ccc8;
            transform: scale(1.02);
        }

        .correct-answer {
            background-color: #a5d6a7 !important;
            animation: correct-pulse 0.5s;
            box-shadow: 0 0 15px #4CAF50;
        }

        .wrong-answer {
            background-color: #ffab91 !important;
            animation: wrong-shake 0.5s;
        }

        @keyframes correct-pulse {
            0% { transform: scale(1); box-shadow: 0 0 5px #4CAF50; }
            50% { transform: scale(1.05); box-shadow: 0 0 20px #4CAF50; }
            100% { transform: scale(1); box-shadow: 0 0 5px #4CAF50; }
        }

        @keyframes wrong-shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-5px); }
            40%, 80% { transform: translateX(5px); }
        }

        #close-btn {
            background-color: #5d4037;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 18px;
            margin-top: 20px;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        #close-btn:hover {
            background-color: #3e2723;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }

        #score-display {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 12px 20px;
            border-radius: 10px;
            font-size: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
            z-index: 50;
            border: 2px solid #5d4037;
            animation: score-pulse 2s infinite;
        }

        @keyframes score-pulse {
            0% { box-shadow: 0 0 5px rgba(93, 64, 55, 0.5); }
            50% { box-shadow: 0 0 15px rgba(93, 64, 55, 0.8); }
            100% { box-shadow: 0 0 5px rgba(93, 64, 55, 0.5); }
        }

        #instructions {
            position: fixed;
            top: 20px;
            left: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 15px;
            border-radius: 10px;
            font-size: 18px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
            z-index: 50;
            max-width: 350px;
            border: 2px solid #5d4037;
            line-height: 1.5;
        }

        #game-over {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            z-index: 200;
            display: none;
            max-width: 90%;
            width: 500px;
            text-align: center;
            border: 3px solid #5d4037;
            animation: game-over-glow 2s infinite;
        }

        @keyframes game-over-glow {
            0% { box-shadow: 0 0 10px rgba(93, 64, 55, 0.5); }
            50% { box-shadow: 0 0 30px rgba(255, 215, 0, 0.8); }
            100% { box-shadow: 0 0 10px rgba(93, 64, 55, 0.5); }
        }

        #game-over h2 {
            color: #5d4037;
            margin-bottom: 20px;
            font-size: 28px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.2);
        }

        #restart-btn {
            background: linear-gradient(to bottom, #5d4037, #3e2723);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 18px;
            margin-top: 20px;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            text-shadow: 1px 1px 1px rgba(0,0,0,0.3);
        }

        #restart-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.4);
        }

        .score-popup {
            position: absolute;
            color: #4CAF50;
            font-size: 24px;
            font-weight: bold;
            animation: score-pop 1s forwards;
            pointer-events: none;
            z-index: 1000;
            text-shadow: 0 0 5px white;
        }

        @keyframes score-pop {
            0% { transform: scale(0.5); opacity: 0; }
            50% { transform: scale(1.5); opacity: 1; }
            100% { transform: scale(1) translateY(-50px); opacity: 0; }
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: #f00;
            animation: confetti-fall 5s linear forwards;
            z-index: 999;
        }

        @keyframes confetti-fall {
            0% { transform: translateY(-100vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="bag"></div>
        <div id="score-display">Ұпай: 0 | Сұрақ: 0/20</div>
        <div id="instructions">
            Асық ойыны<br>
            
        </div>
    </div>

    <div id="question-table">
        <h2>Сұрақ</h2>
        <div id="question-text"></div>
        <table id="answer-table">
            <tr>
                <th>Нұсқа</th>
                <th>Жауап</th>
            </tr>
        </table>
        <button id="close-btn">Жабу</button>
    </div>

    <div id="game-over">
        <h2>Ойын аяқталды!</h2>
        <p id="final-score"></p>
        <p>Барлық 20 сұраққа жауап бердіңіз!</p>
        <button id="restart-btn">Қайта ойнау</button>
    </div>

    <audio id="background-music" loop>
        <source src="Abay.mp3" type="audio/mpeg">
    </audio>

    <audio id="correct-sound" src="correct.mp3"></audio>
    <audio id="wrong-sound" src="wrong.mp3"></audio>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const bag = document.getElementById('bag');
            const gameContainer = document.getElementById('game-container');
            const questionTable = document.getElementById('question-table');
            const questionText = document.getElementById('question-text');
            const answerTable = document.getElementById('answer-table');
            const closeBtn = document.getElementById('close-btn');
            const scoreDisplay = document.getElementById('score-display');
            const gameOverScreen = document.getElementById('game-over');
            const finalScore = document.getElementById('final-score');
            const restartBtn = document.getElementById('restart-btn');
            const backgroundMusic = document.getElementById('background-music');
            const correctSound = document.getElementById('correct-sound');
            const wrongSound = document.getElementById('wrong-sound');
            
            let score = 0;
            let asykCount = 0;
            const maxAsyk = 1;
            let usedQuestions = [];
            let totalQuestionsAnswered = 0;
            const totalQuestions = 20;
            
            // Музыканы басқару функциясы
            function initMusic() {
                backgroundMusic.volume = 0.5;
                correctSound.volume = 0.7;
                wrongSound.volume = 0.7;
                
                const playMusic = () => {
                    backgroundMusic.play()
                        .then(() => console.log("Музыка ойнайды"))
                        .catch(e => {
                            console.log("Автоматты ойнату сөзізді, пайдаланушы әрекетін күтеміз");
                            document.addEventListener('click', () => {
                                backgroundMusic.play()
                                    .then(() => console.log("Музыка пайдаланушы әрекетінен кейін ойнайды"))
                                    .catch(e => console.error("Қате:", e));
                            }, { once: true });
                        });
                };

                window.addEventListener('load', playMusic);
                
                restartBtn.addEventListener('click', function() {
                    backgroundMusic.currentTime = 0;
                    playMusic();
                });
            }

            initMusic();

            // Асық суреттерінің дерекқоры
            const asykImages = [
                'F.png',
                'Y.png',
                'G.png',
                'R.png',
                'B.png'
            ];
            
            // Сұрақтар мен жауаптардың дерекқоры
            const questions = [
                 {
                    question: "1. Абай Құнанбаевтың толық аты-жөні қандай?",
                    answers: [
                        ["A", "Ибраһим Құнанбайұлы"],
                        ["B", "Абай Құнанбаев"],
                        ["C", "Ибраһим Абайұлы"],
                        ["D", "Құнанбай Ибраһимұлы"]
                    ],
                    correct: "A"
                },
                {
                    question: "2. Абай қай жылы дүниеге келген?",
                    answers: [
                        ["A", "1850 жылы"],
                        ["B", "1845 жылы"],
                        ["C", "1840 жылы"],
                        ["D", "1835 жылы"]
                    ],
                    correct: "B"
                },
                {
                    question: "3. Абайдың туған жері?",
                    answers: [
                        ["A", "Қарағанды облысы, Қарқаралы ауданы"],
                        ["B", "Алматы облысы, Жамбыл ауданы"],
                        ["C", "Семей облысы, Шыңғыстау өңірі"],
                        ["D", "Түркістан облысы, Отырар ауданы"]
                    ],
                    correct: "C"
                },
                {
                    question: "4. Абайдың әкесінің аты кім?",
                    answers: [
                        ["A", "Шәкәрім Құнанбайұлы"],
                        ["B", "Өскенбай Құнанбайұлы"],
                        ["C", "Құнанбай Өскенбайұлы"],
                        ["D", "Ибраһим Құнанбайұлы"]
                    ],
                    correct: "C"
                },
                {
                    question: "5. Абайдың анасының аты кім?",
                    answers: [
                        ["A", "Зере"],
                        ["B", "Ұлжан"],
                        ["C", "Қарлығаш"],
                        ["D", "Айғаным"]
                    ],
                    correct: "B"
                },
                {
                    question: "6. Абайдың әжесінің аты кім және ол Абайға қандай әсер еткен?",
                    answers: [
                        ["A", "Ұлжан, өлеңдерімен әсер еткен"],
                        ["B", "Қарлығаш, ақындығымен әсер еткен"],
                        ["C", "Зере, ертегілерімен, аңыз-әңгімелерімен Абайдың қиялын оятқан"],
                        ["D", "Айғаным, діни білімімен әсер еткен"]
                    ],
                    correct: "C"
                },
                {
                    question: "7. Абай алғаш білімді қайдан алды?",
                    answers: [
                        ["A", "Әкесінен үйренген"],
                        ["B", "Медреседе және Семейдегі орыс мектебінде оқыған"],
                        ["C", "Қажылық сапары кезінде"],
                        ["D", "Қазақ даласындағы ауыл мектебінде"]
                    ],
                    correct: "D"
                },
                {
                    question: "8. Абайдың ақындық жолға келуіне әсер еткен орыс классиктері кімдер?",
                    answers: [
                        ["A", "А.П. Чехов, И.С. Тургенев"],
                        ["B", "Н.В. Гоголь, М. Горький"],
                        ["C", "А.С. Пушкин, М.Ю. Лермонтов, И.А. Крылов"],
                        ["D", "Л.Н. Толстой, Ф.М. Достоевский"]
                    ],
                    correct: "C"
                },
                {
                    question: "9. Абайдың шығармашылығында ерекше орын алатын еңбегі?",
                    answers: [
                        ["A", "Өлеңдер"],
                        ["B", "Қара сөздер"],
                        ["C", "Аудармалар"],
                        ["D", "Аңыздар"]
                    ],
                    correct: "B"
                },
                {
                    question: "10. Абай неше қара сөз жазды?",
                    answers: [
                        ["A", "45 қара сөз"],
                        ["B", "38 қара сөз"],
                        ["C", "45 қара сөз"],
                        ["D", "52 қара сөз"]
                    ],
                    correct: "C"
                },
                {
                    question: "11. Абай аудармашы ретінде кімдердің шығармаларын қазақ тіліне аударды?",
                    answers: [
                        ["A", "Толстой, Достоевский, Чехов"],
                        ["B", "Шекспир, Диккенс, Бальзак"],
                        ["C", "Пушкин, Лермонтов, Крылов, Гете, Байрон"],
                        ["D", "Гоголь, Тургенев, Горький"]
                    ],
                    correct: "C"
                },
                {
                    question: "12. Абайдың қара сөздерінде қандай тақырыптар қамтылған?",
                    answers: [
                        ["A", "Тарих, саясат, қоғам"],
                        ["B", "Ғылым, техника, өнер"],
                        ["C", "Табиғат, махаббат, өмір"],
                        ["D", "Адамгершілік, білім, еңбек, әділет, мінез-құлық, дін"]
                    ],
                    correct: "D"
                },
                {
                    question: "13. Абайдың поэзиясында басты тақырып не болды?",
                    answers: [
                        ["A", "Діни ұғымдарды насихаттау"],
                        ["B", "Тарихи оқиғаларды баяндау"],
                        ["C", "Халықты оқу-білімге, өнерге шақыру, адамгершілікке тәрбиелеу"],
                        ["D", "Табиғатты суреттеу"]
                    ],
                    correct: "C"
                },
                {
                    question: "14. Абайдың шәкірттерінің бірі кім?",
                    answers: [
                        ["A", "Сәкен Сейфуллин"],
                        ["B", "Шәкәрім Құдайбердіұлы"],
                        ["C", "Мағжан Жұмабаев"],
                        ["D", "Мұхтар Әуезов"]
                    ],
                    correct: "B"
                },
                {
                    question: "15. Абайдың композиторлық өнері бар ма?",
                    answers: [
                        ["A", "Жоқ, ол тек ақын болды"],
                        ["B", "Жоқ, ол тек өлең жазып, өзгелердің әндерін жинаған"],
                        ["C", "Иә, ол 'Көзімнің қарасы', 'Желсіз түнде жарық ай' сияқты әндер шығарған"],
                        ["D", "Иә, бірақ тек бірнеше ән жазған"]
                    ],
                    correct: "C"
                },
                {
                    question: "16. Абайдың орыс достары кімдер болды?",
                    answers: [
                        ["A", "А.С. Пушкин, М.Ю. Лермонтов"],
                        ["B", "А.П. Чехов, И.С. Тургенев"],
                        ["C", "Е.П. Михаэлис, С.Г. Гросс, Н.И. Долгополов"],
                        ["D", "Л.Н. Толстой, Ф.М. Достоевский"]
                    ],
                    correct: "C"
                },
                {
                    question: "17. Абай қай жылы қайтыс болды?",
                    answers: [
                        ["A", "1910 жылы"],
                        ["B", "1904 жылы"],
                        ["C", "1899 жылы"],
                        ["D", "1905 жылы"]
                    ],
                    correct: "B"
                },
                {
                    question: "18. Абайдың бейіті қайда орналасқан?",
                    answers: [
                        ["A", "Қарауыл өзенінің жағасында"],
                        ["B", "Семей қаласында"],
                        ["C", "Жидебай қыстағында"],
                        ["D", "Шыңғыстау тауында"]
                    ],
                    correct: "C"
                },
                {
                    question: "19. Абайдың 175 жылдық мерейтойы қай жылы атап өтілді?",
                    answers: [
                        ["A", "2015 жылы"],
                        ["B", "1995 жылы"],
                        ["C", "2020 жылы"],
                        ["D", "2025 жылы"]
                    ],
                    correct: "C"
                },
                {
                    question: "20. Абайдың мұрасын зерттеген белгілі жазушы және ғалым кім?",
                    answers: [
                        ["A", "Ілияс Жансүгіров"],
                        ["B", "Сәбит Мұқанов"],
                        ["C", "Мұхтар Әуезов ('Абай жолы' роман-эпопеясының авторы)"],
                        ["D", "Ғабит Мүсірепов"]
                    ],
                    correct: "C"
                }
            ];
            
            
            // Ұпайды көрсету анимациясы
            function showScorePopup(element, points) {
                const popup = document.createElement('div');
                popup.className = 'score-popup';
                popup.textContent = `+${points}`;
                
                const rect = element.getBoundingClientRect();
                popup.style.left = `${rect.left + rect.width/2}px`;
                popup.style.top = `${rect.top}px`;
                
                document.body.appendChild(popup);
                
                setTimeout(() => {
                    popup.remove();
                }, 1000);
            }
            
            // Конфетти анимациясы
            function createConfetti() {
                const colors = ['#f00', '#0f0', '#00f', '#ff0', '#f0f', '#0ff'];
                
                for (let i = 0; i < 50; i++) {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.left = `${Math.random() * 100}vw`;
                    confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        confetti.remove();
                    }, 5000);
                }
            }
            
            // Қоржынды басқанда асықтарды шығару
            bag.addEventListener('click', function(e) {
                if (asykCount >= maxAsyk) return;
                
                createAsyk();
                asykCount++;
            });
            
            // Асықтарды жасау функциясы
            function createAsyk() {
                const asyk = document.createElement('div');
                asyk.className = 'asyk';
                
                const randomImageIndex = Math.floor(Math.random() * asykImages.length);
                asyk.style.backgroundImage = `url('${asykImages[randomImageIndex]}')`;
                
                const bagRect = bag.getBoundingClientRect();
                const x = bagRect.left + bagRect.width / 2 - 50;
                const y = bagRect.top - 50;
                
                asyk.style.left = x + 'px';
                asyk.style.top = y + 'px';
                
                asyk.addEventListener('click', function(e) {
                    e.stopPropagation();
                    showRandomQuestion();
                    this.remove();
                    asykCount--;
                });
                
                setTimeout(() => {
                    const containerWidth = gameContainer.offsetWidth;
                    const containerHeight = gameContainer.offsetHeight;
                    
                    const randomX = Math.random() * (containerWidth - 200) + 100;
                    const randomY = Math.random() * (containerHeight - bagRect.height - 200) + 100;
                    
                    asyk.style.left = randomX + 'px';
                    asyk.style.top = randomY + 'px';
                    asyk.style.transition = 'left 1s, top 1s';
                }, 10);
                
                gameContainer.appendChild(asyk);
            }
            
            // Кездейсоқ сұрақты көрсету
            function showRandomQuestion() {
                if (usedQuestions.length === questions.length) {
                    usedQuestions = [];
                }
                
                let randomIndex;
                do {
                    randomIndex = Math.floor(Math.random() * questions.length);
                } while (usedQuestions.includes(randomIndex));
                
                usedQuestions.push(randomIndex);
                const currentQuestion = questions[randomIndex];
                
                questionText.textContent = currentQuestion.question;
                
                while (answerTable.rows.length > 1) {
                    answerTable.deleteRow(1);
                }
                
                currentQuestion.answers.forEach(answer => {
                    const row = answerTable.insertRow();
                    const cell1 = row.insertCell(0);
                    const cell2 = row.insertCell(1);
                    
                    cell1.textContent = answer[0];
                    cell2.textContent = answer[1];
                    
                    row.addEventListener('click', function() {
                        const isCorrect = answer[0] === currentQuestion.correct;
                        
                        if (isCorrect) {
                            this.classList.add('correct-answer');
                            correctSound.play();
                            showScorePopup(this, 10);
                            score += 10;
                            updateScore();
                            
                            if (score % 50 === 0) {
                                createConfetti();
                            }
                        } else {
                            this.classList.add('wrong-answer');
                            wrongSound.play();
                            
                            // Дұрыс жауапты табу
                            const rows = answerTable.querySelectorAll('tr');
                            rows.forEach(r => {
                                if (r.cells[0].textContent === currentQuestion.correct) {
                                    r.classList.add('correct-answer');
                                }
                            });
                        }
                        
                        const rows = answerTable.querySelectorAll('tr');
                        rows.forEach(r => {
                            if (r !== answerTable.rows[0]) {
                                r.style.pointerEvents = 'none';
                            }
                        });
                        
                        totalQuestionsAnswered++;
                        checkGameEnd();
                        
                        setTimeout(() => {
                            questionTable.style.display = 'none';
                            rows.forEach(r => {
                                if (r !== answerTable.rows[0]) {
                                    r.style.pointerEvents = '';
                                    r.classList.remove('correct-answer', 'wrong-answer');
                                }
                            });
                        }, 2000);
                    });
                });
                
                questionTable.style.display = 'block';
            }
            
            // Ойын аяқталғанын тексеру
            function checkGameEnd() {
                updateScore();
                if (totalQuestionsAnswered >= totalQuestions) {
                    finalScore.textContent = `Құттықтаймыз! Сіз ${score} ұпай жинадыңыз!`;
                    gameOverScreen.style.display = 'block';
                    createConfetti();
                }
            }
            
            // Жабу батырмасы
            closeBtn.addEventListener('click', function() {
                questionTable.style.display = 'none';
            });
            
            // Қайта бастау батырмасы
            restartBtn.addEventListener('click', function() {
                score = 0;
                asykCount = 0;
                usedQuestions = [];
                totalQuestionsAnswered = 0;
                updateScore();
                gameOverScreen.style.display = 'none';
                document.querySelectorAll('.asyk').forEach(asyk => asyk.remove());
            });
            
            // Ұпайды жаңарту
            function updateScore() {
                scoreDisplay.textContent = `Ұпай: ${score} | Сұрақ: ${totalQuestionsAnswered}/${totalQuestions}`;
            }
            
            // Мобильді құрылғылар үшін сипалау функциясы
            let touchStartX = 0;
            let touchStartY = 0;
            
            gameContainer.addEventListener('touchstart', function(e) {
                touchStartX = e.touches[0].clientX;
                touchStartY = e.touches[0].clientY;
            }, false);
            
            gameContainer.addEventListener('touchend', function(e) {
                const touchEndX = e.changedTouches[0].clientX;
                const touchEndY = e.changedTouches[0].clientY;
                
                const dx = touchEndX - touchStartX;
                const dy = touchEndY - touchStartY;
                
                if (Math.abs(dx) < 10 && Math.abs(dy) < 10) {
                    const element = document.elementFromPoint(touchEndX, touchEndY);
                    if (element && element.classList.contains('asyk')) {
                        element.click();
                    }
                }
            }, false);
        });
    </script>
