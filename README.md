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
      <img class="front-face" src="img/aurelia.svg" alt="Aurelia" />
      <img class="back-face" src="img/js-badge.svg" alt="JS Badge" />
    </div>
    <div class="memory-card" data-framework="aurelia">
      <img class="front-face" src="img/aurelia.svg" alt="Aurelia" />
      <img class="back-face" src="img/js-badge.svg" alt="JS Badge" />
    </div>

   <section class="memory-game">
  <div class="memory-card">
    <img class="front-face" src="img/react.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/react.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/angular.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/angular.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/ember.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/ember.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/vue.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/vue.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/backbone.svg" Face da Carta="Backbone">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/backbone.svg" Face da Carta="Backbone">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/aurelia.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>

  <div class="memory-card">
    <img class="front-face" src="img/aurelia.svg" alt="Face da Carta">
    <img class="back-face" src="img/js-badge.svg" alt="Verso da Carta">
  </div>
</section>

  <script src="scripts.js"></script>
</body>
</html>
const cards = document.querySelectorAll('.memory-card');

let hasFlippedCard = false;
let lockBoard = false;
let firstCard, secondCard;

function flipCard() {
  if (lockBoard) return;
  if (this === firstCard) return;

  this.classList.add('flip');

  if (!hasFlippedCard) {
    hasFlippedCard = true;
    firstCard = this;

    return;
  }

  secondCard = this;
  checkForMatch();
}

function checkForMatch() {
  let isMatch = firstCard.dataset.framework === secondCard.dataset.framework;

  isMatch ? disableCards() : unflipCards();
}

function disableCards() {
  firstCard.removeEventListener('click', flipCard);
  secondCard.removeEventListener('click', flipCard);

  resetBoard();
}

function unflipCards() {
  lockBoard = true;

  setTimeout(() => {
    firstCard.classList.remove('flip');
    secondCard.classList.remove('flip');

    resetBoard();
  }, 1500);
}

function resetBoard() {
  [hasFlippedCard, lockBoard] = [false, false];
  [firstCard, secondCard] = [null, null];
}

(function shuffle() {
  cards.forEach(card => {
    let randomPos = Math.floor(Math.random() * 12);
    card.style.order = randomPos;
  });
})();

cards.forEach(card => card.addEventListener('click', flipCard));
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
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
  transform-style: preserve-3d;
  transition: transform .5s;
  box-shadow: 1px 1px 1px rgba(0,0,0,.3);
}

.memory-card:active {
  transform: scale(0.97);
  transition: transform .2s;
}

.memory-card.flip {
  transform: rotateY(180deg);
}

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 5px;
  background: #1C7CCC;
  backface-visibility: hidden;
}

.front-face {
  transform: rotateY(180deg);
}
