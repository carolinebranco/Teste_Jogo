# Teste_Jogo
Ponho rosa
<!DOCTYPE html>
<html>
  <head>
    <style>
      canvas {
        border: 1px solid #000;
      }
      
      /* Estilos para o cabeçalho */
      header {
        background-color: #f9f9f9;
        padding: 10px;
        text-align: center;
      }
      
      /* Estilos para o rodapé */
      footer {
        background-color: #f9f9f9;
        padding: 10px;
        text-align: center;
        font-size: 0.8em;
        color: #888;
      }
    </style>
  </head>
  <body>
    <header>
      <h1>Meu Jogo Arcade</h1>
    </header>

    <canvas id="gameCanvas" width="800" height="400"></canvas>

    <footer>
      <p>&copy; 2023 Caroline. Todos os direitos reservados.</p>
    </footer>

    <script>
      // Obtendo a referência para o elemento canvas
      var canvas = document.getElementById("gameCanvas");
      var context = canvas.getContext("2d");

      // Definindo as variáveis do jogo
      var ballX = canvas.width / 2;
      var ballY = canvas.height / 2;
      var ballSpeedX = 5;
      var ballSpeedY = 5;
      var paddleHeight = 100;
      var paddleWidth = 10;
      var player1Y = canvas.height / 2 - paddleHeight / 2;
      var player2Y = canvas.height / 2 - paddleHeight / 2;

      // Função de atualização do jogo
      function update() {
        // Atualizar a posição da bola
        ballX += ballSpeedX;
        ballY += ballSpeedY;

        // Lógica de rebatimento da bola nas paredes
        if (ballY < 0 || ballY > canvas.height) {
          ballSpeedY = -ballSpeedY;
        }

        // Lógica de rebatimento da bola nos jogadores
        if (
          ballX < paddleWidth &&
          ballY > player1Y &&
          ballY < player1Y + paddleHeight
        ) {
          ballSpeedX = -ballSpeedX;
        }

        if (
          ballX > canvas.width - paddleWidth &&
          ballY > player2Y &&
          ballY < player2Y + paddleHeight
        ) {
          ballSpeedX = -ballSpeedX;
        }

        // Limpar o canvas
        context.clearRect(0, 0, canvas.width, canvas.height);

        // Desenhar os jogadores
        context.fillStyle = "pink";
        context.fillRect(0, player1Y, paddleWidth, paddleHeight);
        context.fillRect(
          canvas.width - paddleWidth,
          player2Y,
          paddleWidth,
          paddleHeight
        );

        // Desenhar a bola
        context.beginPath();
        context.arc(ballX, ballY, 10, 0, Math.PI * 2);
        context.fillStyle = "pink";
        context.fill();

        // Chamar a função de atualização novamente
        requestAnimationFrame(update);
      }

      // Função para lidar com o movimento do jogador
      function handleMouseMove(event) {
        var relativeY = event.clientY - canvas.offsetTop;
        player1Y = relativeY - paddleHeight / 2
