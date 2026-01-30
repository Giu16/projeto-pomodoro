<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Pomodoro Técnica</title>
<style>
  :root {
    --cor-primaria: #1abc9c;
    --cor-fundo-escuro: #0a192f;
    --cor-texto-escuro: #ecf0f1;
    --cor-botao-escuro: #16a085;
  }

  body {
    margin: 0; 
    padding: 25px;
    font-family: 'Poppins', sans-serif;
    background: var(--cor-fundo-escuro);
    color: var(--cor-texto-escuro);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    transition: background 0.4s, color 0.4s;
    user-select: none;
  }
  

  h1 {
    font-weight: 600;
    font-size: 2rem;
    color: #FFFFFF;
    margin-bottom: 40px;
    text-shadow: 0 0 10px var(--cor-botao-escuro);
    letter-spacing: 3px;
    transition: color 0.4s, text-shadow 0.4s;
  }

  .timer-wrapper {
    position: relative;
    width: 280px;
    height: 280px;
    margin-bottom: 25px;
  }

  svg {
    transform: rotate(-90deg);
    width: 280px;
    height: 280px;
    transition: stroke 0.4s;
  }

  circle {
    fill: none;
    stroke-width: 15;
    stroke-linecap: round;
  }

  .circle-bg {
    stroke: rgba(255, 255, 255, 0.1);
  }

 .circle-progress {
  stroke: var(--cor-primaria);
  transition: stroke-dashoffset 1s linear;
  position: relative;
  z-index: 2;
}

  .timer {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 6rem;
  font-weight: 600;
  color: #FFFFFF;
  text-shadow:
    0 0 1px var(--cor-primaria),
    0 0 0px var(--cor-botao-escuro),
    0 0 5px var(--cor-botao-escuro);
  transition: color 0.4s, text-shadow 0.4s;
  user-select: none;
  letter-spacing: normal; /* Ajuste aqui */
}

  .status {
    font-size: 2rem;
    font-weight: 600;
    color: #FFFFFF;
    text-shadow: 0 0 8px var(--cor-botao-escuro);
    margin-bottom: 35px;
    letter-spacing: 2px;
    transition: color 0.4s, text-shadow 0.4s;
    user-select: none;
  }

  .buttons {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: 30px;
  }

  button {
    background: transparent;
    border: 2.5px solid #FFFFFF;
    color: #FFFFFF;
    padding: 10px 10px;
    font-size: 1.2rem;
    font-weight: 600;
    border-radius: 45px;
    cursor: pointer;
    transition:
      background-color 0.4s ease,
      color 0.4s ease,
      box-shadow 0.4s ease,
      transform 0.2s ease;
    box-shadow: 0 0 10px transparent;
    user-select: none;
  }

  button:hover:not(:disabled),
  button:focus:not(:disabled) {
    background-color: #FFFFFF;
    color: #0a192f;
    box-shadow:
      0 0 15px var(--cor-primaria),
      0 0 25px var(--cor-botao-escuro);
    outline: none;
    transform: scale(1.05);
  }

  button:disabled {
    border-color: #555;
    color: #555;
    cursor: not-allowed;
    box-shadow: none;
    background-color: transparent;
  }

  /* Formulário customização */
  .config-container {
    max-width: 300px;
    width: 100%;
    margin-bottom: 40px;
    background: rgba(255 255 255 / 0.05);
    border-radius: 15px;
    padding: 20px 25px;
    box-shadow: 0 0 25px rgba(0, 0, 0, 0.3);
    user-select: none;
    transition: background 0.4s;
    text-align: center; /* centraliza todo conteúdo */
  }

  .config-container label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #FFFFFF;
    transition: color 0.4s;
    text-align: center; /* centraliza texto do label */
  }

  .config-container input[type="number"] {           
    margin: 0 auto 15px;    /* centraliza e espaça abaixo */
    display: block;         /* para margin auto funcionar */
    padding: 10px 12px;
    font-size: 1rem;
    border-radius: 8px;
    border: none;
    outline: none;
    background: rgba(255 255 255 / 0.1);
    color: #fff;
    transition: background 0.4s, color 0.4s;
  }

  .config-container input[type="number"]::-webkit-inner-spin-button,
  .config-container input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  /* Cabeçalho fixo no topo */
.top-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 60px;
  background: rgba(10, 25, 47, 0.5); /* fundo transparente escuro */
  backdrop-filter: blur(8px); /* efeito vidro fosco */
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0,0,0,0.4);
  user-select: none;
}

/* Texto neon no header */
.top-header h1 {
  color: #FFFFFF;
  font-family: 'Poppins', sans-serif;
  font-weight: 700;
  font-size: 2rem;
  letter-spacing: 2px;
  text-shadow:
    0 0 4px #ffffff,
    0 0 0px #ffffff,
    0 0 0px #ffffff,
    0 0 0px #ffffff;
  margin: 0;
}

