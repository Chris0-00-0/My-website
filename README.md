# Chris0-00-0.github.io
Super cool website

<!DOCTYPE html>
<html>
<head>
    <title>Rules for a New World</title>
    <style>
        body {
            background: #111;
            color: #00ff88;
            font-family: monospace;
            padding: 20px;
            white-space: pre-wrap;
            font-size: 18px;
        }
        #game { margin-top: 20px; }
        button {
            background: #00ff88;
            color: #111;
            border: none;
            padding: 10px 20px;
            margin: 10px 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background: #00cc66;
        }
    </style>
</head>
<body>

<h1>RULES FOR A NEW WORLD</h1>

<div id="output"></div>
<div id="game"></div>

<script>
let moral = 100;
let lose_limit = 50;
const output = document.getElementById("output");
const game = document.getElementById("game");

function log(text) {
    output.innerHTML += text + "\n";
}

function status_check() {
    if (moral <= lose_limit) {
        log("\nYour moral has dropped too low. The citizens start a revolution. You lose the game.");
        game.innerHTML = "";
        return false;
    }
    log("Your country continues forward. Current moral: " + moral + "\n");
    return true;
}

function moral_check() {
    if (moral >= 89) log("Citizens are thrilled\n");
    else if (moral >= 79) log("Citizens are happy\n");
    else if (moral >= 69) log("Citizens are ok\n");
    else if (moral >= 50) log("Citizens are worried\n");
}

function normal_event() {
    let roll = Math.random();
    let split = 0.09;
    let unite = 0.09;

    if (roll < split) {
        let p = Math.floor(Math.random() * 6) + 3;
        log("Citizens are splitting. Moral -" + p);
        moral -= p;
    } else if (roll < split + unite) {
        let b = Math.floor(Math.random() * 6) + 3;
        log("Citizens unite. Moral +" + b);
        moral += b;
    } else {
        log("Citizens calm down. No change.");
    }
}

function choice(promptText, yesFn, noFn) {
    game.innerHTML = `
        <p>${promptText}</p>
        <button onclick="(${yesFn})(); next()">Yes</button>
        <button onclick="(${noFn})(); next()">No</button>
    `;
}

let step = 0;
function next() {
    if (!status_check()) return;
    moral_check();
    step++;

    if (step === 1) democracy();
    if (step === 2) education();
    if (step === 3) terrorism();
    if (step === 4) guns();
    if (step === 5) death_penalty();
    if (step > 5) game.innerHTML = "<h2>You finished the game!</h2>";
}

// ------------------ SCENES ------------------

function democracy() {
    choice(
        "Will your government follow a democracy?",
        () => { log("You choose democracy."); normal_event(); },
        () => { log("You reject democracy. Moral -20"); moral -= 20; }
    );
}

function education() {
    choice(
        "Will you fund education over war/inflation?",
        () => { log("You choose education."); normal_event(); },
        () => { log("You choose war and inflation. Moral -10"); moral -= 10; }
    );
}

function terrorism() {
    log("Will you focus on terrorism over drugs/crime?");
    let drop = Math.floor(Math.random() * 20) + 1;
    moral -= drop;
    log("Citizens are split. Moral -" + drop);
    game.innerHTML = `<button onclick="next()">Continue</button>`;
}

function guns() {
    choice(
        "Will you allow the right to bear arms?",
        () => {
            log("You allow right to bear arms.");
            if (Math.random() < 0.2) {
                let p = Math.floor(Math.random() * 6) + 3;
                log("Citizens split. Moral -" + p);
                moral -= p;
            } else log("Citizens calm down.");
        },
        () => {
            log("You deny right to bear arms.");
            if (Math.random() < 0.2) {
                let b = Math.floor(Math.random() * 6) + 3;
                log("Citizens unite. Moral +" + b);
                moral += b;
            } else log("Citizens divided. No change.");
        }
    );
}

function death_penalty() {
    choice(
        "Are you anti-death penalty?",
        () => { log("You choose anti-death penalty."); normal_event(); },
        () => { log("You support death penalty."); normal_event(); }
    );
}

// Start the intro
log(
"You are a new leader for an up-and-coming country.\n" +
"Your job is to set new rules for citizens.\n" +
"Bad choices lower moral; if moral hits 50 or below, you lose.\n" +
"Citizens may split (- moral) or unite (+ moral).\nGood luck!\n\n"
);

next();
</script>

</body>
</html>

