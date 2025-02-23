<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sorpresa per Te</title>
  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Quicksand', sans-serif;
      text-align: center;
      background-color: #ffffff; /* Sfondo bianco */
      color: #333;
      margin: 0;
      padding: 20px;
    }
    h1 {
      font-size: 2.5rem;
      margin-bottom: 1rem;
      color: #d63384;
    }
    video {
      width: 90%;
      max-width: 600px;
      margin: 20px 0;
      border-radius: 10px;
    }
    #hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      font-size: 2rem;
      color: #ff0000; /* Rosso per i cuori */
    }
    .hidden {
      display: none;
    }
    .message {
      margin-top: 20px;
      font-size: 1.2rem;
      color: #555;
    }
    button {
      background-color: #d63384;
      color: white;
      border: none;
      padding: 10px 20px;
      font-size: 1rem;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 20px;
    }
    button:hover {
      background-color: #b52a6e;
    }
    @keyframes float {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(-100vh); opacity: 0; }
    }
  </style>
</head>
<body>
  <h1>Una sorpresa solo per te</h1>
  <p>"Perché ogni giorno con te è un giorno speciale."</p>

  <button id="startMusic">Avvia la Musica</button>
  <button id="changeTrack" class="hidden">Cambia Canzone</button>
  <p id="instructions" class="hidden">Puoi cambiare canzone cliccando sul tasto sopra!</p>

  <video id="video" controls>
    <source src="videorara.MP4" type="video/mp4">
    Il tuo browser non supporta il video.
  </video>

  <p class="message hidden" id="finalMessage">Ancora non ti sei stancata? Okay, un'altra canzone per te!</p>

  <div id="hearts"></div>

  <audio id="audio" src="song1.mp3" preload="auto"></audio>

  <script>
    const audioTracks = ["song1.mp3", "song2.mp3", "song3.mp3", "song4.mp3"];
    let currentTrack = 0;
    let shakeCount = 0;

    const audio = document.getElementById('audio');
    const message = document.getElementById('finalMessage');
    const startMusicButton = document.getElementById('startMusic');
    const changeTrackButton = document.getElementById('changeTrack');
    const instructions = document.getElementById('instructions');
    const heartsContainer = document.getElementById('hearts');

    startMusicButton.addEventListener('click', () => {
      audio.play();
      instructions.classList.remove('hidden');
      changeTrackButton.classList.remove('hidden');
      startMusicButton.classList.add('hidden');
    });

    changeTrackButton.addEventListener('click', changeTrack);

    function changeTrack() {
      currentTrack = (currentTrack + 1) % audioTracks.length;
      audio.src = audioTracks[currentTrack];
      audio.play();

      if (currentTrack === 1) { // song2.mp3 triggers the hearts
        showHearts();
      } else {
        heartsContainer.innerHTML = ''; // Clear hearts if not song2
      }

      shakeCount++;
      if (shakeCount === 3) {
        message.classList.remove('hidden');
      }
    }

    // Heart animation
    function showHearts() {
      heartsContainer.innerHTML = ''; // Clear previous hearts
      for (let i = 0; i < 100; i++) { // Increased number of hearts
        const heart = document.createElement('div');
        heart.textContent = '♥️';
        heart.style.position = 'absolute';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.top = 100 + 'vh';
        heart.style.fontSize = Math.random() * 2 + 1 + 'rem';
        heart.style.animation = `float ${Math.random() * 3 + 2}s ease-in infinite`;
        heartsContainer.appendChild(heart);
      }
    }
  </script>
</body>
</html>
