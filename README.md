# <!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Whip Slap Game</title>
    <style>
        body { font-family: sans-serif; text-align: center; background: #f0f0f0; overflow: hidden; }
        #game-container { position: relative; width: 100vw; height: 80vh; display: flex; justify-content: center; align-items: center; cursor: crosshair; }
        #target { max-width: 300px; max-height: 300px; transition: transform 0.05s; user-select: none; -webkit-user-drag: none; }
        .slap-effect { transform: scale(0.9) rotate(5deg) !important; filter: brightness(1.5) sepia(1) hue-rotate(-50deg); }
        #ui { padding: 20px; background: white; border-bottom: 2px solid #ddd; }
        .score-board { font-size: 24px; font-weight: bold; color: #ff4757; }
        #whip { position: absolute; width: 100px; pointer-events: none; transform-origin: top left; display: none; }
    </style>
</head>
<body>

<div id="ui">
    <div class="score-board">SCORE: <span id="score">0</span></div>
    <p>対象の画像を選択してください：<input type="file" id="imageInput" accept="image/*"></p>
</div>

<div id="game-container">
    <img id="target" src="https://via.placeholder.com/300?text=Select+Image" alt="target">
</div>

<audio id="slapSound" src="https://www.soundjay.com/human/sounds/slap-01.mp3"></audio>

<script>
    const target = document.getElementById('target');
    const scoreDisplay = document.getElementById('score');
    const imageInput = document.getElementById('imageInput');
    const slapSound = document.getElementById('slapSound');
    let score = 0;

    // 1. 画像の切り替え機能
    imageInput.addEventListener('change', (e) => {
        const file = e.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = (event) => {
                target.src = event.target.result;
            };
            reader.readAsDataURL(file);
            score = 0;
            scoreDisplay.innerText = score;
        }
    });

    // 2. 叩くアクション
    target.addEventListener('mousedown', slap);
    target.addEventListener('touchstart', (e) => {
        e.preventDefault();
        slap();
    });

    function slap() {
        score++;
        scoreDisplay.innerText = score;

        // 音を再生
        slapSound.currentTime = 0;
        slapSound.play();

        // 視覚エフェクト
        target.classList.add('slap-effect');
        setTimeout(() => {
            target.classList.remove('slap-effect');
        }, 100);

        // 少しランダムに跳ねる動き
        const randomX = (Math.random() - 0.5) * 20;
        const randomY = (Math.random() - 0.5) * 20;
        target.style.transform = `translate(${randomX}px, ${randomY}px)`;
    }
</script>

</body>
</html>

2
