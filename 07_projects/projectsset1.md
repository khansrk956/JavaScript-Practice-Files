# Projects related to DOM

## Project Link

[click here ] (put here your project link.)

# Solumtion code

# Project 1

```JavaScript
const buttons = document.querySelectorAll(".button")
const body = document.querySelector("body")

// every button pass through for each loop
buttons.forEach(function (button){
    console.log(button);
    button.addEventListener('click',function (e) {
        console.log(e);
        console.log(e.target)
        if(e.target.id === 'grey'){
            body.style.background = e.target.id
        }
        if(e.target.id === 'white'){
            body.style.background = e.target.id
        }
        if(e.target.id === 'blue'){
            body.style.background = e.target.id
        }
        if(e.target.id === 'yellow'){
            body.style.background = e.target.id
        }

    })
})
```

# BMI
# Project-2
```JavaScript
const form = document.querySelector("form");


form.addEventListener("submit", function (e) {
  e.preventDefault(); // hold the default action. do not perform any action unill I don't do. exp(submit form)

  const height = parseInt(document.querySelector("#height").value); // get the value in string convert into integer
  const weight = parseInt(document.querySelector("#weight").value); // same

  const results = document.querySelector("#results");
  if (height === "" || height < 0 || isNaN(height)) {
    results.innerHTML = "Please give valid height.";
  } else if (weight === "" || weight < 0 || isNaN(weight)) {
    results.innerHTML = "Please give a valid weight";
  }else{
    const bmi = (weight / ((height * height) / 10000)).toFixed(2);
    // show the result
   // Determine BMI category
    let category;
    if (bmi < 18.6) {
        category = "Underweight";
    } else if (bmi >= 18.6 && bmi < 24.9) {
        category = "Normal weight";
    } else {
        category = "Overweight";
    }
    
    // Display BMI and category
    results.innerHTML = `<span>BMI: ${bmi}</span><br><span>Category: ${category}</span>`;
    }  
});

```

# Digital-clock
# Project-3 solution 

```JavaScript
const clock = document.getElementById("clock");
// const clock = document.querySelector("#clock");


// run every second run continuously
setInterval(function () {

    let date = new Date();
    //   console.log(date.toLocaleTimeString());
    clock.innerHTML = date.toLocaleTimeString();
 
}, 1000);

```

# Random Number
# Project -4 
```JavaScript
let randomNumber = parseInt(Math.random() * 100 + 1)
// console.log(randomNumber)

const submitButton = document.querySelector('#subt');
const userInput = document.querySelector('#guessField');
const guessSlot = document.querySelector('.guesses');
const remainingResult = document.querySelector('.lastResult');
const lowHigh = document.querySelector('.lowOrHi');
const startOver = document.querySelector('.resultParas');

const p = document.createElement('p');

let prevGuess = []
let numGuess = 1
let playGame = true

if(playGame){
    submitButton.addEventListener('click', function(e){
        e.preventDefault()  // hold the values untill I want.
        const guess = parseInt(userInput.value)
        console.log(guess)
        validateGuess(guess)  // number from user input
    })
}

function validateGuess(guess){
    // valid the given input.
    if(isNaN(guess)){
        alert("Please enter a valid number")
    }else if(guess < 1){
        alert("Please enter a number more than 1.")
    }else if(guess > 100){
        alert("Please enter a number less than 100. ")
    }else{
        prevGuess.push(guess)
        if(numGuess === 11){
            displayGuess(guess)
            displayMessage(`Game Over. Random number was ${randomNumber}`)
            endGame()
        }else{
            displayGuess(guess)
            checkGuess(guess)
        }
    }
}

function checkGuess(guess){
    // check the guesses.
    if(guess === randomNumber){
        displayMessage(`You gussed it right number`)
        endGame()
    }else if(guess < randomNumber){
        displayMessage(`Number is Tooo low`)
    }else if(guess > randomNumber){
        displayMessage(`Number is Tooo high`)
    }
}

function displayGuess(guess){
    // values clean last value or update guess remaning and update array also
    userInput.value = ''
    guessSlot.innerHTML += `${guess} `
    numGuess++;
    remainingResult.innerHTML = `${10 - numGuess}`
}

function displayMessage(message){
    // Interact with dom directly.
    lowHigh.innerHTML = `<h2>${message}</h2>`

}

function endGame(){
    //  first clean value , or stop the value from user input
    userInput.value = ''
    userInput.setAttribute('disabled','')
    p.classList.add('button')
    p.innerHTML = `<h2 id="newGame">Start New Game</h2>`
    startOver.appendChild(p)
    playGame = false
    newGame()
}

function newGame(){
    // take button reference
    const newGameButton = document.querySelector('#newGame')
    newGameButton.addEventListener('click',function(e){
        e.preventDefault()
        randomNumber = parseInt(Math.random() * 100 + 1);
        prevGuess = []
        numGuess = 1
        guessSlot.innerHTML = ''
        remainingResult.innerHTML = `${10 - numGuess}`
        userInput.removeAttribute('disabled')
        startOver.removeChild(p)

        playGame = true
    })
}


```