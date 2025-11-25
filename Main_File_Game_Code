# You Can't Eat Cats Kevin


<!DOCTYPE html>
<html>
<head>
    <title>RULES FOR A NEW WORLD</title>
    <style>
        body {
            background-color: #ffffff; /* white background */
            color: #000000; /* black text */
            font-family: monospace;
            padding: 20px;
            font-size: 18px;
            line-height: 1.6;
        }
        #text {
            max-height: 70vh;
            overflow-y: auto;
            border: 1px solid #ccc;
            padding: 15px;
            margin-bottom: 20px;
            background-color: #ffffff;
        }
        button {
            margin: 6px 6px 6px 0;
            padding: 10px 20px;
            background-color: #add8e6; /* light blue */
            color: #000000; /* black text */
            border: 1px solid #87ceeb;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #87ceeb;
        }
    </style>
</head>
<body>

<div id="text"></div>
<div id="buttons"></div>

<script>
let moral = 100;
let lose_limit = 50;

const textEl = document.getElementById("text");
const buttonsEl = document.getElementById("buttons");

function log(msg) {
    textEl.innerHTML += msg + "<br>";
    textEl.scrollTop = textEl.scrollHeight; // auto-scroll
}

function showButtons(options) {
    buttonsEl.innerHTML = "";
    options.forEach(opt => {
        const btn = document.createElement("button");
        btn.textContent = opt.label;
        btn.onclick = opt.action;
        buttonsEl.appendChild(btn);
    });
}

function status_check() {
    if (moral <= lose_limit) {
        log("Your moral has dropped too low. The citizens start a revolution. You lose the game.");
        buttonsEl.innerHTML = "";
        return false;
    } else {
        log("Your country continues forward. Current moral: " + moral + "<br>");
        return true;
    }
}

function moral_check() {
    if (moral >= 89) log("Citizens are thrilled<br>");
    else if (moral >= 79) log("Citizens are happy<br>");
    else if (moral >= 69) log("Citizens are ok<br>");
    else if (moral >= 50) log("Citizens are worried<br>");
}

function normal_event() {
    let roll = Math.random();
    let split_chance = 0.09;
    let unite_chance = 0.09;

    if (roll < split_chance) {
        log("Citizens are splitting. This will hurt moral.");
        let penalty = Math.floor(Math.random() * 6) + 3;
        moral -= penalty;
        log("Moral dropped by " + penalty);
    }
    else if (roll < split_chance + unite_chance) {
        log("Citizens unite. This improves moral.");
        let bonus = Math.floor(Math.random() * 6) + 3;
        moral += bonus;
        log("Moral increased by " + bonus);
    }
    else {
        log("Citizens calm down. Moral remains the same.");
    }
}

// -------------------- Choices --------------------

function choice1() {
    showButtons([
        {label: "yes", action: () => {
            log("You choose to follow democracy.");
            normal_event();
            log("Moral: " + moral);
            next();
        }},
        {label: "no", action: () => {
            log("You choose not to follow democracy.");
            log("Moral -20");
            moral -= 20;
            log("Moral: " + moral);
            next();
        }}
    ]);
}

function choice2() {
    showButtons([
        {label: "yes", action: () => {
            log("You choose education.");
            normal_event();
            log("Moral: " + moral);
            next();
        }},
        {label: "no", action: () => {
            log("You choose war and inflation focus.");
            log("Moral -10");
            moral -= 10;
            log("Moral: " + moral);
            next();
        }}
    ]);
}

function choice3() {
    log("Will you focus on terrorism over drugs/crime? (yes or no):");
    showButtons([
        {label: "yes", action: () => {
            let change = -1 * (Math.floor(Math.random() * 20) + 1);
            moral += change;
            log("Citizens are split. This will hurt moral.");
            log("Moral dropped by " + Math.abs(change));
            log("Moral: " + moral);
            next();
        }},
        {label: "no", action: () => {
            let change = -1 * (Math.floor(Math.random() * 20) + 1);
            moral += change;
            log("Citizens are split. This will hurt moral.");
            log("Moral dropped by " + Math.abs(change));
            log("Moral: " + moral);
            next();
        }}
    ]);
}

function choice4() {
    showButtons([
        {label: "yes", action: () => {
            log("You allow the right to bear arms.");
            if (Math.random() < 0.2) {
                let penalty = Math.floor(Math.random() * 6) + 3;
                log("Citizens are splitting. This will hurt moral.");
                moral -= penalty;
                log("Moral dropped by " + penalty);
            } else {
                log("Citizens calmed down. Moral remains the same.");
            }
            log("Moral: " + moral);
            next();
        }},
        {label: "no", action: () => {
            log("You deny the right to bear arms.");
            if (Math.random() < 0.2) {
                let bonus = Math.floor(Math.random() * 6) + 3;
                log("Citizens unite. This improves moral.");
                moral += bonus;
                log("Moral increased by " + bonus);
            } else {
                log("Citizens are divided. No major change in moral.");
            }
            log("Moral: " + moral);
            next();
        }}
    ]);
}

function choice5() {
    showButtons([
        {label: "anti-death penalty", action: () => {
            log("You choose to be Anti-death penalty.");
            normal_event();
            log("Moral: " + moral);
            next();
        }},
        {label: "for death penalty", action: () => {
            log("You choose to support the death penalty.");
            normal_event();
            log("Moral: " + moral);
            next();
        }}
    ]);
}

// -------------------- Game Flow --------------------

let step = 0;
function next() {
    if (!status_check()) return;
    moral_check();
    step++;
    if (step === 1) choice1();
    if (step === 2) choice2();
    if (step === 3) choice3();
    if (step === 4) choice4();
    if (step === 5) choice5();
    if (step > 5) {
        log("You have finished the game!");
        buttonsEl.innerHTML = "";
    }
}

// -------------------- Start Game --------------------

log("RULES FOR A NEW WORLD\n");
log(
    "You are a new leader for a new and up and coming country." +
    " Your job is to set new rules for citizens of your country." +
    " As you set up these new rules and laws citizens will react to these choices." +
    " If they do not like the choices you are making the citizens will lose moral." +
    " You start off with 100 moral if you get to 50 moral or lower you lose the game and the citizens will start a revolution." +
    " Citizens have a chance to split which will hurt moral." +
    " Good luck!\n\n"
);

next();
</script>

</body>
</html>
