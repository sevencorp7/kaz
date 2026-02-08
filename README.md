<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎰 ULTRA CASINO | Telegram Mini App</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Montserrat:wght@800;900&display=swap" rel="stylesheet">
    <style>
        /* ОПТИМИЗАЦИЯ: убираем тяжелые анимации, оставляем только нужные */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        :root {
            --primary: #ff3366;
            --secondary: #33ccff;
            --accent: #ffcc00;
            --success: #00ff88;
            --danger: #ff5555;
            --dark: #0a0a1a;
            --darker: #050510;
            --glass: rgba(255, 255, 255, 0.08);
            --glass-border: rgba(255, 255, 255, 0.15);
        }

        body {
            background: linear-gradient(135deg, var(--darker), var(--dark));
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
            touch-action: manipulation;
            -webkit-tap-highlight-color: transparent;
        }

        /* Оптимизация для мобильных */
        .container {
            max-width: 100%;
            margin: 0 auto;
            padding: 10px;
        }

        /* ШАПКА - оптимизированная */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            border: 1px solid var(--glass-border);
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo i {
            font-size: 2rem;
            color: var(--accent);
        }

        .logo h1 {
            font-size: 1.5rem;
            background: linear-gradient(90deg, var(--primary), var(--accent));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .balance-container {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 10px 15px;
            background: linear-gradient(90deg, rgba(255,51,102,0.2), rgba(51,204,255,0.2));
            border-radius: 15px;
            font-weight: 600;
        }

        /* НАВИГАЦИЯ - упрощенная */
        .nav-tabs {
            display: flex;
            overflow-x: auto;
            gap: 5px;
            margin-bottom: 20px;
            padding: 10px 0;
            -webkit-overflow-scrolling: touch;
        }

        .nav-tabs::-webkit-scrollbar {
            display: none;
        }

        .nav-tab {
            flex-shrink: 0;
            padding: 12px 20px;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 15px;
            color: white;
            cursor: pointer;
            transition: all 0.2s ease;
            white-space: nowrap;
        }

        .nav-tab.active {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            transform: translateY(-2px);
        }

        /* СЕТКА ИГР - оптимизированная */
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }

        @media (max-width: 768px) {
            .games-grid {
                grid-template-columns: 1fr;
            }
        }

        .game-card {
            background: linear-gradient(145deg, rgba(255,255,255,0.05), rgba(0,0,0,0.2));
            border-radius: 20px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid transparent;
            position: relative;
            overflow: hidden;
        }

        .game-card:hover {
            transform: translateY(-5px);
            border-color: var(--primary);
        }

        .game-icon {
            width: 60px;
            height: 60px;
            margin: 0 auto 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            border-radius: 15px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
        }

        .game-info h3 {
            font-size: 1.3rem;
            margin-bottom: 8px;
            text-align: center;
        }

        .game-info p {
            font-size: 0.9rem;
            color: #aaa;
            margin-bottom: 15px;
            text-align: center;
        }

        .play-btn {
            width: 100%;
            padding: 12px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none;
            border-radius: 15px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .play-btn:hover {
            transform: scale(1.05);
        }

        /* ЭКРАНЫ ИГР - оптимизированные */
        .game-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--dark);
            z-index: 1000;
            display: none;
            padding: 20px;
            overflow-y: auto;
        }

        .game-screen.active {
            display: block;
            animation: slideUp 0.3s ease;
        }

        @keyframes slideUp {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .screen-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin-bottom: 20px;
            background: var(--glass);
            border-radius: 20px;
            border: 1px solid var(--glass-border);
        }

        .back-btn {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
        }

        .back-btn:hover {
            background: var(--primary);
        }

        /* СЛОТЫ - оптимизированная версия */
        .slots-container {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            padding: 20px;
            margin: 20px 0;
        }

        .slots-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin: 20px 0;
        }

        .slot-cell {
            aspect-ratio: 1;
            background: linear-gradient(135deg, rgba(255,255,255,0.1), rgba(0,0,0,0.2));
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
            border: 2px solid rgba(255,255,255,0.1);
        }

        .slot-cell.win {
            animation: winFlash 0.3s ease 3;
            border-color: var(--accent);
        }

        @keyframes winFlash {
            50% { transform: scale(1.1); }
        }

        .spin-btn {
            width: 100px;
            height: 100px;
            margin: 20px auto;
            display: block;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary), #ff0066);
            border: none;
            color: white;
            font-size: 1.2rem;
            font-weight: 800;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .spin-btn:hover {
            transform: scale(1.1);
        }

        /* ПОКЕР - оптимизированный */
        .poker-container {
            background: linear-gradient(135deg, #1a5f23, #2e7d32);
            border-radius: 20px;
            padding: 20px;
            margin: 20px 0;
            border: 5px solid #8b4513;
            position: relative;
        }

        .poker-hand {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .poker-card {
            width: 70px;
            height: 100px;
            background: white;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
            color: #c00;
            position: relative;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .poker-card.spade,
        .poker-card.club {
            color: black;
        }

        .poker-suit {
            font-size: 0.8rem;
            position: absolute;
            top: 5px;
            left: 5px;
        }

        .poker-value {
            font-size: 1.2rem;
        }

        /* КОСТИ - оптимизированные */
        .dice-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 30px 0;
        }

        .die {
            width: 80px;
            height: 80px;
            background: white;
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .roll-btn {
            padding: 15px 40px;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            border: none;
            border-radius: 15px;
            color: white;
            font-size: 1.2rem;
            font-weight: 600;
            cursor: pointer;
            display: block;
            margin: 20px auto;
            transition: all 0.2s ease;
        }

        .roll-btn:hover {
            transform: scale(1.05);
        }

        /* РУЛЕТКА - оптимизированная */
        .roulette-container {
            max-width: 300px;
            margin: 30px auto;
            position: relative;
        }

        .roulette-wheel {
            width: 100%;
            height: 300px;
            background: conic-gradient(
                #ff0000, #000000, #ff0000, #000000, #ff0000, #000000,
                #ff0000, #000000, #ff0000, #000000, #ff0000, #000000,
                #ff0000, #000000, #ff0000, #000000, #ff0000, #000000,
                #008000, #008000, #008000, #008000, #008000, #008000
            );
            border-radius: 50%;
            position: relative;
            animation: wheelIdle 20s linear infinite;
        }

        @keyframes wheelIdle {
            100% { transform: rotate(360deg); }
        }

        .roulette-ball {
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 30px;
            height: 30px;
            background: white;
            border-radius: 50%;
            z-index: 2;
        }

        /* УПРАВЛЕНИЕ СТАВКАМИ */
        .bet-controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
            flex-wrap: wrap;
        }

        .bet-btn {
            padding: 10px 20px;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 10px;
            color: white;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .bet-btn:hover {
            background: var(--primary);
            transform: translateY(-2px);
        }

        .current-bet {
            text-align: center;
            font-size: 1.5rem;
            font-weight: 600;
            margin: 15px 0;
            color: var(--accent);
        }

        /* УВЕДОМЛЕНИЯ - упрощенные */
        .notification {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 15px 25px;
            border-radius: 15px;
            font-weight: 600;
            z-index: 10000;
            transition: transform 0.3s ease;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .notification.show {
            transform: translateX(-50%) translateY(0);
        }

        /* КОНФЕТТИ - оптимизированные */
        .confetti-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 9999;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            animation: confettiFall 2s linear forwards;
        }

        @keyframes confettiFall {
            to { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }

        /* ИНФОРМАЦИОННЫЕ БЛОКИ */
        .game-rules {
            background: var(--glass);
            border-radius: 15px;
            padding: 15px;
            margin: 20px 0;
            border: 1px solid var(--glass-border);
        }

        .game-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin: 20px 0;
        }

        .stat-item {
            background: rgba(255,255,255,0.05);
            padding: 10px;
            border-radius: 10px;
            text-align: center;
        }

        /* АДАПТИВНОСТЬ */
        @media (max-width: 480px) {
            .container {
                padding: 5px;
            }
            
            .slots-grid {
                grid-template-columns: repeat(3, 1fr);
                gap: 5px;
            }
            
            .slot-cell {
                font-size: 1.5rem;
            }
            
            .spin-btn {
                width: 80px;
                height: 80px;
                font-size: 1rem;
            }
            
            .poker-card {
                width: 55px;
                height: 80px;
                font-size: 1.2rem;
            }
            
            .die {
                width: 60px;
                height: 60px;
                font-size: 2rem;
            }
        }

        /* УБИРАЕМ ВСЕ ТЯЖЕЛЫЕ АНИМАЦИИ */
        .bg-effect,
        .particles-container,
        .floating-coins {
            display: none !important;
        }

        /* УПРОЩАЕМ СЛОЖНЫЕ ЭФФЕКТЫ */
        * {
            animation-duration: 0.3s !important;
            transition-duration: 0.2s !important;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ШАПКА -->
        <div class="header">
            <div class="logo">
                <i class="fas fa-dice"></i>
                <h1>ULTRA CASINO</h1>
            </div>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="balance">10,000</span>
            </div>
        </div>

        <!-- НАВИГАЦИЯ -->
        <div class="nav-tabs">
            <button class="nav-tab active" onclick="showCategory('all')">Все игры</button>
            <button class="nav-tab" onclick="showCategory('slots')">Слоты</button>
            <button class="nav-tab" onclick="showCategory('cards')">Карты</button>
            <button class="nav-tab" onclick="showCategory('dice')">Кости</button>
        </div>

        <!-- ГЛАВНЫЙ ЭКРАН -->
        <div class="main-content" id="mainContent">
            <div class="games-grid" id="gamesGrid">
                <!-- Игры загружаются через JS -->
            </div>
        </div>

        <!-- УВЕДОМЛЕНИЯ -->
        <div class="notification" id="notification"></div>
        
        <!-- КОНФЕТТИ -->
        <div class="confetti-container" id="confettiContainer"></div>
    </div>

    <!-- ========== ЭКРАНЫ ИГР ========== -->

    <!-- 1. СЛОТЫ -->
    <div class="game-screen" id="slotsScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>🎰 КЛАССИЧЕСКИЕ СЛОТЫ</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="slotsBalance">10,000</span>
            </div>
        </div>

        <div class="slots-container">
            <div class="current-bet">Ставка: <span id="slotsBet">100</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeSlotsBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeSlotsBet(-10)">-10</button>
                <button class="bet-btn" onclick="changeSlotsBet(10)">+10</button>
                <button class="bet-btn" onclick="changeSlotsBet(50)">+50</button>
                <button class="bet-btn" onclick="maxSlotsBet()">MAX</button>
            </div>

            <div class="slots-grid" id="slotsGrid">
                <!-- 3x3 слоты -->
            </div>

            <button class="spin-btn" id="spinBtn" onclick="spinSlots()">SPIN</button>

            <div class="game-stats">
                <div class="stat-item">
                    <div>Линии</div>
                    <div id="linesCount">9</div>
                </div>
                <div class="stat-item">
                    <div>Множитель</div>
                    <div id="multiplier">x1</div>
                </div>
                <div class="stat-item">
                    <div>Последний выигрыш</div>
                    <div id="lastWin">0</div>
                </div>
                <div class="stat-item">
                    <div>Общий выигрыш</div>
                    <div id="totalWins">0</div>
                </div>
            </div>

            <div class="game-rules">
                <h3>📖 Правила игры:</h3>
                <p>• 3 одинаковых символа в линии = выигрыш</p>
                <p>• 7 = x10, BAR = x5, 🍒 = x3</p>
                <p>• 2 одинаковых = возврат ставки</p>
            </div>
        </div>
    </div>

    <!-- 2. ПОКЕР -->
    <div class="game-screen" id="pokerScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>♠️ ТЕХАС ХОЛДЕМ</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="pokerBalance">10,000</span>
            </div>
        </div>

        <div class="poker-container">
            <div class="current-bet">Ставка: <span id="pokerBet">500</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changePokerBet(-100)">-100</button>
                <button class="bet-btn" onclick="changePokerBet(100)">+100</button>
                <button class="bet-btn" onclick="dealPoker()">РАЗДАТЬ</button>
                <button class="bet-btn" onclick="foldPoker()">ПАС</button>
                <button class="bet-btn" onclick="callPoker()">КОЛЛ</button>
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent); margin-bottom: 10px;">
                    Статус: <span id="pokerStatus">Ждем ставку</span>
                </div>
                <div style="font-size: 1rem; color: #aaa;">
                    Банк: <span id="pokerPot">0</span>
                </div>
            </div>

            <div class="poker-hand" id="playerHand">
                <!-- Карты игрока -->
            </div>

            <div style="text-align: center; margin: 20px 0; color: var(--danger);">
                <div>ДИЛЕР</div>
                <div class="poker-hand" id="dealerHand">
                    <!-- Карты дилера -->
                </div>
            </div>

            <div class="game-rules">
                <h3>📖 Правила покера:</h3>
                <p>• Соберите сильную комбинацию</p>
                <p>• Ставьте, пасуйте или повышайте</p>
                <p>• Побеждает сильнейшая рука</p>
            </div>
        </div>
    </div>

    <!-- 3. КОСТИ -->
    <div class="game-screen" id="diceScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>🎲 ИГРА В КОСТИ</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="diceBalance">10,000</span>
            </div>
        </div>

        <div style="padding: 20px;">
            <div class="current-bet">Ставка: <span id="diceBet">100</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeDiceBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeDiceBet(50)">+50</button>
                <button class="bet-btn" onclick="rollDice()">БРОСИТЬ</button>
                <button class="bet-btn" onclick="doubleDice()">УДВОИТЬ</button>
                <button class="bet-btn" onclick="autoDice()">АВТО</button>
            </div>

            <div class="dice-container" id="diceResult">
                <div class="die" id="die1">⚀</div>
                <div class="die" id="die2">⚀</div>
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.5rem; color: var(--accent);">
                    Сумма: <span id="diceSum">2</span>
                </div>
                <div style="font-size: 1rem; color: #aaa; margin-top: 10px;">
                    Ставка на: <span id="diceTarget">7 или 11</span>
                </div>
            </div>

            <div class="game-stats">
                <div class="stat-item">
                    <div>Побед подряд</div>
                    <div id="diceStreak">0</div>
                </div>
                <div class="stat-item">
                    <div>Макс. выигрыш</div>
                    <div id="diceMaxWin">0</div>
                </div>
                <div class="stat-item">
                    <div>Всего бросков</div>
                    <div id="diceRolls">0</div>
                </div>
                <div class="stat-item">
                    <div>Процент побед</div>
                    <div id="diceWinRate">0%</div>
                </div>
            </div>

            <div class="game-rules">
                <h3>📖 Правила игры в кости:</h3>
                <p>• 7 или 11 = x3 выигрыша</p>
                <p>• Дубль (одинаковые) = x5</p>
                <p>• Сумма 8-10 = x2</p>
                <p>• Сумма 2-6 = x1.5</p>
            </div>
        </div>
    </div>

    <!-- 4. РУЛЕТКА -->
    <div class="game-screen" id="rouletteScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>🎯 ЕВРОПЕЙСКАЯ РУЛЕТКА</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="rouletteBalance">10,000</span>
            </div>
        </div>

        <div style="padding: 20px;">
            <div class="current-bet">Ставка: <span id="rouletteBet">100</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeRouletteBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeRouletteBet(50)">+50</button>
                <button class="bet-btn" onclick="placeRouletteBet('red')">КРАСНОЕ</button>
                <button class="bet-btn" onclick="placeRouletteBet('black')">ЧЕРНОЕ</button>
                <button class="bet-btn" onclick="spinRoulette()">КРУТИТЬ</button>
            </div>

            <div class="roulette-container">
                <div class="roulette-wheel" id="rouletteWheel">
                    <div class="roulette-ball"></div>
                </div>
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent);">
                    Последнее число: <span id="lastNumber">0</span>
                </div>
                <div style="font-size: 1rem; color: #aaa; margin-top: 10px;">
                    Цвет: <span id="lastColor" style="color: red;">Красное</span>
                </div>
            </div>

            <div class="game-stats">
                <div class="stat-item">
                    <div>Красное</div>
                    <div id="redCount">0</div>
                </div>
                <div class="stat-item">
                    <div>Черное</div>
                    <div id="blackCount">0</div>
                </div>
                <div class="stat-item">
                    <div>Зеро</div>
                    <div id="zeroCount">0</div>
                </div>
                <div class="stat-item">
                    <div>Баланс</div>
                    <div id="rouletteProfit">0</div>
                </div>
            </div>

            <div class="game-rules">
                <h3>📖 Правила рулетки:</h3>
                <p>• Красное/Черное = x2</p>
                <p>• Четное/Нечетное = x2</p>
                <p>• Конкретное число = x35</p>
                <p>• 1-12, 13-24, 25-36 = x3</p>
            </div>
        </div>
    </div>

    <!-- 5. БЛЭКДЖЕК -->
    <div class="game-screen" id="blackjackScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>♣️ БЛЭКДЖЕК 21</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="blackjackBalance">10,000</span>
            </div>
        </div>

        <div class="poker-container">
            <div class="current-bet">Ставка: <span id="blackjackBet">200</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeBlackjackBet(-100)">-100</button>
                <button class="bet-btn" onclick="changeBlackjackBet(100)">+100</button>
                <button class="bet-btn" onclick="dealBlackjack()">РАЗДАТЬ</button>
                <button class="bet-btn" onclick="hitBlackjack()">ЕЩЕ</button>
                <button class="bet-btn" onclick="standBlackjack()">ХВАТИТ</button>
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent);">
                    Ваша рука: <span id="playerScore">0</span>
                </div>
                <div class="poker-hand" id="blackjackPlayer">
                    <!-- Карты игрока -->
                </div>
            </div>

            <div style="text-align: center; margin: 20px 0; color: var(--danger);">
                <div>Рука дилера: <span id="dealerScore">?</span></div>
                <div class="poker-hand" id="blackjackDealer">
                    <!-- Карты дилера -->
                </div>
            </div>

            <div class="game-rules">
                <h3>📖 Правила блэкджека:</h3>
                <p>• Цель - набрать 21 или ближе к 21</p>
                <p>• Туз = 1 или 11</p>
                <p>• Картинки = 10</p>
                <p>• Перебор (>21) = проигрыш</p>
            </div>
        </div>
    </div>

    <!-- 6. КОЛЕСО УДАЧИ -->
    <div class="game-screen" id="wheelScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2>🎡 КОЛЕСО ФОРТУНЫ</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="wheelBalance">10,000</span>
            </div>
        </div>

        <div style="padding: 20px; text-align: center;">
            <div class="current-bet">Ставка: <span id="wheelBet">100</span></div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeWheelBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeWheelBet(50)">+50</button>
                <button class="bet-btn" onclick="spinWheel()">КРУТИТЬ!</button>
            </div>

            <div style="
                width: 250px;
                height: 250px;
                margin: 30px auto;
                background: conic-gradient(
                    #ff0000 0deg 45deg,
                    #0000ff 45deg 90deg,
                    #00ff00 90deg 135deg,
                    #ffff00 135deg 180deg,
                    #ff00ff 180deg 225deg,
                    #00ffff 225deg 270deg,
                    #ff8800 270deg 315deg,
                    #8800ff 315deg 360deg
                );
                border-radius: 50%;
                position: relative;
                border: 10px solid #8b4513;
            " id="fortuneWheel">
                <div style="
                    position: absolute;
                    top: -20px;
                    left: 50%;
                    transform: translateX(-50%);
                    width: 40px;
                    height: 40px;
                    background: gold;
                    clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
                "></div>
            </div>

            <div style="margin: 20px 0; font-size: 1.5rem; color: var(--accent);">
                Выигрыш: <span id="wheelWin">0</span>
            </div>

            <div class="game-rules">
                <h3>📖 Призы на колесе:</h3>
                <p>• x2 ставки (красный)</p>
                <p>• x3 ставки (синий)</p>
                <p>• x5 ставки (зеленый)</p>
                <p>• x10 ставки (желтый)</p>
                <p>• Джекпот x100 (фиолетовый)</p>
            </div>
        </div>
    </div>

    <script>
        // ========== ОПТИМИЗАЦИЯ: убираем все тяжелые вычисления ==========
        
        // Инициализация Telegram
        const tg = window.Telegram.WebApp;
        tg.expand();
        tg.ready();

        // Глобальные переменные
        let balance = 10000;
        let currentGame = null;
        let games = [];

        // Инициализация игр
        function initGames() {
            games = [
                {
                    id: 'slots',
                    name: '🎰 КЛАССИЧЕСКИЕ СЛОТЫ',
                    description: '3x3 поле, 9 линий, бонусные раунды',
                    icon: 'fas fa-sliders-h',
                    category: 'slots',
                    color: '#ff3366'
                },
                {
                    id: 'poker',
                    name: '♠️ ТЕХАС ХОЛДЕМ',
                    description: 'Карточная игра против дилера',
                    icon: 'fas fa-spade',
                    category: 'cards',
                    color: '#33ccff'
                },
                {
                    id: 'dice',
                    name: '🎲 ИГРА В КОСТИ',
                    description: 'Брось кости и выигрывай',
                    icon: 'fas fa-dice',
                    category: 'dice',
                    color: '#ffcc00'
                },
                {
                    id: 'roulette',
                    name: '🎯 ЕВРОПЕЙСКАЯ РУЛЕТКА',
                    description: 'Красное или черное?',
                    icon: 'fas fa-circle',
                    category: 'table',
                    color: '#00ff88'
                },
                {
                    id: 'blackjack',
                    name: '♣️ БЛЭКДЖЕК 21',
                    description: 'Набери 21 и обыграй дилера',
                    icon: 'fas fa-club',
                    category: 'cards',
                    color: '#9d4edd'
                },
                {
                    id: 'wheel',
                    name: '🎡 КОЛЕСО ФОРТУНЫ',
                    description: 'Испытай удачу на колесе',
                    icon: 'fas fa-gift',
                    category: 'special',
                    color: '#ff6b35'
                }
            ];
        }

        // Обновление баланса
        function updateBalance() {
            document.getElementById('balance').textContent = balance.toLocaleString();
            
            // Обновляем баланс на всех экранах
            const screens = ['slots', 'poker', 'dice', 'roulette', 'blackjack', 'wheel'];
            screens.forEach(screen => {
                const el = document.getElementById(`${screen}Balance`);
                if (el) el.textContent = balance.toLocaleString();
            });
        }

        // Показать уведомление
        function showNotification(text, duration = 3000) {
            const notification = document.getElementById('notification');
            notification.textContent = text;
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, duration);
        }

        // Создать конфетти
        function createConfetti(count = 50) {
            const container = document.getElementById('confettiContainer');
            const colors = ['#ff3366', '#33ccff', '#ffcc00', '#00ff88'];
            
            for (let i = 0; i < count; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.animationDuration = (Math.random() * 2 + 1) + 's';
                container.appendChild(confetti);
                
                setTimeout(() => {
                    confetti.remove();
                }, 2000);
            }
        }

        // Рендер игр
        function renderGames(category = 'all') {
            const grid = document.getElementById('gamesGrid');
            grid.innerHTML = '';
            
            const filteredGames = category === 'all' 
                ? games 
                : games.filter(game => game.category === category);
            
            filteredGames.forEach(game => {
                const card = document.createElement('div');
                card.className = 'game-card';
                card.onclick = () => openGame(game.id);
                
                card.innerHTML = `
                    <div class="game-icon" style="background: linear-gradient(135deg, ${game.color}, ${game.color}80);">
                        <i class="${game.icon}"></i>
                    </div>
                    <div class="game-info">
                        <h3>${game.name}</h3>
                        <p>${game.description}</p>
                        <button class="play-btn">ИГРАТЬ СЕЙЧАС</button>
                    </div>
                `;
                
                grid.appendChild(card);
            });
        }

        // Показать категорию
        function showCategory(category) {
            // Обновить активную вкладку
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Показать игры категории
            renderGames(category);
        }

        // Открыть игру
        function openGame(gameId) {
            currentGame = gameId;
            document.getElementById('mainContent').style.display = 'none';
            document.getElementById(`${gameId}Screen`).classList.add('active');
            
            // Инициализировать игру
            switch(gameId) {
                case 'slots':
                    initSlots();
                    break;
                case 'poker':
                    initPoker();
                    break;
                case 'dice':
                    initDice();
                    break;
                case 'roulette':
                    initRoulette();
                    break;
                case 'blackjack':
                    initBlackjack();
                    break;
                case 'wheel':
                    initWheel();
                    break;
            }
            
            updateBalance();
        }

        // Закрыть игру
        function closeGame() {
            if (currentGame) {
                document.getElementById(`${currentGame}Screen`).classList.remove('active');
            }
            document.getElementById('mainContent').style.display = 'block';
            currentGame = null;
            updateBalance();
        }

        // ========== ИГРА: СЛОТЫ ==========
        let slotsBet = 100;
        let slotsSymbols = ['🍒', '7️⃣', '⭐', '💎', '🔔'];
        let lastWin = 0;
        let totalWins = 0;

        function initSlots() {
            // Создать сетку 3x3
            const grid = document.getElementById('slotsGrid');
            grid.innerHTML = '';
            
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement('div');
                cell.className = 'slot-cell';
                cell.textContent = slotsSymbols[Math.floor(Math.random() * slotsSymbols.length)];
                grid.appendChild(cell);
            }
            
            // Обновить информацию
            document.getElementById('slotsBet').textContent = slotsBet;
            document.getElementById('lastWin').textContent = lastWin;
            document.getElementById('totalWins').textContent = totalWins;
        }

        function changeSlotsBet(amount) {
            slotsBet += amount;
            if (slotsBet < 10) slotsBet = 10;
            if (slotsBet > 10000) slotsBet = 10000;
            document.getElementById('slotsBet').textContent = slotsBet;
        }

        function maxSlotsBet() {
            slotsBet = Math.min(10000, balance);
            document.getElementById('slotsBet').textContent = slotsBet;
        }

        function spinSlots() {
            if (balance < slotsBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            balance -= slotsBet;
            updateBalance();
            
            // Анимация вращения
            const cells = document.querySelectorAll('#slotsGrid .slot-cell');
            const spinBtn = document.getElementById('spinBtn');
            spinBtn.disabled = true;
            spinBtn.textContent = '...';
            
            // Случайные символы
            setTimeout(() => {
                cells.forEach(cell => {
                    cell.textContent = slotsSymbols[Math.floor(Math.random() * slotsSymbols.length)];
                    cell.classList.remove('win');
                });
                
                // Проверить выигрыш
                checkSlotsWin(cells);
                spinBtn.disabled = false;
                spinBtn.textContent = 'SPIN';
            }, 500);
        }

        function checkSlotsWin(cells) {
            let winAmount = 0;
            const lines = [
                [0,1,2], [3,4,5], [6,7,8], // Горизонтальные
                [0,3,6], [1,4,7], [2,5,8], // Вертикальные
                [0,4,8], [2,4,6]           // Диагонали
            ];
            
            lines.forEach(line => {
                const [a,b,c] = line;
                if (cells[a].textContent === cells[b].textContent && 
                    cells[b].textContent === cells[c].textContent) {
                    
                    // Подсветить выигрышную линию
                    cells[a].classList.add('win');
                    cells[b].classList.add('win');
                    cells[c].classList.add('win');
                    
                    // Определить выигрыш
                    const symbol = cells[a].textContent;
                    const multipliers = {
                        '🍒': 3,
                        '7️⃣': 10,
                        '⭐': 5,
                        '💎': 8,
                        '🔔': 4
                    };
                    
                    winAmount += slotsBet * (multipliers[symbol] || 2);
                }
            });
            
            if (winAmount > 0) {
                balance += winAmount;
                lastWin = winAmount;
                totalWins += winAmount;
                
                // Обновить статистику
                document.getElementById('lastWin').textContent = lastWin;
                document.getElementById('totalWins').textContent = totalWins;
                
                // Эффекты
                createConfetti();
                showNotification(`🎉 ВЫИГРЫШ ${winAmount}!`);
                
                // Обновить множитель
                const multiplier = Math.floor(winAmount / slotsBet);
                document.getElementById('multiplier').textContent = `x${multiplier}`;
            } else {
                showNotification('Повезет в следующий раз!');
            }
            
            updateBalance();
        }

        // ========== ИГРА: ПОКЕР ==========
        let pokerBet = 500;
        let pokerPot = 0;
        let playerCards = [];
        let dealerCards = [];

        function initPoker() {
            document.getElementById('pokerBet').textContent = pokerBet;
            document.getElementById('pokerPot').textContent = pokerPot;
            document.getElementById('pokerStatus').textContent = 'Сделайте ставку';
            
            // Очистить карты
            document.getElementById('playerHand').innerHTML = '';
            document.getElementById('dealerHand').innerHTML = '';
            
            playerCards = [];
            dealerCards = [];
        }

        function changePokerBet(amount) {
            pokerBet += amount;
            if (pokerBet < 100) pokerBet = 100;
            if (pokerBet > 5000) pokerBet = 5000;
            document.getElementById('pokerBet').textContent = pokerBet;
        }

        function dealPoker() {
            if (balance < pokerBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            balance -= pokerBet;
            pokerPot = pokerBet * 2;
            updateBalance();
            
            // Раздать карты
            playerCards = [getRandomCard(), getRandomCard()];
            dealerCards = [getRandomCard(), getRandomCard()];
            
            // Отобразить карты
            displayPokerCards();
            
            document.getElementById('pokerPot').textContent = pokerPot;
            document.getElementById('pokerStatus').textContent = 'Ваш ход';
        }

        function getRandomCard() {
            const suits = ['heart', 'diamond', 'spade', 'club'];
            const values = ['A', 'K', 'Q', 'J', '10', '9', '8'];
            const suit = suits[Math.floor(Math.random() * suits.length)];
            const value = values[Math.floor(Math.random() * values.length)];
            return { suit, value };
        }

        function displayPokerCards() {
            const playerHand = document.getElementById('playerHand');
            const dealerHand = document.getElementById('dealerHand');
            
            playerHand.innerHTML = '';
            dealerHand.innerHTML = '';
            
            // Карты игрока
            playerCards.forEach(card => {
                const cardEl = createCardElement(card);
                playerHand.appendChild(cardEl);
            });
            
            // Карты дилера (первая скрыта)
            dealerCards.forEach((card, index) => {
                const cardEl = index === 0 
                    ? createCardElement({ suit: 'back', value: '?' })
                    : createCardElement(card);
                dealerHand.appendChild(cardEl);
            });
        }

        function createCardElement(card) {
            const div = document.createElement('div');
            div.className = `poker-card ${card.suit}`;
            
            if (card.suit === 'back') {
                div.innerHTML = '❓';
                div.style.color = '#333';
            } else {
                const suitSymbol = {
                    'heart': '♥',
                    'diamond': '♦',
                    'spade': '♠',
                    'club': '♣'
                }[card.suit];
                
                const color = card.suit === 'heart' || card.suit === 'diamond' ? '#c00' : '#000';
                
                div.innerHTML = `
                    <div class="poker-suit" style="color: ${color}">${suitSymbol}</div>
                    <div class="poker-value" style="color: ${color}">${card.value}</div>
                `;
            }
            
            return div;
        }

        function foldPoker() {
            if (playerCards.length === 0) return;
            
            pokerPot = 0;
            document.getElementById('pokerPot').textContent = pokerPot;
            document.getElementById('pokerStatus').textContent = 'Вы спасовали';
            
            showNotification('Вы спасовали');
        }

        function callPoker() {
            if (playerCards.length === 0 || balance < pokerBet) {
                showNotification('Сначала сделайте ставку!');
                return;
            }
            
            balance -= pokerBet;
            pokerPot += pokerBet;
            updateBalance();
            
            // Открыть карты дилера
            const dealerHand = document.getElementById('dealerHand');
            dealerHand.innerHTML = '';
            dealerCards.forEach(card => {
                dealerHand.appendChild(createCardElement(card));
            });
            
            // Определить победителя
            const playerScore = evaluatePokerHand(playerCards);
            const dealerScore = evaluatePokerHand(dealerCards);
            
            if (playerScore > dealerScore) {
                balance += pokerPot * 2;
                showNotification(`🎉 ПОБЕДА! Вы выиграли ${pokerPot * 2}!`);
                createConfetti();
            } else if (playerScore === dealerScore) {
                balance += pokerPot;
                showNotification('Ничья! Ставка возвращена');
            } else {
                showNotification('Дилер победил');
            }
            
            pokerPot = 0;
            document.getElementById('pokerPot').textContent = pokerPot;
            document.getElementById('pokerStatus').textContent = 'Игра окончена';
            updateBalance();
        }

        function evaluatePokerHand(cards) {
            // Упрощенная оценка руки
            let score = 0;
            
            // Пары
            if (cards[0].value === cards[1].value) {
                score += 100;
            }
            
            // Одинаковые масти
            if (cards[0].suit === cards[1].suit) {
                score += 50;
            }
            
            // Высокие карты
            const highCards = ['A', 'K', 'Q', 'J'];
            cards.forEach(card => {
                if (highCards.includes(card.value)) {
                    score += 20;
                }
            });
            
            return score;
        }

        // ========== ИГРА: КОСТИ ==========
        let diceBet = 100;
        let diceStreak = 0;
        let diceRolls = 0;
        let diceWins = 0;
        let diceMaxWin = 0;

        function initDice() {
            document.getElementById('diceBet').textContent = diceBet;
            document.getElementById('diceStreak').textContent = diceStreak;
            document.getElementById('diceRolls').textContent = diceRolls;
            document.getElementById('diceMaxWin').textContent = diceMaxWin;
            
            const winRate = diceRolls > 0 ? Math.round((diceWins / diceRolls) * 100) : 0;
            document.getElementById('diceWinRate').textContent = winRate + '%';
        }

        function changeDiceBet(amount) {
            diceBet += amount;
            if (diceBet < 10) diceBet = 10;
            if (diceBet > 5000) diceBet = 5000;
            document.getElementById('diceBet').textContent = diceBet;
        }

        function rollDice() {
            if (balance < diceBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            balance -= diceBet;
            diceRolls++;
            updateBalance();
            
            // Анимация броска
            const die1 = document.getElementById('die1');
            const die2 = document.getElementById('die2');
            
            die1.style.transform = 'rotate(360deg)';
            die2.style.transform = 'rotate(-360deg)';
            
            setTimeout(() => {
                // Случайные значения
                const d1 = Math.floor(Math.random() * 6) + 1;
                const d2 = Math.floor(Math.random() * 6) + 1;
                const sum = d1 + d2;
                
                // Установить значения
                die1.textContent = getDiceFace(d1);
                die2.textContent = getDiceFace(d2);
                die1.style.transform = 'rotate(0)';
                die2.style.transform = 'rotate(0)';
                
                document.getElementById('diceSum').textContent = sum;
                
                // Определить выигрыш
                let multiplier = 0;
                
                if (sum === 7 || sum === 11) {
                    multiplier = 3;
                } else if (d1 === d2) {
                    multiplier = 5;
                } else if (sum >= 8 && sum <= 10) {
                    multiplier = 2;
                } else if (sum >= 2 && sum <= 6) {
                    multiplier = 1.5;
                }
                
                if (multiplier > 0) {
                    const winAmount = Math.floor(diceBet * multiplier);
                    balance += winAmount;
                    diceStreak++;
                    diceWins++;
                    
                    if (winAmount > diceMaxWin) {
                        diceMaxWin = winAmount;
                    }
                    
                    showNotification(`🎲 Выпало ${sum}! Выигрыш: ${winAmount} (x${multiplier})`);
                    
                    if (multiplier >= 3) {
                        createConfetti();
                    }
                } else {
                    diceStreak = 0;
                    showNotification(`🎲 Выпало ${sum}. Попробуйте еще!`);
                }
                
                // Обновить статистику
                initDice();
                updateBalance();
            }, 500);
        }

        function getDiceFace(value) {
            const faces = ['⚀', '⚁', '⚂', '⚃', '⚄', '⚅'];
            return faces[value - 1];
        }

        function doubleDice() {
            diceBet *= 2;
            if (diceBet > 5000) diceBet = 5000;
            document.getElementById('diceBet').textContent = diceBet;
            showNotification('Ставка удвоена!');
        }

        function autoDice() {
            if (balance >= diceBet) {
                rollDice();
                setTimeout(() => {
                    if (balance >= diceBet * 2) {
                        autoDice();
                    }
                }, 1000);
            }
        }

        // ========== ИГРА: РУЛЕТКА ==========
        let rouletteBet = 100;
        let redCount = 0;
        let blackCount = 0;
        let zeroCount = 0;
        let rouletteProfit = 0;

        function initRoulette() {
            document.getElementById('rouletteBet').textContent = rouletteBet;
            document.getElementById('redCount').textContent = redCount;
            document.getElementById('blackCount').textContent = blackCount;
            document.getElementById('zeroCount').textContent = zeroCount;
            document.getElementById('rouletteProfit').textContent = rouletteProfit;
        }

        function changeRouletteBet(amount) {
            rouletteBet += amount;
            if (rouletteBet < 10) rouletteBet = 10;
            if (rouletteBet > 5000) rouletteBet = 5000;
            document.getElementById('rouletteBet').textContent = rouletteBet;
        }

        function placeRouletteBet(type) {
            showNotification(`Ставка на ${type === 'red' ? 'красное' : 'черное'}`);
        }

        function spinRoulette() {
            if (balance < rouletteBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            balance -= rouletteBet;
            
            // Анимация вращения
            const wheel = document.getElementById('rouletteWheel');
            wheel.style.animation = 'none';
            
            setTimeout(() => {
                // Случайное число от 0 до 36
                const number = Math.floor(Math.random() * 37);
                const isRed = [1,3,5,7,9,12,14,16,18,19,21,23,25,27,30,32,34,36].includes(number);
                const isBlack = number !== 0 && !isRed;
                
                // Обновить статистику
                if (number === 0) zeroCount++;
                else if (isRed) redCount++;
                else blackCount++;
                
                // Определить выигрыш
                let winAmount = 0;
                if (Math.random() > 0.5) { // 50% шанс на победу
                    winAmount = rouletteBet * 2;
                    balance += winAmount;
                    rouletteProfit += rouletteBet;
                    showNotification(`🎯 Выпало ${number} ${isRed ? '🔴' : isBlack ? '⚫' : '🟢'}. ВЫИГРЫШ ${winAmount}!`);
                    
                    if (winAmount > rouletteBet * 5) {
                        createConfetti();
                    }
                } else {
                    rouletteProfit -= rouletteBet;
                    showNotification(`🎯 Выпало ${number} ${isRed ? '🔴' : isBlack ? '⚫' : '🟢'}. Попробуйте еще!`);
                }
                
                // Обновить интерфейс
                document.getElementById('lastNumber').textContent = number;
                const colorEl = document.getElementById('lastColor');
                colorEl.textContent = number === 0 ? 'Зеро' : (isRed ? 'Красное' : 'Черное');
                colorEl.style.color = number === 0 ? 'green' : (isRed ? 'red' : 'black');
                
                initRoulette();
                updateBalance();
                
                // Восстановить анимацию
                setTimeout(() => {
                    wheel.style.animation = 'wheelIdle 20s linear infinite';
                }, 100);
            }, 10);
        }

        // ========== ИГРА: БЛЭКДЖЕК ==========
        let blackjackBet = 200;
        let playerScore = 0;
        let dealerScore = 0;
        let playerCardsBJ = [];
        let dealerCardsBJ = [];
        let gameActive = false;

        function initBlackjack() {
            document.getElementById('blackjackBet').textContent = blackjackBet;
            document.getElementById('playerScore').textContent = '0';
            document.getElementById('dealerScore').textContent = '?';
            
            // Очистить карты
            document.getElementById('blackjackPlayer').innerHTML = '';
            document.getElementById('blackjackDealer').innerHTML = '';
            
            playerCardsBJ = [];
            dealerCardsBJ = [];
            gameActive = false;
        }

        function changeBlackjackBet(amount) {
            blackjackBet += amount;
            if (blackjackBet < 100) blackjackBet = 100;
            if (blackjackBet > 5000) blackjackBet = 5000;
            document.getElementById('blackjackBet').textContent = blackjackBet;
        }

        function dealBlackjack() {
            if (balance < blackjackBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            if (gameActive) return;
            
            balance -= blackjackBet;
            gameActive = true;
            updateBalance();
            
            // Раздать карты
            playerCardsBJ = [getRandomCardBJ(), getRandomCardBJ()];
            dealerCardsBJ = [getRandomCardBJ(), getRandomCardBJ()];
            
            // Отобразить карты
            displayBlackjackCards();
            
            // Проверить блэкджек
            playerScore = calculateScore(playerCardsBJ);
            dealerScore = calculateScore([dealerCardsBJ[0]]); // только одна карта дилера видна
            
            document.getElementById('playerScore').textContent = playerScore;
            document.getElementById('dealerScore').textContent = '?';
            
            if (playerScore === 21) {
                setTimeout(() => standBlackjack(), 1000);
            }
        }

        function getRandomCardBJ() {
            const values = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'];
            const suits = ['heart', 'diamond', 'spade', 'club'];
            return {
                value: values[Math.floor(Math.random() * values.length)],
                suit: suits[Math.floor(Math.random() * suits.length)]
            };
        }

        function displayBlackjackCards() {
            const playerArea = document.getElementById('blackjackPlayer');
            const dealerArea = document.getElementById('blackjackDealer');
            
            playerArea.innerHTML = '';
            dealerArea.innerHTML = '';
            
            // Карты игрока
            playerCardsBJ.forEach(card => {
                playerArea.appendChild(createCardElementBJ(card));
            });
            
            // Карты дилера (первая скрыта)
            dealerCardsBJ.forEach((card, index) => {
                const cardEl = index === 0 
                    ? createCardElementBJ({ value: '?', suit: 'back' })
                    : createCardElementBJ(card);
                dealerArea.appendChild(cardEl);
            });
        }

        function createCardElementBJ(card) {
            const div = document.createElement('div');
            div.className = 'poker-card';
            
            if (card.suit === 'back') {
                div.innerHTML = '❓';
                div.style.color = '#333';
            } else {
                const suitSymbol = {
                    'heart': '♥',
                    'diamond': '♦',
                    'spade': '♠',
                    'club': '♣'
                }[card.suit];
                
                const color = card.suit === 'heart' || card.suit === 'diamond' ? '#c00' : '#000';
                
                div.innerHTML = `
                    <div class="poker-suit" style="color: ${color}">${suitSymbol}</div>
                    <div class="poker-value" style="color: ${color}">${card.value}</div>
                `;
            }
            
            return div;
        }

        function calculateScore(cards) {
            let score = 0;
            let aces = 0;
            
            cards.forEach(card => {
                if (card.value === 'A') {
                    aces++;
                    score += 11;
                } else if (['K', 'Q', 'J'].includes(card.value)) {
                    score += 10;
                } else {
                    score += parseInt(card.value);
                }
            });
            
            // Корректировка тузов
            while (score > 21 && aces > 0) {
                score -= 10;
                aces--;
            }
            
            return score;
        }

        function hitBlackjack() {
            if (!gameActive || playerScore >= 21) return;
            
            playerCardsBJ.push(getRandomCardBJ());
            playerScore = calculateScore(playerCardsBJ);
            
            displayBlackjackCards();
            document.getElementById('playerScore').textContent = playerScore;
            
            if (playerScore > 21) {
                showNotification('Перебор! Вы проиграли');
                gameActive = false;
            } else if (playerScore === 21) {
                setTimeout(() => standBlackjack(), 1000);
            }
        }

        function standBlackjack() {
            if (!gameActive) return;
            
            // Открыть карты дилера
            const dealerArea = document.getElementById('blackjackDealer');
            dealerArea.innerHTML = '';
            dealerCardsBJ.forEach(card => {
                dealerArea.appendChild(createCardElementBJ(card));
            });
            
            // Дилер добирает карты
            dealerScore = calculateScore(dealerCardsBJ);
            while (dealerScore < 17) {
                dealerCardsBJ.push(getRandomCardBJ());
                dealerScore = calculateScore(dealerCardsBJ);
            }
            
            // Обновить отображение
            displayBlackjackCards();
            document.getElementById('dealerScore').textContent = dealerScore;
            
            // Определить победителя
            if (playerScore > 21) {
                showNotification('Перебор! Дилер победил');
            } else if (dealerScore > 21) {
                const winAmount = blackjackBet * 2;
                balance += winAmount;
                showNotification(`🎉 Дилер перебрал! Вы выиграли ${winAmount}!`);
                createConfetti();
            } else if (playerScore > dealerScore) {
                const winAmount = blackjackBet * 2;
                balance += winAmount;
                showNotification(`🎉 Вы победили! Выигрыш ${winAmount}!`);
                createConfetti();
            } else if (playerScore === dealerScore) {
                balance += blackjackBet;
                showNotification('Ничья! Ставка возвращена');
            } else {
                showNotification('Дилер победил');
            }
            
            gameActive = false;
            updateBalance();
        }

        // ========== ИГРА: КОЛЕСО УДАЧИ ==========
        let wheelBet = 100;

        function initWheel() {
            document.getElementById('wheelBet').textContent = wheelBet;
        }

        function changeWheelBet(amount) {
            wheelBet += amount;
            if (wheelBet < 10) wheelBet = 10;
            if (wheelBet > 5000) wheelBet = 5000;
            document.getElementById('wheelBet').textContent = wheelBet;
        }

        function spinWheel() {
            if (balance < wheelBet) {
                showNotification('Недостаточно средств!');
                return;
            }
            
            balance -= wheelBet;
            
            // Анимация вращения
            const wheel = document.getElementById('fortuneWheel');
            wheel.style.transition = 'transform 3s cubic-bezier(0.1, 0.7, 0.1, 1)';
            wheel.style.transform = 'rotate(1440deg)';
            
            setTimeout(() => {
                // Определить выигрыш
                const segments = 8;
                const segment = Math.floor(Math.random() * segments);
                const multipliers = [2, 3, 5, 10, 2, 3, 5, 100]; // Джекпот на последнем сегменте
                const multiplier = multipliers[segment];
                const winAmount = wheelBet * multiplier;
                
                balance += winAmount;
                
                document.getElementById('wheelWin').textContent = winAmount;
                
                if (multiplier >= 5) {
                    showNotification(`🎡 ВЫИГРЫШ ${winAmount}! (x${multiplier})`);
                    createConfetti();
                } else {
                    showNotification(`Выигрыш ${winAmount} (x${multiplier})`);
                }
                
                updateBalance();
                
                // Сброс анимации
                setTimeout(() => {
                    wheel.style.transition = 'none';
                    wheel.style.transform = 'rotate(0)';
                    setTimeout(() => {
                        wheel.style.transition = '';
                    }, 50);
                }, 1000);
            }, 3000);
        }

        // ========== ИНИЦИАЛИЗАЦИЯ ПРИЛОЖЕНИЯ ==========
        document.addEventListener('DOMContentLoaded', () => {
            initGames();
            renderGames();
            updateBalance();
            
            // Добавить Telegram кнопку для пополнения
            tg.MainButton.setText('ПОПОЛНИТЬ БАЛАНС');
            tg.MainButton.show();
            tg.MainButton.onClick(() => {
                addBalance(5000);
                showNotification('Баланс пополнен на 5,000!');
            });
            
            // Показать приветственное сообщение
            setTimeout(() => {
                showNotification('Добро пожаловать в казино! Удачи!');
            }, 1000);
        });

        function addBalance(amount) {
            balance += amount;
            updateBalance();
        }

        // Обработка клавиш
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && currentGame) {
                closeGame();
            }
            
            // Быстрые клавиши для слотов
            if (currentGame === 'slots' && e.code === 'Space') {
                spinSlots();
                e.preventDefault();
            }
        });
    </script>
</body>
</html>
