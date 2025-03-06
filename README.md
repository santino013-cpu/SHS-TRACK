<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Career Finder</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            text-align: center;
        }
        .header {
            width: 90.1%;
            padding: 20px;
            background: green;
            color: white;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
        }
        .container {
            background: white;
            padding: 27px;
            border-radius: 20px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 85.9%;
            max-width: 700px;
            margin: 30px auto;
        }
        select, input, button {
            width: 90%;
            padding: 11px;
            margin: 16px 0;
            border: 1px solid #ccc;
            border-radius: 11px;
        }
        .hidden {
            display: none;
        }
        .footer {
            background-color: #2E7D32;
            color: white;
            padding: 14px;
            font-size: 12px;
            position: absolute;
            bottom: 0;
            width: 93.2%;
        }
    </style>
</head>
<body>

<div class="header">CAREER FINDER</div>

<div class="container" id="loginForm">
    <h2>Login</h2>
    <input type="text" id="name" placeholder="Enter your name" required>
    <input type="text" id="school" placeholder="Enter your school" required>
    <button onclick="enterWebsite()">Enter</button>
</div>

<div class="container hidden" id="quizContainer">
    <h2>Answer the quiz</h2>
    <form id="quizForm">
        <div id="questions"></div>
        <button type="button" onclick="submitQuiz()">Submit</button>
    </form>
</div>

<div class="container hidden" id="resultContainer">
    <h2>Recommended SHS Strand</h2>
    <p id="result"></p>
    <h3>Search for Courses</h3>
    <input type="text" id="searchStrand" placeholder="Enter a strand (e.g., STEM)" oninput="searchCourses()">
    <ul id="courseResults"></ul>
    <button onclick="restart()">Restart</button>
</div>

<div class="footer" id="footer">
    Made by Clyde Acobo, Mark Matias, Marielle Navarro, Santino Marquez, Christine Villanueva, Judy Ann Bisen
</div>

<script>
    const quizData = [
        { question: "Do you enjoy solving math problems?", strand: "STEM" },
        { question: "Are you interested in running a business?", strand: "ABM" },
        { question: "Do you like writing essays and analyzing literature?", strand: "HUMSS" },
        { question: "Do you enjoy working with your hands (e.g., fixing things, cooking)?", strand: "TVL" },
        { question: "Do you like learning about different subjects instead of focusing on one?", strand: "GAS" },
        { question: "Do you want to pursue a career in engineering or medicine?", strand: "STEM" },
        { question: "Are you good at public speaking and debate?", strand: "HUMSS" },
        { question: "Do you enjoy working with computers and technology?", strand: "STEM" },
        { question: "Are you interested in marketing and advertising?", strand: "ABM" },
        { question: "Would you enjoy teaching or social work?", strand: "HUMSS" },
        { question: "Do you prefer learning through hands-on experience rather than theory?", strand: "TVL" },
        { question: "Are you interested in hospitality and tourism management?", strand: "ABM" },
        { question: "Do you like designing and crafting?", strand: "TVL" },
        { question: "Do you enjoy general knowledge and discussions about various topics?", strand: "GAS" },
        { question: "Would you prefer a job that involves numbers and analysis?", strand: "STEM" },
        { question: "Do you want to run your own company someday?", strand: "ABM" },
        { question: "Are you passionate about history and politics?", strand: "HUMSS" },
        { question: "Do you like working with electrical or mechanical tools?", strand: "TVL" },
        { question: "Are you interested in pursuing multiple academic disciplines?", strand: "GAS" },
        { question: "Do you like helping others understand difficult concepts?", strand: "HUMSS" }
    ];

    const courseList = {
        "STEM": ["Engineering", "Computer Science", "Medicine", "Mathematics", "Biology"],
        "ABM": ["Business Administration", "Marketing", "Accountancy", "Entrepreneurship"],
        "HUMSS": ["Political Science", "Psychology", "Communication", "Education"],
        "TVL": ["Culinary Arts", "Electrical Technology", "Automotive Technology", "IT"],
        "GAS": ["Liberal Arts", "Education", "General Studies"]
    };

    function enterWebsite() {
        let name = document.getElementById("name").value;
        let school = document.getElementById("school").value;

        if (name === "" || school === "") {
            alert("Please enter your name and school.");
            return;
        }

        document.getElementById("loginForm").classList.add("hidden");
        document.getElementById("quizContainer").classList.remove("hidden");
        document.getElementById("footer").style.display = "none";
        loadQuiz();
    }

    function loadQuiz() {
        const questionsDiv = document.getElementById("questions");
        questionsDiv.innerHTML = "";
        quizData.forEach((q, index) => {
            questionsDiv.innerHTML += `
                <p>${index + 1}. ${q.question}</p>
                <label><input type="radio" name="q${index}" value="${q.strand}"> Yes</label>
                <label><input type="radio" name="q${index}" value="none"> No</label>
                <br><br>
            `;
        });
    }

    function submitQuiz() {
        let scores = { STEM: 0, ABM: 0, HUMSS: 0, TVL: 0, GAS: 0 };
        quizData.forEach((q, index) => {
            let answer = document.querySelector(`input[name="q${index}"]:checked`);
            if (answer && answer.value !== "none") {
                scores[answer.value]++;
            }
        });

        let recommendedStrand = Object.keys(scores).reduce((a, b) => (scores[a] > scores[b] ? a : b));
        document.getElementById("result").innerHTML = `Based on your answers, your recommended SHS strand is <b>${recommendedStrand}</b>.`;
        document.getElementById("quizContainer").classList.add("hidden");
        document.getElementById("resultContainer").classList.remove("hidden");
    }

    function searchCourses() {
        let input = document.getElementById("searchStrand").value.toUpperCase();
        let results = courseList[input] || [];
        document.getElementById("courseResults").innerHTML = results.map(course => `<li>${course}</li>`).join("");
    }

    function restart() {
        location.reload();
    }
</script>

</body>
</html>
