
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎰 MEGA CASINO | Telegram Mini App</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Montserrat:wght@800;900&family=Orbitron:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* БАЗОВЫЕ СТИЛИ - ОПТИМИЗИРОВАННЫЕ */
        :root {
            --primary: #ff3366;
            --secondary: #33ccff;
            --accent: #ffcc00;
            --success: #00ff88;
            --danger: #ff5555;
            --dark: #0a0a1a;
            --darker: #050510;
            --glass: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
            --gradient: linear-gradient(135deg, var(--primary), var(--secondary));
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: linear-gradient(135deg, var(--darker), var(--dark));
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .container {
            max-width: 100%;
            padding: 15px;
        }

        /* ШАПКА С УЛУЧШЕННОЙ ГРАФИКОЙ */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background: var(--glass);
            backdrop-filter: blur(15px);
            border-radius: 25px;
            border: 2px solid var(--glass-border);
            margin-bottom: 25px;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            100% { left: 100%; }
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
            z-index: 1;
        }

        .logo-icon {
            font-size: 2.2rem;
            color: var(--accent);
            filter: drop-shadow(0 0 10px var(--accent));
        }

        .logo-text {
            font-family: 'Montserrat', sans-serif;
            font-size: 1.8rem;
            background: linear-gradient(90deg, var(--primary), var(--accent), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            background-size: 200%;
            animation: gradientShift 3s infinite alternate;
        }

        @keyframes gradientShift {
            0% { background-position: 0%; }
            100% { background-position: 100%; }
        }

        .balance-container {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 12px 20px;
            background: linear-gradient(135deg, rgba(255,51,102,0.2), rgba(51,204,255,0.2));
            border-radius: 20px;
            border: 2px solid rgba(255,255,255,0.1);
            position: relative;
            z-index: 1;
        }

        .balance-container i {
            color: var(--accent);
            font-size: 1.5rem;
        }

        .balance {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.6rem;
            font-weight: 700;
            color: white;
            text-shadow: 0 0 10px rgba(255,255,255,0.5);
        }

        /* НАВИГАЦИЯ */
        .nav-tabs {
            display: flex;
            overflow-x: auto;
            gap: 10px;
            margin-bottom: 25px;
            padding-bottom: 10px;
            -webkit-overflow-scrolling: touch;
        }

        .nav-tabs::-webkit-scrollbar {
            display: none;
        }

        .nav-tab {
            flex-shrink: 0;
            padding: 14px 25px;
            background: var(--glass);
            border: 2px solid var(--glass-border);
            border-radius: 15px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            white-space: nowrap;
        }

        .nav-tab:hover {
            background: var(--primary);
            transform: translateY(-3px);
        }

        .nav-tab.active {
            background: var(--gradient);
            box-shadow: 0 5px 20px rgba(255,51,102,0.4);
            transform: translateY(-3px);
        }

        /* СЕТКА ИГР */
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        @media (max-width: 768px) {
            .games-grid {
                grid-template-columns: 1fr;
            }
        }

        .game-card {
            background: linear-gradient(145deg, rgba(255,255,255,0.05), rgba(0,0,0,0.3));
            border-radius: 25px;
            padding: 25px;
            position: relative;
            overflow: hidden;
            cursor: pointer;
            transition: all 0.4s ease;
            border: 2px solid transparent;
        }

        .game-card:hover {
            transform: translateY(-10px);
            border-color: var(--primary);
            box-shadow: 0 15px 30px rgba(0,0,0,0.3);
        }

        .game-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.6s ease;
        }

        .game-card:hover::before {
            left: 100%;
        }

        .game-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            padding: 5px 15px;
            background: var(--primary);
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 700;
        }

        .game-icon {
            width: 80px;
            height: 80px;
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            border-radius: 20px;
            background: var(--gradient);
            position: relative;
        }

        .game-icon::after {
            content: '';
            position: absolute;
            inset: -5px;
            background: inherit;
            filter: blur(15px);
            opacity: 0.5;
            z-index: -1;
            border-radius: 25px;
        }

        .game-info h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
            text-align: center;
        }

        .game-info p {
            color: #aaa;
            text-align: center;
            margin-bottom: 20px;
            font-size: 0.95rem;
        }

        .play-btn {
            width: 100%;
            padding: 15px;
            background: var(--gradient);
            border: none;
            border-radius: 15px;
            color: white;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .play-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 25px rgba(255,51,102,0.4);
        }

        /* ЭКРАНЫ ИГР */
        .game-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--darker), var(--dark));
            z-index: 1000;
            display: none;
            overflow-y: auto;
        }

        .game-screen.active {
            display: block;
            animation: screenAppear 0.4s ease;
        }

        @keyframes screenAppear {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }

        .screen-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background: rgba(0, 0, 0, 0.5);
            border-bottom: 2px solid var(--primary);
            backdrop-filter: blur(10px);
        }

        .back-btn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient);
            border: none;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .back-btn:hover {
            transform: rotate(-90deg);
        }

        /* СТИЛИ ДЛЯ ВСЕХ ИГР */
        .game-container {
            max-width: 800px;
            margin: 30px auto;
            padding: 20px;
        }

        .bet-controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
            flex-wrap: wrap;
        }

        .bet-btn {
            padding: 12px 25px;
            background: var(--glass);
            border: 2px solid var(--glass-border);
            border-radius: 15px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .bet-btn:hover {
            background: var(--primary);
            transform: translateY(-3px);
        }

        .current-bet {
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            margin: 20px 0;
            color: var(--accent);
            text-shadow: 0 0 15px var(--accent);
        }

        /* УВЕДОМЛЕНИЯ */
        .notification {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: var(--gradient);
            color: white;
            padding: 20px 30px;
            border-radius: 20px;
            font-weight: 700;
            z-index: 10000;
            transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 15px 35px rgba(0,0,0,0.3);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.2);
            text-align: center;
            max-width: 90%;
        }

        .notification.show {
            transform: translateX(-50%) translateY(0);
        }

        /* КОНФЕТТИ */
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
            width: 12px;
            height: 12px;
            background: var(--accent);
            animation: confettiFall 3s linear forwards;
            border-radius: 2px;
        }

        @keyframes confettiFall {
            to {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }

        /* АВАТАР И СТАТИСТИКА */
        .user-stats {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            margin: 30px 0;
            padding: 20px;
            background: var(--glass);
            border-radius: 20px;
            border: 2px solid var(--glass-border);
        }

        .stat-item {
            text-align: center;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--accent);
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 0.9rem;
            color: #aaa;
        }

        /* ПРОГРЕСС БАР */
        .progress-bar {
            width: 100%;
            height: 20px;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
            position: relative;
        }

        .progress-fill {
            height: 100%;
            background: var(--gradient);
            transition: width 0.5s ease;
            position: relative;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: progressShine 2s infinite;
        }

        @keyframes progressShine {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        /* МОДАЛЬНОЕ ОКНО */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 11000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: linear-gradient(135deg, var(--darker), var(--dark));
            border-radius: 30px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            border: 3px solid var(--primary);
            position: relative;
        }

        /* АДАПТИВНОСТЬ */
        @media (max-width: 480px) {
            .games-grid {
                grid-template-columns: 1fr;
            }
            
            .user-stats {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .nav-tab {
                padding: 12px 20px;
                font-size: 0.9rem;
            }
            
            .game-icon {
                width: 60px;
                height: 60px;
                font-size: 2rem;
            }
            
            .balance {
                font-size: 1.3rem;
            }
        }

        /* ПОДВАЛ */
        .footer {
            text-align: center;
            padding: 20px;
            color: #aaa;
            font-size: 0.9rem;
            margin-top: 30px;
            border-top: 1px solid rgba(255,255,255,0.1);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ШАПКА -->
        <div class="header">
            <div class="logo">
                <i class="fas fa-crown logo-icon"></i>
                <div class="logo-text">MEGA CASINO</div>
            </div>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span class="balance" id="balance">100,000</span>
            </div>
        </div>

        <!-- НАВИГАЦИЯ -->
        <div class="nav-tabs">
            <button class="nav-tab active" onclick="showCategory('all')">Все игры</button>
            <button class="nav-tab" onclick="showCategory('slots')">Слоты</button>
            <button class="nav-tab" onclick="showCategory('cards')">Карты</button>
            <button class="nav-tab" onclick="showCategory('dice')">Кости</button>
            <button class="nav-tab" onclick="showCategory('roulette')">Рулетка</button>
            <button class="nav-tab" onclick="showCategory('special')">Специальные</button>
        </div>

        <!-- СТАТИСТИКА -->
        <div class="user-stats">
            <div class="stat-item">
                <div class="stat-value" id="totalWins">0</div>
                <div class="stat-label">Выиграно</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="gamesPlayed">0</div>
                <div class="stat-label">Игр сыграно</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="winStreak">0</div>
                <div class="stat-label">Побед подряд</div>
            </div>
            <div class="stat-item">
                <div class="stat-value" id="level">1</div>
                <div class="stat-label">Уровень</div>
            </div>
        </div>

        <!-- ПРОГРЕСС БАР УРОВНЯ -->
        <div class="progress-bar">
            <div class="progress-fill" id="xpBar" style="width: 25%;"></div>
        </div>
        <div style="text-align: center; color: #aaa; margin-bottom: 20px;">
            До следующего уровня: <span id="xpText">250/1000</span> XP
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

        <!-- ПОДВАЛ -->
        <div class="footer">
            © 2024 MEGA CASINO | Только для лиц старше 18 лет
        </div>
    </div>

    <!-- ========== 15 ИГРОВЫХ ЭКРАНОВ ========== -->

    <!-- 1. МЕГА СЛОТЫ -->
    <div class="game-screen" id="slotsScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎰 MEGA SLOTS 5x3</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="slotsBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="slotsBetDisplay">Ставка: 1,000</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeSlotsBet(-1000)">-1000</button>
                <button class="bet-btn" onclick="changeSlotsBet(-100)">-100</button>
                <button class="bet-btn" onclick="changeSlotsBet(100)">+100</button>
                <button class="bet-btn" onclick="changeSlotsBet(1000)">+1000</button>
                <button class="bet-btn" onclick="maxSlotsBet()" style="background: var(--accent);">MAX</button>
            </div>

            <div style="
                display: grid;
                grid-template-columns: repeat(5, 1fr);
                gap: 15px;
                margin: 40px 0;
                perspective: 1000px;
            " id="slotsGrid">
                <!-- 5x3 слоты -->
            </div>

            <div style="text-align: center;">
                <button id="spinBtn" style="
                    width: 150px;
                    height: 150px;
                    border-radius: 50%;
                    background: var(--gradient);
                    border: none;
                    color: white;
                    font-family: 'Orbitron', sans-serif;
                    font-size: 1.5rem;
                    font-weight: 900;
                    cursor: pointer;
                    transition: all 0.3s ease;
                    box-shadow: 0 0 30px var(--primary);
                " onclick="spinSlots()">
                    SPIN
                </button>
            </div>

            <div style="
                background: rgba(0,0,0,0.3);
                border-radius: 20px;
                padding: 20px;
                margin-top: 30px;
            ">
                <h3 style="color: var(--accent); margin-bottom: 15px;">💰 Выплаты:</h3>
                <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px;">
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">7️⃣</div>
                        <div>x10</div>
                    </div>
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">💎</div>
                        <div>x8</div>
                    </div>
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">⭐</div>
                        <div>x6</div>
                    </div>
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">🍒</div>
                        <div>x5</div>
                    </div>
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">🔔</div>
                        <div>x4</div>
                    </div>
                    <div style="text-align: center;">
                        <div style="font-size: 2rem;">🍀</div>
                        <div>x3</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 2. ТЕХАС ПОКЕР -->
    <div class="game-screen" id="pokerScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">♠️ TEXAS HOLD'EM</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="pokerBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="pokerBetDisplay">Ставка: 2,000</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changePokerBet(-500)">-500</button>
                <button class="bet-btn" onclick="changePokerBet(500)">+500</button>
                <button class="bet-btn" onclick="dealPoker()" style="background: var(--success);">РАЗДАТЬ</button>
                <button class="bet-btn" onclick="callPoker()" style="background: var(--secondary);">КОЛЛ</button>
                <button class="bet-btn" onclick="foldPoker()" style="background: var(--danger);">ПАС</button>
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 1.2rem; color: var(--accent); margin-bottom: 10px;">
                    Банк: <span id="pokerPot">0</span>
                </div>
                <div style="color: #aaa;">Статус: <span id="pokerStatus">Ждем ставку</span></div>
            </div>

            <div style="
                display: flex;
                justify-content: center;
                gap: 15px;
                margin: 30px 0;
                flex-wrap: wrap;
            " id="playerHand">
                <!-- Карты игрока -->
            </div>

            <div style="text-align: center; margin: 40px 0;">
                <div style="color: var(--danger); margin-bottom: 15px;">ДИЛЕР</div>
                <div style="
                    display: flex;
                    justify-content: center;
                    gap: 15px;
                    flex-wrap: wrap;
                " id="dealerHand">
                    <!-- Карты дилера -->
                </div>
            </div>
        </div>
    </div>

    <!-- 3. 3D КОСТИ -->
    <div class="game-screen" id="diceScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎲 3D DICE</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="diceBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="diceBetDisplay">Ставка: 500</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeDiceBet(-100)">-100</button>
                <button class="bet-btn" onclick="changeDiceBet(100)">+100</button>
                <button class="bet-btn" onclick="rollDice()" style="background: var(--success);">БРОСИТЬ</button>
                <button class="bet-btn" onclick="doubleDice()" style="background: var(--accent);">x2</button>
                <button class="bet-btn" onclick="autoDice()" style="background: var(--secondary);">АВТО</button>
            </div>

            <div style="
                display: flex;
                justify-content: center;
                gap: 50px;
                margin: 50px 0;
            " id="diceResult">
                <!-- Кости -->
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 2.5rem; color: var(--accent);" id="diceSum">
                    Сумма: 7
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    Ставка: <span id="diceTarget">7 или 11 (x3)</span>
                </div>
            </div>

            <div class="user-stats">
                <div class="stat-item">
                    <div class="stat-value" id="diceStreak">0</div>
                    <div class="stat-label">Серия</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="diceBest">0</div>
                    <div class="stat-label">Рекорд</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="diceWins">0</div>
                    <div class="stat-label">Побед</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="diceRate">0%</div>
                    <div class="stat-label">Процент</div>
                </div>
            </div>
        </div>
    </div>

    <!-- 4. РУЛЕТКА -->
    <div class="game-screen" id="rouletteScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎯 ROULETTE</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="rouletteBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="rouletteBetDisplay">Ставка: 200</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeRouletteBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeRouletteBet(50)">+50</button>
                <button class="bet-btn" onclick="placeRouletteBet('red')" style="background: #ff4444;">КРАСНОЕ</button>
                <button class="bet-btn" onclick="placeRouletteBet('black')" style="background: #333;">ЧЕРНОЕ</button>
                <button class="bet-btn" onclick="spinRoulette()" style="background: var(--success);">КРУТИТЬ</button>
            </div>

            <div style="
                width: 300px;
                height: 300px;
                margin: 40px auto;
                background: conic-gradient(
                    #ff0000 0deg 180deg,
                    #000000 180deg 360deg
                );
                border-radius: 50%;
                position: relative;
                border: 10px solid #8b4513;
                box-shadow: 0 20px 40px rgba(0,0,0,0.5);
                transition: transform 3s cubic-bezier(0.1, 0.7, 0.1, 1);
            " id="rouletteWheel">
                <div style="
                    position: absolute;
                    top: -20px;
                    left: 50%;
                    transform: translateX(-50%);
                    width: 40px;
                    height: 40px;
                    background: gold;
                    clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
                    z-index: 2;
                "></div>
                <div style="
                    position: absolute;
                    top: 50%;
                    left: 50%;
                    transform: translate(-50%, -50%);
                    width: 60px;
                    height: 60px;
                    background: #006400;
                    border-radius: 50%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size: 1.5rem;
                    font-weight: bold;
                    color: white;
                ">0</div>
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 2rem; color: var(--accent);" id="rouletteResult">
                    Ждем результат...
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    История: <span id="rouletteHistory">-</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 5. БЛЭКДЖЕК -->
    <div class="game-screen" id="blackjackScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">♣️ BLACKJACK</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="blackjackBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="blackjackBetDisplay">Ставка: 1,000</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeBlackjackBet(-200)">-200</button>
                <button class="bet-btn" onclick="changeBlackjackBet(200)">+200</button>
                <button class="bet-btn" onclick="dealBlackjack()" style="background: var(--success);">РАЗДАТЬ</button>
                <button class="bet-btn" onclick="hitBlackjack()" style="background: var(--secondary);">ЕЩЕ</button>
                <button class="bet-btn" onclick="standBlackjack()" style="background: var(--danger);">ХВАТИТ</button>
            </div>

            <div style="text-align: center; margin: 40px 0;">
                <div style="font-size: 1.5rem; color: var(--accent); margin-bottom: 20px;">
                    Ваша рука: <span id="playerScore">0</span>
                </div>
                <div style="
                    display: flex;
                    justify-content: center;
                    gap: 15px;
                    flex-wrap: wrap;
                " id="blackjackPlayer">
                    <!-- Карты игрока -->
                </div>
            </div>

            <div style="text-align: center; margin: 40px 0;">
                <div style="font-size: 1.5rem; color: var(--danger); margin-bottom: 20px;">
                    Дилер: <span id="dealerScore">?</span>
                </div>
                <div style="
                    display: flex;
                    justify-content: center;
                    gap: 15px;
                    flex-wrap: wrap;
                " id="blackjackDealer">
                    <!-- Карты дилера -->
                </div>
            </div>
        </div>
    </div>

    <!-- 6. БАККАРА -->
    <div class="game-screen" id="baccaratScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">💎 BACCARAT</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="baccaratBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="baccaratBetDisplay">Ставка: 2,000</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeBaccaratBet(-500)">-500</button>
                <button class="bet-btn" onclick="changeBaccaratBet(500)">+500</button>
                <button class="bet-btn" onclick="placeBaccaratBet('player')" style="background: var(--success);">ИГРОК</button>
                <button class="bet-btn" onclick="placeBaccaratBet('banker')" style="background: var(--primary);">БАНКИР</button>
                <button class="bet-btn" onclick="placeBaccaratBet('tie')" style="background: var(--accent);">НИЧЬЯ</button>
            </div>

            <div style="text-align: center; margin: 40px 0;">
                <div style="color: var(--accent); margin-bottom: 20px;">ИГРОК</div>
                <div style="
                    display: flex;
                    justify-content: center;
                    gap: 15px;
                    margin-bottom: 40px;
                " id="baccaratPlayer">
                    <!-- Карты игрока -->
                </div>
                
                <div style="color: var(--danger); margin-bottom: 20px;">БАНКИР</div>
                <div style="
                    display: flex;
                    justify-content: center;
                    gap: 15px;
                " id="baccaratBanker">
                    <!-- Карты банкира -->
                </div>
            </div>

            <div style="text-align: center; font-size: 2rem; color: var(--accent);" id="baccaratResult">
                Сделайте ставку
            </div>
        </div>
    </div>

    <!-- 7. КРЕПС -->
    <div class="game-screen" id="crapsScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎲 CRAPS</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="crapsBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="crapsBetDisplay">Ставка: 500</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeCrapsBet(-100)">-100</button>
                <button class="bet-btn" onclick="changeCrapsBet(100)">+100</button>
                <button class="bet-btn" onclick="placeCrapsBet('pass')" style="background: var(--success);">PASS</button>
                <button class="bet-btn" onclick="placeCrapsBet('dont')" style="background: var(--danger);">DON'T</button>
                <button class="bet-btn" onclick="rollCraps()" style="background: var(--accent);">БРОСИТЬ</button>
            </div>

            <div style="
                display: flex;
                justify-content: center;
                gap: 30px;
                margin: 50px 0;
            " id="crapsDice">
                <!-- Кости для крепса -->
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 2.5rem; color: var(--accent);" id="crapsSum">
                    Сумма: -
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    Точка: <span id="crapsPoint">-</span>
                </div>
            </div>

            <div style="
                background: rgba(0,0,0,0.3);
                border-radius: 20px;
                padding: 20px;
                margin-top: 30px;
            ">
                <h3 style="color: var(--accent); margin-bottom: 15px;">🎯 Выигрышные комбинации:</h3>
                <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px;">
                    <div>7 или 11 (Pass) - x1</div>
                    <div>2, 3, 12 (Don't) - x1</div>
                    <div>Повтор точки - x2</div>
                    <div>7 до точки - x1.5</div>
                </div>
            </div>
        </div>
    </div>

    <!-- 8. КЕНО -->
    <div class="game-screen" id="kenoScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🔢 KENO</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="kenoBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="kenoBetDisplay">Ставка: 100</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeKenoBet(-10)">-10</button>
                <button class="bet-btn" onclick="changeKenoBet(10)">+10</button>
                <button class="bet-btn" onclick="pickKenoNumbers()" style="background: var(--success);">ВЫБРАТЬ</button>
                <button class="bet-btn" onclick="playKeno()" style="background: var(--accent);">ИГРАТЬ</button>
                <button class="bet-btn" onclick="clearKeno()" style="background: var(--danger);">СБРОС</button>
            </div>

            <div style="
                display: grid;
                grid-template-columns: repeat(10, 1fr);
                gap: 8px;
                margin: 40px 0;
            " id="kenoGrid">
                <!-- Сетка кено 1-80 -->
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 1.5rem; color: var(--accent);">
                    Выбрано: <span id="kenoSelected">0</span> / 10 чисел
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    Множитель: <span id="kenoMultiplier">x0</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 9. КОЛЕСО ФОРТУНЫ -->
    <div class="game-screen" id="wheelScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎡 WHEEL OF FORTUNE</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="wheelBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="wheelBetDisplay">Ставка: 200</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeWheelBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeWheelBet(50)">+50</button>
                <button class="bet-btn" onclick="spinWheel()" style="background: var(--gradient); font-size: 1.2rem; font-weight: 900;">
                    КРУТИТЬ КОЛЕСО!
                </button>
            </div>

            <div style="
                width: 300px;
                height: 300px;
                margin: 50px auto;
                position: relative;
            " id="fortuneWheel">
                <!-- Колесо фортуны -->
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 2rem; color: var(--accent);" id="wheelResult">
                    УДАЧИ!
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    Последний выигрыш: <span id="wheelLastWin">0</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 10. ПЛИНКО -->
    <div class="game-screen" id="plinkoScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🔶 PLINKO</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="plinkoBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="plinkoBetDisplay">Ставка: 100</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changePlinkoBet(-10)">-10</button>
                <button class="bet-btn" onclick="changePlinkoBet(10)">+10</button>
                <button class="bet-btn" onclick="dropPlinko()" style="background: var(--success);">БРОСИТЬ</button>
                <button class="bet-btn" onclick="multiDropPlinko()" style="background: var(--accent);">5 ШАРИКОВ</button>
                <button class="bet-btn" onclick="autoPlinko()" style="background: var(--secondary);">АВТО</button>
            </div>

            <div style="
                width: 100%;
                height: 400px;
                margin: 30px auto;
                background: linear-gradient(to bottom, #1a1a2e, #16213e);
                border-radius: 10px;
                position: relative;
                overflow: hidden;
            " id="plinkoBoard">
                <!-- Доска плинко -->
            </div>

            <div style="
                display: grid;
                grid-template-columns: repeat(7, 1fr);
                gap: 5px;
                margin: 30px 0;
            " id="plinkoScores">
                <!-- Множители -->
            </div>
        </div>
    </div>

    <!-- 11. МИНИ-ГОЛФ -->
    <div class="game-screen" id="golfScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">⛳ MINI GOLF</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="golfBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="golfBetDisplay">Ставка: 500</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeGolfBet(-100)">-100</button>
                <button class="bet-btn" onclick="changeGolfBet(100)">+100</button>
                <button class="bet-btn" onclick="startGolf()" style="background: var(--success);">СТАРТ</button>
                <button class="bet-btn" onclick="hitGolf()" style="background: var(--accent);">УДАР</button>
                <button class="bet-btn" onclick="resetGolf()" style="background: var(--danger);">СБРОС</button>
            </div>

            <div style="
                width: 100%;
                height: 300px;
                margin: 30px auto;
                background: linear-gradient(135deg, #00a86b, #32cd32);
                border-radius: 20px;
                position: relative;
                overflow: hidden;
                border: 5px solid #8b4513;
            " id="golfCourse">
                <!-- Поле для гольфа -->
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <div style="font-size: 1.5rem; color: var(--accent);">
                    Ударов: <span id="golfStrokes">0</span>
                </div>
                <div style="color: #aaa; margin-top: 10px;">
                    Цель: попасть в лунку за ≤5 ударов
                </div>
            </div>
        </div>
    </div>

    <!-- 12. АРКАНОИД -->
    <div class="game-screen" id="arkanoidScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎮 ARKANOID</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="arkanoidBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="arkanoidBetDisplay">Ставка: 200</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeArkanoidBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeArkanoidBet(50)">+50</button>
                <button class="bet-btn" onclick="startArkanoid()" style="background: var(--success);">СТАРТ</button>
                <button class="bet-btn" onclick="pauseArkanoid()" style="background: var(--accent);">ПАУЗА</button>
                <button class="bet-btn" onclick="resetArkanoid()" style="background: var(--danger);">РЕСТАРТ</button>
            </div>

            <div style="
                width: 100%;
                height: 400px;
                margin: 30px auto;
                background: #111;
                border-radius: 10px;
                position: relative;
                overflow: hidden;
                border: 3px solid var(--accent);
            " id="arkanoidCanvas">
                <!-- Канвас для арканоида -->
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent);">
                    Счёт: <span id="arkanoidScore">0</span> | Жизни: <span id="arkanoidLives">3</span> | Уровень: <span id="arkanoidLevel">1</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 13. СНАЙПЕР -->
    <div class="game-screen" id="sniperScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🎯 SNIPER</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="sniperBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="sniperBetDisplay">Ставка: 300</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeSniperBet(-50)">-50</button>
                <button class="bet-btn" onclick="changeSniperBet(50)">+50</button>
                <button class="bet-btn" onclick="startSniper()" style="background: var(--success);">СТАРТ</button>
                <button class="bet-btn" onclick="fireSniper()" style="background: var(--danger);">ВЫСТРЕЛ</button>
                <button class="bet-btn" onclick="autoSniper()" style="background: var(--secondary);">АВТО</button>
            </div>

            <div style="
                width: 100%;
                height: 400px;
                margin: 30px auto;
                background: linear-gradient(135deg, #87CEEB, #4682B4);
                border-radius: 10px;
                position: relative;
                overflow: hidden;
                border: 3px solid #8b4513;
            " id="sniperRange">
                <!-- Стрельбище -->
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent);">
                    Попадания: <span id="sniperHits">0</span>/<span id="sniperShots">0</span> |
                    Точность: <span id="sniperAccuracy">0%</span>
                </div>
            </div>
        </div>
    </div>

    <!-- 14. ГОНКИ -->
    <div class="game-screen" id="racingScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🏎️ RACING</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="racingBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="racingBetDisplay">Ставка: 1,000</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeRacingBet(-200)">-200</button>
                <button class="bet-btn" onclick="changeRacingBet(200)">+200</button>
                <button class="bet-btn" onclick="startRace()" style="background: var(--success);">СТАРТ</button>
                <button class="bet-btn" onclick="accelerate()" style="background: var(--accent);">ГАЗ</button>
                <button class="bet-btn" onclick="brake()" style="background: var(--danger);">ТОРМОЗ</button>
            </div>

            <div style="
                width: 100%;
                height: 400px;
                margin: 30px auto;
                background: linear-gradient(135deg, #228B22, #32CD32);
                border-radius: 10px;
                position: relative;
                overflow: hidden;
                border: 5px solid #8b4513;
            " id="raceTrack">
                <!-- Трасса -->
            </div>

            <div style="text-align: center; margin: 20px 0;">
                <div style="font-size: 1.2rem; color: var(--accent);">
                    Позиция: <span id="racePosition">1</span> | Скорость: <span id="raceSpeed">0</span> км/ч | Время: <span id="raceTime">0</span>с
                </div>
            </div>
        </div>
    </div>

    <!-- 15. ТЕТРИС -->
    <div class="game-screen" id="tetrisScreen">
        <div class="screen-header">
            <button class="back-btn" onclick="closeGame()">
                <i class="fas fa-arrow-left"></i>
            </button>
            <h2 style="font-family: 'Montserrat', sans-serif; color: var(--accent);">🧩 TETRIS</h2>
            <div class="balance-container">
                <i class="fas fa-coins"></i>
                <span id="tetrisBalance">100,000</span>
            </div>
        </div>

        <div class="game-container">
            <div class="current-bet" id="tetrisBetDisplay">Ставка: 100</div>
            
            <div class="bet-controls">
                <button class="bet-btn" onclick="changeTetrisBet(-10)">-10</button>
                <button class="bet-btn" onclick="changeTetrisBet(10)">+10</button>
                <button class="bet-btn" onclick="startTetris()" style="background: var(--success);">СТАРТ</button>
                <button class="bet-btn" onclick="pauseTetris()" style="background: var(--accent);">ПАУЗА</button>
                <button class="bet-btn" onclick="resetTetris()" style="background: var(--danger);">РЕСТАРТ</button>
            </div>

            <div style="
                display: flex;
                justify-content: center;
                gap: 30px;
                margin: 30px 0;
                flex-wrap: wrap;
            ">
                <div style="
                    width: 200px;
                    height: 400px;
                    background: #111;
                    border: 3px solid var(--accent);
                    position: relative;
                " id="tetrisBoard">
                    <!-- Поле тетриса -->
                </div>
                
                <div style="
                    background: rgba(0,0,0,0.3);
                    padding: 20px;
                    border-radius: 15px;
                    min-width: 150px;
                ">
                    <h3 style="color: var(--accent); margin-bottom: 15px;">ИНФО</h3>
                    <div>Счёт: <span id="tetrisScore">0</span></div>
                    <div>Уровень: <span id="tetrisLevel">1</span></div>
                    <div>Линии: <span id="tetrisLines">0</span></div>
                    <div>Следующая:</div>
                    <div id="tetrisNext" style="margin-top: 10px;"></div>
                </div>
            </div>

            <div style="text-align: center; color: #aaa; margin-top: 20px;">
                Управление: ← → (двигать), ↑ (повернуть), ↓ (ускорить)
            </div>
        </div>
    </div>

    <!-- МОДАЛЬНОЕ ОКНО С ПРАВИЛАМИ -->
    <div class="modal" id="rulesModal">
        <div class="modal-content">
            <h2 style="color: var(--accent); margin-bottom: 20px;">📖 ПРАВИЛА ИГРЫ</h2>
            <div id="modalRules"></div>
            <button class="bet-btn" onclick="closeModal()" style="width: 100%; margin-top: 20px; background: var(--danger);">
                ЗАКРЫТЬ
            </button>
        </div>
    </div>

    <script>
        // ========== ИНИЦИАЛИЗАЦИЯ ==========
        const tg = window.Telegram.WebApp;
        tg.expand();
        tg.ready();
        
        // Глобальные переменные
        let balance = 100000;
        let totalWins = 0;
        let gamesPlayed = 0;
        let winStreak = 0;
        let level = 1;
        let xp = 0;
        let currentGame = null;
        
        // Игры
        const games = [
            { id: 'slots', name: '🎰 MEGA SLOTS', description: '5 барабанов, 20 линий, джекпоты', icon: 'fas fa-sliders-h', category: 'slots' },
            { id: 'poker', name: '♠️ TEXAS HOLD\'EM', description: 'Покер против AI, турниры', icon: 'fas fa-spade', category: 'cards' },
            { id: 'dice', name: '🎲 3D DICE', description: 'Физика броска, множители до x100', icon: 'fas fa-dice', category: 'dice' },
            { id: 'roulette', name: '🎯 ROULETTE', description: 'Европейская рулетка с физикой', icon: 'fas fa-circle', category: 'roulette' },
            { id: 'blackjack', name: '♣️ BLACKJACK', description: '21 очко против дилера', icon: 'fas fa-club', category: 'cards' },
            { id: 'baccarat', name: '💎 BACCARAT', description: 'Punto Banco, Dragon Bonus', icon: 'fas fa-gem', category: 'cards' },
            { id: 'craps', name: '🎲 CRAPS', description: 'Американская игра в кости', icon: 'fas fa-dice-five', category: 'dice' },
            { id: 'keno', name: '🔢 KENO', description: 'Выбери числа и выигрывай', icon: 'fas fa-hashtag', category: 'special' },
            { id: 'wheel', name: '🎡 WHEEL OF FORTUNE', description: 'Колесо удачи с джекпотом', icon: 'fas fa-gift', category: 'special' },
            { id: 'plinko', name: '🔶 PLINKO', description: 'Шарики, пирамиды, выигрыши', icon: 'fas fa-bowling-ball', category: 'special' },
            { id: 'golf', name: '⛳ MINI GOLF', description: 'Мини-гольф с физикой', icon: 'fas fa-golf-ball', category: 'special' },
            { id: 'arkanoid', name: '🎮 ARKANOID', description: 'Классика с бонусами', icon: 'fas fa-gamepad', category: 'arcade' },
            { id: 'sniper', name: '🎯 SNIPER', description: 'Точность и реакция', icon: 'fas fa-crosshairs', category: 'arcade' },
            { id: 'racing', name: '🏎️ RACING', description: 'Гонки на выживание', icon: 'fas fa-flag-checkered', category: 'arcade' },
            { id: 'tetris', name: '🧩 TETRIS', description: 'Классический тетрис', icon: 'fas fa-th', category: 'arcade' }
        ];

        // ========== ОСНОВНЫЕ ФУНКЦИИ ==========
        function initApp() {
            updateUI();
            renderGames();
            setupTelegram();
        }

        function updateUI() {
            document.getElementById('balance').textContent = balance.toLocaleString();
            document.getElementById('totalWins').textContent = totalWins.toLocaleString();
            document.getElementById('gamesPlayed').textContent = gamesPlayed;
            document.getElementById('winStreak').textContent = winStreak;
            document.getElementById('level').textContent = level;
            
            const xpNeeded = level * 1000;
            const xpPercent = (xp / xpNeeded) * 100;
            document.getElementById('xpBar').style.width = `${Math.min(xpPercent, 100)}%`;
            document.getElementById('xpText').textContent = `${xp}/${xpNeeded}`;
        }

        function addBalance(amount) {
            balance += amount;
            if (amount > 0) {
                totalWins += amount;
                winStreak++;
                xp += Math.floor(amount / 100);
                
                // Проверка уровня
                const xpNeeded = level * 1000;
                if (xp >= xpNeeded) {
                    level++;
                    xp = xp - xpNeeded;
                    showNotification(`🎉 УРОВЕНЬ ПОВЫШЕН! Теперь уровень ${level}!`, 'success');
                    createConfetti(200);
                }
            } else {
                winStreak = 0;
            }
            updateUI();
        }

        function deductBalance(amount) {
            if (balance >= amount) {
                balance -= amount;
                gamesPlayed++;
                updateUI();
                return true;
            }
            showNotification('Недостаточно средств!', 'error');
            return false;
        }

        function showNotification(text, type = 'info') {
            const notification = document.getElementById('notification');
            notification.textContent = text;
            notification.style.background = type === 'error' ? 
                'linear-gradient(135deg, var(--danger), #ff0066)' :
                'linear-gradient(135deg, var(--primary), var(--secondary))';
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        function createConfetti(count = 100) {
            const container = document.getElementById('confettiContainer');
            const colors = ['#ff3366', '#33ccff', '#ffcc00', '#00ff88'];
            
            for (let i = 0; i < count; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.animationDuration = (Math.random() * 2 + 1) + 's';
                confetti.style.animationDelay = Math.random() * 1 + 's';
                container.appendChild(confetti);
                
                setTimeout(() => confetti.remove(), 3000);
            }
        }

        function renderGames(category = 'all') {
            const grid = document.getElementById('gamesGrid');
            grid.innerHTML = '';
            
            const filtered = category === 'all' ? games : games.filter(g => g.category === category);
            
            filtered.forEach(game => {
                const card = document.createElement('div');
                card.className = 'game-card';
                card.onclick = () => openGame(game.id);
                
                card.innerHTML = `
                    <div class="game-badge">${game.category.toUpperCase()}</div>
                    <div class="game-icon">
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

        function showCategory(category) {
            document.querySelectorAll('.nav-tab').forEach(tab => tab.classList.remove('active'));
            event.target.classList.add('active');
            renderGames(category);
        }

        function openGame(gameId) {
            currentGame = gameId;
            document.getElementById('mainContent').style.display = 'none';
            document.getElementById(`${gameId}Screen`).classList.add('active');
            
            // Инициализация конкретной игры
            if (typeof window[`init${gameId.charAt(0).toUpperCase() + gameId.slice(1)}`] === 'function') {
                window[`init${gameId.charAt(0).toUpperCase() + gameId.slice(1)}`]();
            }
            
            // Обновить баланс на экране игры
            updateGameBalance(gameId);
        }

        function updateGameBalance(gameId) {
            const balanceEl = document.getElementById(`${gameId}Balance`);
            if (balanceEl) balanceEl.textContent = balance.toLocaleString();
        }

        function closeGame() {
            if (currentGame) {
                document.getElementById(`${currentGame}Screen`).classList.remove('active');
            }
            document.getElementById('mainContent').style.display = 'block';
            currentGame = null;
            updateUI();
        }

        function setupTelegram() {
            tg.MainButton.setText('💎 ПОПОЛНИТЬ +10K');
            tg.MainButton.show();
            tg.MainButton.onClick(() => {
                addBalance(10000);
                showNotification('Баланс пополнен на 10,000!', 'success');
            });
        }

        // ========== ИГРА 1: СЛОТЫ ==========
        let slotsBet = 1000;
        let slotsSymbols = ['7️⃣', '💎', '⭐', '🍒', '🔔', '🍀', '💰', '👑'];

        function initSlots() {
            updateGameBalance('slots');
            document.getElementById('slotsBetDisplay').textContent = `Ставка: ${slotsBet.toLocaleString()}`;
            
            // Создать сетку 5x3
            const grid = document.getElementById('slotsGrid');
            grid.innerHTML = '';
            
            for (let i = 0; i < 15; i++) {
                const cell = document.createElement('div');
                cell.style.cssText = `
                    aspect-ratio: 1;
                    background: linear-gradient(135deg, rgba(255,255,255,0.1), rgba(0,0,0,0.2));
                    border-radius: 15px;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size: 2rem;
                    border: 2px solid rgba(255,255,255,0.1);
                `;
                cell.textContent = slotsSymbols[Math.floor(Math.random() * slotsSymbols.length)];
                grid.appendChild(cell);
            }
        }

        function changeSlotsBet(amount) {
            slotsBet = Math.max(100, Math.min(10000, slotsBet + amount));
            document.getElementById('slotsBetDisplay').textContent = `Ставка: ${slotsBet.toLocaleString()}`;
        }

        function maxSlotsBet() {
            slotsBet = Math.min(10000, Math.floor(balance / 10) * 10 || 100);
            document.getElementById('slotsBetDisplay').textContent = `Ставка: ${slotsBet.toLocaleString()}`;
        }

        function spinSlots() {
            if (!deductBalance(slotsBet)) return;
            
            const grid = document.getElementById('slotsGrid');
            const cells = grid.children;
            const spinBtn = document.getElementById('spinBtn');
            
            // Анимация вращения
            spinBtn.disabled = true;
            spinBtn.textContent = '...';
            
            for (let i = 0; i < cells.length; i++) {
                setTimeout(() => {
                    cells[i].style.transform = 'translateY(-20px)';
                    setTimeout(() => {
                        cells[i].textContent = slotsSymbols[Math.floor(Math.random() * slotsSymbols.length)];
                        cells[i].style.transform = 'translateY(0)';
                    }, 200);
                }, i * 50);
            }
            
            // Проверить выигрыш
            setTimeout(() => {
                checkSlotsWin(cells);
                spinBtn.disabled = false;
                spinBtn.textContent = 'SPIN';
            }, 1000);
        }

        function checkSlotsWin(cells) {
            const lines = [
                [0,1,2,3,4], [5,6,7,8,9], [10,11,12,13,14], // Горизонтальные
                [0,6,12], [4,8,12], // Диагонали
                [0,1,2], [5,6,7], [10,11,12], // Короткие горизонтальные
                [2,3,4], [7,8,9], [12,13,14]
            ];
            
            let winAmount = 0;
            const multipliers = {
                '7️⃣': 10, '💎': 8, '⭐': 6, '🍒': 5,
                '🔔': 4, '🍀': 3, '💰': 2, '👑': 15
            };
            
            lines.forEach(line => {
                const symbols = line.map(idx => cells[idx].textContent);
                if (symbols.every(s => s === symbols[0])) {
                    const multiplier = multipliers[symbols[0]] || 2;
                    winAmount += slotsBet * multiplier;
                    
                    // Подсветка
                    line.forEach(idx => {
                        cells[idx].style.background = 'linear-gradient(135deg, #ffcc00, #ff9900)';
                        cells[idx].style.borderColor = '#ffcc00';
                        setTimeout(() => {
                            cells[idx].style.background = 'linear-gradient(135deg, rgba(255,255,255,0.1), rgba(0,0,0,0.2))';
                            cells[idx].style.borderColor = 'rgba(255,255,255,0.1)';
                        }, 1000);
                    });
                }
            });
            
            if (winAmount > 0) {
                addBalance(winAmount);
                showNotification(`🎰 ДЖЕКПОТ! Выигрыш ${winAmount.toLocaleString()}!`, 'success');
                createConfetti(200);
            } else {
                showNotification('Попробуйте еще раз!', 'info');
            }
            
            updateGameBalance('slots');
        }

        // ========== ИГРА 2: ПОКЕР ==========
        let pokerBet = 2000;
        let pokerPot = 0;

        function initPoker() {
            updateGameBalance('poker');
            document.getElementById('pokerBetDisplay').textContent = `Ставка: ${pokerBet.toLocaleString()}`;
            document.getElementById('pokerPot').textContent = '0';
            document.getElementById('pokerStatus').textContent = 'Сделайте ставку';
            
            // Очистить карты
            document.getElementById('playerHand').innerHTML = '';
            document.getElementById('dealerHand').innerHTML = '';
        }

        function changePokerBet(amount) {
            pokerBet = Math.max(500, Math.min(5000, pokerBet + amount));
            document.getElementById('pokerBetDisplay').textContent = `Ставка: ${pokerBet.toLocaleString()}`;
        }

        function dealPoker() {
            if (!deductBalance(pokerBet)) return;
            
            pokerPot = pokerBet * 2;
            document.getElementById('pokerPot').textContent = pokerPot.toLocaleString();
            document.getElementById('pokerStatus').textContent = 'Ваш ход';
            
            // Создать карты
            const playerHand = document.getElementById('playerHand');
            const dealerHand = document.getElementById('dealerHand');
            playerHand.innerHTML = '';
            dealerHand.innerHTML = '';
            
            const cards = ['A', 'K', 'Q', 'J', '10', '9', '8'];
            const suits = ['♥', '♦', '♠', '♣'];
            
            // Раздать карты игроку
            for (let i = 0; i < 2; i++) {
                const card = document.createElement('div');
                card.style.cssText = `
                    width: 80px;
                    height: 120px;
                    background: white;
                    border-radius: 10px;
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    justify-content: center;
                    font-size: 2rem;
                    font-weight: bold;
                    color: ${Math.random() > 0.5 ? '#c00' : '#000'};
                    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
                `;
                card.textContent = suits[Math.floor(Math.random() * suits.length)];
                playerHand.appendChild(card);
            }
            
            // Раздать карты дилеру (одна скрыта)
            for (let i = 0; i < 2; i++) {
                const card = document.createElement('div');
                card.style.cssText = `
                    width: 80px;
                    height: 120px;
                    background: ${i === 0 ? '#333' : 'white'};
                    border-radius: 10px;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size: ${i === 0 ? '1.5rem' : '2rem'};
                    font-weight: bold;
                    color: ${i === 0 ? '#666' : (Math.random() > 0.5 ? '#c00' : '#000')};
                    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
                `;
                card.textContent = i === 0 ? '?' : suits[Math.floor(Math.random() * suits.length)];
                dealerHand.appendChild(card);
            }
        }

        function foldPoker() {
            if (pokerPot === 0) return;
            
            pokerPot = 0;
            document.getElementById('pokerPot').textContent = '0';
            document.getElementById('pokerStatus').textContent = 'Вы спасовали';
            showNotification('Вы спасовали', 'info');
        }

        function callPoker() {
            if (pokerPot === 0) {
                showNotification('Сначала сделайте ставку!', 'error');
                return;
            }
            
            if (!deductBalance(pokerBet)) return;
            
            pokerPot += pokerBet;
            document.getElementById('pokerPot').textContent = pokerPot.toLocaleString();
            
            // Открыть карты дилера
            const dealerCards = document.getElementById('dealerHand').children;
            dealerCards[0].style.background = 'white';
            dealerCards[0].style.color = Math.random() > 0.5 ? '#c00' : '#000';
            dealerCards[0].style.fontSize = '2rem';
            dealerCards[0].textContent = ['♥', '♦', '♠', '♣'][Math.floor(Math.random() * 4)];
            
            // Определить победителя (случайно)
            setTimeout(() => {
                if (Math.random() > 0.5) {
                    const winAmount = pokerPot * 2;
                    addBalance(winAmount);
                    showNotification(`🎉 ПОБЕДА! Выигрыш ${winAmount.toLocaleString()}!`, 'success');
                    createConfetti(100);
                } else {
                    showNotification('Дилер победил', 'error');
                }
                
                pokerPot = 0;
                document.getElementById('pokerPot').textContent = '0';
                document.getElementById('pokerStatus').textContent = 'Игра окончена';
                updateGameBalance('poker');
            }, 1000);
        }

        // ========== ИГРА 3: КОСТИ ==========
        let diceBet = 500;
        let diceStats = { streak: 0, best: 0, wins: 0, total: 0 };

        function initDice() {
            updateGameBalance('dice');
            document.getElementById('diceBetDisplay').textContent = `Ставка: ${diceBet.toLocaleString()}`;
            
            // Создать кости
            const container = document.getElementById('diceResult');
            container.innerHTML = '';
            
            for (let i = 0; i < 2; i++) {
                const die = document.createElement('div');
                die.style.cssText = `
                    width: 100px;
                    height: 100px;
                    background: white;
                    border-radius: 20px;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    font-size: 4rem;
                    box-shadow: 0 10px 30px rgba(0,0,0,0.3);
                `;
                die.textContent = '⚀';
                container.appendChild(die);
            }
            
            // Обновить статистику
            updateDiceStats();
        }

        function updateDiceStats() {
            document.getElementById('diceStreak').textContent = diceStats.streak;
            document.getElementById('diceBest').textContent = diceStats.best.toLocaleString();
            document.getElementById('diceWins').textContent = diceStats.wins;
            const rate = diceStats.total > 0 ? Math.round((diceStats.wins / diceStats.total) * 100) : 0;
            document.getElementById('diceRate').textContent = rate + '%';
        }

        function changeDiceBet(amount) {
            diceBet = Math.max(100, Math.min(5000, diceBet + amount));
            document.getElementById('diceBetDisplay').textContent = `Ставка: ${diceBet.toLocaleString()}`;
        }

        function rollDice() {
            if (!deductBalance(diceBet)) return;
            
            diceStats.total++;
            const dice = document.querySelectorAll('#diceResult > div');
            const diceFaces = ['⚀', '⚁', '⚂', '⚃', '⚄', '⚅'];
            
            // Анимация
            dice.forEach(die => {
                die.style.transition = 'transform 0.5s';
                die.style.transform = 'rotate(180deg) scale(1.2)';
            });
            
            setTimeout(() => {
                const die1 = Math.floor(Math.random() * 6) + 1;
                const die2 = Math.floor(Math.random() * 6) + 1;
                const sum = die1 + die2;
                
                dice[0].textContent = diceFaces[die1 - 1];
                dice[1].textContent = diceFaces[die2 - 1];
                dice[0].style.transform = 'rotate(0) scale(1)';
                dice[1].style.transform = 'rotate(0) scale(1)';
                
                document.getElementById('diceSum').textContent = `Сумма: ${sum}`;
                
                // Определить выигрыш
                let multiplier = 0;
                let message = '';
                
                if (sum === 7 || sum === 11) {
                    multiplier = 3;
                    message = '🎉 NATURAL!';
                } else if (die1 === die2) {
                    multiplier = die1 >= 4 ? 5 : 3;
                    message = '🎲 ДУБЛЬ!';
                } else if (sum >= 8 && sum <= 10) {
                    multiplier = 2;
                    message = '👍 ХОРОШО!';
                } else {
                    multiplier = 1.5;
                    message = '✨ НЕПЛОХО!';
                }
                
                const winAmount = Math.floor(diceBet * multiplier);
                
                if (multiplier > 1) {
                    addBalance(winAmount);
                    diceStats.wins++;
                    diceStats.streak++;
                    if (winAmount > diceStats.best) diceStats.best = winAmount;
                    showNotification(`${message} Выигрыш ${winAmount.toLocaleString()} (x${multiplier})`, 'success');
                    if (multiplier >= 3) createConfetti(100);
                } else {
                    diceStats.streak = 0;
                    showNotification(`Сумма: ${sum}. Попробуйте еще!`, 'info');
                }
                
                updateDiceStats();
                updateGameBalance('dice');
            }, 500);
        }

        function doubleDice() {
            diceBet *= 2;
            if (diceBet > 5000) diceBet = 5000;
            document.getElementById('diceBetDisplay').textContent = `Ставка: ${diceBet.toLocaleString()}`;
            showNotification('Ставка удвоена!', 'info');
        }

        function autoDice() {
            if (balance >= diceBet * 10) {
                let count = 0;
                const autoRoll = () => {
                    if (count < 10 && balance >= diceBet) {
                        rollDice();
                        count++;
                        setTimeout(autoRoll, 1500);
                    }
                };
                autoRoll();
            } else {
                showNotification('Нужно минимум 10 ставок для автоигры', 'error');
            }
        }

        // ========== ИГРА 4: РУЛЕТКА ==========
        let rouletteBet = 200;
        let rouletteHistory = [];

        function initRoulette() {
            updateGameBalance('roulette');
            document.getElementById('rouletteBetDisplay').textContent = `Ставка: ${rouletteBet.toLocaleString()}`;
        }

        function changeRouletteBet(amount) {
            rouletteBet = Math.max(50, Math.min(5000, rouletteBet + amount));
            document.getElementById('rouletteBetDisplay').textContent = `Ставка: ${rouletteBet.toLocaleString()}`;
        }

        function placeRouletteBet(type) {
            showNotification(`Ставка на ${type === 'red' ? 'красное' : 'черное'} принята`, 'info');
        }

        function spinRoulette() {
            if (!deductBalance(rouletteBet)) return;
            
            const wheel = document.getElementById('rouletteWheel');
            wheel.style.transition = 'transform 3s cubic-bezier(0.1, 0.7, 0.1, 1)';
            
            // Случайное вращение
            const spins = 5 + Math.random() * 3;
            wheel.style.transform = `rotate(${spins * 360}deg)`;
            
            setTimeout(() => {
                // Результат
                const number = Math.floor(Math.random() * 37);
                const isRed = [1,3,5,7,9,12,14,16,18,19,21,23,25,27,30,32,34,36].includes(number);
                const isBlack = number !== 0 && !isRed;
                
                // Добавить в историю
                rouletteHistory.push(number);
                if (rouletteHistory.length > 5) rouletteHistory.shift();
                document.getElementById('rouletteHistory').textContent = rouletteHistory.join(', ');
                
                // Определить выигрыш
                let winAmount = 0;
                let message = '';
                
                if (Math.random() > 0.47) { // 53% шанс на проигрыш
                    if (number === 0) {
                        winAmount = rouletteBet * 35;
                        message = `🎯 ZERO! Выигрыш ${winAmount.toLocaleString()}!`;
                    } else if (Math.random() > 0.5) {
                        winAmount = rouletteBet * 2;
                        message = `🎯 ${number} ${isRed ? '🔴' : '⚫'}! Выигрыш ${winAmount.toLocaleString()}!`;
                    }
                }
                
                if (winAmount > 0) {
                    addBalance(winAmount);
                    showNotification(message, 'success');
                    if (winAmount > rouletteBet * 5) createConfetti(100);
                } else {
                    showNotification(`${number} ${isRed ? '🔴' : isBlack ? '⚫' : '🟢'}. Попробуйте еще!`, 'info');
                }
                
                document.getElementById('rouletteResult').textContent = 
                    `${number} ${isRed ? '🔴' : isBlack ? '⚫' : '🟢'}`;
                document.getElementById('rouletteResult').style.color = 
                    number === 0 ? '#00ff00' : (isRed ? '#ff4444' : '#000');
                
                updateGameBalance('roulette');
                
                // Сброс анимации
                setTimeout(() => {
                    wheel.style.transition = 'none';
                    wheel.style.transform = 'rotate(0)';
                    setTimeout(() => wheel.style.transition = '', 50);
                }, 1000);
            }, 3000);
        }

        // ========== ОСТАЛЬНЫЕ ИГРЫ - КОРОТКАЯ РЕАЛИЗАЦИЯ ==========

        // Блэкджек
        function initBlackjack() {
            updateGameBalance('blackjack');
            showNotification('Блэкджек: Цель - набрать 21 или ближе к 21', 'info');
        }

        // Баккара
        function initBaccarat() {
            updateGameBalance('baccarat');
            showNotification('Баккара: Ставьте на Игрока, Банкира или Ничью', 'info');
        }

        // Крепс
        function initCraps() {
            updateGameBalance('craps');
            showNotification('Крепс: Бросьте кости и сделайте ставку', 'info');
        }

        // Кено
        function initKeno() {
            updateGameBalance('keno');
            // Создать сетку кено
            const grid = document.getElementById('kenoGrid');
            grid.innerHTML = '';
            for (let i = 1; i <= 80; i++) {
                const cell = document.createElement('div');
                cell.style.cssText = `
                    aspect-ratio: 1;
                    background: linear-gradient(135deg, #3498db, #2980b9);
                    border-radius: 10px;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    color: white;
                    font-weight: bold;
                    cursor: pointer;
                    transition: all 0.3s ease;
                `;
                cell.textContent = i;
                cell.onclick = () => {
                    cell.style.background = 'linear-gradient(135deg, #e74c3c, #c0392b)';
                    cell.style.transform = 'scale(1.1)';
                };
                grid.appendChild(cell);
            }
        }

        // Колесо фортуны
        function initWheel() {
            updateGameBalance('wheel');
            showNotification('Колесо фортуны: Крутите и выигрывайте призы!', 'info');
        }

        // Плинко
        function initPlinko() {
            updateGameBalance('plinko');
            showNotification('Плинко: Бросайте шарики и смотрите куда упадут', 'info');
        }

        // Мини-гольф
        function initGolf() {
            updateGameBalance('golf');
            showNotification('Мини-гольф: Попадите в лунку за минимальное количество ударов', 'info');
        }

        // Арканоид
        function initArkanoid() {
            updateGameBalance('arkanoid');
            showNotification('Арканоид: Разбейте все блоки мячиком', 'info');
        }

        // Снайпер
        function initSniper() {
            updateGameBalance('sniper');
            showNotification('Снайпер: Попадите в цель как можно точнее', 'info');
        }

        // Гонки
        function initRacing() {
            updateGameBalance('racing');
            showNotification('Гонки: Обгоняйте соперников и приходите первым', 'info');
        }

        // Тетрис
        function initTetris() {
            updateGameBalance('tetris');
            showNotification('Тетрис: Собирайте линии и набирайте очки', 'info');
        }

        // ========== МОДАЛЬНОЕ ОКНО ==========
        function showRules(gameId) {
            const rules = {
                slots: '🎰 Слоты: Соберите 3+ одинаковых символа в линии для выигрыша',
                poker: '♠️ Покер: Соберите сильнейшую комбинацию карт',
                dice: '🎲 Кости: 7 или 11 = x3, дубль = x5, 8-10 = x2',
                roulette: '🎯 Рулетка: Красное/Черное = x2, число = x35'
            };
            
            document.getElementById('modalRules').textContent = rules[gameId] || 'Правила игры загружаются...';
            document.getElementById('rulesModal').classList.add('active');
        }

        function closeModal() {
            document.getElementById('rulesModal').classList.remove('active');
        }

        // ========== ИНИЦИАЛИЗАЦИЯ ПРИЛОЖЕНИЯ ==========
        document.addEventListener('DOMContentLoaded', initApp);
        
        // Горячие клавиши
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && currentGame) closeGame();
            if (e.code === 'Space' && currentGame === 'slots') spinSlots();
        });
    </script>
</body>
</html>
