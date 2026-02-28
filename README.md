<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anniversary Celebration</title>
    <style>
        :root {
            --gold: #d4af37;
            --crimson: #8b0000;
            --parchment: #fcf5e5;
        }

        body {
            background-color: #1a1a1a;
            margin: 0;
            font-family: 'Georgia', serif;
            color: #332b1a;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
            text-align: center;
        }

        .page {
            display: none;
            width: 90%;
            max-width: 600px;
            animation: fadeIn 1.2s ease-in-out forwards;
            position: relative;
            z-index: 2;
        }

        .active { display: block; }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }

        /* PAGE 1: THE BELL */
        .bell-container { cursor: pointer; }
        .bell {
            font-size: 100px;
            animation: ring 2s infinite ease-in-out;
            display: inline-block;
            filter: drop-shadow(0 0 15px var(--gold));
        }
        @keyframes ring {
            0%, 100% { transform: rotate(0); }
            25% { transform: rotate(20deg); }
            75% { transform: rotate(-20deg); }
        }

        /* PAGE 2: THE HEART & CELEBRATION */
        .heart-container { cursor: pointer; perspective: 1000px; position: relative; }
        .heart {
            font-size: 140px;
            color: #ff0000;
            display: inline-block;
            animation: rotateHeart 3s infinite linear;
            text-shadow: 0 0 30px rgba(255,0,0,0.6);
            margin-bottom: 20px;
        }
        @keyframes rotateHeart {
            from { transform: rotateY(0deg); }
            to { transform: rotateY(360deg); }
        }

        /* Confetti/Celebration Particles */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: var(--gold);
            top: -10%;
            animation: fall linear forwards;
            z-index: 1;
        }
        @keyframes fall {
            to { transform: translateY(110vh) rotate(360deg); }
        }

        /* PAGE 3: THE TEMPLE */
        .temple-icon { font-size: 120px; color: var(--gold); margin-bottom: 20px; }
        .parchment {
            background: var(--parchment);
            border: 8px double var(--gold);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.9);
            position: relative;
        }

        button {
            background: var(--crimson);
            color: var(--gold);
            border: 2px solid var(--gold);
            padding: 15px 35px;
            font-size: 1.2rem;
            cursor: pointer;
            border-radius: 50px;
            margin-top: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        button:hover {
            background: #a50000;
            transform: scale(1.05);
        }

        h2 { color: var(--crimson); font-size: 1.8rem; }
        p { line-height: 1.8; font-size: 1.3rem; }
        .celebration-title { color: var(--gold); font-size: 2rem; margin-bottom: 30px; letter-spacing: 2px; }
    </style>
</head>
<body>

    <div id="page1" class="page active">
        <div class="celebration-title">✨ నిత్య కల్యాణం ✨</div>
        <div class="bell-container" onclick="goToPage2()">
            <div class="bell">🔔</div>
            <p style="color: white; margin-top: 30px; font-size: 1.2rem;">దీవెనల కోసం గంటను నొక్కండి<br><span style="font-size: 0.9rem; opacity: 0.7;">(Tap the Bell for Blessings)</span></p>
        </div>
    </div>

    <div id="page2" class="page">
        <div class="heart-container" onclick="nextPage(3)">
            <div class="heart">❤️</div>
            <div class="parchment">
                <h2>Happy Anniversary!</h2>
                <p>"To the pillars of our family—may your union be blessed by the heavens with the same strength and grace you show us every day."</p>
                <p style="font-size: 1rem; color: #8b0000; font-weight: bold;">(Click the Heart to visit the Temple)</p>
            </div>
        </div>
    </div>

    <div id="page3" class="page">
        <div class="temple-icon">🛕</div>
        <div class="parchment">
            <div id="telugu-content" style="display: none;">
                <h2 style="font-size: 2rem;">శుభాకాంక్షలు!</h2>
                <p>మీ జంట నూరేళ్లు చల్లగా ఉండాలని, ఆ దేవుడి ఆశీస్సులు మీకు ఎల్లప్పుడూ ఉండాలని కోరుకుంటున్నాను.</p>
                <p>మీ వైవాహిక జీవితం సుఖసంతోషాలతో, ఆరోగ్య ఐశ్వర్యాలతో వర్ధిల్లాలని మనసారా ఆకాంక్షిస్తున్నాను.</p>
                <p><strong>వివాహ వార్షికోత్సవ శుభాకాంక్షలు!</strong></p>
            </div>
            <button id="blessBtn" onclick="revealBlessing()">Get Temple Blessings</button>
        </div>
    </div>

    <script>
        function nextPage(num) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById('page' + num).classList.add('active');
        }

        function goToPage2() {
            nextPage(2);
            startCelebration();
        }

        // Confetti / Celebration effect
        function startCelebration() {
            const colors = ['#d4af37', '#ff0000', '#ffffff', '#ff69b4', '#ffd700'];
            for (let i = 0; i < 100; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.classList.add('confetti');
                    confetti.style.left = Math.random() * 100 + 'vw';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.animationDuration = (Math.random() * 3 + 2) + 's';
                    confetti.style.opacity = Math.random();
                    document.body.appendChild(confetti);
                    
                    // Remove confetti after animation
                    setTimeout(() => confetti.remove(), 5000);
                }, i * 50);
            }
        }

        function revealBlessing() {
            document.getElementById('telugu-content').style.display = 'block';
            document.getElementById('blessBtn').style.display = 'none';
        }
    </script>
</body>
</html>
