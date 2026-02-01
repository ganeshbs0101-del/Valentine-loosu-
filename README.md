<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Be My Valentine?</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            overflow: hidden;
            touch-action: manipulation;
        }

        .cursive { font-family: 'Dancing Script', cursive; }

        .bg-heart {
            position: absolute;
            top: -10%;
            color: rgba(255, 192, 203, 0.6);
            animation: floatDown linear infinite;
            z-index: 0;
            user-select: none;
            pointer-events: none;
        }

        @keyframes floatDown {
            0% { transform: translateY(-10vh) rotate(0deg); opacity: 0; }
            10% { opacity: 0.8; }
            100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
        }

        .slide {
            display: none;
            animation: fadeIn 0.8s ease-in-out forwards;
        }
        
        .slide.active { display: flex; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .btn-pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(244, 63, 94, 0.7); }
            70% { box-shadow: 0 0 0 20px rgba(244, 63, 94, 0); }
            100% { box-shadow: 0 0 0 0 rgba(244, 63, 94, 0); }
        }

        .confetti {
            position: absolute;
            width: 10px; height: 10px;
            animation: confetti-fall 3s linear forwards;
            z-index: 50;
            pointer-events: none;
        }

        @keyframes confetti-fall {
            0% { transform: translateY(-10vh) rotate(0deg); }
            100% { transform: translateY(110vh) rotate(720deg); }
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.6);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 8px 32px 0 rgba(255, 105, 135, 0.2);
            transition: all 0.3s ease;
        }

        .loader {
            border: 3px solid #f3f3f3;
            border-top: 3px solid #db2777;
            border-radius: 50%;
            width: 24px; height: 24px;
            animation: spin 1s linear infinite;
            display: inline-block;
        }

        @keyframes spin { 100% { transform: rotate(360deg); } }
        
        #yesBtn { transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), font-size 0.2s ease; }
        #noBtn { transition: all 0.2s ease; cursor: pointer; }
    </style>
