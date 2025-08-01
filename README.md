// Learn with Fun - JavaScript Version // This version uses HTML + CSS + JS (no frameworks)

const app = document.getElementById("app"); let username = ""; let score = 0; let qIndex = 0; let currentTopic = ""; let questions = [];

const QUESTIONS = { Rocket: [ ["What helps rockets fly?", "Fuel", ["Water", "Fuel", "Air", "Rocks"]], ["Where do rockets go?", "Space", ["Jungle", "Sky", "Ocean", "Space"]], ["What shape is a rocket?", "Tall and pointy", ["Flat", "Round", "Tall and pointy", "Square"]], ["Who rides rockets?", "Astronauts", ["Pilots", "Doctors", "Astronauts", "Teachers"]], ["What color can rockets be?", "Any color", ["Only red", "Only white", "Any color", "Only blue"]] ], Animal: [ ["Which animal roars?", "Lion", ["Dog", "Cat", "Lion", "Cow"]], ["Which is the biggest animal?", "Elephant", ["Dog", "Cow", "Cat", "Elephant"]], ["Which animal can fly?", "Bird", ["Tiger", "Fish", "Bird", "Snake"]], ["Which animal lives in water?", "Fish", ["Goat", "Bird", "Dog", "Fish"]], ["What does a dog say?", "Woof", ["Meow", "Woof", "Moo", "Quack"]] ], Plants: [ ["What do plants need to grow?", "Sunlight", ["Milk", "Juice", "Sunlight", "Ice"]], ["Which part is green?", "Leaf", ["Root", "Leaf", "Fruit", "Stem"]], ["What gives us oxygen?", "Plants", ["Cars", "TV", "Plants", "Phone"]], ["What grows underground?", "Roots", ["Leaves", "Flowers", "Roots", "Branches"]], ["What is a flower?", "Plant", ["Animal", "Toy", "Plant", "Car"]] ], Maths: [ ["2 + 2 = ?", "4", ["2", "4", "6", "8"]], ["5 - 3 = ?", "2", ["1", "2", "3", "4"]], ["What comes after 7?", "8", ["6", "8", "9", "10"]], ["10 - 5 = ?", "5", ["4", "5", "6", "7"]], ["3 + 1 = ?", "4", ["3", "4", "5", "6"]] ] };

function showLogin() { app.innerHTML = <h2>Welcome to Learn with Fun!</h2> <input id="username" placeholder="Enter your name" /> <button onclick="startApp()">Start</button>; }

function startApp() { username = document.getElementById("username").value; if (!username) return alert("Please enter your name!"); showTopics(); }

function showTopics() { app.innerHTML = <h2>Hello ${username}!</h2><h3>Pick a topic:</h3>; for (let topic in QUESTIONS) { const btn = document.createElement("button"); btn.textContent = topic; btn.onclick = () => startQuiz(topic); app.appendChild(btn); } }

function startQuiz(topic) { currentTopic = topic; questions = shuffleArray([...QUESTIONS[topic]]).slice(0, 5); qIndex = 0; score = 0; showQuestion(); }

function showQuestion() { const [qText, correct, options] = questions[qIndex]; app.innerHTML = <h3>Question ${qIndex + 1}/5</h3><p>${qText}</p>; shuffleArray(options).forEach(opt => { const btn = document.createElement("button"); btn.textContent = opt; btn.onclick = () => checkAnswer(opt, correct); app.appendChild(btn); }); }

function checkAnswer(selected, correct) { if (selected === correct) score++; qIndex++; if (qIndex < 5) { showQuestion(); } else { showResult(); } }

function showResult() { app.innerHTML = <h2>Great job, ${username}!</h2> <p>Your score in ${currentTopic}: ${score}/5</p> <button onclick="showTopics()">Play Again</button> <button onclick="showLogin()">Exit</button>; }

function shuffleArray(array) { for (let i = array.length - 1; i > 0; i--) { const j = Math.floor(Math.random() * (i + 1)); [array[i], array[j]] = [array[j], array[i]]; } return array; }

// Start app showLogin();
