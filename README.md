<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Iron Heroes - Combate la Anemia</title>
    <style>
        body {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #ff6b6b 0%, #4ecdc4 50%, #45b7d1 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .game-container {
            max-width: 800px;
            width: 95%;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            overflow: hidden;
            position: relative;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            margin: 0;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .subtitle {
            margin: 10px 0 0 0;
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .stats-bar {
            display: flex;
            justify-content: space-between;
            padding: 15px 30px;
            background: rgba(102, 126, 234, 0.1);
            border-bottom: 2px solid #667eea;
        }

        .stat {
            text-align: center;
            flex: 1;
        }

        .stat-label {
            font-size: 0.9rem;
            color: #666;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: #667eea;
        }

        .health-bar {
            width: 100%;
            height: 20px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin-top: 5px;
        }

        .health-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff6b6b, #feca57);
            border-radius: 10px;
            transition: width 0.5s ease;
        }

        .game-screen {
            padding: 30px;
            min-height: 400px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .character {
            font-size: 4rem;
            margin-bottom: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        .question-container {
            text-align: center;
            width: 100%;
        }

        .question {
            font-size: 1.3rem;
            color: #333;
            margin-bottom: 30px;
            line-height: 1.6;
            font-weight: 500;
        }

        .answers {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }

        .answer-btn {
            padding: 15px 20px;
            border: none;
            border-radius: 15px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #f8f9fa, #e9ecef);
            color: #333;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            text-align: left;
        }

        .answer-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.2);
            background: linear-gradient(145deg, #667eea, #764ba2);
            color: white;
        }

        .answer-btn.correct {
            background: linear-gradient(145deg, #43e97b, #38f9d7);
            color: white;
            animation: pulse 0.5s;
        }

        .answer-btn.incorrect {
            background: linear-gradient(145deg, #ff6b6b, #ee5a24);
            color: white;
            animation: shake 0.5s;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .feedback {
            margin: 20px 0;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
        }

        .feedback.correct {
            background: rgba(67, 233, 123, 0.2);
            color: #27ae60;
            border: 2px solid #43e97b;
        }

        .feedback.incorrect {
            background: rgba(255, 107, 107, 0.2);
            color: #e74c3c;
            border: 2px solid #ff6b6b;
        }

        .next-btn {
            padding: 12px 30px;
            border: none;
            border-radius: 25px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            background: linear-gradient(145deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }

        .next-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }

        .start-screen, .end-screen {
            text-align: center;
        }

        .start-screen h2, .end-screen h2 {
            color: #333;
            margin-bottom: 20px;
        }

        .start-btn {
            padding: 15px 40px;
            border: none;
            border-radius: 30px;
            font-size: 1.2rem;
            font-weight: bold;
            cursor: pointer;
            background: linear-gradient(145deg, #43e97b, #38f9d7);
            color: white;
            box-shadow: 0 6px 12px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }

        .start-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 16px rgba(0,0,0,0.3);
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
            margin: 20px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #43e97b, #38f9d7);
            border-radius: 4px;
            transition: width 0.5s ease;
        }

        .tips {
            background: rgba(67, 233, 123, 0.1);
            border-left: 4px solid #43e97b;
            padding: 15px;
            margin: 20px 0;
            border-radius: 0 10px 10px 0;
        }

        .tips h4 {
            margin: 0 0 10px 0;
            color: #27ae60;
        }

        @media (max-width: 768px) {
            .answers {
                grid-template-columns: 1fr;
            }
            
            .stats-bar {
                padding: 10px 15px;
            }
            
            .game-screen {
                padding: 20px;
            }
            
            .header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="header">
            <h1>🦸‍♀️ Iron Heroes 🦸‍♂️</h1>
            <p class="subtitle">¡Conviértete en un héroe contra la anemia!</p>
        </div>

        <div class="stats-bar">
            <div class="stat">
                <div class="stat-label">Nivel de Energía</div>
                <div class="health-bar">
                    <div class="health-fill" id="healthBar" style="width: 100%"></div>
                </div>
            </div>
            <div class="stat">
                <div class="stat-label">Puntos</div>
                <div class="stat-value" id="score">0</div>
            </div>
            <div class="stat">
                <div class="stat-label">Pregunta</div>
                <div class="stat-value"><span id="currentQuestion">0</span>/<span id="totalQuestions">10</span></div>
            </div>
        </div>

        <div class="progress-bar">
            <div class="progress-fill" id="progressBar" style="width: 0%"></div>
        </div>

        <div class="game-screen" id="gameScreen">
            <div class="start-screen" id="startScreen">
                <div class="character">🩸💪</div>
                <h2>¡Bienvenido, futuro Iron Hero!</h2>
                <p>La anemia es un enemigo silencioso que afecta a millones de jóvenes. Tu misión es aprender cómo combatirla y mantener tus niveles de hierro altos.</p>
                <div class="tips">
                    <h4>💡 ¿Sabías que...?</h4>
                    <p>La anemia por deficiencia de hierro es la más común en jóvenes de 15-30 años, especialmente en mujeres.</p>
                </div>
                <button class="start-btn" onclick="startGame()">¡Comenzar Aventura!</button>
            </div>
        </div>
    </div>

    <script>
        let gameState = {
            currentQuestion: 0,
            score: 0,
            health: 100,
            questions: [
                {
                    question: "¿Cuál de estos alimentos es la MEJOR fuente de hierro para prevenir anemia?",
                    answers: [
                        "🥩 Carne roja magra",
                        "🥬 Espinacas crudas",
                        "🥛 Leche entera",
                        "🍞 Pan blanco"
                    ],
                    correct: 0,
                    explanation: "¡Correcto! La carne roja contiene hierro hemo, que se absorbe mejor que el hierro de origen vegetal.",
                    tip: "Combina alimentos ricos en hierro con vitamina C para mejorar la absorción."
                },
                {
                    question: "¿Qué síntoma NO es típico de la anemia?",
                    answers: [
                        "😴 Fatiga constante",
                        "💓 Palpitaciones",
                        "🔥 Fiebre alta",
                        "🥶 Manos y pies fríos"
                    ],
                    correct: 2,
                    explanation: "¡Exacto! La fiebre alta no es un síntoma típico de anemia. Los otros síntomas sí son comunes.",
                    tip: "Si sientes fatiga constante, consulta a un médico para descartar anemia."
                },
                {
                    question: "¿Cuál es la mejor combinación para absorber hierro?",
                    answers: [
                        "🥩 Carne + 🥛 Leche",
                        "🍃 Espinacas + 🍊 Naranja",
                        "🍞 Pan + ☕ Café",
                        "🐟 Pescado + 🍵 Té"
                    ],
                    correct: 1,
                    explanation: "¡Perfecto! La vitamina C de la naranja ayuda a absorber el hierro de las espinacas.",
                    tip: "Evita tomar té o café con comidas ricas en hierro, ya que pueden inhibir su absorción."
                },
                {
                    question: "¿Con qué frecuencia deberías hacerte análisis de sangre si sospechas anemia?",
                    answers: [
                        "🗓️ Cada mes",
                        "📅 Cada 6 meses",
                        "🩺 Solo cuando te sientes mal",
                        "📋 Según recomendación médica"
                    ],
                    correct: 3,
                    explanation: "¡Correcto! La frecuencia debe ser determinada por un profesional de la salud según tu caso.",
                    tip: "Un chequeo anual básico puede ayudar a detectar anemia temprano."
                },
                {
                    question: "¿Qué grupo tiene MAYOR riesgo de anemia por deficiencia de hierro?",
                    answers: [
                        "👨 Hombres deportistas",
                        "👩 Mujeres en edad fértil",
                        "👴 Adultos mayores",
                        "👶 Niños pequeños"
                    ],
                    correct: 1,
                    explanation: "¡Exacto! Las mujeres en edad fértil tienen mayor riesgo debido a la menstruación.",
                    tip: "Las mujeres con períodos abundantes deben prestar especial atención a su consumo de hierro."
                },
                {
                    question: "¿Cuál de estos hábitos EMPEORA la absorción de hierro?",
                    answers: [
                        "🏃‍♀️ Hacer ejercicio",
                        "☕ Tomar café con las comidas",
                        "💧 Beber mucha agua",
                        "😴 Dormir 8 horas"
                    ],
                    correct: 1,
                    explanation: "¡Correcto! El café y el té contienen taninos que reducen la absorción de hierro.",
                    tip: "Espera al menos 1 hora después de comer para tomar café o té."
                },
                {
                    question: "¿Cuál es una excelente fuente de hierro para vegetarianos?",
                    answers: [
                        "🥗 Lechuga iceberg",
                        "🫘 Lentejas",
                        "🧀 Queso",
                        "🍌 Plátano"
                    ],
                    correct: 1,
                    explanation: "¡Perfecto! Las lentejas son ricas en hierro y proteínas, ideales para vegetarianos.",
                    tip: "Combina legumbres con alimentos ricos en vitamina C para maximizar la absorción de hierro."
                },
                {
                    question: "¿Qué vitamina ayuda a absorber mejor el hierro?",
                    answers: [
                        "🌞 Vitamina D",
                        "🍊 Vitamina C",
                        "🥑 Vitamina E",
                        "🥕 Vitamina A"
                    ],
                    correct: 1,
                    explanation: "¡Excelente! La vitamina C es clave para mejorar la absorción del hierro no hemo.",
                    tip: "Agrega limón, naranja o pimientos a tus comidas ricas en hierro."
                },
                {
                    question: "¿Cuál es el primer paso si sospechas que tienes anemia?",
                    answers: [
                        "💊 Tomar suplementos de hierro",
                        "🩺 Consultar a un médico",
                        "🥩 Comer más carne",
                        "⏰ Esperar a que mejore solo"
                    ],
                    correct: 1,
                    explanation: "¡Correcto! Siempre consulta a un profesional antes de autodiagnosticarte o automedicarte.",
                    tip: "Un análisis de sangre simple puede confirmar si tienes anemia y qué tipo."
                },
                {
                    question: "¿Cuál es el beneficio de cocinar en sartenes de hierro fundido?",
                    answers: [
                        "🍳 Solo mejora el sabor",
                        "⚡ Cocina más rápido",
                        "🔧 Añade hierro a los alimentos",
                        "🧽 Es más fácil de limpiar"
                    ],
                    correct: 2,
                    explanation: "¡Genial! Cocinar en hierro fundido puede aumentar el contenido de hierro en los alimentos.",
                    tip: "Especialmente efectivo con alimentos ácidos como salsa de tomate."
                }
            ]
        };

        function startGame() {
            document.getElementById('startScreen').style.display = 'none';
            gameState.currentQuestion = 0;
            gameState.score = 0;
            gameState.health = 100;
            updateStats();
            showQuestion();
        }

        function showQuestion() {
            const question = gameState.questions[gameState.currentQuestion];
            const character = getCharacterForHealth();
            
            document.getElementById('gameScreen').innerHTML = `
                <div class="question-container">
                    <div class="character">${character}</div>
                    <div class="question">${question.question}</div>
                    <div class="answers" id="answers">
                        ${question.answers.map((answer, index) => 
                            `<button class="answer-btn" onclick="selectAnswer(${index})">${answer}</button>`
                        ).join('')}
                    </div>
                </div>
            `;
            
            updateStats();
        }

        function selectAnswer(selectedIndex) {
            const question = gameState.questions[gameState.currentQuestion];
            const answerButtons = document.querySelectorAll('.answer-btn');
            
            // Deshabilitar todos los botones
            answerButtons.forEach(btn => btn.style.pointerEvents = 'none');
            
            // Marcar respuesta correcta e incorrecta
            answerButtons[question.correct].classList.add('correct');
            if (selectedIndex !== question.correct) {
                answerButtons[selectedIndex].classList.add('incorrect');
                gameState.health = Math.max(0, gameState.health - 10);
            } else {
                gameState.score += 100;
            }
            
            // Mostrar feedback
            setTimeout(() => {
                showFeedback(selectedIndex === question.correct, question);
            }, 1000);
            
            updateStats();
        }

        function showFeedback(isCorrect, question) {
            const feedbackClass = isCorrect ? 'correct' : 'incorrect';
            const emoji = isCorrect ? '🎉' : '💪';
            
            document.getElementById('gameScreen').innerHTML += `
                <div class="feedback ${feedbackClass}">
                    <div>${emoji} ${question.explanation}</div>
                    <div class="tips">
                        <h4>💡 Consejo Iron Hero:</h4>
                        <p>${question.tip}</p>
                    </div>
                </div>
                <button class="next-btn" onclick="nextQuestion()">
                    ${gameState.currentQuestion < gameState.questions.length - 1 ? 'Siguiente Desafío' : 'Ver Resultados'}
                </button>
            `;
        }

        function nextQuestion() {
            gameState.currentQuestion++;
            
            if (gameState.currentQuestion >= gameState.questions.length) {
                showEndScreen();
            } else {
                showQuestion();
            }
        }

        function showEndScreen() {
            const percentage = (gameState.score / (gameState.questions.length * 100)) * 100;
            let rank, message, character;
            
            if (percentage >= 90) {
                rank = "🏆 Iron Hero Legendario";
                message = "¡Increíble! Eres un verdadero experto en prevención de anemia.";
                character = "🦸‍♀️💪";
            } else if (percentage >= 70) {
                rank = "🥇 Iron Hero Avanzado";
                message = "¡Excelente! Tienes muy buenos conocimientos sobre anemia.";
                character = "🦸‍♂️⚡";
            } else if (percentage >= 50) {
                rank = "🥈 Iron Hero en Entrenamiento";
                message = "¡Bien! Sigues aprendiendo, continúa así.";
                character = "💪🔥";
            } else {
                rank = "🥉 Futuro Iron Hero";
                message = "¡No te rindas! Cada héroe empezó desde abajo.";
                character = "🌟💫";
            }
            
            document.getElementById('gameScreen').innerHTML = `
                <div class="end-screen">
                    <div class="character">${character}</div>
                    <h2>${rank}</h2>
                    <p>${message}</p>
                    <div class="tips">
                        <h4>📊 Tus Resultados:</h4>
                        <p>Puntuación: ${gameState.score} puntos</p>
                        <p>Precisión: ${percentage.toFixed(1)}%</p>
                        <p>Energía restante: ${gameState.health}%</p>
                    </div>
                    <div class="tips">
                        <h4>🎯 Recuerda siempre:</h4>
                        <p>• Consume alimentos ricos en hierro regularmente</p>
                        <p>• Combina hierro con vitamina C</p>
                        <p>• Consulta a un médico si tienes síntomas</p>
                        <p>• Mantén chequeos médicos regulares</p>
                    </div>
                    <button class="start-btn" onclick="location.reload()">¡Jugar de Nuevo!</button>
                </div>
            `;
        }

        function updateStats() {
            document.getElementById('score').textContent = gameState.score;
            document.getElementById('currentQuestion').textContent = gameState.currentQuestion + 1;
            document.getElementById('totalQuestions').textContent = gameState.questions.length;
            document.getElementById('healthBar').style.width = gameState.health + '%';
            
            const progress = ((gameState.currentQuestion) / gameState.questions.length) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function getCharacterForHealth() {
            if (gameState.health >= 80) return '🦸‍♀️💪';
            if (gameState.health >= 60) return '😊⚡';
            if (gameState.health >= 40) return '😐🔋';
            if (gameState.health >= 20) return '😰⚠️';
            return '😵💔';
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'987fb6eb46d1b4e3',t:'MTc1OTM2MTA3Ny4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
