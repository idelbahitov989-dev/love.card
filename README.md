# love.card
a little love letter for my favorite person ♡
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Наша первая годовщина месяца ♡</title>
  
  <!-- Подключение винтажных каллиграфических шрифтов -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Marck+Script&family=Pinyon+Script&family=Great+Vibes&display=swap" rel="stylesheet">

  <style>
    /* ==========================================================================
       1. ПЕРЕМЕННЫЕ И БАЗОВЫЕ СТИЛИ
       ========================================================================== */
    :root {
      --bg-color: #f5f0eb;
      --table-wood: #3a2e2b;
      --paper-color: #fcf8f2;
      --paper-aged: #f3ebd8;
      --ink-color: #2c1d11;
      --accent-burgundy: #7a2021;
      --dusty-pink: #d48393;
      --soft-pink: #f2c6d0;
      --font-hand: 'Pinyon Script', cursive;
      --font-decor: 'Great Vibes', cursive;
      --font-body: 'Marck Script', cursive;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg-color);
      background-image: radial-gradient(circle, #fcf8f2 0%, #ecdcca 100%);
      color: var(--ink-color);
      font-family: var(--font-body);
      min-height: 100vh;
      overflow-x: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* ==========================================================================
       2. ЭКРАН КОНВЕРТА (ХЕРОУ)
       ========================================================================== */
    .envelope-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 100;
      transition: opacity 1s ease, transform 1s ease;
    }

    .envelope-screen.hidden {
      opacity: 0;
      pointer-events: none;
      transform: scale(1.1);
    }

    .envelope-wrapper {
      position: relative;
      width: 320px;
      height: 220px;
      cursor: pointer;
      filter: drop-shadow(0 15px 25px rgba(44, 29, 17, 0.25));
      transition: transform 0.4s ease;
    }

    .envelope-wrapper:hover {
      transform: scale(1.03);
    }

    /* Крылья ангела по бокам */
    .angel-wings {
      position: absolute;
      top: 50%;
      width: 90px;
      height: 140px;
      transform: translateY(-50%);
      z-index: 5;
      pointer-events: none;
      opacity: 0.85;
      animation: wingBreathe 4s ease-in-out infinite;
    }
    .angel-wings.left {
      left: -80px;
      transform: translateY(-50%) scaleX(-1);
    }
    .angel-wings.right {
      right: -80px;
    }

    @keyframes wingBreathe {
      0%, 100% { transform: translateY(-50%) scale(1); }
      50% { transform: translateY(-50%) scale(1.04); }
    }

    /* Сам конверт */
    .envelope {
      width: 100%;
      height: 100%;
      background: #e6dbcb;
      border-radius: 4px;
      position: relative;
      box-shadow: inset 0 0 20px rgba(138, 116, 91, 0.3);
      border: 1px solid #d4c2a8;
    }

    .envelope-flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid transparent;
      border-right: 160px solid transparent;
      border-top: 115px solid #ded0bd;
      transform-origin: top;
      transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 10;
    }

    .envelope.open .envelope-flap {
      transform: rotateX(180deg);
      z-index: 1;
    }

    /* Сердечко на конверте */
    .envelope-heart {
      position: absolute;
      top: 95px;
      left: 50%;
      transform: translateX(-50%);
      width: 32px;
      height: 32px;
      background: var(--accent-burgundy);
      clip-path: polygon(50% 15%, 100% 0%, 100% 70%, 50% 100%, 0% 70%, 0% 0%);
      z-index: 15;
      box-shadow: 0 2px 6px rgba(0,0,0,0.3);
      transition: transform 0.3s ease;
    }
    .envelope-wrapper:hover .envelope-heart {
      transform: translateX(-50%) scale(1.15);
    }

    .tap-instruction {
      margin-top: 25px;
      font-family: var(--font-hand);
      font-size: 2rem;
      color: var(--accent-burgundy);
      letter-spacing: 1px;
      text-shadow: 0 1px 2px rgba(0,0,0,0.1);
      animation: pulseText 2s ease-in-out infinite;
    }

    @keyframes pulseText {
      0%, 100% { opacity: 0.7; }
      50% { opacity: 1; }
    }

    /* ==========================================================================
       3. ОСНОВНОЙ ЭКРАН -- ПИСЬМО
       ========================================================================== */
    .letter-screen {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 40px 15px 80px;
      opacity: 0;
      pointer-events: none;
      transition: opacity 1s ease 0.5s;
      z-index: 50;
    }

    .letter-screen.visible {
      opacity: 1;
      pointer-events: auto;
    }

    .letter-container {
      position: relative;
      width: 100%;
      max-width: 680px;
      background-color: var(--paper-color);
      background-image: 
        radial-gradient(ellipse at center, rgba(243, 235, 216, 0.6) 0%, rgba(224, 210, 189, 0.4) 100%),
        repeating-linear-gradient(0deg, transparent, transparent 31px, rgba(184, 163, 140, 0.12) 32px);
      border: 1px solid #d4c2a8;
      border-radius: 6px;
      padding: 50px 45px;
      box-shadow: 0 20px 40px rgba(44, 29, 17, 0.2), inset 0 0 60px rgba(184, 163, 140, 0.25);
    }

    /* Винтажное кружево по краям */
    .lace-border {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      border: 12px double rgba(212, 131, 147, 0.25);
      pointer-events: none;
      margin: 8px;
      border-radius: 4px;
    }

    /* Текст письма */
    .letter-content {
      font-family: var(--font-hand);
      font-size: 1.85rem;
      line-height: 1.8;
      color: var(--ink-color);
      white-space: pre-wrap;
      word-break: break-word;
      position: relative;
      z-index: 2;
    }

    /* Чернильное перо для анимации написания */
    .quill-pen {
      position: absolute;
      width: 45px;
      height: 45px;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%237a2021"><path d="M20 2c-4 0-10 2-14 8-3 4-4 8-4 8s4-1 8-4c6-4 8-10 8-10z"/></svg>');
      background-repeat: no-repeat;
      pointer-events: none;
      transition: transform 0.1s linear;
      display: none;
      z-index: 10;
      transform: translate(-10px, -35px);
    }

    /* Декоративные элементы и Пушины */
    .pusheen-corner {
      position: absolute;
      bottom: 25px;
      right: 25px;
      width: 90px;
      height: auto;
      opacity: 0.85;
      pointer-events: none;
    }

    /* Панель управления (Музыка и Пауза) */
    .control-panel {
      position: fixed;
      bottom: 20px;
      right: 20px;
      display: flex;
      gap: 10px;
      z-index: 200;
    }

    .ctrl-btn {
      background: rgba(252, 248, 242, 0.9);
      border: 1px solid var(--dusty-pink);
      color: var(--accent-burgundy);
      width: 44px;
      height: 44px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.2rem;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      transition: all 0.3s ease;
    }

    .ctrl-btn:hover {
      background: var(--dusty-pink);
      color: #fff;
      transform: scale(1.08);
    }

    /* Падающие лепестки */
    .petal {
      position: fixed;
      top: -20px;
      background-color: var(--soft-pink);
      border-radius: 150% 0 150% 0;
      opacity: 0.7;
      pointer-events: none;
      animation: fallPetal linear infinite;
      z-index: 1;
    }

    @keyframes fallPetal {
      0% {
        transform: translateY(-20px) rotate(0deg) translateX(0);
        opacity: 0.8;
      }
      50% {
        transform: translateY(50vh) rotate(180deg) translateX(30px);
      }
      100% {
        transform: translateY(105vh) rotate(360deg) translateX(-20px);
        opacity: 0;
      }
    }

    /* Финальная подпись */
    .final-signature {
      margin-top: 35px;
      text-align: right;
      font-family: var(--font-decor);
      font-size: 2.2rem;
      color: var(--accent-burgundy);
      opacity: 0;
      transition: opacity 1.5s ease;
    }
    .final-signature.visible {
      opacity: 1;
    }

    /* Адаптивность для телефонов */
    @media (max-width: 600px) {
      .letter-container {
        padding: 30px 20px;
      }
      .letter-content {
        font-size: 1.5rem;
        line-height: 1.7;
      }
      .angel-wings {
        width: 65px;
      }
      .angel-wings.left { left: -50px; }
      .angel-wings.right { right: -50px; }
    }
  </style>