</head>
<body class="bg-gradient-to-br from-rose-100 via-pink-100 to-rose-200 h-screen w-screen flex items-center justify-center relative p-4">

    <div id="bg-container" class="absolute inset-0 pointer-events-none overflow-hidden"></div>

    <div id="main-card" class="glass-card w-full max-w-lg p-6 md:p-8 rounded-3xl relative z-10 flex flex-col items-center justify-center min-h-[500px] text-center transition-all duration-500">
        
        <!-- Slide 0 -->
        <div id="slide-0" class="slide active flex-col items-center justify-center w-full">
            <div class="text-6xl mb-6 animate-bounce">💕</div>
            <h1 class="text-3xl md:text-4xl text-rose-600 mb-4 cursive font-bold">Hey my love...</h1>
            <p class="text-lg text-gray-700 mb-8 font-semibold">I made something special just for you.</p>
        </div>

        <!-- Slide 1 -->
        <div id="slide-1" class="slide flex-col items-center justify-center w-full">
            <div class="text-6xl mb-6 text-pink-500">🌸</div>
            <h2 class="text-2xl md:text-3xl text-rose-700 mb-6 cursive">"You make my world brighter and my heart happier."</h2>
        </div>

        <!-- Slide 2 -->
        <div id="slide-2" class="slide flex-col items-center justify-center w-full">
            <div class="text-6xl mb-6 text-red-500 animate-pulse">❤️</div>
            <h2 class="text-2xl md:text-3xl text-rose-800 mb-6 cursive">"You are my favorite thought, my safest place, my forever."</h2>
        </div>

        <!-- Slide 3: The Dynamic Question -->
        <div id="slide-3" class="slide flex-col items-center justify-center w-full relative h-full min-h-[300px]">
            <div class="text-6xl mb-4">💘</div>
            <h1 id="question-text" class="text-4xl md:text-5xl text-rose-600 mb-8 cursive font-bold z-20">Will you be my Valentine?</h1>
            
            <div id="button-area" class="flex flex-col md:flex-row gap-6 items-center justify-center w-full min-h-[150px] relative">
                <button id="yesBtn" onclick="handleYes()" class="bg-rose-500 hover:bg-rose-600 text-white font-bold py-3 px-10 rounded-full shadow-lg btn-pulse text-xl z-30">
                    YES 💖
                </button>
                <button id="noBtn" class="bg-gray-300 text-gray-600 font-bold py-3 px-8 rounded-full shadow-md z-20 whitespace-nowrap">
                    NO 😅
                </button>
            </div>
        </div>

        <!-- Slide 4: Celebration -->
        <div id="slide-4" class="slide flex-col items-center justify-center w-full">
            <div class="text-7xl mb-4 animate-bounce">🌹</div>
            <h1 class="text-4xl md:text-5xl text-rose-600 mb-2 cursive font-bold">Happy Valentine’s Day!</h1>
            <p class="text-xl text-rose-800 font-bold cursive mb-6">I choose you—always.</p>
            
            <div class="w-full bg-white/40 rounded-xl p-4 mt-2 shadow-inner">
                <p class="text-rose-700 text-sm font-semibold mb-3">✨ Ask AI Cupid for a surprise ✨</p>
                <div class="flex flex-wrap gap-2 justify-center mb-3">
                    <button onclick="generatePoem()" id="btn-poem" class="bg-pink-500 hover:bg-pink-600 text-white text-xs md:text-sm font-bold py-2 px-4 rounded-full transition-all">Write a Poem ✨</button>
                    <button onclick="generateDate()" id="btn-date" class="bg-indigo-500 hover:bg-indigo-600 text-white text-xs md:text-sm font-bold py-2 px-4 rounded-full transition-all">Plan a Date ✨</button>
                </div>
                <div id="ai-result-container" class="hidden min-h-[60px] flex items-center justify-center">
                    <div id="loader" class="loader hidden"></div>
                    <div id="ai-content" class="text-rose-900 text-sm italic px-2 whitespace-pre-wrap"></div>
                </div>
            </div>
        </div>

        <div id="nav-container" class="mt-8 z-40">
            <button onclick="nextSlide()" class="bg-white text-rose-500 border-2 border-rose-200 hover:bg-rose-50 font-semibold py-2 px-6 rounded-full flex items-center gap-2">
                Next 💖
            </button>
        </div>
    </div>

    <script>
        const apiKey = "";
        let currentSlide = 0;
        let yesScale = 1;
        let noScale = 1;
        const slides = document.querySelectorAll('.slide');
        const navContainer = document.getElementById('nav-container');
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const bgContainer = document.getElementById('bg-container');
        const mainCard = document.getElementById('main-card');

        // Background Hearts
        setInterval(() => {
            const heart = document.createElement('div');
            heart.classList.add('bg-heart');
            heart.innerHTML = Math.random() > 0.5 ? '❤️' : '🌸';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = Math.random() * 3 + 4 + 's'; 
            bgContainer.appendChild(heart);
            setTimeout(() => heart.remove(), 7000);
        }, 600);

        function nextSlide() {
            slides[currentSlide].classList.remove('active');
            currentSlide++;
            slides[currentSlide].classList.add('active');

            if (currentSlide === 3) {
                navContainer.style.display = 'none';
                initGrowthLogic();
            } else if (currentSlide === 4) {
                navContainer.style.display = 'none';
                startCelebration();
            }
        }

        function initGrowthLogic() {
            const manipulateButtons = (e) => {
                if (e.type === 'touchstart') e.preventDefault();

                // Grow YES
                yesScale += 0.4;
                yesBtn.style.transform = `scale(${yesScale})`;

                // Shrink NO
                noScale = Math.max(0.1, noScale - 0.15);
                noBtn.style.transform = `scale(${noScale})`;
                if (noScale < 0.2) noBtn.style.opacity = "0.5";

                // Move NO Button
                const area = document.getElementById('slide-3');
                const rect = area.getBoundingClientRect();
                const btnRect = noBtn.getBoundingClientRect();
                
                noBtn.style.position = 'absolute';
                const maxX = rect.width - btnRect.width;
                const maxY = rect.height - btnRect.height;
                
                noBtn.style.left = Math.random() * maxX + 'px';
                noBtn.style.top = Math.random() * maxY + 'px';

                // If Yes gets too big, make it take over
                if (yesScale > 4) {
                    yesBtn.style.zIndex = "100";
                    mainCard.style.overflow = "visible";
                }
            };

            noBtn.addEventListener('mouseover', manipulateButtons);
            noBtn.addEventListener('touchstart', manipulateButtons);
            noBtn.addEventListener('click', manipulateButtons);
        }

        function handleYes() {
            nextSlide();
        }

        // Gemini AI Functions
        async function callGemini(prompt) {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            const delays = [1000, 2000, 4000];
            for (let i = 0; i < delays.length; i++) {
                try {
                    const response = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
                    });
                    const data = await response.json();
                    return data.candidates[0].content.parts[0].text;
                } catch (e) {
                    if (i === delays.length - 1) return "Cupid is a bit busy! ❤️";
                    await new Promise(r => setTimeout(r, delays[i]));
                }
            }
        }

        async function generatePoem() {
            toggleAI(true);
            const text = await callGemini("Write a very short 4-line romantic rhyme for Valentine's Day with emojis.");
            displayAI(text);
        }

        async function generateDate() {
            toggleAI(true);
            const text = await callGemini("Suggest one unique romantic date idea in 15 words or less.");
            displayAI(text);
        }

        function toggleAI(loading) {
            document.getElementById('ai-result-container').classList.remove('hidden');
            document.getElementById('loader').classList.toggle('hidden', !loading);
            document.getElementById('ai-content').textContent = '';
        }

        function displayAI(t) {
            document.getElementById('loader').classList.add('hidden');
            document.getElementById('ai-content').textContent = t;
        }

        function startCelebration() {
            const colors = ['#ff0000', '#ff69b4', '#ffffff', '#ff1493'];
            for (let i = 0; i < 120; i++) {
                setTimeout(() => {
                    const c = document.createElement('div');
                    c.classList.add('confetti');
                    c.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    c.style.left = Math.random() * 100 + 'vw';
                    c.style.animationDuration = Math.random() * 2 + 2 + 's';
                    c.style.width = Math.random() * 10 + 5 + 'px';
                    c.style.height = c.style.width;
                    document.body.appendChild(c);
                    setTimeout(() => c.remove(), 4000);
                }, i * 40);
            }
        }
    </script>
</body>
</html>
