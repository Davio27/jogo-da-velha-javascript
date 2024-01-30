# Jogo da Velha

Este é um simples projeto de Jogo da Velha desenvolvido em HTML, CSS e JavaScript. 

## Como Jogar

1. Abra o arquivo `index.html` no seu navegador.
2. Clique nos botões dentro da grade para fazer a sua jogada. Os jogadores se alternam entre "X" e "O".
3. O jogo alertará quando um jogador vencer ou se houver empate.
4. Reinicie o jogo clicando novamente no botão de recarregar a página.

## Estrutura do Projeto

- `index.html`: Contém a estrutura HTML do jogo.
- `style.css`: Define o estilo e layout do jogo.
- `script.js`: Contém a lógica do jogo em JavaScript.

## Estrutura HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jogo da Velha</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <main>
    <h1>JOGO DA VELHA</h1>
    <hr />
    <div class="game">
      <button data-i="1"></button>
      <button data-i="2"></button>
      <button data-i="3"></button>
      <button data-i="4"></button>
      <button data-i="5"></button>
      <button data-i="6"></button>
      <button data-i="7"></button>
      <button data-i="8"></button>
      <button data-i="9"></button>
    </div>
    <h2 class="currentPlayer"></h2>
  </main>
  <script src="script.js"></script>
</body>
</html>
```

## Estilo CSS

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: cursive;
}

body {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f7f7f7;
}

main {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

h1 {
  text-align: center;
}

hr {
  font-weight: bold;
  height: 3px;
  background: black;
  margin-bottom: 10px;
}

.game {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.game button {
  width: 100px;
  height: 100px;
  margin: 5px;
  cursor: pointer;
  font-size: 50px;
  background: #f7f7f7;
}
```

## Lógica JavaScript

```js
const currentPlayer = document.querySelector(".currentPlayer");

let selected;
let player = "X";

let positions = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],
  [1, 5, 9],
  [3, 5, 7],
];

function init() {
  selected = [];

  currentPlayer.innerHTML = `JOGADOR DA VEZ: ${player}`;

  document.querySelectorAll(".game button").forEach((item) => {
    item.innerHTML = "";
    item.addEventListener("click", newMove);
  });
}

init();

function newMove(e) {
  const index = e.target.getAttribute("data-i");
  e.target.innerHTML = player;
  e.target.removeEventListener("click", newMove);
  selected[index] = player;

  setTimeout(() => {
    check();
  }, [100]);

  player = player === "X" ? "O" : "X";
  currentPlayer.innerHTML = `JOGADOR DA VEZ: ${player}`;
}

function check() {
  let playerLastMove = player === "X" ? "O" : "X";

  const items = selected
    .map((item, i) => [item, i])
    .filter((item) => item[0] === playerLastMove)
    .map((item) => item[1]);

  for (pos of positions) {
    if (pos.every((item) => items.includes(item))) {
      alert("O JOGADOR '" + playerLastMove + "' GANHOU!");
      init();
      return;
    }
  }

  if (selected.filter((item) => item).length === 9) {
    alert("DEU EMPATE!");
    init();
    return;
  }
}
```

Divirta-se jogando o Jogo da Velha! 😊
