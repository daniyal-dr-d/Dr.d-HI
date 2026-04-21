# Dr.d-HI
# can you prove to be worthy enough to access our training program let's find out
<script>
    let lives = 2;
    let currentQuestion = 0;

    // YOUR EXAM DATA
    const questions = [
        { q: "12 + 8 ÷ 2 - 3 = ?", options: ["7", "10", "15", "13"], answer: "13" },
        { q: "What is 25% of $40?", options: ["$5", "$10", "$15", "$20"], answer: "$10" },
        { q: "Solve for x: 3x = 18", options: ["3", "6", "9", "15"], answer: "6" },
        { q: "How many faces does a cube have?", options: ["4", "6", "8", "12"], answer: "6" }
    ];

    function loadQuestion() {
        // Reset Dr. D to his happy face at the start of each question
        document.getElementById("dr-d-img").src = "drd_professor.png";
        
        if (lives <= 0) {
            document.getElementById("game-container").innerHTML = "<h1>❌ GAME OVER</h1><p>Dr. D: 'Time for more practice!'</p><button onclick='location.reload()'>Restart Exam</button>";
            return;
        }

        if (currentQuestion >= questions.length) {
            document.getElementById("game-container").innerHTML = "<h1>🏆 MASTER ARCHITECT</h1><p>Business is booming! You passed!</p>";
            return;
        }

        let qData = questions[currentQuestion];
        document.getElementById("question-text").innerText = qData.q;
        const optionsDiv = document.getElementById("options");
        optionsDiv.innerHTML = "";

        qData.options.forEach(opt => {
            let btn = document.createElement("button");
            btn.innerText = opt;
            btn.className = "game-btn"; // You can style this in CSS
            btn.onclick = () => checkAnswer(opt);
            optionsDiv.appendChild(btn);
        });
    }

    function checkAnswer(choice) {
        if (choice === questions[currentQuestion].answer) {
            document.getElementById("message").innerText = "Correct! Dr. D is impressed.";
            currentQuestion++;
            setTimeout(loadQuestion, 1000);
        } else {
            lives--;
            updateLives();
            // TRIGGER REACTION: Switch to the open-mouth image
            document.getElementById("dr-d-img").src = "drd_open_mouth.png";
            document.getElementById("message").innerText = "Ouch! That's a life lost.";
            
            if (lives <= 0) {
                setTimeout(loadQuestion, 1000);
            }
        }
    }

    function updateLives() {
        let icons = "";
        for(let i=0; i<lives; i++) icons += "❤️ ";
        document.getElementById("lives").innerText = icons || "💀";
    }

    loadQuestion();
</script>
