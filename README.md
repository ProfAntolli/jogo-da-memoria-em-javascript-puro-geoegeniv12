index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">

  <title>Memory Game</title>

  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <section class="memory-game">
    <div class="memory-card" data-framework="aurelia">
      <img class="front-face" src="img/aurelia.svg"
       alt="Aurelia" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="aurelia">
      <img class="front-face" src="img/aurelia.svg"
       alt="Aurelia" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="vue">
      <img class="front-face" src="img/vue.svg" alt="Vue" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="vue">
      <img class="front-face" src="img/vue.svg" alt="Vue" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="angular" >
      <img class="front-face" src="img/angular.svg"
       alt="Angular" />
      <img class="back-face" src="img/js-badge.svg" alt="JS
       Badge" />
    </div>
    <div class="memory-card" data-framework="angular" >
      <img class="front-face" src="img/angular.svg"
       alt="Angular" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="ember">
      <img class="front-face" src="img/ember.svg"
       alt="Ember" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="ember" >
      <img class="front-face" src="img/ember.svg"
       alt="Ember" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="backbone">
      <img class="front-face" src="img/backbone.svg"
       alt="Backbone" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="backbone">
      <img class="front-face" src="img/backbone.svg" 
       alt="Backbone" />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
    <div class="memory-card" data-framework="react">
      <img class="front-face" src="img/react.svg" alt="React"
       />
      <img class="back-face" src="img/js-badge.svg" alt="JS
       Badge" />
    </div>
    <div class="memory-card" data-framework="react">
      <img class="front-face" src="img/react.svg" alt="React"
       />
      <img class="back-face" src="img/js-badge.svg" alt="JS 
      Badge" />
    </div>
  </section>

  <script src="scripts.js"></script>
</body>
</html>

styles.css
 
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  
  body {
    height: 100vh;
    display: flex;
    background: #060AB2;
  }
  
  .memory-game {
    width: 640px;
    height: 640px;
    margin: auto;
    display: flex;
    flex-wrap: wrap;
    perspective: 1000px;
  }
  
  .memory-card {
    width:calc(25% - 10px);
    height:calc(33.333% - 10px);
    margin: 5px;
    position: relative;
    transform: scale(1);
    transform-style: preserve-3d;
    transition: transform .5s;
}

  .memory-card:active{
    transform:scale(.97);
    transition: transform .2s;
  }

  .memory-card.flip {
    transition: rotateY(180deg);
}

  .front-face,
  .back-face {
    width: 100%;
    height: 100%;
    padding: 20px;
    position:absolute;
    border-radius: 5px;
   background: #5c5eba;
   backface-visibility: hidden;
  }

  .front-face{
    transform: rotateY(180deg);
  }
  
scripts.js

 const cards = document.querySelectorAll('.memory-card');

let hasFlipCard = false;
let lockBoard = false;
let firsCard, secondCard;

function flipCard() {
  if(lockBoard) return;
  if(this === firsCard) return;

    this.classList.addEventListener('flip');

    if(!hasFlippedCard) {
      // first click  
      hasFlippedCard = true;
      firsCard = this;

      return;
    }

     // second click
     secondCard = this;

     checkForMatch();
    }

function checkForMatch() {
    let isMatch = firsCard.dataset.framework === 
        secondCard.dataset.framework;

   isMatch ? disableCards() : unflipCards();
}

function disableCards() {
  firsCard.removeEventListener('click', flipCard);
  secondCard.removeEventListener('click', flipCard);

  resetBoard();
}

function unflipCards() {
  lockBoard = true;


     setTimeout(() => {
       firsCard.classList.remove('flip');
       secondCard.classList.remove('flip');

       resetBoard();
    }, 1500);
}

function resetBoard() {
   [hasFlippedCard, lockBoard] = [false, false];
   [firsCard, secondCard] = [null, null];
}

(function shuffle() {
  cards.forEach(card => {
    let randomPos = Math.floor(Math.random() * 12)
    card.style.order = randomPos;
  });
})();

cards.forEach(card => card.addEventListener('click', flipCard))
  ;
