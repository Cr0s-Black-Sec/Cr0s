<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Cr0s Dice</title>
    
    <!-- Configuración para iPhone (PWA Nativa) -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Cr0s">
    
    <!-- Icono de la App para iOS (Generado en SVG/Base64 con branding Cr0s) -->
    <link rel="apple-touch-icon" href="data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180' viewBox='0 0 180 180'><rect width='180' height='180' rx='40' fill='%23121212'/><rect x='35' y='35' width='110' height='110' rx='22' fill='%231e1e1e' stroke='%23333333' stroke-width='4'/><circle cx='65' cy='65' r='10' fill='%2300ffcc'/><circle cx='115' cy='115' r='10' fill='%2300ffcc'/><circle cx='90' cy='90' r='10' fill='%2300ffcc'/><text x='90' y='160' font-family='Arial, sans-serif' font-weight='900' font-size='16' fill='%2300ffcc' text-anchor='middle' letter-spacing='2'>Cr0s</text></svg>">

    <style>
        * {
            box-sizing: border-box;
            user-select: none;
            -webkit-user-select: none;
            -webkit-touch-callout: none;
        }
        body {
            margin: 0;
            padding: 0;
            width: 100vw;
            height: 100vh;
            background-color: #0a0a0a;
            color: #ffffff;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            overflow: hidden;
        }
        header {
            margin-top: 60px;
            text-align: center;
        }
        .brand {
            font-size: 28px;
            font-weight: 900;
            letter-spacing: 4px;
            color: #00ffcc;
            text-transform: uppercase;
            text-shadow: 0 0 12px rgba(0, 255, 204, 0.4);
        }
        .subtitle {
            font-size: 12px;
            color: #666;
            margin-top: 4px;
            letter-spacing: 1px;
        }
        .dice-container {
            perspective: 1000px;
            width: 140px;
            height: 140px;
        }
        .dice {
            width: 100%;
            height: 100%;
            background: linear-gradient(145deg, #1e1e1e, #141414);
            border: 2px solid #333;
            border-radius: 28px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8), inset 0 2px 4px rgba(255,255,255,0.1);
            display: grid;
            grid-template: repeat(3, 1fr) / repeat(3, 1fr);
            padding: 16px;
            transition: transform 0.15s ease-out;
        }
        .dot {
            width: 18px;
            height: 18px;
            background-color: #00ffcc;
            border-radius: 50%;
            justify-self: center;
            align-self: center;
            box-shadow: 0 0 8px rgba(0, 255, 204, 0.6);
            opacity: 0;
        }
        /* Posicionamiento de puntos según valor */
        .val-1 .d5 { opacity: 1; }
        .val-2 .d1, .val-2 .d9 { opacity: 1; }
        .val-3 .d1, .val-3 .d5, .val-3 .d9 { opacity: 1; }
        .val-4 .d1, .val-4 .d3, .val-4 .d7, .val-4 .d9 { opacity: 1; }
        .val-5 .d1, .val-5 .d3, .val-5 .d5, .val-5 .d7, .val-5 .d9 { opacity: 1; }
        .val-6 .d1, .val-6 .d3, .val-6 .d4, .val-6 .d6, .val-6 .d7, .val-6 .d9 { opacity: 1; }

        .controls {
            margin-bottom: 60px;
            width: 100%;
            padding: 0 30px;
        }
        .btn-roll {
            width: 100%;
            padding: 18px;
            background: #00ffcc;
            color: #000;
            border: none;
            border-radius: 16px;
            font-size: 18px;
            font-weight: 700;
            letter-spacing: 1px;
            box-shadow: 0 8px 24px rgba(0, 255, 204, 0.3);
            active: scale(0.98);
        }
        .rolling {
            animation: shake 0.4s infinite ease-in-out;
        }
        @keyframes shake {
            0% { transform: rotate(0deg) scale(1); }
            25% { transform: rotate(-12deg) scale(0.95); }
            75% { transform: rotate(12deg) scale(1.05); }
            100% { transform: rotate(0deg) scale(1); }
        }
    </style>
</head>
<body>

    <header>
        <div class="brand">Cr0s</div>
        <div class="subtitle">DICE UTILITY</div>
    </header>

    <div class="dice-container">
        <div class="dice val-1" id="dice">
            <div class="dot d1"></div><div class="dot d2"></div><div class="dot d3"></div>
            <div class="dot d4"></div><div class="dot d5"></div><div class="dot d6"></div>
            <div class="dot d7"></div><div class="dot d8"></div><div class="dot d9"></div>
        </div>
    </div>

    <div class="controls">
        <button class="btn-roll" onclick="rollDice()">LANZAR DADO</button>
    </div>

    <script>
        function rollDice() {
            const dice = document.getElementById('dice');
            
            // Vibración háptica nativa en iOS/Mobile
            if (navigator.vibrate) {
                navigator.vibrate(40);
            }

            dice.classList.add('rolling');
            
            setTimeout(() => {
                const result = Math.floor(Math.random() * 6) + 1;
                dice.className = 'dice val-' + result;
                dice.classList.remove('rolling');
            }, 400);
        }
    </script>
</body>
</html>
