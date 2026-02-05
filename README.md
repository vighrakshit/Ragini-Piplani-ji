<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Ragini, Will You Be My Valentine?</title>
  <style>
    body {
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      font-family: 'Arial', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      text-align: center;
      color: #fff;
      overflow: hidden;
    }

    .container {
      background: rgba(255, 255, 255, 0.15);
      padding: 35px;
      border-radius: 20px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
      max-width: 420px;
      position: relative;
      z-index: 2;
    }

    h1 {
      font-size: 2.1rem;
      margin-bottom: 15px;
    }

    .slideshow {
      position: relative;
      width: 220px;
      height: 220px;
      margin: 0 auto 15px;
      border-radius: 50%;
      overflow: hidden;
      border: 4px solid white;
    }

    .slideshow img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      position: absolute;
      top: 0;
      left: 0;
      opacity: 0;
      transition: opacity 1s ease-in-out;
    }

    .slideshow img.active {
      opacity: 1;
    }

    .buttons {
      margin-top: 15px;
      position: relative;
      height: 80px;
    }

    button {
      font-size: 1.2rem;
      padding: 12px 25px;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      margin: 10px;
      transition: all 0.2s ease;
    }

    #yesBtn {
      background-color: #ff4d6d;
      color: white;
    }

    #noBtn {
      background-color: #fff;
      color: #ff4d6d;
      position: fixed;
      z-index: 3;
    }

    #message {
      margin-top: 20px;
      font-size: 1.6rem;
      display: none;
    }

    #signature {
      margin-top: 12px;
      font-size: 1.3rem;
      display: none;
    }

    /* Floating hearts */
    .heart {
      position: fixed;
      bottom: -20px;
      font-size: 24px;
      animation: floatUp 6s linear infinite;
      opacity: 0.8;
      z-index: 1;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(0) scale(1);
        opacity: 0.9;
      }
      100% {
        transform: translateY(-100vh) scale(1.5);
        opacity: 0;
      }
    }

    /* Modal Styles */
    .modal {
      display: none;
      position: fixed;
      z-index: 10;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
      justify-content: center;
      align-items: center;
      animation: fadeIn 0.5s ease;
    }

    .modal-content {
      background: linear-gradient(135deg, #ff758c, #ff7eb3);
      padding: 30px;
      border-radius: 20px;
      max-width: 400px;
      text-align: center;
      color: white;
      box-shadow: 0 0 30px rgba(0,0,0,0.4);
      animation: popIn 0.5s ease;
    }

    .modal-content h2 {
      font-size: 2rem;
      margin-bottom: 15px;
    }

    .modal-content p {
      font-size: 1.2rem;
      line-height: 1.5;
    }

    .close-btn {
      margin-top: 20px;
      padding: 10px 20px;
      border: none;
      border-radius: 20px;
      background: white;
      color: #ff4d6d;
      font-size: 1rem;
      cursor: pointer;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    @keyframes popIn {
      from { transform: scale(0.7); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }
  </style>
</head>
<body>

  <!-- Background Music -->
  <audio id="bgMusic" loop>
    <source src="music.mp3" type="audio/mpeg">
  </audio>

  <div class="container">
    <div class="slideshow">
      <img src="ragini1.jpg" class="active" alt="Ragini Photo 1">
      <img src="ragini2.jpg" alt="Ragini Photo 2">
      <img src="ragini3.jpg" alt="Ragini Photo 3">
    </div>

    <h1>💖 Ragini, will you be my Valentine? 💖</h1>

    <div class="buttons">
      <button id="yesBtn" onclick="sayYes()">Yes 💘</button>
    </div>

    <div id="message">YAY Ragini!!! I love you so much ❤️🥰</div>
    <div id="signature">Forever yours,<br>Hrakshit Vig 💌</div>
  </div>

  <!-- Floating No Button -->
  <button id="noBtn">No 😢</button>

  <!-- Modal -->
  <div id="loveModal" class="modal">
    <div class="modal-content">
      <h2>💖 For You, Ragini 💖</h2>
      <p>
        No matter what happens, I’m always here for you. <br><br>
        I always got your back — today, tomorrow, and forever. ❤️<br><br>
        Love you endlessly, <br>
        — Hrakshit 💌
      </p>
      <button class="close-btn" onclick="closeModal()">Close 💕</button>
    </div>
  </div>

  <script>
    // Play music on first interaction
    document.body.addEventListener('click', () => {
      const music = document.getElementById('bgMusic');
      if (music.paused) {
        music.play().catch(() => {});
      }
    }, { once: true });

    function sayYes() {
      document.getElementById("message").style.display = "block";
      document.getElementById("signature").style.display = "block";
      document.getElementById("loveModal").style.display = "flex";
      stopFloatingNo();
    }

    function closeModal() {
      document.getElementById("loveModal").style.display = "none";
    }

    // Floating No button logic
    const noBtn = document.getElementById("noBtn");
    let floatInterval;

    function startFloatingNo() {
      moveNo();
      floatInterval = setInterval(moveNo, 1200);
    }

    function stopFloatingNo() {
      clearInterval(floatInterval);
      noBtn.style.display = "none";
    }

    function moveNo() {
      const x = Math.random() * (window.innerWidth - 120);
      const y = Math.random() * (window.innerHeight - 60);
      noBtn.style.left = x + "px";
      noBtn.style.top = y + "px";
    }

    startFloatingNo();

    // Floating hearts generator
    function createHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.textContent = '💖';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.fontSize = (16 + Math.random() * 24) + 'px';
      heart.style.animationDuration = (4 + Math.random() * 4) + 's';
      document.body.appendChild(heart);

      setTimeout(() => {
        heart.remove();
      }, 8000);
    }

    setInterval(createHeart, 500);

    // Slideshow logic
    const slides = document.querySelectorAll('.slideshow img');
    let currentSlide = 0;

    setInterval(() => {
      slides[currentSlide].classList.remove('active');
      currentSlide = (currentSlide + 1) % slides.length;
      slides[currentSlide].classList.add('active');
    }, 3000);
  </script>

</body>
</html>
