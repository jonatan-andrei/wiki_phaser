# Phaser
Esta é uma wiki sobre o framework Phaser, escrita para a disciplina de Construção de Páginas Web II.

## Integrantes do grupo:
- Jonatan Andrei Haas
- Felipe Ibias dos Santos

## Sobre a Wiki:
Nesta Wiki, nosso objetivo é falar sobre o funcionamento do framework Phaser e especialmente como controlar a interação do usuário com o teclado durante o jogo.

Neste tutorial, utilizaremos o popular jogo Snake e nos basearemos no seguinte exemplo: https://labs.phaser.io/index.html?dir=games/snake/&q=
Este exemplo foi disponibilizado pela equipe de desenvolvedores do Phaser.

## O Phaser
O Phaser é um framework Javascript para facilitar o desenvolvimento de jogos.
Para utilizá-lo, basta fazer o download no site oficial dos desenvolvedores: https://phaser.io/download

## Introdução ao desenvolvimento com Phaser
[Nesta etapa falaremos sobre a parte 1 do tutorial do exemplo acima](https://labs.phaser.io/edit.html?src=src\games\snake\part1.js)

O primeiro passo é criarmos um objeto `Game` do Phaser. Essa instância será responsável por iniciar o Phaser:
```javascript
var game = new Phaser.Game(config);
```

Passamos como parâmetro o objeto config. Neste parâmetro devemos indicar algumas configurações de como nosso jogo deve ser. 
No exemplo que estamos seguindo, foram passadas as configurações:
- `type`: que pode ter os seguintes valores: `Phaser.CANVAS`, `Phaser.WEBGL` ou `Phaser.AUTO`. Ela determina a tecnologia de renderização do jogo.
O valor recomendado é o AUTO, isso porque ele tentará utilizar o WEBGL, mas se não for suportado pelo navegador, ele utilizará o CANVAS.
No exemplo, foi utilizado WEBGL, mais indicado para navegadores.
- `width`: A largura da tela do nosso jogo.
- `height`: A altura da tela do jogo.
- `parent`: Essa propriedade indica o contêiner pai do nosso jogo na página HTML.
- `backgroundColor`: Passamos a cor de fundo da nossa tela.
- `scene`: o último parâmetro de configuração, é também um objeto e tem a indicação de 3 métodos que serão fundamentais para o nosso jogo. São eles: preload, create e update. Nesta primeira etapa, utilizaremos apenas o preload. O preload é um método executado pelo Phaser ao ser iniciado e fará o carregamento dos recursos, como as imagens, que precisaremos para o jogo (a cobra e a comida).
No create é que de fato definimos (“criamos” o que utilizaremos durante o jogo, instanciamos as variáveis, por exemplo.
Já o update funciona como o “loop” do jogo. É onde estará a nossa lógica. Onde trataremos colisões, mudanças, movimentações do personagem e etc.

## Interação com o teclado
Este é o principal tema do nosso tutorial e também uma das necessidades mais comuns no desenvolvimento de um jogo. 
Para facilitar o desenvolvimento, temos no Phaser uma função de atalho que configura as teclas mais utilizadas em um jogo. São elas: o shift, o espaço e as setas. A função é a seguinte: 
```javascript
this.input.keyboard.createCursorKeys();
```

Utilizá-la é bastante simples. Primeiro, precisamos de uma variável global, que no exemplo é chamada de `cursors`. No create então atribuímos a nossa variável o retorno do `createCursorKeys`.

Agora, no loop do jogo, ou seja, no update, poderemos utilizar a variável cursors.
Dentro da nossa variável cursors, temos uma propriedade para cada tecla que temos configurada. São elas:
`right`: flecha para direita;
`left`: flecha para esquerda;
`down`: flecha para baixo;
`up`: flecha para cima;
`shift`: tecla shift;
`space`: tecla espaço.

Temos ainda, dentro do objeto de cada tecla, propriedades que indicam determinados “estados” de interação com a tecla. O mais comum e que é utilizado no jogo, é o `isDown`. A propriedade `isDown` indica se a tecla está pressionada ou não. No exemplo que estamos seguindo, a propriedade `isDown` das setas dentro do `cursors` é utilizada para controlar os movimentos da cobra. No momento que uma tecla é disparada, como estamos dentro do método update, o loop, é verificado se o movimento é válido e a direção do jogador é alterada. A propriedade `isDown` retorna um booleano (verdadeiro ou falso) assim como a `isUp`, que retorna true quando a tecla está ativa, ou seja, não pressionada.
Existem várias outras propriedades disponíveis para serem utilizadas no objeto de cada tecla. São elas:
- `altKey`: A tecla pressionada junto (ao mesmo tempo que) a tecla Alt.
- `ctrlKey`: A tecla pressionada junto (ao mesmo tempo que) a tecla Control.
- `metaKey`: Semelhante ao altKey e ao ctrlKey, mas retorna verdadeiro quando a tecla em questão é pressionada junto com a tecla de comando no Mac ou a tecla Windows.
- `shiftKey`: Mesmo funcionamento das demais, mas relacionada a tecla shift pressionada em conjunto com a tecla principal.
- `duration`: Retorna o número de milissegundos em que a tecla esteve pressionada pela última vez.
- `emitOnRepeat`: Por padrão, o isDown irá emitir o evento de clique na tecla apenas uma vez. Mas se ativarmos essa propriedade, o isDown passará a disparar enquanto a tecla está pressionada.
- `keyCode`: O código keyCode da tecla.
- `repeats`: A quantidade de vezes que a tecla foi pressionada.
- `timeDown`: O registro da data e hora que a tecla foi pressionada pela última vez.
- `timeUp`: A data e hora da última vez que a tecla foi liberada (deixou de estar pressionada).

Para boa parte dos jogos mais simples, estas 6 teclas, mais as combinações, serão suficientes para realizarmos a interação do usuário com nosso jogo. Porém, podemos ter a necessidade de controlar mais teclas. 

Também é bastante simples realizar esse controle. Poderíamos, por exemplo, querer ter o controle da letra P para pausar o jogo. Bastaríamos ter:
```javascript
`var keyP = scene.input.keyboard.addKey('P');
```
E então teríamos também acesso a maioria das propriedades descritas acima do `createCursorKeys()`. Entre eles o `isDown` e o `isUp`. Conforme exemplo:
```javascript
`var isDown = keyP.isDown;`
var isUp = keyP.isUp;
```
Outro método interessante é o `getDuration()`. Ele nos retorna, em milissegundos, a quantidade de tempo em que a tecla esteve pressionada.
```javascript
var duration = keyP.getDuration();
```

Uma maneira alternativa de obter o controle sobre uma tecla é a seguinte:
```javascript
var keyP = scene.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.P);
```

## Mapa de teclas que podem ser controladas pelo Phaser:
- A ~ Z;
- F1 ~ F12;
- BACKSPACE;
- TAB;
- ENTER;
- SHIFT;
- CTRL, ALT;
- PAUSE;
- CAPS_LOCK;
- ESC;
- SPACE;
- PAGE_UP, PAGE_DOWN;
- END, HOME;
- LEFT, UP, RIGHT, DOWN;
- PRINT_SCREEN;
- INSERT, DELETE;
- ZERO, ONE, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE;
- NUMPAD_ZERO, NUMPAD_ONE, NUMPAD_TWO, NUMPAD_THREE, NUMPAD_FOUR, NUMPAD_FIVE, NUMPAD_SIX, NUMPAD_SEVEN, NUMPAD_EIGHT, NUMPAD_NINE;
- OPEN_BRACKET, CLOSED_BRACKET;
- SEMICOLON_FIREFOX, COLON, COMMA_FIREFOX_WINDOWS, COMMA_FIREFOX, BRACKET_RIGHT_FIREFOX, BRACKET_LEFT_FIREFOX.

Fontes: 
http://phaser.io/tutorials/making-your-first-phaser-3-game-portuguese
https://rexrainbow.github.io/phaser3-rex-notes/docs/site/keyboardevents/
https://photonstorm.github.io/phaser3-docs/Phaser.Input.Keyboard.Key.html
https://stackoverflow.com/questions/58383619/how-to-use-a-s-d-w-keys-in-phaser
https://www.youtube.com/watch?v=8SwYzPrqaD0
