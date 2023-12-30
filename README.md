## CodePipeline - S3 - Game

### 1 - Code Implementation 
Simple memory matching game using JavaScript, HTML and CSS.

### Breakdown of what the code does:

### Initialization:
   - The code starts by selecting all elements with the class "card" using `document.querySelectorAll(".card")` and stores them in the `cards` variable.
```
const cards = document.querySelectorAll(".card");
```

### Variables:
   - `matched`, `cardOne`, `cardTwo`, and `disableDeck` are initialized to keep track of matched cards, the two cards being compared, and to control the interaction of flipping cards.
```
let matched = 0;
let cardOne, cardTwo;
let disableDeck = false;
```

### Event Listener and Functions:**
   - `flipCard()` is an event handler attached to each card. It triggers when a card is clicked and flips the card.
   - When a card is flipped, it checks if the deck is not disabled and if the clicked card is not the same as the first card that was clicked.
   - If it's the first card clicked, it sets `cardOne` to the clicked card.
   - If it's the second card clicked, it sets `cardTwo` to the clicked card, disables the deck, and tries to match the cards by comparing their images.
```
function flipCard({target: clickedCard}) {
    if(cardOne !== clickedCard && !disableDeck) {
        clickedCard.classList.add("flip");
        if(!cardOne) {
            return cardOne = clickedCard;
        }
        cardTwo = clickedCard;
        disableDeck = true;
        let cardOneImg = cardOne.querySelector(".back-view img").src,
        cardTwoImg = cardTwo.querySelector(".back-view img").src;
        matchCards(cardOneImg, cardTwoImg);
    }
}
```

### Matching Cards:
   - `matchCards()` compares the images of `cardOne` and `cardTwo`.
   - If the images match, the `matched` count increases. If all cards are matched (8 pairs in total), it calls `shuffleCard()` after a delay of 1000 milliseconds using `setTimeout()`.
   - If the images do not match, the cards briefly shake using CSS classes, then flip back to their original state after a delay using `setTimeout()`.
```
function matchCards(img1, img2) {
    if(img1 === img2) {
        matched++;
        if(matched == 8) {
            setTimeout(() => {
                return shuffleCard();
            }, 1000);
        }
        cardOne.removeEventListener("click", flipCard);
        cardTwo.removeEventListener("click", flipCard);
        cardOne = cardTwo = "";
        return disableDeck = false;
    }
    setTimeout(() => {
        cardOne.classList.add("shake");
        cardTwo.classList.add("shake");
    }, 400);

    setTimeout(() => {
        cardOne.classList.remove("shake", "flip");
        cardTwo.classList.remove("shake", "flip");
        cardOne = cardTwo = "";
        disableDeck = false;
    }, 1200);
}
```

### Shuffling Cards:
   - `shuffleCard()` resets the game state by resetting variables, shuffling the images in the cards randomly, and adding event listeners for clicking cards.
```
function shuffleCard() {
    matched = 0;
    disableDeck = false;
    cardOne = cardTwo = "";
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 4, 5, 6, 7, 8];
    arr.sort(() => Math.random() > 0.5 ? 1 : -1);
    cards.forEach((card, i) => {
        card.classList.remove("flip");
        let imgTag = card.querySelector(".back-view img");
        imgTag.src = `images/img-${arr[i]}.png`;
        card.addEventListener("click", flipCard);
    });
}
```

### Initialization:
   - `shuffleCard()` is called initially to set up the game by shuffling the cards.
   - Event listeners are attached to each card using `forEach` to trigger the `flipCard()` function when clicked.
```
shuffleCard();
    
cards.forEach(card => {
    card.addEventListener("click", flipCard);
}
```
### 2 - 
