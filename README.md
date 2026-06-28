<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Crypto Wave</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Loading -->
    <div id="loading-screen" class="screen active">
        <div class="loading-container">
            <div class="character">
                <div class="head"></div>
                <div class="body"></div>
            </div>
            <h1 class="loading-text">Loading...</h1>
        </div>
    </div>

    <!-- Welcome -->
    <div id="welcome-screen" class="screen">
        <div class="welcome-container">
            <h1>WELCOME TO CRYPTO WAVE!</h1>
            <p class="subtitle">Join our channels to get started</p>
            
            <div class="join-card">
                <div class="join-item">
                    <span class="icon">📢</span>
                    <div>
                        <h3>Join Crypto Wave Official</h3>
                        <p>Get news & updates</p>
                    </div>
                    <button class="join-btn">JOIN</button>
                </div>
            </div>
            <button id="continue-btn" class="primary-btn">Continue to App</button>
        </div>
    </div>

    <!-- Main App -->
    <div id="main-app" class="screen">
        <header>
            <div class="logo">🌊 Crypto Wave</div>
            <button id="connect-wallet" class="connect-btn">CONNECT WALLET</button>
        </header>

        <div class="balance-section">
            <h3>Total Balance</h3>
            <div class="balance-amount">$2.45</div>
            <div class="balance-change">+0.68 (↑38%)</div>
        </div>

        <div class="assets-section">
            <h3>Your Assets</h3>
            <div class="asset-item">🌊 WAVE — 245.50 <span>$1.23</span></div>
            <div class="asset-item">💎 TON — 12.4 <span>$0.98</span></div>
            <div class="asset-item">💵 USDT — 0.24 <span>$0.24</span></div>
        </div>

        <nav class="bottom-nav">
            <div class="nav-item active" data-screen="wallet">💰 Wallet</div>
            <div class="nav-item" data-screen="mission">📋 Mission</div>
            <div class="nav-item" data-screen="refer">👥 Refer</div>
        </nav>

        <div id="mission-screen" class="sub-screen hidden">
            <h3>Daily Missions</h3>
            <div class="mission-card">Watch Ad & Earn <button class="go-btn">GO</button></div>
            <div class="mission-card">Follow on X <button class="go-btn">GO</button></div>
        </div>

        <div id="refer-screen" class="sub-screen hidden">
            <h2>Invite Friends</h2>
            <input type="text" id="referral-link" value="https://t.me/yourbot/wallet?startapp=ref123" readonly>
            <button onclick="copyLink()">Copy Link</button>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
    font-family: system-ui, sans-serif;
    background: linear-gradient(135deg, #0f4c8a, #1e90ff);
    color: white;
    min-height: 100vh;
}

.screen { display: none; position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
.screen.active { display: flex; flex-direction: column; }

.loading-container { flex: 1; align-items: center; justify-content: center; background: #1e90ff; }
.character { width: 120px; height: 150px; position: relative; }
.head { width: 60px; height: 60px; background: #0a2540; border: 6px solid #ffd700; border-radius: 50%; position: absolute; top: 10px; left: 30px; }
.body { width: 80px; height: 90px; background: #ffd700; border: 6px solid #0a2540; border-radius: 30px; position: absolute; top: 55px; left: 20px; }

.balance-amount { font-size: 3rem; font-weight: bold; color: #ffd700; }
.primary-btn, .connect-btn, .join-btn, .go-btn {
    background: #ffd700;
    color: #0a2540;
    border: none;
    padding: 15px 30px;
    border-radius: 50px;
    font-weight: bold;
    margin: 10px;
}

.bottom-nav {
    display: flex; background: #0a2540; position: fixed; bottom: 0; width: 100%; padding: 10px 0;
}
.nav-item { flex: 1; text-align: center; color: #ccc; }
.nav-item.active { color: #ffd700; }

.sub-screen { padding: 20px; overflow-y: auto; }
const tg = window.Telegram.WebApp;
tg.ready();
tg.expand();

document.getElementById('continue-btn').addEventListener('click', () => {
    document.getElementById('welcome-screen').classList.remove('active');
    document.getElementById('main-app').classList.add('active');
});

document.getElementById('connect-wallet').addEventListener('click', () => {
    tg.showAlert("✅ Wallet Connected Successfully!");
});

function copyLink() {
    const link = document.getElementById('referral-link');
    link.select();
    document.execCommand('copy');
    tg.showAlert("✅ Link Copied!");
}

// Navigation
document.querySelectorAll('.nav-item').forEach(item => {
    item.addEventListener('click', () => {
        document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        item.classList.add('active');
        
        document.querySelectorAll('.sub-screen').forEach(s => s.classList.add('hidden'));
        if (item.dataset.screen === 'mission') {
            document.getElementById('mission-screen').classList.remove('hidden');
        } else if (item.dataset.screen === 'refer') {
            document.getElementById('refer-screen').classList.remove('hidden');
        }
    });
});

// Auto hide loading
setTimeout(() => {
    document.getElementById('loading-screen').classList.remove('active');
    document.getElementById('welcome-screen').classList.add('active');
}, 1800);
