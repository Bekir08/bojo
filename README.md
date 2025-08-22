[galavoy.html](https://github.com/user-attachments/files/21942904/galavoy.html)
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gay Testi: Nuri mi, Yusuf mu?</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 90%;
            max-width: 700px;
            padding: 30px;
            text-align: center;
        }
        
        h1 {
            color: #e84393;
            margin-bottom: 20px;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .subtitle {
            color: #6c5ce7;
            margin-bottom: 30px;
            font-size: 1.3rem;
        }
        
        .pride-flag {
            height: 10px;
            background: linear-gradient(to right, red, orange, yellow, green, blue, violet);
            border-radius: 5px;
            margin: 15px 0;
        }
        
        .question-container {
            margin-bottom: 25px;
        }
        
        .question {
            font-size: 1.4rem;
            margin-bottom: 20px;
            color: #fd79a8;
            font-weight: 600;
            background-color: #f8efba;
            padding: 15px;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .option {
            background: linear-gradient(to right, #6c5ce7, #fd79a8);
            color: white;
            border: none;
            border-radius: 50px;
            padding: 15px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        .option:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
        }
        
        .option:active {
            transform: translateY(0);
        }
        
        .option.selected {
            background: linear-gradient(to right, #fd79a8, #e84393);
            transform: scale(1.05);
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        .nav-btn {
            background: linear-gradient(to right, #fd79a8, #e84393);
            color: white;
            border: none;
            border-radius: 50px;
            padding: 12px 25px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .nav-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        .nav-btn:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .progress {
            margin-top: 20px;
            font-size: 1.1rem;
            color: #6c5ce7;
            font-weight: 600;
        }
        
        .result {
            font-size: 1.5rem;
            margin-top: 30px;
            padding: 20px;
            border-radius: 15px;
            background: linear-gradient(135deg, #6c5ce7 0%, #fd79a8 100%);
            color: white;
            display: none;
        }
        
        .rainbow {
            background: linear-gradient(to right, red, orange, yellow, green, blue, indigo, violet);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: bold;
        }
        
        .result-btn {
            background: linear-gradient(to right, #00b894, #55efc4);
            color: white;
            border: none;
            border-radius: 50px;
            padding: 15px 30px;
            font-size: 1.2rem;
            cursor: pointer;
            margin-top: 20px;
            transition: all 0.3s ease;
        }
        
        .result-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
        }
        
        .result-btn:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        @media (max-width: 600px) {
            .options {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>GAY TESTİ</h1>
        <div class="pride-flag"></div>
        <div class="subtitle">Nuri mi, Yusuf mu? Gerçeği öğren!</div>
        
        <div id="quiz-container">
            <div class="question-container">
                <div id="question" class="question"></div>
                <div class="options">
                    <button class="option" id="option1"></button>
                    <button class="option" id="option2"></button>
                </div>
            </div>
            
            <div class="navigation">
                <button id="prev-btn" class="nav-btn">Önceki Soru</button>
                <button id="next-btn" class="nav-btn">Sonraki Soru</button>
            </div>
            
            <div class="progress">
                <span id="current">1</span> / <span id="total">30</span>
            </div>
            
            <button id="result-btn" class="result-btn" disabled>Sonucu Gör</button>
        </div>
        
        <div id="result" class="result"></div>
    </div>

    <script>
        // Sorular ve cevaplar
        const questions = [
            {"question": "Hangisi daha iyi giyinir?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha romantiktir?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi yemek yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi dans eder?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi şarkı söyler?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha yakışıklı?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha komiktir?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi araba kullanır?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi öpüşür?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi flört eder?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi hediye seçer?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi sarılır?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi masaj yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi alışveriş yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi fotoğraf çeker?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi seyahat eder?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi kitap okur?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi film seçer?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi müzik zevkine sahip?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi spor yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi yüzer?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iji dans eder?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi şaka yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi arkadaş canlısı?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi parti verir?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi ev temizler?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iji bahçe işleri yapar?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi hayvan besler?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi çocuklarla ilgilenir?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0},
            {"question": "Hangisi daha iyi aşık olur?", "options": ["Nuri", "Yusuf"], "correctAnswer": 0}
        ];

        let currentQuestion = 0;
        let score = 0;
        let userAnswers = new Array(questions.length).fill(null);

        const questionElement = document.getElementById('question');
        const option1Element = document.getElementById('option1');
        const option2Element = document.getElementById('option2');
        const prevButton = document.getElementById('prev-btn');
        const nextButton = document.getElementById('next-btn');
        const resultButton = document.getElementById('result-btn');
        const currentElement = document.getElementById('current');
        const totalElement = document.getElementById('total');
        const resultElement = document.getElementById('result');
        const quizContainer = document.getElementById('quiz-container');

        // Toplam soru sayısını göster
        totalElement.textContent = questions.length;

        // İlk soruyu yükle
        loadQuestion();

        function loadQuestion() {
            const question = questions[currentQuestion];
            questionElement.textContent = question.question;
            option1Element.textContent = question.options[0];
            option2Element.textContent = question.options[1];
            
            // Seçenekleri sıfırla
            option1Element.classList.remove('selected');
            option2Element.classList.remove('selected');
            
            // Önceki cevabı işaretle
            if (userAnswers[currentQuestion] !== null) {
                if (userAnswers[currentQuestion] === 0) {
                    option1Element.classList.add('selected');
                } else {
                    option2Element.classList.add('selected');
                }
            }
            
            // İlerleme durumunu güncelle
            currentElement.textContent = currentQuestion + 1;
            
            // Gezinme düğmelerini güncelle
            prevButton.disabled = currentQuestion === 0;
            
            if (currentQuestion === questions.length - 1) {
                nextButton.textContent = "Son Soru";
            } else {
                nextButton.textContent = "Sonraki Soru";
            }
            
            // Sonuç butonunu kontrol et
            checkAllAnswered();
        }

        // Seçeneklere tıklama olaylarını ekle
        option1Element.addEventListener('click', function() {
            selectOption(0);
        });

        option2Element.addEventListener('click', function() {
            selectOption(1);
        });

        function selectOption(optionIndex) {
            userAnswers[currentQuestion] = optionIndex;
            
            // Seçimi göster
            option1Element.classList.remove('selected');
            option2Element.classList.remove('selected');
            
            if (optionIndex === 0) {
                option1Element.classList.add('selected');
            } else {
                option2Element.classList.add('selected');
            }
            
            // Puanı güncelle
            const question = questions[currentQuestion];
            if (optionIndex === question.correctAnswer) {
                score++;
            }
            
            // Sonuç butonunu kontrol et
            checkAllAnswered();
        }
        
        function checkAllAnswered() {
            const allAnswered = userAnswers.every(answer => answer !== null);
            resultButton.disabled = !allAnswered;
        }

        // Önceki soru butonu
        prevButton.addEventListener('click', function() {
            if (currentQuestion > 0) {
                currentQuestion--;
                loadQuestion();
            }
        });

        // Sonraki soru butonu
        nextButton.addEventListener('click', function() {
            if (userAnswers[currentQuestion] === null) {
                alert("Lütfen bir cevap seçin!");
                return;
            }
            
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                loadQuestion();
            }
        });
        
        // Sonuç butonu
        resultButton.addEventListener('click', function() {
            showResult();
        });

        function showResult() {
            quizContainer.style.display = 'none';
            resultElement.style.display = 'block';
            
            let resultMessage = "";
            if (score >= 20) {
                resultMessage = `
                    <h2>Tebrikler!</h2>
                    <p>Sen bir <span class="rainbow">Nuri</span> hayranısın!</p>
                    <p>Nuri seninle gurur duyuyor! 🌈</p>
                    <p>Puanın: ${score} / ${questions.length}</p>
                `;
            } else if (score >= 10) {
                resultMessage = `
                    <h2>İlginç!</h2>
                    <p>Hem <span class="rainbow">Nuri</span>'yi hem <span class="rainbow">Yusuf</span>'u seviyorsun!</p>
                    <p>İkisi de seninle çıkmak ister! 💖</p>
                    <p>Puanın: ${score} / ${questions.length}</p>
                `;
            } else {
                resultMessage = `
                    <h2>Vay be!</h2>
                    <p>Sen daha çok bir <span class="rainbow">Yusuf</span> hayranısın!</p>
                    <p>Yusuf seninle çıkmak için can atıyor! 🌠</p>
                    <p>Puanın: ${score} / ${questions.length}</p>
                `;
            }
            
            resultElement.innerHTML = resultMessage;
        }
    </script>
</body>
</html>