body {
  padding-top: 100px; /* Ajuste para diminuir o espaçamento */

}
  #bola-timer {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 60px;
  height: 60px;
  background-color: var(--cor-primaria); /* cor principal do tema */
  color: #fff;
  font-weight: 700;
  font-size: 1.2rem;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  user-select: none;
  cursor: grab;
  box-shadow:
    0 0 10px var(--cor-primaria),
    0 0 20px var(--cor-botao-escuro);
  z-index: 9999;
  touch-action: none; /* importante para funcionar no mobile */
}

#bola-timer:active {
  cursor: grabbing;
}

.wave-circle {
  fill: none;
  stroke: var(--cor-primaria);
  stroke-width: 15;
  stroke-linecap: round;
  opacity: 0.15;
  transform-origin: center;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}

.wave1 {
  animation-name: wavePulse;
  animation-duration: 3.0s;
}

.wave2 {
  animation-name: wavePulse;
  animation-duration: 3.5s;
  
}

.wave3 {
  animation-name: wavePulse;
  animation-duration: 4.0s;
  
}

@keyframes wavePulse {
  0% {
    stroke-opacity: 0.20;
    transform: scale(1);
  }
  50% {
    stroke-opacity: 0.20;
    transform: scale(1.04);
  }
  100% {
    stroke-opacity: 0.20;
    transform: scale(1);
  }
}

</style>
</head>
<body>
  <header class="top-header" role="banner">
    <h1>PomoRitual</h1>
  </header>

    <div class="timer-wrapper" aria-live="polite" aria-atomic="true">
    <svg width="290" height="290" viewBox="0 0 300 290" xmlns="http://www.w3.org/2000/svg">
  <circle class="circle-bg" cx="140" cy="140" r="1300"></circle>
  <circle class="circle-progress" cx="140" cy="140" r="130" stroke-dasharray="817" stroke-dashoffset="0"></circle>
  <!-- Círculos para onda -->
  <circle class="wave-circle wave1" cx="140" cy="140" r="130"></circle>
  <circle class="wave-circle wave2" cx="140" cy="140" r="130"></circle>
  <circle class="wave-circle wave3" cx="140" cy="140" r="130"></circle>
