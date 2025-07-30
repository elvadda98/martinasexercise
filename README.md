<!DOCTYPE html>
<html>
<head>
    <title>Business Vocabulary Challenge</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f9fc;
            line-height: 1.6;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 10px;
        }
        .word-bank {
            background-color: #e8f4f8;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
        .word-bank span {
            display: inline-block;
            background-color: #3498db;
            color: white;
            padding: 6px 12px;
            margin: 5px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
        }
        .sentence {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            position: relative;
        }
        input {
            padding: 10px;
            border: 2px solid #3498db;
            border-radius: 6px;
            width: 150px;
            font-size: 16px;
            margin: 0 5px;
        }
        .check-btn {
            background-color: #2ecc71;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 6px;
            cursor: pointer;
            margin-left: 10px;
            font-weight: bold;
            transition: all 0.3s;
        }
        .check-btn:hover {
            background-color: #27ae60;
            transform: translateY(-2px);
        }
        .hint-btn {
            background-color: #f39c12;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 6px;
            cursor: pointer;
            margin-left: 10px;
            font-weight: bold;
            transition: all 0.3s;
        }
        .hint-btn:hover {
            background-color: #e67e22;
            transform: translateY(-2px);
        }
        .feedback {
            margin-top: 12px;
            padding: 10px;
            border-radius: 6px;
            display: none;
            font-size: 15px;
        }
        .correct {
            background-color: #e8f8f5;
            color: #27ae60;
            border-left: 4px solid #2ecc71;
        }
        .incorrect {
            background-color: #fdedec;
            color: #e74c3c;
            border-left: 4px solid #e74c3c;
        }
        #score {
            text-align: center;
            font-size: 20px;
            margin: 25px 0;
            font-weight: bold;
            color: #2c3e50;
        }
        #restart {
            display: block;
            margin: 30px auto;
            padding: 12px 25px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s;
        }
        #restart:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        .hint-text {
            color: #7f8c8d;
            font-size: 14px;
            margin-top: 8px;
            padding: 8px;
            background-color: #f8f9fa;
            border-radius: 4px;
            display: none;
        }
        .correct-answer {
            font-weight: bold;
            color: #27ae60;
        }
        .progress-container {
            width: 100%;
            background-color: #e0e0e0;
            border-radius: 10px;
            margin: 20px 0;
        }
        .progress-bar {
            height: 10px;
            background-color: #2ecc71;
            border-radius: 10px;
            width: 0%;
            transition: width 0.5s;
        }
    </style>
</head>
<body>
    <h1>📊 Business Vocabulary Challenge</h1>
    
    <div class="word-bank">
        <h3>Word Bank:</h3>
        <span>depending on</span>
        <span>headquarters</span>
        <span>overcome</span>
        <span>main</span>
        <span>convenient</span>
        <span>write down</span>
        <span>meet up</span>
        <span>topic</span>
        <span>come up with</span>
        <span>kick off</span>
    </div>
    
    <div id="score">Score: 0/15</div>
    <div class="progress-container">
        <div class="progress-bar" id="progress"></div>
    </div>
    
    <div id="sentences-container">
        <!-- Sentences will be added by JavaScript -->
    </div>
    
    <button id="restart">Restart Game</button>

    <script>
        // Vocabulary words and sentences
        const wordBank = [
            "depending on", "headquarters", "overcome", "main", "convenient",
            "write down", "meet up", "topic", "come up with", "kick off"
        ];
        
        const sentences = [
            { text: "We'll ______ the meeting at 9 AM sharp tomorrow morning.", answer: "kick off", hint: "Means 'start' (especially an event)" },
            { text: "The company's ______ are located in New York City.", answer: "headquarters", hint: "Main office of a company" },
            { text: "Please ______ your ideas so we don't forget them.", answer: "write down", hint: "Put on paper" },
            { text: "Let's ______ after work to discuss the project.", answer: "meet up", hint: "Get together" },
            { text: "The ______ reason for our success is our great team.", answer: "main", hint: "Most important" },
            { text: "We need to ______ these technical difficulties before launch.", answer: "overcome", hint: "Solve a problem" },
            { text: "Is 2 PM a ______ time for our appointment?", answer: "convenient", hint: "Suitable or easy" },
            { text: "The ______ for today's discussion is workplace safety.", answer: "topic", hint: "Subject of discussion" },
            { text: "Can you ______ a better solution to this problem?", answer: "come up with", hint: "Invent or suggest" },
            { text: "Our decision will be ______ the results of the survey.", answer: "depending on", hint: "Determined by" },
            { text: "The team worked hard to ______ all obstacles.", answer: "overcome", hint: "Deal with successfully" },
            { text: "The ______ entrance is on the south side of the building.", answer: "main", hint: "Primary or most important" },
            { text: "We'll ______ at the coffee shop near the office.", answer: "meet up", hint: "Gather together" },
            { text: "The conference will ______ with a keynote speech.", answer: "kick off", hint: "Begin officially" },
            { text: "This location is ______ for all team members.", answer: "convenient", hint: "Easy to access" }
        ];

        let score = 0;
        
        // Initialize the game
        function initGame() {
            score = 0;
            document.getElementById("score").textContent = "Score: 0/15";
            document.getElementById("progress").style.width = "0%";
            const container = document.getElementById("sentences-container");
            container.innerHTML = "";
            
            // Create sentence elements
            sentences.forEach((sentence, index) => {
                const sentenceDiv = document.createElement("div");
                sentenceDiv.className = "sentence";
                
                const parts = sentence.text.split("______");
                
                sentenceDiv.innerHTML = `
                    <p>${index + 1}. ${parts[0]}<input type="text" id="answer-${index}" data-answer="${sentence.answer.toLowerCase()}">${parts[1]}</p>
                    <button class="check-btn" onclick="checkAnswer(${index})">Check Answer</button>
                    <button class="hint-btn" onclick="showHint(${index})">Get Hint</button>
                    <div class="hint-text" id="hint-${index}">💡 ${sentence.hint}</div>
                    <div class="feedback" id="feedback-${index}"></div>
                `;
                
                container.appendChild(sentenceDiv);
            });
        }
        
        // Show hint
        function showHint(index) {
            const hint = document.getElementById(`hint-${index}`);
            hint.style.display = "block";
        }
        
        // Check answer
        function checkAnswer(index) {
            const input = document.getElementById(`answer-${index}`);
            const feedback = document.getElementById(`feedback-${index}`);
            const userAnswer = input.value.trim().toLowerCase();
            const correctAnswer = input.dataset.answer;
            
            if (userAnswer === correctAnswer) {
                feedback.innerHTML = "✓ <span class='correct-answer'>Correct!</span> Well done!";
                feedback.className = "feedback correct";
                feedback.style.display = "block";
                input.style.borderColor = "#2ecc71";
                score++;
                updateScore();
            } else {
                feedback.innerHTML = `✗ <span class='correct-answer'>Answer: ${correctAnswer}</span> - Try again!`;
                feedback.className = "feedback incorrect";
                feedback.style.display = "block";
                input.style.borderColor = "#e74c3c";
            }
        }
        
        // Update score and progress
        function updateScore() {
            document.getElementById("score").textContent = `Score: ${score}/15`;
            const progress = (score / 15) * 100;
            document.getElementById("progress").style.width = `${progress}%`;
            
            if (score === 15) {
                document.getElementById("score").innerHTML += " 🎉 Perfect!";
            }
        }
        
        // Restart game
        document.getElementById("restart").onclick = initGame;
        
        // Start the game
        initGame();
    </script>
</body>
</html>
