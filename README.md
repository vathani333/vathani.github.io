# vathani.github.io
<!DOCTYPE html>
<html>
<head>
<title>Be My Valentine 💘</title>

<style>
body {
    background: linear-gradient(to right, #ff9a9e, #fad0c4);
    font-family: 'Comic Sans MS', cursive;
    text-align: center;
    margin-top: 100px;
    overflow: hidden;
}

.heart {
    position: fixed;
    bottom: -20px;
    font-size: 20px;
    animation: floatUp 5s linear infinite;
    opacity: 0.7;
}

@keyframes floatUp {
    from { transform: translateY(0); }
    to { transform: translateY(-120vh); }
}

h1 {
    font-size: 40px;
    color: #fff;
    margin-bottom: 5px;
}

#tinyText {
    font-size: 12px;
    color: white;
    opacity: 0.7;
    margin-bottom: 30px;
}

button {
    padding: 15px 30px;
    font-size: 20px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    margin: 15px;
    transition: 0.3s ease;
}

#yesBtn {
    background-color: #4CAF50;
    color: white;
}

#noBtn {
    background-color: #ff4d4d;
    color: white;
    position: relative;
}

.confetti {
    position: fixed;
    width: 10px;
    height: 10px;
    top: 0;
    animation: fall 3s linear forwards;
}

@keyframes fall {
    to { transform: translateY(100vh); opacity: 0; }
}
</style>
</head>

<body>

<h1 id="question">Will you be my Valentine? 🤗💖</h1>
<p id="tinyText">(try clicking no until it disappears‼️)</p>

<button id="yesBtn">Yes 😍</button>
<button id="noBtn">No 🙄</button>

<!-- Sound Effects -->
<audio id="sadSound" src="https://www.myinstants.com/media/sounds/vine-boom.mp3"></audio>
<audio id="happySound" src="https://www.myinstants.com/media/sounds/tada-fanfare.mp3"></audio>

<script>
let noBtn = document.getElementById("noBtn");
let yesBtn = document.getElementById("yesBtn");
let question = document.getElementById("question");
let sadSound = document.getElementById("sadSound");
let happySound = document.getElementById("happySound");

let messages = [
    "are you sure? 🤨",
    "think again lovey...",
    "my mom already likes you though 😔",
    "this is literally illegal actually 🚨",
    "please? i’ll share curly fries with you, hun 🍟",
    "you're so mean!!! 🙄",
    "last chance before I start 'crying' dramatically 😒"
];
let i = 0;

// NO button shrinking variables
let noBtnSize = 1; // 1 = 100%
let noShrinkAmount = 0.05; // shrinks 5% each hover

// YES button growing variables
let yesBtnSize = 1;
let yesGrowAmount = 0.1; // grows 10% each hover

// Floating hearts
setInterval(() => {
    let heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerHTML = "💖";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (Math.random() * 20 + 10) + "px";
    document.body.appendChild(heart);
    setTimeout(() => { heart.remove(); }, 5000);
}, 300);

// NO button behavior
noBtn.addEventListener("mouseover", function() {
    sadSound.currentTime = 0;
    sadSound.play();

    // shrink NO button
    noBtnSize -= noShrinkAmount;
    if(noBtnSize < 0.2) noBtnSize = 0.2; // minimum size
    noBtn.style.transform = `scale(${noBtnSize})`;

    // move button randomly
    let maxX = window.innerWidth - noBtn.offsetWidth - 20;
    let maxY = window.innerHeight - noBtn.offsetHeight - 20;
    let x = Math.random() * maxX;
    let y = Math.random() * maxY;
    noBtn.style.position = "absolute";
    noBtn.style.left = x + "px";
    noBtn.style.top = y + "px";

    // change messages
    if(i < messages.length){
        question.innerText = messages[i];
        i++;
    }
});

// YES button growing effect
yesBtn.addEventListener("mouseover", function() {
    yesBtnSize += yesGrowAmount;
    yesBtn.style.transform = `scale(${yesBtnSize})`;
});

// Confetti generator
function createConfetti() {
    for(let i=0; i<120; i++){
        let confetti = document.createElement("div");
        confetti.classList.add("confetti");
        confetti.style.left = Math.random() * 100 + "vw";
        confetti.style.backgroundColor = `hsl(${Math.random()*360}, 100%, 50%)`;
        document.body.appendChild(confetti);
        setTimeout(() => { confetti.remove(); }, 3000);
    }
}

// YES button click
yesBtn.addEventListener("click", function(){
    happySound.play();
    createConfetti();

    setTimeout(() => {
        document.body.innerHTML = `
            <h1>YOU SAID YES 🫦🥂💘</h1>
            <h2>i’m legally obligated to adore you now</h2>
            <p>valentine secured successfully ✅</p>
            <p style="font-size:30px;">💖💖💖</p>
        `;
    }, 800);
});
</script>
</body>
</html>