</svg>
    <div class="timer" id="timer" role="timer" aria-label="Tempo restante">25:00</div>
  </div>

  <div class="status" id="status" aria-live="polite" aria-atomic="true">FOCO</div>

  <div class="buttons">
    <button id="startBtn">Iniciar</button>
    <button id="pauseBtn">Pausar</button>
    <button id="resetBtn">Resetar</button>
  </div>

 <div class="config-container" aria-label="Configurações do temporizador">
    <label for="inputFoco">Duração do Pomodoro (minutos)</label>
    <input type="number" id="inputFoco" min="1" max="60" value="25" />

    <label for="inputPausaCurta">Duração da Pausa Curta (minutos)</label>
    <input type="number" id="inputPausaCurta" min="1" max="30" value="5" />

    <label for="inputPausaLonga">Duração da Pausa Longa (minutos)</label>
    <input type="number" id="inputPausaLonga" min="1" max="60" value="15" />
  </div>

  <audio id="alertSound" src="https://actions.google.com/sounds/v1/alarms/beep_short.ogg" preload="auto"></audio>
  <audio id="beepSound" src="https://actions.google.com/sounds/v1/alarms/beep_short.ogg" preload="auto"></audio>
  <audio id="finalSound" src="https://actions.google.com/sounds/v1/alarms/alarm_clock.ogg" preload="auto"></audio>
  <div id="bola-timer" style="display:none;">00:00</div>
  <script>
    // Elementos DOM
    
    const timerEl = document.getElementById("timer");
    const statusEl = document.getElementById("status");
    const startBtn = document.getElementById("startBtn");''
    const pauseBtn = document.getElementById("pauseBtn");
    const resetBtn = document.getElementById("resetBtn");
    const alertSound = document.getElementById("alertSound");
    const inputFoco = document.getElementById("inputFoco");
    const inputPausaCurta = document.getElementById("inputPausaCurta");
    const inputPausaLonga = document.getElementById("inputPausaLonga");
    const circle = document.querySelector(".circle-progress");
    const bolaTimer = document.getElementById("bola-timer");

    // Variáveis do timer
    let DURACOES = {
      foco: 25 * 60,
      pausaCurta: 5 * 60,
      pausaLonga: 15 * 60
    };
    let tempoRestante = DURACOES.foco;
    let ciclo = 0;
    let status = "foco";
    let timerInterval = null;

    // SVG circle properties
    const radius = circle.r.baseVal.value;
    const circumference = 2 * Math.PI * radius;
    circle.style.strokeDasharray = circumference;
    circle.style.strokeDashoffset = 0;

    // Função para atualizar progresso circular
    function setProgress(percent) {
      const offset = circumference - percent * circumference;
      circle.style.strokeDashoffset = offset;
    }

    // Formatar tempo para mm:ss
    function formatarTempo(segundos) {
      const min = String(Math.floor(segundos / 60)).padStart(2, "0");
      const seg = String(segundos % 60).padStart(2, "0");
      return `${min}:${seg}`;
    }

    // Atualizar display e progresso
   function atualizarDisplay() {
  timerEl.textContent = formatarTempo(tempoRestante);
  let statusTexto = "";
  switch(status) {
    case "foco":
      statusTexto = "FOCO";
      break;
    case "pausaCurta":
      statusTexto = "PAUSA CURTA";
      break;
    case "pausaLonga":
      statusTexto = "PAUSA LONGA";
      break;
  }
  statusEl.textContent = statusTexto;

  const total = DURACOES[status];
  const percent = (total - tempoRestante) / total;
  setProgress(percent);

  // Atualiza o título da aba
  document.title = `${formatarTempo(tempoRestante)} - ${statusTexto}`;

  // Atualiza o texto da bola móvel se ela estiver visível
  if (bolaTimer.style.display === "flex") {
    atualizarBola();
  }
}
    // Função para mudar de status após o fim do tempo
    function proximoStatus() {
      if (status === "foco") {
        ciclo++;
        if (ciclo % 4 === 0) {
          status = "pausaLonga";
          tempoRestante = DURACOES.pausaLonga;
        } else {
          status = "pausaCurta";
          tempoRestante = DURACOES.pausaCurta;
        }
      } else {
        status = "foco";
        tempoRestante = DURACOES.foco;
      }
    }

    // Iniciar timer
    function iniciarTimer() {
      if (timerInterval) return;

    
      inputPausaCurta.disabled = true;
      inputPausaLonga.disabled = true;

      timerInterval = setInterval(() => {
  if (tempoRestante > 0) {
    if (tempoRestante <= 5) {
      beepSound.play().catch(() => {/* som bloqueado */});
    }
    tempoRestante--;
    atualizarDisplay();
  } else {
    clearInterval(timerInterval);
    timerInterval = null;

    finalSound.play().catch(() => {/* som bloqueado */});
    alertSound.play().catch(() => {/* som bloqueado */});
    mostrarNotificacao();

    proximoStatus();
    atualizarDisplay();
    iniciarTimer();
  }
}, 1000);
    }

    // Pausar timer
    function pausarTimer() {
      if(timerInterval) {
        clearInterval(timerInterval);
        timerInterval = null;

      }
    }

    // Resetar timer
    function resetarTimer() {
      if(timerInterval) {
        clearInterval(timerInterval);
        timerInterval = null;
      }
      status = "foco";
      tempoRestante = DURACOES.foco;
      ciclo = 0;
      atualizarDisplay();


      inputFoco.disabled = false;
      inputPausaCurta.disabled = false;
      inputPausaLonga.disabled = false;
    }

    // Atualizar DURACOES quando usuário muda os inputs
    function atualizarDuracoes() {
      const focoMin = parseInt(inputFoco.value, 10);
      const pausaCurtaMin = parseInt(inputPausaCurta.value, 10);
      const pausaLongaMin = parseInt(inputPausaLonga.value, 10);

      if (focoMin > 0 && focoMin <= 60) DURACOES.foco = focoMin * 60;
      if (pausaCurtaMin > 0 && pausaCurtaMin <= 30) DURACOES.pausaCurta = pausaCurtaMin * 60;
      if (pausaLongaMin > 0 && pausaLongaMin <= 60) DURACOES.pausaLonga = pausaLongaMin * 60;

      if (status === "foco") tempoRestante = DURACOES.foco;
      else if (status === "pausaCurta") tempoRestante = DURACOES.pausaCurta;
      else tempoRestante = DURACOES.pausaLonga;

      atualizarDisplay();
    }

    document.addEventListener('DOMContentLoaded', solicitarPermissaoNotificacao);

    // Solicitar permissão para notificações
    function solicitarPermissaoNotificacao() {
      if (!("Notification" in window)) return;
      if (Notification.permission === "default") {
        Notification.requestPermission();
      }
    }

    // Mostrar notificação quando o tempo acabar
    
    function mostrarNotificacao() {
  if (Notification.permission !== "granted") return;

  // Detecta se o navegador é Safari (desktop ou iOS)
  const isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

  const titulo = "Pomodoro Timer";
  let mensagem = "";
  switch(status) {
    case "foco": mensagem = "Hora de focar!"; break;
    case "pausaCurta": mensagem = "Pausa curta. Descanse!"; break;
    case "pausaLonga": mensagem = "Pausa longa. Aproveite!"; break;
  }

  if (isSafari) {
    // Notificação simples para Safari/iOS (sem botões)
    new Notification(titulo, {
      body: mensagem,
      icon: "https://img.icons8.com/ios-filled/50/268bd2/timer.png"
    });
  } else {
    // Notificação avançada para outros navegadores
    const options = {
      body: mensagem,
      icon: "https://img.icons8.com/ios-filled/50/268bd2/timer.png",
      requireInteraction: true,
      actions: [
        {action: 'iniciar', title: 'Iniciar', icon: 'https://img.icons8.com/ios-glyphs/30/268bd2/play--v1.png'},
        {action: 'pausar', title: 'Pausar', icon: 'https://img.icons8.com/ios-glyphs/30/268bd2/pause--v1.png'},
        {action: 'resetar', title: 'Resetar', icon: 'https://img.icons8.com/ios-glyphs/30/268bd2/reset.png'}
      ]
    };
    const notificacao = new Notification(titulo, options);

    notificacao.onclick = () => window.focus();

    notificacao.addEventListener('action', event => {
      switch(event.action) {
        case 'iniciar': iniciarTimer(); break;
        case 'pausar': pausarTimer(); break;
        case 'resetar': resetarTimer(); break;
      }
      notificacao.close();
    });

    setTimeout(() => notificacao.close(), 30000);
  }
}

    // Atualizar DURACOES ao mudar inputs
    inputFoco.addEventListener("change", atualizarDuracoes);
    inputPausaCurta.addEventListener("change", atualizarDuracoes);
    inputPausaLonga.addEventListener("change", atualizarDuracoes);

    // Botões
    startBtn.addEventListener("click", iniciarTimer);
    pauseBtn.addEventListener("click", pausarTimer);
    resetBtn.addEventListener("click", resetarTimer);

    // Inicializações
    solicitarPermissaoNotificacao();
    atualizarDisplay();
    