</head>
<body>

  <!-- Фоновые падающие лепестки -->
  <div id="petalsContainer"></div>

  <!-- ЭКРАН КОНВЕРТА -->
  <div class="envelope-screen" id="envelopeScreen">
    <div class="envelope-wrapper" id="envelopeWrapper" onclick="openLetter()">
      <!-- Левое крыло ангела -->
      <svg class="angel-wings left" viewBox="0 0 100 150" fill="none">
        <path d="M90 10 C60 10 20 40 10 80 C5 100 15 130 30 145 C40 120 45 90 70 70 C85 55 95 30 90 10 Z" fill="#fff" stroke="#ebdcd0" stroke-width="2"/>
        <path d="M80 30 C55 35 30 60 20 95 C30 90 45 75 60 65 C75 50 82 40 80 30 Z" fill="#fcf8f2"/>
      </svg>

      <!-- Конверт -->
      <div class="envelope" id="envelope">
        <div class="envelope-flap"></div>
        <div class="envelope-heart"></div>
      </div>

      <!-- Правое крыло ангела -->
      <svg class="angel-wings right" viewBox="0 0 100 150" fill="none">
        <path d="M90 10 C60 10 20 40 10 80 C5 100 15 130 30 145 C40 120 45 90 70 70 C85 55 95 30 90 10 Z" fill="#fff" stroke="#ebdcd0" stroke-width="2"/>
        <path d="M80 30 C55 35 30 60 20 95 C30 90 45 75 60 65 C75 50 82 40 80 30 Z" fill="#fcf8f2"/>
      </svg>
    </div>
    <div class="tap-instruction">Tap the little heart ♡</div>
  </div>

  <!-- ЭКРАН РАСКРЫТОГО ПИСЬМА -->
  <div class="letter-screen" id="letterScreen">
    <div class="letter-container">
      <div class="lace-border"></div>
      
      <!-- Текст письма с чернильным пером -->
      <div class="letter-content" id="letterContent"></div>
      <div class="quill-pen" id="quillPen"></div>

      <!-- Пушин с сердечком (SVG) в углу -->
      <svg class="pusheen-corner" viewBox="0 0 100 100" fill="none">
        <ellipse cx="50" cy="60" rx="32" ry="22" fill="#a89f91"/>
        <polygon points="25,42 32,25 42,38" fill="#a89f91"/>
        <polygon points="58,38 68,25 75,42" fill="#a89f91"/>
        <circle cx="39" cy="53" r="2.5" fill="#2d251e"/>
        <circle cx="61" cy="53" r="2.5" fill="#2d251e"/>
        <path d="M47 58 Q50 61 53 58" stroke="#2d251e" stroke-width="1.5" fill="none"/>
        <path d="M50 45 C50 45 42 38 42 33 C42 29 46 27 50 31 C54 27 58 29 58 33 C58 38 50 45 50 45 Z" fill="#ff85a2"/>
      </svg>

      <div class="final-signature" id="finalSignature">твой мальчик ♡</div>
    </div>
  </div>

  <!-- ПАНЕЛЬ УПРАВЛЕНИЯ (МУЗЫКА И ПАУЗА) -->
  <div class="control-panel">
    <button class="ctrl-btn" id="pauseBtn" onclick="toggleTypingPause()" title="Пауза / Продолжить печать" style="display:none;">⏸</button>
    <button class="ctrl-btn" id="musicBtn" onclick="toggleMusic()" title="Включить / Выключить музыку">🎵</button>
  </div>

  <!-- АУДИО (Wave to Earth - Love instrumental / Romantic Piano) -->
  <audio id="bgMusic" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/05/27/audio_1808fbf07a.mp3?filename=romantic-piano-112199.mp3" type="audio/mpeg">
  </audio>

  <!-- СКРИПТ АНИМАЦИИ И ЛОГИКИ -->
  <script>
    // ПОЛНЫЙ ТЕКСТ ПИСЬМА (сохранен каждый абзац, обращения и детали)
    const fullText = `Моя девочка, моя милая, моя жаным...

Сегодня ровно месяц, как мы вместе. Один месяц рядом, а впереди ещё столько всего. 
 целый месяц, как ты делаешь меня счастливым. каждый день, проведённый с тобой делает меня самым счастливым мальчиком на свете. 
и знаешь, я хочу написать все все самого начала когда я даже не думал что однажды ты станешь для меня настолько особенной
Всё началось с 7 марта -- нашей первой встречи. 
я помню тот день, когда мы впервые увиделись. помню тот вечер когда я не обратил на тебя внимания
если задуматся то это не так
потому что внутри меня что то было, чувство, которое я тогда просто не понял я правда не знаю, что это было. 

В июле я заметил тебя в TikTok, твои видео, которые я потом показывал Азизу. 
проходит время, я остаюсь один работал каждый день. и я помню тот день когда увидел что ты заходила на мой аккаунт в тиктоке. точно не помню, но кажется это было с 20 по 27 июля.
я помню, как показывал тебя всем подряд
первым был азиз. я показывал ему твои видео, смотрел на тебя, улыбался и восхищался тобой
вот именно тогда внутри меня было такое, что я не могу объяснить словами. это нужно почувствовать, чтобы понять, что я чувствовал когда смотрел на тебя.
я продолжил работать, как обычно и вроде бы забыл об этом. но все равно заходил к тебе на аккаунт, смотрел твои видео, наблюдал за тобой. сам не понимал зачем,
меня тянуло к тебе

Были моменты, когда я выходил на улицу во время работы и чувствовал себя так, будто кого-то искал. 
если честно, я сам до сих пор не понимаю зачем это делал. будто что то искал или кого то, либо тебя
я  просто сидел на работе, потом мог  встать и пойти на улицу. сидеть там час, полтора, смотреть на всех, разглядывать всех , будто ждал чего то
со стороны это наверно выглядело странна очент 
но иногда мне кажется, что сердце чувствует кого то, когда мы сами понимаем, может, я ничего и не искал, а просто не знал, кого мне так хотелось увидеть
ты была так близко ко мне

2 сентября пришло сообщение от Ислама, и так началось наше знакомство. 
утром я просыпаюсь, и ислам пишет мне о тебе. говорит, что ты хочешь со мной познакомиться. я помню тот день когда я написал «пока не хочу»
Жаным, я  написал так не потому что  не хотел с тобой познакомиться. я просто не знал, как сказать, что одновременно и хочу, и боюсь. хотел ответить так, чтобы это не звучало как отказ. в итоге написал чат гпт
 
Но твои  100 тенге тогда буквально украли моё сердце.
я не знаю почему это так сильно меня зацепил. вроде бы 100 тенге, но для меня она это было  чем то особенным. ты сама наверное даже не представляла, что этими 100 тенге заставишь меня страдать , думая о тебе целую ночь, и ждать пока ты мне напишешь
я ждал, когда ты напишешь мне. постоянно думал о тебе, проверял телефон, и чем дольше я ждал, тем сильнее ты стала для меня не просто девочка, которая мне интересна
ты начала становится тем с кем я хотел быть 

6 сентября -- день нашей встречи.
когда я ехал к тебе, у меня в голове было столько мыслей. а вдруг я тебе не понравлюсь а вдруг что то пойдет не так
но когда я был рядом с тобой, я больше не хотел думать об этом потому что в моей голове была только ты.

А помнишь день, когда ты позаботилась обо мне и заказала мне покушать? В тот момент я так почувствовал твою заботу. 
в этот день я влюбился в тебя 
я не думал , что ты после работы закажешь мне покушать. что ты будешь думать обо мне, 
чтобы я не был голодным 
и для меня это было настолько мило, ты даже не представляешь.
и дело даже не в том что ты заказала мне еду, дело в тебе. в твоей заботе, в том, что ты подумала обо мне
в тот момент я почувствовал, что рядом со мной человек, которому не все равно.
и, наверное, именно тогда я понял что я твой, только твой

Моя любовь, моя жаным, ты стала для меня самым дорогим человеком. Если бы можно было начать всё сначала, я бы прожил каждую секунду наших моментов.
я люблю тебя. очень сильно.
не передать слова насколько много ты для меня значишь, и насколько сильно я тебя люблю.

мне хочется, чтобы ты всегда знала как сильно я тебя люблю. чтобы ты никогда не думала что я могу тебя разлюбить, потому что ты для меня особенная. 
я надеюсь, ты помнишь все милые слова, которые я тебе говорил, я хочу, чтобы ты знала я никогда не устану говорить тебе о своих чувствах
я люблю твои глазки, когда они светятся. люблю смотреть на тебя, люблю когда ты  стесняешься. люблю когда ты смотришь на меня, улыбаешься, как держишь меня за руку. люблю моменты, когда мы просто рядом
я люблю каждую секунду с тобой, потому что во всём этом есть ты.
и самое главное, жаным, с тобой я по настоящему чувствую себя счастливым.

Я хочу, чтобы ты могла смотреть на меня и знать, что рядом с тобой человек, которому ты действительно дорога. чтобы ты могла быть собой, не боялась показывать свои чувства и всегда помнила, что для меня ты не просто моя девушка.

ты человек, которого я очень сильно люблю, и буду любить
я люблю тебя, моя девочка. люблю твои глазки, твою улыбку, твою нежность, твою заботу и все то, что делает тебя именно тобой

пусть это будет только начало нашей истории. я хочу ещё много раз говорить тебе, как сильно я тебя люблю, еще много раз обнимать тебя, держать за руку, целовать и видеть как ты стесняешься, когда я смотрю на тебя.
и если ты когда-нибудь спросишь меня, почему именно ты, я, наверное, не смогу назвать одну конкретную причину.
потому что дело не в чем то одном.
дело во всем, что связано с тобой.

Это только начало нашей истории...`;

    let typingIndex = 0;
    let isPaused = false;
    let isPlayingMusic = false;
    const typingSpeed = 35; // скорость печати (мс на символ)

    // Создание падающих лепестков
    function createPetals() {
      const container = document.getElementById('petalsContainer');
      for (let i = 0; i < 15; i++) {
        const petal = document.createElement('div');
        petal.className = 'petal';
        petal.style.left = Math.random() * 100 + 'vw';
        petal.style.top = (Math.random() * -20) + 'vh';
        petal.style.width = (Math.random() * 10 + 10) + 'px';
        petal.style.height = (Math.random() * 15 + 15) + 'px';
        petal.style.animationDuration = (Math.random() * 8 + 7) + 's';
        petal.style.animationDelay = (Math.random() * 5) + 's';
        container.appendChild(petal);
      }
    }

    // Открытие конверта и запуск письма
    function openLetter() {
      const envelope = document.getElementById('envelope');
      const envelopeScreen = document.getElementById('envelopeScreen');
      const letterScreen = document.getElementById('letterScreen');
      const bgMusic = document.getElementById('bgMusic');
      const pauseBtn = document.getElementById('pauseBtn');

      // Запуск музыки
      bgMusic.play().then(() => {
        isPlayingMusic = true;
        document.getElementById('musicBtn').innerText = '🎶';
      }).catch(e => console.log("Автовоспроизведение заблокировано браузером"));

      // Анимация открытия конверта
      envelope.classList.add('open');

      setTimeout(() => {
        envelopeScreen.classList.add('hidden');
        letterScreen.classList.add('visible');
        pauseBtn.style.display = 'flex';
        startTyping();
      }, 900);
    }

    // Постепенная печать текста с перьевой ручкой
    function startTyping() {
      const contentEl = document.getElementById('letterContent');
      const quill = document.getElementById('quillPen');
      quill.style.display = 'block';

      function typeChar() {
        if (isPaused) {
          setTimeout(typeChar, 200);
          return;
        }

        if (typingIndex < fullText.length) {
          let char = fullText.charAt(typingIndex);
          contentEl.textContent += char;
          typingIndex++;

          // Движение пера около текста
          const rect = contentEl.getBoundingClientRect();
          // Простая имитация движения ручки внизу текста
          quill.style.transform = `translate(${Math.random() * 5 + 10}px, ${contentEl.offsetHeight - 20}px)`;

          // Естественные паузы после знаков препинания
          let delay = typingSpeed;
          if (['.', '!', '?', '--'].includes(char)) {
            delay = 350;
          } else if ([',', '...'].includes(char)) {
            delay = 180;
          }

          setTimeout(typeChar, delay);
        } else {
          // Завершение печати
          quill.style.display = 'none';
          document.getElementById('finalSignature').classList.add('visible');
          document.getElementById('pauseBtn').style.display = 'none';
        }
      }

      typeChar();
    }

    // Пауза / Продолжить печать
    function toggleTypingPause() {
      isPaused = !isPaused;
      document.getElementById('pauseBtn').innerText = isPaused ? '▶' : '⏸';
    }

    // Управление музыкой
    function toggleMusic() {
      const bgMusic = document.getElementById('bgMusic');
      const musicBtn = document.getElementById('musicBtn');
      if (isPlayingMusic) {
        bgMusic.pause();
        musicBtn.innerText = '🔇';
      } else {
        bgMusic.play();
        musicBtn.innerText = '🎶';
      }
      isPlayingMusic = !isPlayingMusic;
    }

    // Инициализация при загрузке
    window.onload = () => {
      createPetals();
    };
  </script>
</body>
</html>