// Variáveis para controlar posição e arraste
let bolaPos = { x: window.innerWidth - 80, y: window.innerHeight - 80 };
let isDragging = false;
let dragOffset = { x: 0, y: 0 };

moverBola(bolaPos.x, bolaPos.y);

// Função para mover a bola limitando dentro da tela
function moverBola(x, y) {
  bolaPos.x = Math.min(Math.max(0, x), window.innerWidth - bolaTimer.offsetWidth);
  bolaPos.y = Math.min(Math.max(0, y), window.innerHeight - bolaTimer.offsetHeight);
  bolaTimer.style.left = bolaPos.x + "px";
  bolaTimer.style.top = bolaPos.y + "px";
}

// Eventos para iniciar arraste com mouse (desktop)
bolaTimer.addEventListener("mousedown", e => {
  isDragging = true;
  dragOffset.x = e.clientX - bolaPos.x;
  dragOffset.y = e.clientY - bolaPos.y;
  bolaTimer.style.cursor = "grabbing";
});

// Evento para mover a bola com o mouse
document.addEventListener("mousemove", e => {
  if (isDragging) {
    moverBola(e.clientX - dragOffset.x, e.clientY - dragOffset.y);
  }
});

// Evento para finalizar o arraste com o mouse
document.addEventListener("mouseup", () => {
  isDragging = false;
  bolaTimer.style.cursor = "grab";
});

// Eventos para arraste com touch (mobile)
bolaTimer.addEventListener("touchstart", e => {
  isDragging = true;
  const touch = e.touches[0];
  dragOffset.x = touch.clientX - bolaPos.x;
  dragOffset.y = touch.clientY - bolaPos.y;
});

document.addEventListener("touchmove", e => {
  if (isDragging) {
    const touch = e.touches[0];
    moverBola(touch.clientX - dragOffset.x, touch.clientY - dragOffset.y);
  }
});

document.addEventListener("touchend", () => {
  isDragging = false;
});

// Mostrar ou esconder a bola dependendo se a aba está ativa ou não
document.addEventListener("visibilitychange", () => {
  if (document.hidden) {
    bolaTimer.style.display = "flex";
    atualizarBola();
    moverBola(bolaPos.x, bolaPos.y);
  } else {
    bolaTimer.style.display = "none";
  }
});

document.addEventListener('keydown', e => {
  if (e.code === 'Space') {
    e.preventDefault(); // evita scroll na página
    if (!timerInterval) iniciarTimer();
    else pausarTimer();
  }
});

// Atualizar o texto da bola com o tempo formatado
function atualizarBola() {
  bolaTimer.textContent = formatarTempo(tempoRestante);
}
  </script>
</body>
</html>
