<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, maximum-scale=1.0, user-scalable=no">
<title>Sanrio Kawaii Jump - Hành Trình Bầu Trời</title>
<style>
  * {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
    -webkit-user-select: none;
  }

  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    min-height: 100%;
    height: 100%;
    overflow: hidden;
    overscroll-behavior: none;
    touch-action: manipulation;
  }

  body {
    min-height: 100vh;
    min-height: 100dvh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    background: radial-gradient(circle at top, #fff8fc, #ffd9eb 60%, #ffc2df);
    font-family: "Quicksand", "Nunito", "Segoe UI", Arial, sans-serif;
    color: #9e2761;
    transition: background 0.8s ease;
  }

  .shell {
    width: min(100%, 520px);
    height: 100vh;
    height: 100dvh;
    max-height: 980px;
    padding: max(6px, env(safe-area-inset-top)) 9px max(6px, env(safe-area-inset-bottom));
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  /* Thanh tiêu đề phía trên */
  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 6px;
    margin: 0 2px 8px;
    color: #b0286a;
    font-weight: 800;
    flex-shrink: 0;
  }

  .coin-wallet {
    font-size: 13px;
    background: linear-gradient(180deg, #fffdf2, #fff1b8);
    border: 2px solid #fff;
    color: #9e6500;
    padding: 5px 11px;
    border-radius: 20px;
    box-shadow: 0 3px 10px rgba(216, 155, 25, 0.25);
    display: flex;
    align-items: center;
    gap: 4px;
  }

  .brand {
    font-size: 14px;
    letter-spacing: 0.2px;
    display: flex;
    align-items: center;
    gap: 4px;
    text-shadow: 0 1px 0 #fff;
  }

  .top-actions {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .record {
    font-size: 12px;
    background: #fff9fc;
    border: 2px solid #fff;
    padding: 5px 9px;
    border-radius: 20px;
    box-shadow: 0 3px 10px #d86b9d25;
  }

  .sound-btn {
    border: 2px solid #fff;
    background: #fff9fc;
    color: #b0286a;
    width: 34px;
    height: 32px;
    border-radius: 50%;
    font-size: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    box-shadow: 0 3px 10px #d86b9d25;
    transition: transform 0.15s ease;
  }

  .sound-btn:active {
    transform: scale(0.92);
  }

  /* Khung trò chơi chính */
  .game {
    position: relative;
    flex: 1;
    min-height: 0;
    overflow: hidden;
    border: 4px solid #fff;
    border-radius: 26px;
    box-shadow: 0 12px 35px #d86b9d50;
    background: #ffe8f3;
    touch-action: none;
  }

  canvas#gameCanvas {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    touch-action: none;
  }

  /* Thanh chỉ số HUD trong màn chơi */
  .hud {
    position: absolute;
    top: 10px;
    left: 11px;
    right: 11px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    pointer-events: none;
    font-weight: 800;
    font-size: 13px;
    color: #9e2761;
    z-index: 4;
  }

  .pill {
    background: rgba(255, 250, 253, 0.9);
    border: 1.5px solid #fff;
    border-radius: 20px;
    padding: 5px 10px;
    box-shadow: 0 4px 12px rgba(190, 68, 126, 0.14);
  }

  /* Màn hình chờ & Màn hình kết thúc */
  .overlay {
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: max(12px, env(safe-area-inset-top)) 12px max(12px, env(safe-area-inset-bottom));
    overflow-y: auto;
    text-align: center;
    background: rgba(255, 240, 248, 0.78);
    backdrop-filter: blur(4px);
    -webkit-backdrop-filter: blur(4px);
    z-index: 10;
  }

  .panel {
    width: min(100%, 430px);
    max-width: 430px;
    max-height: min(92dvh, 900px);
    overflow-y: auto;
    padding: 16px 14px;
    border: 3px solid #fff;
    border-radius: 24px;
    background: rgba(255, 250, 253, 0.96);
    box-shadow: 0 10px 28px rgba(201, 78, 138, 0.25);
  }

  .panel h1 {
    margin: 0 0 4px;
    font-size: 21px;
    color: #d9418c;
    letter-spacing: 0.3px;
  }

  .subtitle {
    margin: 0 0 10px;
    font-size: 12.5px;
    color: #8f3b64;
    line-height: 1.35;
  }

  /* Lưới chọn 5 nhân vật Sanrio */
  .char-section-title {
    font-size: 12px;
    font-weight: 800;
    color: #b83374;
    margin-bottom: 7px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .char-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 7px;
    margin-bottom: 10px;
  }

  /* Căn giữa 2 thẻ hàng dưới cho cân đối 3 + 2 */
  .char-card {
    background: #fff;
    border: 2.5px solid #ffd1e6;
    border-radius: 16px;
    padding: 6px 4px 7px;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: all 0.18s ease;
    position: relative;
  }

  .char-card:hover {
    transform: translateY(-2px);
    border-color: #f487ba;
  }

  .char-card.selected {
    background: linear-gradient(180deg, #fff5fa, #ffe3f1);
    border-color: #e64994;
    box-shadow: 0 4px 12px rgba(230, 73, 148, 0.28);
    transform: translateY(-2px) scale(1.02);
  }

  .char-card.selected::after {
    content: "♥";
    position: absolute;
    top: 4px;
    right: 6px;
    font-size: 11px;
    color: #e64994;
  }

  .char-preview {
    width: 60px;
    height: 60px;
    display: block;
  }

  .char-name {
    font-size: 11px;
    font-weight: 800;
    color: #5c3144;
    margin-top: 2px;
    line-height: 1.15;
  }

  .char-card.selected .char-name {
    color: #d63682;
  }

  /* Ô nhập tên người dùng & Thẻ thông tin hồ sơ */
  .profile-box {
    background: linear-gradient(180deg, #fff5fa, #ffe9f4);
    border: 2px solid #ffc7e2;
    border-radius: 16px;
    padding: 9px 11px;
    margin-bottom: 10px;
  }

  .name-row {
    display: flex;
    align-items: center;
    gap: 6px;
    margin-bottom: 6px;
  }

  .name-input {
    flex: 1;
    min-width: 0;
    border: 2px solid #f7a8ce;
    border-radius: 12px;
    padding: 6px 10px;
    font-size: 13px;
    font-weight: 700;
    color: #7d234e;
    background: #fff;
    outline: none;
    user-select: text;
    -webkit-user-select: text;
  }

  .name-input:focus {
    border-color: #e64994;
    box-shadow: 0 0 0 3px rgba(230, 73, 148, 0.16);
  }

  .record-banner {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 12px;
    font-weight: 800;
    color: #a32b64;
    background: rgba(255, 255, 255, 0.8);
    padding: 5px 9px;
    border-radius: 10px;
  }

  .lobby-preview-wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle, #ffffff 35%, #ffe6f2 100%);
    border: 2px solid #ffd1e6;
    border-radius: 20px;
    padding: 6px 10px 8px;
    margin-bottom: 10px;
    position: relative;
  }

  .lobby-char-tag {
    font-size: 12px;
    font-weight: 800;
    color: #d63682;
    background: #fff;
    padding: 3px 10px;
    border-radius: 12px;
    border: 1.5px solid #ffc4e0;
  }

  .lobby-btn-group {
    display: flex;
    flex-direction: column;
    gap: 7px;
  }

  .dual-btns {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 7px;
  }

  .nav-btn {
    border: 2px solid #f594c2;
    border-radius: 18px;
    background: #fff;
    color: #c9347c;
    padding: 9px 8px;
    font-size: 12.5px;
    font-weight: 800;
    cursor: pointer;
    box-shadow: 0 3px 0 #f3b2d1;
    transition: transform 0.1s ease;
  }

  .nav-btn:active {
    transform: translateY(2px);
    box-shadow: 0 1px 0 #f3b2d1;
  }

  /* Cửa hàng / Tủ đồ phụ kiện */
  .tabs-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 6px;
    margin-bottom: 8px;
  }

  .tab-btn {
    border: 2px solid #ffd1e6;
    background: #fff;
    color: #9e3868;
    border-radius: 14px;
    padding: 6px 4px;
    font-size: 12px;
    font-weight: 800;
    cursor: pointer;
  }

  .tab-btn.active {
    background: #ff6eb0;
    border-color: #e34990;
    color: #fff;
  }

  .acc-list {
    display: flex;
    flex-direction: column;
    gap: 6px;
    max-height: 215px;
    overflow-y: auto;
    padding-right: 2px;
    margin-bottom: 10px;
  }

  .acc-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    background: #fff;
    border: 2px solid #ffd6e9;
    border-radius: 14px;
    padding: 6px 9px;
    text-align: left;
  }

  .acc-item.equipped {
    border-color: #e64994;
    background: #fff3f9;
  }

  .acc-info {
    display: flex;
    align-items: center;
    gap: 8px;
    min-width: 0;
  }

  .acc-swatch {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    border: 2px solid #4a2c38;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
  }

  .acc-title {
    font-size: 12px;
    font-weight: 800;
    color: #5c3144;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .acc-sub {
    font-size: 10.5px;
    color: #9e5377;
    font-weight: 700;
  }

  .acc-action-btn {
    border: 0;
    border-radius: 12px;
    padding: 6px 10px;
    font-size: 11.5px;
    font-weight: 800;
    cursor: pointer;
    flex-shrink: 0;
  }

  .btn-buy {
    background: linear-gradient(180deg, #ffe066, #f5b800);
    color: #6b4200;
    box-shadow: 0 2px 0 #c99200;
  }

  .btn-equip {
    background: #ff77b7;
    color: #fff;
    box-shadow: 0 2px 0 #cf4687;
  }

  .btn-equipped {
    background: #7cd992;
    color: #1b5e2b;
    box-shadow: 0 2px 0 #4ea864;
  }

  .shop-toast {
    font-size: 11.5px;
    font-weight: 800;
    color: #d9267e;
    min-height: 16px;
    margin-bottom: 4px;
  }

  .rules-box {
    background: #fff3f9;
    border: 1.5px dashed #f5a6cb;
    border-radius: 14px;
    padding: 8px 10px;
    font-size: 11.5px;
    line-height: 1.45;
    color: #7d3558;
    margin-bottom: 10px;
    text-align: left;
  }

  .main-btn {
    width: 100%;
    border: 0;
    border-radius: 24px;
    background: linear-gradient(180deg, #f57bb4, #e35296);
    color: #fff;
    padding: 12px 20px;
    font-size: 15px;
    font-weight: 800;
    letter-spacing: 0.4px;
    cursor: pointer;
    box-shadow: 0 4px 0 #ba3876, 0 8px 16px rgba(227, 82, 150, 0.3);
    transition: transform 0.1s ease;
  }

  .main-btn:active {
    transform: translateY(2px);
    box-shadow: 0 2px 0 #ba3876;
  }

  .secondary-btn {
    width: 100%;
    margin-top: 8px;
    border: 2px solid #f294c0;
    border-radius: 22px;
    background: #fff;
    color: #d14186;
    padding: 9px 16px;
    font-size: 13.5px;
    font-weight: 800;
    cursor: pointer;
  }

  /* Thanh điều khiển phía dưới */
  .bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    margin: 8px 2px 0;
    color: #9e2761;
    font-size: 11.5px;
    flex-shrink: 0;
  }

  .legend {
    line-height: 1.38;
    font-weight: 600;
  }

  .pad {
    display: flex;
    gap: 10px;
  }

  .pad button {
    width: clamp(58px, 16vw, 72px);
    height: clamp(46px, 7vh, 58px);
    border: 2.5px solid #fff;
    border-radius: 18px;
    background: linear-gradient(180deg, #f896c2, #eb6da6);
    color: #fff;
    font-size: 21px;
    font-weight: bold;
    box-shadow: 0 4px 0 #c74c84;
    cursor: pointer;
    touch-action: none;
  }

  .pad button:active, .pad button.active {
    transform: translateY(2px);
    box-shadow: 0 2px 0 #c74c84;
    background: #df5895;
  }

  .stat-row {
    display: flex;
    justify-content: space-between;
    background: #fff3f9;
    padding: 8px 12px;
    border-radius: 12px;
    margin: 6px 0;
    font-size: 13.5px;
  }

  /* Menu là một màn hình riêng; chỉ hiện canvas và HUD sau khi bấm bắt đầu. */
  body.lobby-mode .topbar,
  body.lobby-mode .game,
  body.lobby-mode .bottom { display: none; }
  body.lobby-mode .shell { display: contents; }
  body.lobby-mode .overlay { z-index: 50; background: radial-gradient(circle at 50% 15%, #fffaff, #ffe5f2 62%, #ffc9e2); backdrop-filter: none; }
  body.lobby-mode .panel { box-shadow: 0 16px 44px rgba(207, 93, 151, .2); }

  @media (max-width: 600px) {
    .shell { width: 100%; max-width: none; max-height: none; padding-left: 7px; padding-right: 7px; }
    .topbar { margin: 0 1px 6px; }
    .brand { font-size: 12px; }
    .record { font-size: 11px; padding: 5px 7px; }
    .coin-wallet { font-size: 12px; padding: 5px 8px; }
    .game { border-width: 3px; border-radius: 20px; }
    .hud { top: 7px; left: 7px; right: 7px; font-size: 11px; }
    .pill { padding: 5px 7px; }
    .bottom { margin-top: 6px; min-height: 50px; }
    .legend { font-size: 10px; }
    .pad { gap: 8px; }
    .pad button { border-radius: 16px; font-size: 20px; }
    .panel { padding: 13px 11px; border-radius: 21px; }
    .panel h1 { font-size: clamp(18px, 5vw, 22px); }
    .subtitle { font-size: 12px; }
    .char-grid { gap: 6px; }
    .char-preview { width: 54px; height: 54px; }
  }

  @media (max-height: 560px) and (orientation: landscape) {
    .shell { max-width: 900px; padding-top: 4px; padding-bottom: 4px; }
    .topbar { margin-bottom: 3px; }
    .bottom { margin-top: 3px; min-height: 42px; }
    .pad button { height: 40px; }
    .panel { max-height: 94dvh; padding: 9px 12px; }
    .lobby-preview-wrap { display: none; }
  }
</style>
</head>
<body>
<div class="shell">
  <!-- Thanh tiêu đề trên cùng: Tiền xu bên trái, Kỷ lục & Âm thanh bên phải -->
  <div class="topbar">
    <div class="coin-wallet" title="Tổng số xu tích lũy">🪙 <span id="coinTop">0</span></div>
    <div class="brand">🎀 SANRIO JUMP</div>
    <div class="top-actions">
      <div class="record">🏆 <span id="bestTop">0</span></div>
      <button class="sound-btn" id="soundToggle" title="Bật/Tắt âm thanh" aria-label="Bật hoặc tắt âm thanh">🔊</button>
    </div>
  </div>

  <!-- Khung Canvas Trò Chơi -->
  <div class="game" id="gameContainer">
    <canvas id="gameCanvas" width="420" height="700"></canvas>

    <div class="hud">
      <div class="pill">💗 Điểm: <span id="score">0</span></div>
      <div class="pill" id="themeBadge">🌸 Kẹo Bông Hồng</div>
      <div class="pill">🪙 +<span id="runCoins">0</span></div>
    </div>

  </div>

  <!-- Menu độc lập, không nằm trong khung canvas của màn chơi -->
  <div class="overlay" id="overlay" aria-live="polite">
    <div class="panel" id="panel"></div>
  </div>

  <!-- Điều khiển dưới chân trang -->
  <div class="bottom">
    <div class="legend">
      PC: Phím <b>← →</b> hoặc <b>A / D</b><br>
      Mobile: Giữ nút hoặc chạm/vuốt màn hình
    </div>
    <div class="pad">
      <button id="leftBtn" aria-label="Di chuyển sang trái">◀</button>
      <button id="rightBtn" aria-label="Di chuyển sang phải">▶</button>
    </div>
  </div>
</div>

<script>
/**
 * ============================================================================
 * 1. HỆ THỐNG ÂM THANH WEB AUDIO API (NHẠC NỀN MUSIC-BOX + HIỆU ỨNG ÂM THANH)
 * ============================================================================
 */
class KawaiiAudio {
  constructor() {
    this.ctx = null;
    this.muted = false;
    this.bgmTimer = null;
    this.noteIndex = 0;
    this.isPlayingBgm = false;

    // Giai điệu music-box dễ thương (tần số Hz & độ dài nhịp)
    this.melody = [
      [523.25, 0.22], [659.25, 0.22], [783.99, 0.22], [1046.50, 0.44],
      [880.00, 0.22], [1046.50, 0.22], [783.99, 0.44], [0, 0.15],
      [698.46, 0.22], [880.00, 0.22], [783.99, 0.22], [659.25, 0.22],
      [587.33, 0.22], [659.25, 0.22], [523.25, 0.44], [0, 0.20],
      [587.33, 0.22], [698.46, 0.22], [880.00, 0.22], [987.77, 0.35],
      [880.00, 0.22], [783.99, 0.22], [659.25, 0.44], [0, 0.15],
      [698.46, 0.22], [659.25, 0.22], [587.33, 0.22], [493.88, 0.22],
      [523.25, 0.55], [0, 0.25]
    ];
  }

  init() {
    if (!this.ctx) {
      const AudioCtx = window.AudioContext || window.webkitAudioContext;
      if (AudioCtx) {
        this.ctx = new AudioCtx();
      }
    }
    if (this.ctx && this.ctx.state === "suspended") {
      this.ctx.resume();
    }
  }

  toggleMute() {
    this.muted = !this.muted;
    const btn = document.getElementById("soundToggle");
    btn.textContent = this.muted ? "🔇" : "🔊";
    if (this.muted) {
      this.stopBgm();
    } else {
      this.init();
      this.startBgm();
      this.playClick();
    }
  }

  playTone(freq, duration, type = "sine", volume = 0.08, delay = 0) {
    if (this.muted || !this.ctx || freq <= 0) return;
    const now = this.ctx.currentTime + delay;
    const osc = this.ctx.createOscillator();
    const gain = this.ctx.createGain();

    osc.type = type;
    osc.frequency.setValueAtTime(freq, now);

    gain.gain.setValueAtTime(0.0001, now);
    gain.gain.exponentialRampToValueAtTime(volume, now + 0.02);
    gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);

    osc.connect(gain);
    gain.connect(this.ctx.destination);

    osc.start(now);
    osc.stop(now + duration + 0.02);
  }

  startBgm() {
    this.init();
    if (this.muted || this.isPlayingBgm) return;
    this.isPlayingBgm = true;

    const scheduleNext = () => {
      if (!this.isPlayingBgm || this.muted) return;
      const [freq, dur] = this.melody[this.noteIndex % this.melody.length];
      if (freq > 0) {
        // Tiếng chuông hộp nhạc trong trẻo
        this.playTone(freq, dur * 1.15, "sine", 0.045, 0);
        this.playTone(freq * 2, dur * 0.6, "triangle", 0.015, 0);
      }
      this.noteIndex++;
      this.bgmTimer = setTimeout(scheduleNext, dur * 1000);
    };
    scheduleNext();
  }

  stopBgm() {
    this.isPlayingBgm = false;
    if (this.bgmTimer) {
      clearTimeout(this.bgmTimer);
      this.bgmTimer = null;
    }
  }

  playClick() {
    this.init();
    this.playTone(784, 0.08, "sine", 0.08, 0);
    this.playTone(1046.5, 0.12, "sine", 0.08, 0.05);
  }

  playJumpNormal() {
    this.init();
    if (this.muted || !this.ctx) return;
    const now = this.ctx.currentTime;
    const osc = this.ctx.createOscillator();
    const gain = this.ctx.createGain();
    osc.type = "sine";
    osc.frequency.setValueAtTime(340, now);
    osc.frequency.exponentialRampToValueAtTime(640, now + 0.13);
    gain.gain.setValueAtTime(0.09, now);
    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.14);
    osc.connect(gain);
    gain.connect(this.ctx.destination);
    osc.start(now);
    osc.stop(now + 0.15);
  }

  playJumpSpecial() {
    this.init();
    this.playTone(523.25, 0.11, "triangle", 0.09, 0);
    this.playTone(783.99, 0.12, "triangle", 0.09, 0.05);
    this.playTone(1046.5, 0.16, "sine", 0.09, 0.10);
  }

  playBoost() {
    this.init();
    const notes = [523.25, 659.25, 783.99, 1046.5, 1318.5, 1567.98];
    notes.forEach((f, idx) => {
      this.playTone(f, 0.14, "triangle", 0.09, idx * 0.045);
    });
  }

  playFirework() {
    this.init();
    if (this.muted || !this.ctx) return;
    // Tiếng vút lên & tiếng nổ lấp lánh
    this.playTone(600, 0.18, "sine", 0.06, 0);
    this.playTone(1200, 0.25, "sine", 0.07, 0.12);
    this.playTone(1568, 0.28, "triangle", 0.07, 0.18);
    this.playTone(2093, 0.35, "sine", 0.06, 0.24);
  }

  playGameOver() {
    this.init();
    const notes = [659.25, 587.33, 523.25, 392.0];
    notes.forEach((f, idx) => {
      this.playTone(f, 0.24, "sine", 0.09, idx * 0.16);
    });
  }

  playCoin() {
    this.init();
    this.playTone(987.77, 0.08, "sine", 0.09, 0);
    this.playTone(1318.51, 0.14, "sine", 0.09, 0.055);
  }

  playBuy() {
    this.init();
    const notes = [587.33, 783.99, 987.77, 1174.66];
    notes.forEach((f, idx) => {
      this.playTone(f, 0.12, "triangle", 0.09, idx * 0.05);
    });
  }
}

const audio = new KawaiiAudio();
document.getElementById("soundToggle").addEventListener("click", () => audio.toggleMute());

/**
 * ============================================================================
 * 2. DỮ LIỆU 5 NHÂN VẬT SANRIO, KHO PHỤ KIỆN & BỘ VẼ NÉT VECTOR CHI TIẾT
 * ============================================================================
 */
const CHARACTERS = [
  { id: "melody", name: "My Melody", color: "#ff8ac0" },
  { id: "kuromi", name: "Kuromi", color: "#7f5899" },
  { id: "kitty", name: "Hello Kitty", color: "#ff5c7c" },
  { id: "purin", name: "Pompompurin", color: "#f5c25b" },
  { id: "cinna", name: "Cinnamoroll", color: "#7bc8f6" }
];

// Danh sách phụ kiện chia làm 3 nhóm: Nơ (bow), Mũ (hat), Cây kẹo (candy) - Giá từ thấp đến cao
const ACCESSORIES = {
  bow: [
    { id: "bow_none", name: "Không đeo nơ", price: 0, main: "#ffd6e8", sub: "#fff", icon: "🚫" },
    { id: "bow_pink", name: "Nơ Hồng Kẹo Ngọt", price: 30, main: "#ff5ca8", sub: "#ffe066", icon: "🎀" },
    { id: "bow_sky", name: "Nơ Xanh Sao Băng", price: 65, main: "#4db8ff", sub: "#ffffff", icon: "🩵" },
    { id: "bow_purple", name: "Nơ Tím Pha Lê", price: 110, main: "#a855f7", sub: "#f9a8d4", icon: "💜" },
    { id: "bow_mint", name: "Nơ Bạc Hà Chấm Bi", price: 170, main: "#34d399", sub: "#fef08a", icon: "🍀" },
    { id: "bow_rainbow", name: "Nơ Cầu Vồng Thiên Thần", price: 250, main: "rainbow", sub: "#fff380", icon: "🌈" }
  ],
  hat: [
    { id: "hat_none", name: "Không đội mũ", price: 0, main: "#ffd6e8", sub: "#fff", icon: "🚫" },
    { id: "hat_straw", name: "Mũ Rơm Hoa Cúc", price: 40, main: "#f6d365", sub: "#ff6b9d", icon: "👒" },
    { id: "hat_beret", name: "Mũ Beret Dâu Tây", price: 80, main: "#ff4d6d", sub: "#80ed99", icon: "🍓" },
    { id: "hat_witch", name: "Mũ Phù Thủy Sao Đêm", price: 130, main: "#5e3a87", sub: "#ffd166", icon: "🧙‍♀️" },
    { id: "hat_cake", name: "Mũ Bánh Kem Sinh Nhật", price: 190, main: "#fff5f7", sub: "#ff477e", icon: "🎂" },
    { id: "hat_crown", name: "Vương Miện Công Chúa", price: 280, main: "#ffd700", sub: "#ff3385", icon: "👑" }
  ],
  candy: [
    { id: "candy_none", name: "Không cầm kẹo", price: 0, main: "#ffd6e8", sub: "#fff", icon: "🚫" },
    { id: "candy_pink", name: "Kẹo Mút Dâu Hồng", price: 35, main: "#ff66a3", sub: "#ffffff", icon: "🍭" },
    { id: "candy_mint", name: "Kẹo Xoáy Bạc Hà", price: 75, main: "#38bdf8", sub: "#e0f2fe", icon: "🌀" },
    { id: "candy_choco", name: "Kẹo Cam Sô-cô-la", price: 120, main: "#fb923c", sub: "#78350f", icon: "🍊" },
    { id: "candy_heart", name: "Kẹo Trái Tim Pha Lê", price: 185, main: "#f43f5e", sub: "#fecdd3", icon: "💖" },
    { id: "candy_magic", name: "Gậy Kẹo Phép Thuật Sao", price: 270, main: "rainbow", sub: "#fde047", icon: "🪄" }
  ]
};

// Quản lý dữ liệu lưu trữ người chơi
const STORAGE_KEY = "sanrioKawaiiJumpSave_v2";
const defaultSave = {
  playerName: "Bé Thỏ Hồng",
  coins: 50, // Tặng sẵn 50 xu khởi đầu để trải nghiệm mua sắm
  bestScore: Number(localStorage.getItem("sanrioJumpBest") || localStorage.getItem("melodyJumpBest") || 0),
  selectedChar: "melody",
  owned: ["bow_none", "hat_none", "candy_none"],
  equipped: {
    bow: "bow_none",
    hat: "hat_none",
    candy: "candy_none"
  },
  achievements: [],
  progress: null
};

let saveData = (() => {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) {
      const parsed = JSON.parse(raw);
      return {
        ...defaultSave,
        ...parsed,
        equipped: { ...defaultSave.equipped, ...(parsed.equipped || {}) },
        owned: Array.from(new Set([...defaultSave.owned, ...(parsed.owned || [])])),
        achievements: Array.isArray(parsed.achievements) ? parsed.achievements : [],
        progress: null
      };
    }
  } catch (e) {}
  return { ...defaultSave };
})();

function persistSave() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(saveData));
    localStorage.setItem("sanrioJumpBest", String(saveData.bestScore));
  } catch (e) {}
  updateTopBarUI();
}

function updateTopBarUI() {
  const coinEl = document.getElementById("coinTop");
  const bestEl = document.getElementById("bestTop");
  if (coinEl) coinEl.textContent = saveData.coins;
  if (bestEl) bestEl.textContent = saveData.bestScore;
}

let selectedCharId = saveData.selectedChar;
const STROKE_COLOR = "#4a2c38"; // Nét viền nâu sẫm đặc trưng phong cách Sanrio

/**
 * Vẽ các phụ kiện đang đeo (Nơ, Mũ, Cây kẹo) trực tiếp lên nhân vật
 */
function drawCharacterAccessories(c, charId, equipped, time = 0) {
  const bowItem = ACCESSORIES.bow.find(i => i.id === equipped.bow);
  const hatItem = ACCESSORIES.hat.find(i => i.id === equipped.hat);
  const candyItem = ACCESSORIES.candy.find(i => i.id === equipped.candy);

  // 1. VẼ CÂY KẸO CẦM TAY (BÊN TAY PHẢI NHÂN VẬT)
  if (candyItem && candyItem.id !== "candy_none") {
    c.save();
    const sway = Math.sin(time * 0.1) * 0.08;
    c.translate(21, 16);
    c.rotate(0.28 + sway);

    // Que kẹo trắng
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2;
    c.fillStyle = "#ffffff";
    c.beginPath();
    c.roundRect(-2, -14, 4, 22, 2);
    c.fill();
    c.stroke();

    // Nơ nhỏ trên que kẹo
    c.fillStyle = "#ff85be";
    c.beginPath();
    c.ellipse(-3.5, -6, 3.5, 2.2, -0.2, 0, Math.PI * 2);
    c.ellipse(3.5, -6, 3.5, 2.2, 0.2, 0, Math.PI * 2);
    c.fill();

    // Viên kẹo phía trên biến đổi theo loại
    c.translate(0, -21);
    if (candyItem.id === "candy_heart") {
      // Kẹo trái tim
      c.fillStyle = candyItem.main;
      c.beginPath();
      c.moveTo(0, 6);
      c.bezierCurveTo(-11, -2, -8, -11, 0, -5);
      c.bezierCurveTo(8, -11, 11, -2, 0, 6);
      c.fill();
      c.stroke();
    } else if (candyItem.id === "candy_magic") {
      // Gậy kẹo ngôi sao phép thuật
      c.fillStyle = "#fde047";
      c.beginPath();
      for (let i = 0; i < 10; i++) {
        const r = i % 2 === 0 ? 10 : 4.5;
        const a = (i * Math.PI) / 5 - Math.PI / 2;
        if (i === 0) c.moveTo(Math.cos(a) * r, Math.sin(a) * r);
        else c.lineTo(Math.cos(a) * r, Math.sin(a) * r);
      }
      c.closePath();
      c.fill();
      c.stroke();
      // Viên ngọc hồng giữa sao
      c.fillStyle = "#ff4da6";
      c.beginPath();
      c.arc(0, 0, 3, 0, Math.PI * 2);
      c.fill();
    } else {
      // Kẹo mút tròn xoáy nhiều màu
      if (candyItem.main === "rainbow") {
        const rg = c.createLinearGradient(-9, -9, 9, 9);
        rg.addColorStop(0, "#ff6b9d");
        rg.addColorStop(0.5, "#fde047");
        rg.addColorStop(1, "#60a5fa");
        c.fillStyle = rg;
      } else {
        c.fillStyle = candyItem.main;
      }
      c.beginPath();
      c.arc(0, 0, 9.5, 0, Math.PI * 2);
      c.fill();
      c.stroke();

      // Đường xoắn ốc kẹo ngọt
      c.strokeStyle = candyItem.sub;
      c.lineWidth = 2;
      c.beginPath();
      for (let a = 0; a < Math.PI * 3.2; a += 0.25) {
        const r = (a / (Math.PI * 3.2)) * 7.5;
        const px = Math.cos(a) * r;
        const py = Math.sin(a) * r;
        if (a === 0) c.moveTo(px, py);
        else c.lineTo(px, py);
      }
      c.stroke();
    }
    c.restore();
  }

  // 2. VẼ MŨ THỜI TRANG TRÊN ĐỈNH ĐẦU
  if (hatItem && hatItem.id !== "hat_none") {
    c.save();
    // Điều chỉnh độ cao mũ tùy dáng đầu nhân vật
    const hatY = charId === "kitty" ? -16 : -17;
    c.translate(0, hatY);
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.1;

    if (hatItem.id === "hat_straw") {
      // Mũ rơm hoa cúc
      c.fillStyle = hatItem.main;
      c.beginPath();
      c.ellipse(0, 1, 21, 5.5, 0, 0, Math.PI * 2);
      c.fill();
      c.stroke();
      c.beginPath();
      c.arc(0, 0, 11, Math.PI, 0);
      c.fill();
      c.stroke();
      // Dải ruy băng hồng
      c.fillStyle = hatItem.sub;
      c.fillRect(-10.5, -3, 21, 3.2);
    } else if (hatItem.id === "hat_beret") {
      // Mũ Beret dâu tây
      c.fillStyle = hatItem.main;
      c.beginPath();
      c.ellipse(0, -1, 15, 7, -0.08, 0, Math.PI * 2);
      c.fill();
      c.stroke();
      // Lá dâu xanh trên đỉnh
      c.fillStyle = hatItem.sub;
      c.beginPath();
      c.ellipse(-4, -7, 4.5, 2, -0.4, 0, Math.PI * 2);
      c.ellipse(4, -7, 4.5, 2, 0.4, 0, Math.PI * 2);
      c.fill();
      c.stroke();
    } else if (hatItem.id === "hat_witch") {
      // Mũ phù thủy nhỏ xinh
      c.fillStyle = hatItem.main;
      c.beginPath();
      c.ellipse(0, 1, 20, 5, 0, 0, Math.PI * 2);
      c.fill();
      c.stroke();
      c.beginPath();
      c.moveTo(-11, 0);
      c.lineTo(2, -19);
      c.lineTo(11, 0);
      c.closePath();
      c.fill();
      c.stroke();
      // Ngôi sao vàng trên mũ
      c.fillStyle = hatItem.sub;
      c.beginPath();
      c.arc(0, -7, 2.8, 0, Math.PI * 2);
      c.fill();
    } else if (hatItem.id === "hat_cake") {
      // Mũ bánh kem sinh nhật có quả dâu
      c.fillStyle = hatItem.main;
      c.beginPath();
      c.roundRect(-11, -11, 22, 12, 4);
      c.fill();
      c.stroke();
      // Lớp kem hồng chảy
      c.fillStyle = "#ff85be";
      c.beginPath();
      c.roundRect(-11.5, -11, 23, 5, 3);
      c.fill();
      // Quả dâu đỏ trên đỉnh
      c.fillStyle = hatItem.sub;
      c.beginPath();
      c.arc(0, -14, 3.8, 0, Math.PI * 2);
      c.fill();
      c.stroke();
    } else if (hatItem.id === "hat_crown") {
      // Vương miện công chúa lấp lánh
      c.fillStyle = hatItem.main;
      c.beginPath();
      c.moveTo(-12, 1);
      c.lineTo(-14, -11);
      c.lineTo(-6, -5);
      c.lineTo(0, -14);
      c.lineTo(6, -5);
      c.lineTo(14, -11);
      c.lineTo(12, 1);
      c.closePath();
      c.fill();
      c.stroke();
      // Viên ngọc hồng
      c.fillStyle = hatItem.sub;
      c.beginPath();
      c.arc(0, -4, 2.5, 0, Math.PI * 2);
      c.fill();
    }
    c.restore();
  }

  // 3. VẼ NƠ THỜI TRANG BÊN TAI / TRÊN ĐẦU
  if (bowItem && bowItem.id !== "bow_none") {
    c.save();
    // Vị trí đeo nơ hài hòa cho từng nhân vật
    const bowPos = charId === "kitty" ? { x: 14, y: -12, rot: 0.3 } : { x: -14, y: -11, rot: -0.32 };
    c.translate(bowPos.x, bowPos.y);
    c.rotate(bowPos.rot);

    if (bowItem.main === "rainbow") {
      const rg = c.createLinearGradient(-12, -5, 12, 5);
      rg.addColorStop(0, "#ff6b9d");
      rg.addColorStop(0.5, "#fde047");
      rg.addColorStop(1, "#60a5fa");
      c.fillStyle = rg;
    } else {
      c.fillStyle = bowItem.main;
    }

    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2;
    c.beginPath();
    c.ellipse(-6.5, 0, 6.5, 4.8, -0.2, 0, Math.PI * 2);
    c.ellipse(6.5, 0, 6.5, 4.8, 0.2, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Hạt ngọc/nút giữa nơ
    c.fillStyle = bowItem.sub;
    c.beginPath();
    c.arc(0, 0, 3.2, 0, Math.PI * 2);
    c.fill();
    c.stroke();
    c.restore();
  }
}

/**
 * Hàm vẽ nét vector chi tiết cho từng nhân vật Sanrio
 * @param {CanvasRenderingContext2D} c - Context vẽ
 * @param {string} charId - ID nhân vật
 * @param {number} cx - Tâm X
 * @param {number} cy - Tâm Y
 * @param {number} scale - Tỷ lệ phóng
 * @param {number} vy - Vận tốc dọc (tạo biểu cảm/độ nhún tai)
 * @param {number} time - Thời gian animation
 * @param {object} equipped - Phụ kiện đang đeo (tùy chọn)
 */
function drawSanrioCharacter(c, charId, cx, cy, scale = 1, vy = 0, time = 0, equipped = saveData.equipped) {
  c.save();
  c.translate(cx, cy);

  // Hiệu ứng co giãn nhẹ theo lực nhảy (Squash & Stretch)
  const stretchY = vy < -5 ? 1.06 : (vy > 6 ? 0.95 : 1);
  const stretchX = 2 - stretchY;
  c.scale(scale * stretchX, scale * stretchY);

  c.lineJoin = "round";
  c.lineCap = "round";
  const earFlap = Math.sin(time * 0.12) * 0.08 + Math.max(-0.25, Math.min(0.25, vy * 0.015));

  if (charId === "melody") {
    // MY MELODY theo mẫu thú bông: mũ hồng lớn, một tai dựng, một tai cụp,
    // nơ xanh ngọc, mặt trắng, mũi vàng và bàn chân có đệm hồng.
    const outline = "#e9a5b8";

    // Thân trắng nhỏ phía dưới đầu
    c.fillStyle = "#fffafd";
    c.strokeStyle = "#f0dce4";
    c.lineWidth = 1.25;
    c.beginPath();
    c.ellipse(0, 28, 14.5, 15, 0, 0, Math.PI * 2);
    c.fill(); c.stroke();

    // Hai chân ngắn và bàn chân tròn
    c.fillStyle = "#fffdfd";
    c.beginPath();
    c.ellipse(-8, 37, 9.2, 7.2, -0.12, 0, Math.PI * 2);
    c.ellipse(8, 37, 9.2, 7.2, 0.12, 0, Math.PI * 2);
    c.fill(); c.stroke();

    // Đệm chân màu hồng và các chấm nhỏ
    c.fillStyle = "#f6a9bd";
    c.beginPath();
    c.ellipse(-8, 39, 2.8, 3.4, -0.2, 0, Math.PI * 2);
    c.ellipse(8, 39, 2.8, 3.4, 0.2, 0, Math.PI * 2);
    c.arc(-12, 34.5, 1.15, 0, Math.PI * 2);
    c.arc(-7.5, 33.7, 1.15, 0, Math.PI * 2);
    c.arc(-3.5, 35, 1.15, 0, Math.PI * 2);
    c.arc(12, 34.5, 1.15, 0, Math.PI * 2);
    c.arc(7.5, 33.7, 1.15, 0, Math.PI * 2);
    c.arc(3.5, 35, 1.15, 0, Math.PI * 2);
    c.fill();

    // Hai tay/paw trắng ôm hai bên má
    c.fillStyle = "#fffdfd";
    c.strokeStyle = "#f0dce4";
    c.lineWidth = 1.15;
    c.beginPath();
    c.ellipse(-19, 18, 7.5, 9, -0.45, 0, Math.PI * 2);
    c.ellipse(19, 18, 7.5, 9, 0.45, 0, Math.PI * 2);
    c.fill(); c.stroke();

    // Tai dựng bên trái (hơi đung đưa khi nhảy)
    c.save();
    c.translate(-10, -18);
    c.rotate(-0.08 + earFlap * 0.22);
    c.fillStyle = "#f7aec6";
    c.strokeStyle = outline;
    c.lineWidth = 1.45;
    c.beginPath();
    c.moveTo(-8, 9);
    c.bezierCurveTo(-11, -7, -10, -34, -2, -39);
    c.bezierCurveTo(8, -44, 12, -23, 10, -5);
    c.quadraticCurveTo(8, 7, 2, 12);
    c.closePath();
    c.fill(); c.stroke();
    c.fillStyle = "#ffd9e6";
    c.beginPath();
    c.ellipse(0, -17, 4.2, 16, -0.05, 0, Math.PI * 2);
    c.fill();
    c.restore();

    // Tai phải tròn, cụp xuống như mẫu
    c.save();
    c.translate(12, -12);
    c.rotate(0.12 - earFlap * 0.18);
    c.fillStyle = "#f7aec6";
    c.strokeStyle = outline;
    c.lineWidth = 1.45;
    c.beginPath();
    c.moveTo(-5, 0);
    c.bezierCurveTo(-10, -15, 1, -26, 13, -22);
    c.bezierCurveTo(27, -17, 29, 1, 19, 13);
    c.bezierCurveTo(11, 23, 1, 17, -3, 9);
    c.closePath();
    c.fill(); c.stroke();
    c.restore();

    // Mũ trùm hồng lớn, phom tròn mềm
    c.fillStyle = "#f6aec5";
    c.strokeStyle = outline;
    c.lineWidth = 1.65;
    c.beginPath();
    c.moveTo(-23, -7);
    c.bezierCurveTo(-27, -24, -17, -31, -5, -29);
    c.bezierCurveTo(7, -34, 24, -25, 25, -9);
    c.bezierCurveTo(31, 3, 28, 20, 19, 25);
    c.bezierCurveTo(10, 31, -13, 31, -22, 23);
    c.bezierCurveTo(-31, 15, -30, 0, -23, -7);
    c.closePath();
    c.fill(); c.stroke();

    // Ánh bóng dịu trên mũ
    c.fillStyle = "rgba(255,255,255,.22)";
    c.beginPath();
    c.ellipse(-12, -19, 5.2, 2.2, -0.5, 0, Math.PI * 2);
    c.fill();

    // Mặt trắng lớn, bầu bĩnh
    c.fillStyle = "#fffdfd";
    c.strokeStyle = "#f3dfe7";
    c.lineWidth = 1.1;
    c.beginPath();
    c.ellipse(0, 9, 19.5, 13.8, 0, 0, Math.PI * 2);
    c.fill(); c.stroke();

    // Nơ xanh ngọc đặt lệch trên tai trái
    c.save();
    c.translate(-17, -17);
    c.rotate(-0.12);
    c.fillStyle = "#9adfe0";
    c.strokeStyle = "#83cfd2";
    c.lineWidth = 1.2;
    c.beginPath();
    c.moveTo(-1, 0);
    c.bezierCurveTo(-9, -9, -18, -8, -18, 0);
    c.bezierCurveTo(-18, 7, -9, 10, -1, 2);
    c.bezierCurveTo(6, 10, 17, 8, 17, 0);
    c.bezierCurveTo(17, -8, 7, -9, -1, -1);
    c.closePath();
    c.fill(); c.stroke();
    c.fillStyle = "#b7eeee";
    c.beginPath(); c.ellipse(0, 0, 3.8, 4.2, 0, 0, Math.PI * 2); c.fill(); c.stroke();
    c.restore();

    // Mắt đen hình oval đơn giản giống figure trong ảnh
    c.fillStyle = "#28252a";
    c.beginPath();
    c.ellipse(-9, 8.5, 3.2, 5.3, 0, 0, Math.PI * 2);
    c.ellipse(9, 8.5, 3.2, 5.3, 0, 0, Math.PI * 2);
    c.fill();

    // Mũi vàng nhỏ
    c.fillStyle = "#f6d22e";
    c.beginPath();
    c.ellipse(0, 13, 4.1, 2.5, 0, 0, Math.PI * 2);
    c.fill();

    // Nụ cười cong nhẹ
    c.strokeStyle = "#40363a";
    c.lineWidth = 1;
    c.beginPath();
    c.moveTo(-3.2, 17);
    c.quadraticCurveTo(0, 19.2, 3.2, 17);
    c.stroke();
  } else if (charId === "kuromi") {
    // --- KUROMI ---
    // Đuôi quỷ nhỏ phía sau
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.4;
    c.beginPath();
    c.moveTo(12, 22);
    c.quadraticCurveTo(24, 20, 22, 11);
    c.stroke();
    c.fillStyle = "#3c3246";
    c.beginPath();
    c.moveTo(22, 11);
    c.lineTo(18, 14);
    c.lineTo(25, 15);
    c.closePath();
    c.fill();
    c.stroke();

    // Hai tai mũ hề nhọn có quả cầu hồng ở chóp
    [-1, 1].forEach(dir => {
      c.save();
      c.translate(dir * 12, -13);
      c.rotate(dir * (0.38 - earFlap * 0.4));
      c.fillStyle = "#3c3246";
      c.strokeStyle = STROKE_COLOR;
      c.lineWidth = 2.3;
      c.beginPath();
      c.moveTo(-7, 2);
      c.quadraticCurveTo(-4, -15, 0, -21);
      c.quadraticCurveTo(4, -15, 7, 2);
      c.closePath();
      c.fill();
      c.stroke();

      // Quả cầu hồng trên đỉnh tai
      c.fillStyle = "#ff7eb9";
      c.beginPath();
      c.arc(0, -22, 4.2, 0, Math.PI * 2);
      c.fill();
      c.stroke();
      c.restore();
    });

    // Cổ áo viền trắng răng cưa
    c.fillStyle = "#ffffff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2;
    c.beginPath();
    c.moveTo(-15, 20);
    c.lineTo(-10, 28);
    c.lineTo(-4, 24);
    c.lineTo(0, 29);
    c.lineTo(4, 24);
    c.lineTo(10, 28);
    c.lineTo(15, 20);
    c.closePath();
    c.fill();
    c.stroke();

    // Mũ trùm đen Kuromi
    c.fillStyle = "#3c3246";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.4;
    c.beginPath();
    c.ellipse(0, 2, 23, 20.5, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Biểu tượng đầu lâu hồng giữa trán
    c.fillStyle = "#ff7eb9";
    c.beginPath();
    c.arc(0, -10.5, 4.2, 0, Math.PI * 2);
    c.fill();
    c.fillRect(-2.4, -7.5, 4.8, 2.5);
    c.fillStyle = "#3c3246";
    c.beginPath();
    c.arc(-1.5, -10.5, 1, 0, Math.PI * 2);
    c.arc(1.5, -10.5, 1, 0, Math.PI * 2);
    c.fill();

    // Khuôn mặt trắng
    c.fillStyle = "#ffffff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.1;
    c.beginPath();
    c.ellipse(0, 7, 16.5, 13.5, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Mắt tinh nghịch + lông mi
    c.fillStyle = STROKE_COLOR;
    c.beginPath();
    c.ellipse(-7, 6, 2.6, 3.1, 0, 0, Math.PI * 2);
    c.ellipse(7, 6, 2.6, 3.1, 0, 0, Math.PI * 2);
    c.fill();
    // Lông mi & lông mày nhếch
    c.lineWidth = 1.7;
    c.beginPath();
    c.moveTo(-10, 2); c.lineTo(-4, 4);
    c.moveTo(10, 2); c.lineTo(4, 4);
    c.moveTo(-9.5, 5); c.lineTo(-11.5, 4);
    c.moveTo(9.5, 5); c.lineTo(11.5, 4);
    c.stroke();

    // Má hồng tím nhạt
    c.fillStyle = "rgba(255, 126, 185, 0.55)";
    c.beginPath();
    c.ellipse(-11.5, 11, 3.3, 2, 0, 0, Math.PI * 2);
    c.ellipse(11.5, 11, 3.3, 2, 0, 0, Math.PI * 2);
    c.fill();

    // Mũi hồng nhỏ & nụ cười tinh nghịch
    c.fillStyle = "#ff7eb9";
    c.beginPath();
    c.ellipse(0, 9.5, 2.1, 1.5, 0, 0, Math.PI * 2);
    c.fill();
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.6;
    c.beginPath();
    c.arc(0, 12, 3, 0.1 * Math.PI, 0.9 * Math.PI);
    c.stroke();

  } else if (charId === "kitty") {
    // --- HELLO KITTY ---
    // Yếm xanh & áo vàng xinh xắn
    c.fillStyle = "#4da6ff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.2;
    c.beginPath();
    c.moveTo(-13, 17);
    c.lineTo(-16, 29);
    c.lineTo(16, 29);
    c.lineTo(13, 17);
    c.closePath();
    c.fill();
    c.stroke();

    // Cúc áo vàng
    c.fillStyle = "#ffd633";
    c.beginPath();
    c.arc(-7, 22, 2, 0, Math.PI * 2);
    c.arc(7, 22, 2, 0, Math.PI * 2);
    c.fill();

    // Đầu mèo bầu bĩnh + 2 tai nhọn liền khối
    c.fillStyle = "#ffffff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.4;
    c.beginPath();
    c.moveTo(-19, -4);
    c.lineTo(-18, -21);
    c.lineTo(-6, -14);
    c.quadraticCurveTo(0, -15.5, 6, -14);
    c.lineTo(18, -21);
    c.lineTo(19, -4);
    c.bezierCurveTo(24, 5, 20, 19, 0, 19);
    c.bezierCurveTo(-20, 19, -24, 5, -19, -4);
    c.closePath();
    c.fill();
    c.stroke();

    // Nơ đỏ đặc trưng bên tai phải (góc nhìn người chơi)
    c.save();
    c.translate(13, -13);
    c.rotate(0.32);
    c.fillStyle = "#ff3b5c";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2;
    c.beginPath();
    c.ellipse(-6, 0, 5.8, 4.5, -0.15, 0, Math.PI * 2);
    c.ellipse(6, 0, 5.8, 4.5, 0.15, 0, Math.PI * 2);
    c.fill();
    c.stroke();
    c.beginPath();
    c.arc(0, 0, 3.2, 0, Math.PI * 2);
    c.fill();
    c.stroke();
    c.restore();

    // Mắt đen oval
    c.fillStyle = STROKE_COLOR;
    c.beginPath();
    c.ellipse(-8.5, 5, 2.2, 3, 0, 0, Math.PI * 2);
    c.ellipse(8.5, 5, 2.2, 3, 0, 0, Math.PI * 2);
    c.fill();

    // Mũi vàng oval đặc trưng
    c.fillStyle = "#ffcc00";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.6;
    c.beginPath();
    c.ellipse(0, 9.5, 2.8, 2, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // 3 râu mèo mỗi bên má
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.9;
    c.beginPath();
    // Trái
    c.moveTo(-17, 4); c.lineTo(-24, 2.5);
    c.moveTo(-17.5, 8.5); c.lineTo(-24.5, 8.5);
    c.moveTo(-16.5, 13); c.lineTo(-23, 14.5);
    // Phải
    c.moveTo(17, 4); c.lineTo(24, 2.5);
    c.moveTo(17.5, 8.5); c.lineTo(24.5, 8.5);
    c.moveTo(16.5, 13); c.lineTo(23, 14.5);
    c.stroke();

  } else if (charId === "purin") {
    // --- POMPOMPURIN ---
    // Hai tai cụp mềm mại hai bên
    [-1, 1].forEach(dir => {
      c.save();
      c.translate(dir * 16, -6);
      c.rotate(dir * (0.28 - earFlap * 0.6));
      c.fillStyle = "#ffe28a";
      c.strokeStyle = STROKE_COLOR;
      c.lineWidth = 2.3;
      c.beginPath();
      c.ellipse(dir * 3, 10, 6.5, 14, dir * 0.15, 0, Math.PI * 2);
      c.fill();
      c.stroke();
      c.restore();
    });

    // Thân mũm mĩm vàng kem
    c.fillStyle = "#ffe28a";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.4;
    c.beginPath();
    c.moveTo(-16, 12);
    c.quadraticCurveTo(-20, 28, 0, 28);
    c.quadraticCurveTo(20, 28, 16, 12);
    c.fill();
    c.stroke();

    // Đầu tròn mũm mĩm
    c.fillStyle = "#ffe89e";
    c.beginPath();
    c.ellipse(0, 3, 21, 18.5, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Mũ nồi (Beret) màu nâu sô-cô-la đặc trưng trên đỉnh đầu
    c.fillStyle = "#7a442a";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.2;
    c.beginPath();
    c.ellipse(0, -14.5, 13.5, 5.5, -0.06, 0, Math.PI * 2);
    c.fill();
    c.stroke();
    // Cuống mũ nồi nhỏ
    c.beginPath();
    c.moveTo(0, -20);
    c.lineTo(2, -23);
    c.stroke();

    // Mắt tròn nâu sẫm
    c.fillStyle = STROKE_COLOR;
    c.beginPath();
    c.arc(-7.5, 4, 2.3, 0, Math.PI * 2);
    c.arc(7.5, 4, 2.3, 0, Math.PI * 2);
    c.fill();

    // Má hồng ấm áp
    c.fillStyle = "rgba(255, 138, 138, 0.55)";
    c.beginPath();
    c.ellipse(-12, 9.5, 3.6, 2.2, 0, 0, Math.PI * 2);
    c.ellipse(12, 9.5, 3.6, 2.2, 0, 0, Math.PI * 2);
    c.fill();

    // Mũi nâu & miệng chữ w dễ thương
    c.fillStyle = "#7a442a";
    c.beginPath();
    c.ellipse(0, 7.5, 2.4, 1.7, 0, 0, Math.PI * 2);
    c.fill();

    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.8;
    c.beginPath();
    c.moveTo(0, 9.2);
    c.lineTo(0, 11);
    c.moveTo(-3.5, 11.5);
    c.quadraticCurveTo(-1.8, 13.5, 0, 11);
    c.quadraticCurveTo(1.8, 13.5, 3.5, 11.5);
    c.stroke();

  } else if (charId === "cinna") {
    // --- CINNAMOROLL ---
    // Đôi tai trắng dài bay phấp phới hai bên đầu
    [-1, 1].forEach(dir => {
      c.save();
      c.translate(dir * 16, -2);
      c.rotate(dir * (0.2 - earFlap * 1.1));
      c.fillStyle = "#ffffff";
      c.strokeStyle = STROKE_COLOR;
      c.lineWidth = 2.3;
      c.beginPath();
      c.moveTo(0, -4);
      c.bezierCurveTo(dir * 16, -8, dir * 27, 4, dir * 23, 14);
      c.bezierCurveTo(dir * 19, 21, dir * 7, 13, 0, 5);
      c.closePath();
      c.fill();
      c.stroke();
      c.restore();
    });

    // Thân trắng nhỏ xinh
    c.fillStyle = "#ffffff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.2;
    c.beginPath();
    c.ellipse(0, 21, 12, 8.5, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Tay nhỏ dang ra
    c.beginPath();
    c.ellipse(-12, 19, 4.5, 3, -0.3, 0, Math.PI * 2);
    c.ellipse(12, 19, 4.5, 3, 0.3, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Đầu trắng bông xù
    c.fillStyle = "#ffffff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 2.4;
    c.beginPath();
    c.ellipse(0, 3, 21, 17, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Mắt xanh dương to long lanh đặc trưng của Cinnamoroll
    c.fillStyle = "#4db8ff";
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.4;
    c.beginPath();
    c.ellipse(-8.5, 4.5, 2.7, 3.4, 0, 0, Math.PI * 2);
    c.ellipse(8.5, 4.5, 2.7, 3.4, 0, 0, Math.PI * 2);
    c.fill();
    c.stroke();

    // Điểm sáng trong mắt
    c.fillStyle = "#ffffff";
    c.beginPath();
    c.arc(-9.2, 3.3, 1, 0, Math.PI * 2);
    c.arc(7.8, 3.3, 1, 0, Math.PI * 2);
    c.fill();

    // Má hồng phấn
    c.fillStyle = "rgba(255, 145, 185, 0.7)";
    c.beginPath();
    c.ellipse(-13.5, 9.5, 3.8, 2.3, 0, 0, Math.PI * 2);
    c.ellipse(13.5, 9.5, 3.8, 2.3, 0, 0, Math.PI * 2);
    c.fill();

    // Miệng nhỏ hình chữ w
    c.strokeStyle = STROKE_COLOR;
    c.lineWidth = 1.8;
    c.beginPath();
    c.moveTo(-3.2, 8.5);
    c.quadraticCurveTo(-1.6, 11, 0, 8.5);
    c.quadraticCurveTo(1.6, 11, 3.2, 8.5);
    c.stroke();
  }

  // Vẽ các phụ kiện đang trang bị (Nơ, Mũ, Cây kẹo) lên nhân vật
  if (equipped) {
    drawCharacterAccessories(c, charId, equipped, time);
  }

  c.restore();
}

/**
 * ============================================================================
 * 3. CHỦ ĐỀ BACKGROUND ĐỔI SAU MỖI 500 ĐIỂM & HIỆU ỨNG PHÁO HOA HỒNG
 * ============================================================================
 */
const BG_THEMES = [
  {
    name: "🌸 Kẹo Bông Hồng",
    top: "#ffcce6",
    mid: "#ffe6f3",
    bot: "#fff8fc",
    cloud: "rgba(255, 255, 255, 0.72)",
    accent: "#f28ab8",
    stars: false
  },
  {
    name: "🍑 Hoàng Hôn Đào Mật",
    top: "#ff9ebb",
    mid: "#ffc7b2",
    bot: "#fff3e6",
    cloud: "rgba(255, 248, 240, 0.68)",
    accent: "#ff6f91",
    stars: false
  },
  {
    name: "🌙 Đêm Sao Tím Mộng Mơ",
    top: "#4a2c6b",
    mid: "#8c5299",
    bot: "#f2b8d8",
    cloud: "rgba(255, 230, 250, 0.35)",
    accent: "#ffd6f0",
    stars: true
  },
  {
    name: "🌈 Vườn Cầu Vồng Pastel",
    top: "#b8e4ff",
    mid: "#f9d5ec",
    bot: "#fff7d6",
    cloud: "rgba(255, 255, 255, 0.78)",
    accent: "#e86aa7",
    stars: false
  },
  {
    name: "✨ Thiên Hà Ánh Trăng",
    top: "#262254",
    mid: "#6b3e82",
    bot: "#e38eb9",
    cloud: "rgba(255, 220, 245, 0.28)",
    accent: "#ff9ed2",
    stars: true
  }
];

let fireworks = [];
let milestoneBanner = { text: "", timer: 0 };

function triggerPinkFireworks(milestoneScore) {
  audio.playFirework();
  milestoneBanner = {
    text: `🎆 CHÚC MỪNG ${milestoneScore} ĐIỂM! 🎆`,
    timer: 140
  };

  const pinkPalette = [
    "#ff1e8a", "#ff5ca8", "#ff8cc6", "#ffb8dc",
    "#ff3399", "#ffffff", "#ffe0f0", "#ff66b2"
  ];

  // Bắn 6 chùm pháo hoa hồng liên tiếp ở các vị trí đẹp trên bầu trời
  for (let b = 0; b < 6; b++) {
    const bx = 65 + Math.random() * (W - 130);
    const by = 110 + Math.random() * 240;
    const delay = b * 10;
    const count = 34;

    for (let i = 0; i < count; i++) {
      const angle = (Math.PI * 2 * i) / count + (Math.random() - 0.5) * 0.15;
      const speed = 2.2 + Math.random() * 4.2;
      fireworks.push({
        x: bx,
        y: by,
        vx: Math.cos(angle) * speed,
        vy: Math.sin(angle) * speed,
        color: pinkPalette[Math.floor(Math.random() * pinkPalette.length)],
        size: 2.5 + Math.random() * 3,
        life: 65 + Math.floor(Math.random() * 25),
        maxLife: 85,
        delay,
        isHeart: i % 5 === 0
      });
    }
  }
}

/**
 * ============================================================================
 * 4. LOGIC & VÒNG LẶP TRÒ CHƠI CHÍNH
 * ============================================================================
 */
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");
const scoreEl = document.getElementById("score");
const runCoinsEl = document.getElementById("runCoins");
const themeBadgeEl = document.getElementById("themeBadge");
const bestTop = document.getElementById("bestTop");
const overlay = document.getElementById("overlay");
const panel = document.getElementById("panel");

const W = canvas.width;
const H = canvas.height;
const GRAVITY = 0.38;
const BOW_W = 78;
const BOW_H = 44;

let player, platforms, particles, coins;
let cameraY = 0, score = 0, levels = 0, highestY = 0, sessionCoins = 0;
let playing = false, left = false, right = false;
let platformSerial = 0, lastBoostAt = -999;
let currentThemeIndex = 0;
let lastMilestone = 0;
let frameCount = 0;

updateTopBarUI();

// Hiển thị màn hình chờ chính với Tên người chơi, Kỷ lục, Nút Bắt đầu, Đổi nhân vật, Đổi trang phục
function showStartScreen() {
  playing = false;
  document.body.classList.add("lobby-mode");
  overlay.style.display = "flex";

  const charObj = CHARACTERS.find(c => c.id === selectedCharId) || CHARACTERS[0];

  panel.innerHTML = `
    <h1>SANRIO KAWAII JUMP 🎀</h1>
    <p class="subtitle">Thu thập xu vàng, diện phụ kiện xinh và chinh phục bầu trời!</p>

    <div class="profile-box">
      <div class="name-row">
        <span style="font-size:12px;font-weight:800;">🏷️ Tên:</span>
        <input type="text" id="playerNameInput" class="name-input" maxlength="18" placeholder="Nhập tên của bạn..." value="${escapeHtml(saveData.playerName)}">
      </div>
      <div class="record-banner">
        <span>👤 <b id="displayPlayerName">${escapeHtml(saveData.playerName)}</b></span>
        <span>🏆 Kỷ lục: <b>${saveData.bestScore}</b> điểm</span>
      </div>
    </div>

    <div class="lobby-preview-wrap">
      <canvas id="lobbyHeroCanvas" width="130" height="115"></canvas>
      <div class="lobby-char-tag">✨ ${charObj.name} ✨</div>
    </div>

    <div class="lobby-btn-group">
      <button class="main-btn" id="startBtn">▶ BẮT ĐẦU CHƠI</button>
      <div class="dual-btns">
        <button class="nav-btn" id="openCharBtn">🐰 ĐỔI NHÂN VẬT</button>
        <button class="nav-btn" id="openWardrobeBtn">👗 ĐỔI TRANG PHỤC</button>
      </div>
      <button class="nav-btn" id="openAchievementsBtn">🏅 THÀNH TÍCH & PHẦN THƯỞNG</button>
    </div>
  `;

  // Vẽ nhân vật hiện tại kèm đầy đủ phụ kiện đang đeo trên màn hình chờ
  const heroCanvas = document.getElementById("lobbyHeroCanvas");
  if (heroCanvas) {
    const hCtx = heroCanvas.getContext("2d");
    hCtx.clearRect(0, 0, 130, 115);
    drawSanrioCharacter(hCtx, selectedCharId, 65, 64, 1.55, 0, 0, saveData.equipped);
  }

  // Lưu tên người chơi ngay khi nhập
  const nameInput = document.getElementById("playerNameInput");
  nameInput.addEventListener("input", () => {
    const val = nameInput.value.trim();
    saveData.playerName = val || "Bé Thỏ Hồng";
    document.getElementById("displayPlayerName").textContent = saveData.playerName;
    persistSave();
  });

  document.getElementById("startBtn").addEventListener("click", () => {
    audio.playClick();
    audio.startBgm();
    resetGame();
  });

  document.getElementById("openCharBtn").addEventListener("click", () => {
    audio.playClick();
    showCharacterSelectScreen();
  });

  document.getElementById("openWardrobeBtn").addEventListener("click", () => {
    audio.playClick();
    showWardrobeScreen("bow");
  });
  document.getElementById("openAchievementsBtn").addEventListener("click", () => {
    audio.playClick();
    showAchievementsScreen();
  });

  drawBackground();
}

function showAchievementsScreen() {
  playing = false;
  document.body.classList.add("lobby-mode");
  const completed = new Set(saveData.achievements || []);
  const rows = Array.from({ length: Math.max(10, Math.max(0, ...completed) + 2) }, (_, i) => i + 1);
  panel.innerHTML = `
    <h1>🏅 THÀNH TÍCH BẦU TRỜI</h1>
    <p class="subtitle">Mỗi tầng được chinh phục lần đầu sẽ thưởng 5 xu. Phần thưởng chỉ nhận một lần!</p>
    <div class="stat-row"><span>✨ Tầng đã mở khóa</span><b>${completed.size}</b></div>
    <div class="stat-row"><span>🪙 Tổng xu thưởng</span><b>${completed.size * 5}</b></div>
    <div class="acc-list" style="max-height:280px">
      ${rows.map(n => `<div class="acc-item">
        <div class="acc-info"><div class="acc-swatch" style="background:#ffe3f1">🏆</div>
        <div><div class="acc-title">Tầng ${n}</div><div class="acc-sub">${completed.has(n) ? "Đã nhận thưởng" : "Chưa chinh phục"}</div></div></div>
        <b style="color:${completed.has(n) ? "#269b58" : "#c9347c"}">${completed.has(n) ? "✓ +5 xu" : "🔒 5 xu"}</b>
      </div>`).join("")}
    </div>
    <button class="main-btn" id="backAchievementsBtn">← QUAY LẠI MENU</button>`;
  document.getElementById("backAchievementsBtn").addEventListener("click", () => {
    audio.playClick();
    showStartScreen();
  });
}

function escapeHtml(str) {
  return String(str).replace(/[&<>"']/g, m => ({
    "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;"
  }[m]));
}

// Giao diện Đổi Nhân Vật (5 nhân vật Sanrio)
function showCharacterSelectScreen() {
  playing = false;
  document.body.classList.add("lobby-mode");
  overlay.style.display = "flex";
  const cardsHtml = CHARACTERS.map(ch => `
    <div class="char-card ${ch.id === selectedCharId ? "selected" : ""}" data-id="${ch.id}">
      <canvas class="char-preview" id="preview-${ch.id}" width="90" height="90"></canvas>
      <div class="char-name">${ch.name}</div>
    </div>
  `).join("");

  panel.innerHTML = `
    <h1>CHỌN NHÂN VẬT 🐰</h1>
    <p class="subtitle">Chạm vào nhân vật bạn yêu thích để đồng hành nhé!</p>
    <div class="char-grid">${cardsHtml}</div>
    <button class="main-btn" id="confirmCharBtn">✔ XÁC NHẬN & QUAY LẠI</button>
  `;

  CHARACTERS.forEach(ch => {
    const pCanvas = document.getElementById(`preview-${ch.id}`);
    if (pCanvas) {
      const pCtx = pCanvas.getContext("2d");
      pCtx.clearRect(0, 0, 90, 90);
      drawSanrioCharacter(pCtx, ch.id, 45, 52, 1.3, 0, 0, saveData.equipped);
    }
  });

  panel.querySelectorAll(".char-card").forEach(card => {
    card.addEventListener("click", () => {
      selectedCharId = card.dataset.id;
      saveData.selectedChar = selectedCharId;
      persistSave();
      audio.playClick();
      panel.querySelectorAll(".char-card").forEach(el => {
        el.classList.toggle("selected", el.dataset.id === selectedCharId);
      });
    });
  });

  document.getElementById("confirmCharBtn").addEventListener("click", () => {
    audio.playClick();
    showStartScreen();
  });
}

// Giao diện Đổi Trang Phục / Cửa Hàng Phụ Kiện (Nơ, Mũ, Cây kẹo)
function showWardrobeScreen(activeTab = "bow", toastMsg = "") {
  playing = false;
  document.body.classList.add("lobby-mode");
  overlay.style.display = "flex";
  const items = ACCESSORIES[activeTab] || [];

  const listHtml = items.map(item => {
    const isOwned = saveData.owned.includes(item.id);
    const isEquipped = saveData.equipped[activeTab] === item.id;
    const swatchBg = item.main === "rainbow"
      ? "linear-gradient(135deg, #ff6b9d, #fde047, #60a5fa)"
      : item.main;

    let btnHtml = "";
    if (isEquipped) {
      btnHtml = `<button class="acc-action-btn btn-equipped" disabled>Đang đeo</button>`;
    } else if (isOwned) {
      btnHtml = `<button class="acc-action-btn btn-equip" data-action="equip" data-id="${item.id}">Đeo vào</button>`;
    } else {
      btnHtml = `<button class="acc-action-btn btn-buy" data-action="buy" data-id="${item.id}">🪙 ${item.price}</button>`;
    }

    return `
      <div class="acc-item ${isEquipped ? "equipped" : ""}">
        <div class="acc-info">
          <div class="acc-swatch" style="background:${swatchBg}">${item.icon}</div>
          <div>
            <div class="acc-title">${item.name}</div>
            <div class="acc-sub">${item.price === 0 ? "Miễn phí" : (isOwned ? "Đã sở hữu" : `Giá: ${item.price} xu`)}</div>
          </div>
        </div>
        ${btnHtml}
      </div>
    `;
  }).join("");

  panel.innerHTML = `
    <h1>TỦ ĐỒ PHỤ KIỆN 👗</h1>
    <div class="lobby-preview-wrap" style="padding:4px 8px; margin-bottom:7px;">
      <canvas id="wardrobeHeroCanvas" width="110" height="96"></canvas>
    </div>

    <div class="tabs-row">
      <button class="tab-btn ${activeTab === "bow" ? "active" : ""}" data-tab="bow">🎀 Nơ</button>
      <button class="tab-btn ${activeTab === "hat" ? "active" : ""}" data-tab="hat">👑 Mũ</button>
      <button class="tab-btn ${activeTab === "candy" ? "active" : ""}" data-tab="candy">🍭 Cây Kẹo</button>
    </div>

    <div class="shop-toast" id="shopToast">${toastMsg}</div>
    <div class="acc-list">${listHtml}</div>

    <button class="main-btn" id="backLobbyBtn">✔ XONG & QUAY LẠI</button>
  `;

  const wCanvas = document.getElementById("wardrobeHeroCanvas");
  if (wCanvas) {
    const wCtx = wCanvas.getContext("2d");
    wCtx.clearRect(0, 0, 110, 96);
    drawSanrioCharacter(wCtx, selectedCharId, 55, 54, 1.32, 0, 0, saveData.equipped);
  }

  panel.querySelectorAll(".tab-btn").forEach(btn => {
    btn.addEventListener("click", () => {
      audio.playClick();
      showWardrobeScreen(btn.dataset.tab);
    });
  });

  panel.querySelectorAll(".acc-action-btn[data-action]").forEach(btn => {
    btn.addEventListener("click", () => {
      const id = btn.dataset.id;
      const action = btn.dataset.action;
      const item = items.find(i => i.id === id);
      if (!item) return;

      if (action === "equip") {
        saveData.equipped[activeTab] = item.id;
        persistSave();
        audio.playClick();
        showWardrobeScreen(activeTab, `✨ Đã đeo: ${item.name}!`);
      } else if (action === "buy") {
        if (saveData.coins >= item.price) {
          saveData.coins -= item.price;
          saveData.owned.push(item.id);
          saveData.equipped[activeTab] = item.id;
          persistSave();
          audio.playBuy();
          showWardrobeScreen(activeTab, `🎉 Mua thành công ${item.name}!`);
        } else {
          audio.playClick();
          showWardrobeScreen(activeTab, `😢 Bạn cần thêm ${item.price - saveData.coins} xu nữa!`);
        }
      }
    });
  });

  document.getElementById("backLobbyBtn").addEventListener("click", () => {
    audio.playClick();
    showStartScreen();
  });
}

function newPlatform(y, forcedType) {
  platformSerial++;
  let type = forcedType || "normal";
  if (!forcedType) {
    if (platformSerial - lastBoostAt >= 13) {
      type = "boost";
      lastBoostAt = platformSerial;
    } else {
      const r = Math.random();
      type = r < 0.28 ? "special" : "normal";
    }
  }
  const px = 48 + Math.random() * (W - 96);
  platforms.push({
    id: platformSerial,
    x: px,
    y,
    type,
    used: false,
    counted: false
  });

  // Sinh đồng xu kawaii phía trên bệ nhảy (tỷ lệ ~55% mỗi tầng)
  if (platformSerial > 1 && Math.random() < 0.55) {
    const coinX = Math.max(32, Math.min(W - 32, px + (Math.random() - 0.5) * 70));
    coins.push({
      x: coinX,
      y: y - 36,
      collected: false,
      phase: Math.random() * Math.PI * 2
    });
  }
}

function resetGame() {
  document.body.classList.remove("lobby-mode");
  score = 0;
  levels = 0;
  sessionCoins = 0;
  cameraY = 0;
  highestY = 0;
  platformSerial = 0;
  lastBoostAt = -999;
  currentThemeIndex = 0;
  lastMilestone = 0;
  platforms = [];
  particles = [];
  coins = [];
  fireworks = [];
  milestoneBanner = { text: "", timer: 0 };

  player = {
    x: W / 2,
    y: 560,
    vx: 0,
    vy: -10.5,
    w: 44,
    h: 54,
    boostFlash: 0
  };

  newPlatform(625, "normal");
  for (let y = 530; y >= -500; y -= 92) {
    newPlatform(y);
  }

  scoreEl.textContent = "0";
  runCoinsEl.textContent = "0";
  themeBadgeEl.textContent = BG_THEMES[0].name;
  overlay.style.display = "none";
  playing = true;
  requestAnimationFrame(loop);
}

function addScore(p) {
  if (!p.counted) {
    p.counted = true;
    levels++;
    score += 10;
    if (!saveData.achievements.includes(levels)) {
      saveData.achievements.push(levels);
      saveData.coins += 5;
      sessionCoins += 5;
      audio.playCoin();
      milestoneBanner = { text: `🏅 TẦNG ${levels} MỚI! +5 XU`, timer: 90 };
    }
  }
}

function collectCoin(amount, x, y) {
  sessionCoins += amount;
  saveData.coins += amount;
  runCoinsEl.textContent = sessionCoins;
  burst(x, y, "🪙");
}

function burst(x, y, symbol = "♡") {
  for (let i = 0; i < 8; i++) {
    particles.push({
      x,
      y,
      vx: (Math.random() - 0.5) * 4.5,
      vy: -Math.random() * 4 - 1,
      life: 36,
      symbol
    });
  }
}

function cloudBurst(x, y, rainbow = false) {
  const palette = rainbow
    ? ["#ff78ad", "#ffbd70", "#fff080", "#8fe6a9", "#83d8ff", "#c5a0ff"]
    : ["#ffb6d9", "#ffd0e6", "#fff0f7", "#f58cbd"];
  for (let i = 0; i < (rainbow ? 12 : 7); i++) {
    particles.push({
      x, y,
      vx: (Math.random() - 0.5) * (rainbow ? 5 : 3.5),
      vy: (Math.random() - 0.5) * (rainbow ? 4 : 2.8) + (rainbow ? 0.5 : -0.2),
      life: 24 + Math.random() * 20,
      color: palette[i % palette.length],
      radius: 1.5 + Math.random() * 3,
      cloud: true
    });
  }
  // Giới hạn số hạt để tránh giảm FPS trên máy cấu hình thấp.
  if (particles.length > 100) particles.splice(0, particles.length - 100);
}

function checkMilestoneAndTheme() {
  const milestone = Math.floor(score / 500) * 500;
  if (milestone >= 500 && milestone > lastMilestone) {
    lastMilestone = milestone;
    currentThemeIndex = Math.floor(score / 500) % BG_THEMES.length;
    themeBadgeEl.textContent = BG_THEMES[currentThemeIndex].name;
    // Thưởng 25 xu khi đạt mỗi mốc 500 điểm
    collectCoin(25, W / 2, 130);
    triggerPinkFireworks(milestone);
  }
}

function update() {
  frameCount++;

  if (left) player.vx = -5.1;
  else if (right) player.vx = 5.1;
  else player.vx *= 0.82;

  player.x += player.vx;

  // CƠ CHẾ CHẶN TƯỜNG HAI BÊN: Nhân vật không đi xuyên mép mà dừng lại ở biên trái/phải
  const minX = player.w / 2 + 4;
  const maxX = W - player.w / 2 - 4;
  if (player.x < minX) {
    player.x = minX;
    if (player.vx < 0) player.vx = 0;
  } else if (player.x > maxX) {
    player.x = maxX;
    if (player.vx > 0) player.vx = 0;
  }

  const oldBottom = player.y + player.h / 2;
  player.vy += GRAVITY;
  player.y += player.vy;
  const newBottom = player.y + player.h / 2;

  // Va chạm khi nhân vật rơi xuống
  if (player.vy > 0) {
    for (const p of platforms) {
      const overlapsX = player.x + 17 > p.x - BOW_W / 2 &&
                        player.x - 17 < p.x + BOW_W / 2;
      const crossesTop = oldBottom <= p.y + 6 && newBottom >= p.y;
      if (!overlapsX || !crossesTop) continue;

      if (p.type === "normal") {
        player.y = p.y - player.h / 2;
        player.vy = -11.6;
        addScore(p);
        audio.playJumpNormal();
        burst(p.x, p.y - cameraY, "♡");
        cloudBurst(p.x, p.y - cameraY, false);
      } else if (p.type === "special" && !p.used) {
        player.y = p.y - player.h / 2;
        player.vy = -16.2;
        p.used = true;
        addScore(p);
        score += 10;
        audio.playJumpSpecial();
        burst(p.x, p.y - cameraY, "✧");
        cloudBurst(p.x, p.y - cameraY, true);
      } else if (p.type === "boost" && !p.used) {
        player.y = p.y - player.h / 2;
        player.vy = -40;
        p.used = true;
        addScore(p);
        score += 100;
        player.boostFlash = 58;
        audio.playBoost();
        cloudBurst(p.x, p.y - cameraY, true);
        collectCoin(10, p.x, p.y - cameraY);
        burst(p.x, p.y - cameraY, "🚀");
      }
      break;
    }
  }

  // Kiểm tra ăn đồng xu vàng trên đường bay
  for (const cItem of coins) {
    if (cItem.collected) continue;
    const dx = player.x - cItem.x;
    const dy = player.y - cItem.y;
    if (dx * dx + dy * dy < 34 * 34) {
      cItem.collected = true;
      audio.playCoin();
      collectCoin(5, cItem.x, cItem.y - cameraY);
    }
  }

  if (player.y - cameraY < 255) {
    cameraY = player.y - 255;
  }
  highestY = Math.min(highestY, player.y);
  score = Math.max(score, Math.floor((560 - highestY) / 12));

  // Kiểm tra cột mốc mỗi 500 điểm
  checkMilestoneAndTheme();

  // Sinh thêm các tầng nơ mới phía trên
  let topY = Math.min(...platforms.map(p => p.y));
  while (topY > player.y - 2700) {
    topY -= 88 + Math.random() * 18;
    newPlatform(topY);
  }

  platforms = platforms.filter(p => p.y - cameraY < H + 100);
  coins = coins.filter(cItem => !cItem.collected && cItem.y - cameraY < H + 100);

  if (player.boostFlash > 0) player.boostFlash--;
  if (milestoneBanner.timer > 0) milestoneBanner.timer--;

  for (const q of particles) {
    q.x += q.vx;
    q.y += q.vy;
    q.vy += 0.08;
    q.life--;
  }
  particles = particles.filter(q => q.life > 0);

  // Tài nguyên trong lượt chỉ giữ trong bộ nhớ; ghi xuống máy khi kết thúc lượt.
  // Cập nhật hạt pháo hoa màu hồng
  for (const fw of fireworks) {
    if (fw.delay > 0) {
      fw.delay--;
      continue;
    }
    fw.x += fw.vx;
    fw.y += fw.vy;
    fw.vx *= 0.96;
    fw.vy = fw.vy * 0.96 + 0.05;
    fw.life--;
  }
  fireworks = fireworks.filter(fw => fw.life > 0);

  scoreEl.textContent = score;

  if (player.y - cameraY > H + 65) {
    finishGame();
  }
}

function drawBackground() {
  const theme = BG_THEMES[currentThemeIndex];
  const grad = ctx.createLinearGradient(0, 0, 0, H);
  grad.addColorStop(0, theme.top);
  grad.addColorStop(0.55, theme.mid);
  grad.addColorStop(1, theme.bot);
  ctx.fillStyle = grad;
  ctx.fillRect(0, 0, W, H);

  // Vẽ sao lấp lánh cho chủ đề ban đêm
  if (theme.stars) {
    ctx.fillStyle = "#fff9d6";
    for (let i = 0; i < 24; i++) {
      const sx = (i * 97 + 31) % W;
      const sy = ((i * 131 + 40 - cameraY * 0.1) % H + H) % H;
      const r = (i % 3 === 0) ? 2.2 : 1.3;
      ctx.globalAlpha = 0.45 + 0.5 * Math.sin(frameCount * 0.08 + i);
      ctx.beginPath();
      ctx.arc(sx, sy, r, 0, Math.PI * 2);
      ctx.fill();
    }
    ctx.globalAlpha = 1;
  }

  // Mây bồng bềnh
  for (let i = 0; i < 9; i++) {
    const x = (i * 73 + 25) % (W + 50) - 20;
    const y = ((i * 113 + 70 - cameraY * 0.22) % (H + 100) + H + 100) % (H + 100);
    ctx.fillStyle = theme.cloud;
    ctx.beginPath();
    ctx.arc(x, y, 17, 0, Math.PI * 2);
    ctx.arc(x + 18, y - 8, 21, 0, Math.PI * 2);
    ctx.arc(x + 39, y, 16, 0, Math.PI * 2);
    ctx.fill();
  }

  // Ký hiệu trang trí
  ctx.font = "19px Arial";
  ctx.fillStyle = theme.accent;
  ctx.fillText("♡", 38, 180);
  ctx.fillText("✧", 365, 330);
  ctx.fillText("♡", 75, 510);
}

function drawBow(p) {
  const x = p.x;
  const y = p.y - cameraY;
  ctx.save();

  // Bệ mây bồng bềnh viền hồng ruby, nơ cũ nằm nổi bật ở chính giữa.
  ctx.shadowColor = "rgba(235, 92, 165, 0.35)";
  ctx.shadowBlur = 4;
  ctx.fillStyle = "#fff8fd";
  ctx.strokeStyle = "#f4a0c8";
  ctx.lineWidth = 2.5;
  ctx.beginPath();
  ctx.arc(x - 25, y + 1, 12, 0, Math.PI * 2);
  ctx.arc(x - 12, y - 7, 15, 0, Math.PI * 2);
  ctx.arc(x + 7, y - 9, 17, 0, Math.PI * 2);
  ctx.arc(x + 25, y + 1, 12, 0, Math.PI * 2);
  ctx.arc(x, y + 5, 29, 0, Math.PI * 2);
  ctx.fill();
  ctx.stroke();
  ctx.shadowBlur = 0;

  let mainFill = "#ff8ec2";
  let innerFill = "#ffc2de";
  if (p.type === "special") {
    mainFill = "#c97bff";
    innerFill = "#ebd1ff";
  } else if (p.type === "boost") {
    mainFill = "#ff4797";
    innerFill = "#ffadd2";
    ctx.shadowColor = "#ff2a85";
    ctx.shadowBlur = 9;
  }

  ctx.strokeStyle = STROKE_COLOR;
  ctx.lineWidth = 2.2;

  // Cánh nơ trái
  ctx.fillStyle = mainFill;
  ctx.beginPath();
  ctx.moveTo(x - 5, y);
  ctx.bezierCurveTo(x - 24, y - 18, x - 38, y - 10, x - 36, y);
  ctx.bezierCurveTo(x - 38, y + 10, x - 24, y + 18, x - 5, y);
  ctx.closePath();
  ctx.fill();
  ctx.stroke();

  // Cánh nơ phải
  ctx.beginPath();
  ctx.moveTo(x + 5, y);
  ctx.bezierCurveTo(x + 24, y - 18, x + 38, y - 10, x + 36, y);
  ctx.bezierCurveTo(x + 38, y + 10, x + 24, y + 18, x + 5, y);
  ctx.closePath();
  ctx.fill();
  ctx.stroke();

  // Nếp gấp bên trong nơ
  ctx.fillStyle = innerFill;
  ctx.beginPath();
  ctx.ellipse(x - 19, y, 8, 4, -0.15, 0, Math.PI * 2);
  ctx.ellipse(x + 19, y, 8, 4, 0.15, 0, Math.PI * 2);
  ctx.fill();

  // Nút thắt ở giữa nơ
  ctx.fillStyle = mainFill;
  ctx.beginPath();
  ctx.roundRect(x - 8, y - 8, 16, 16, 6);
  ctx.fill();
  ctx.stroke();

  if (p.type === "boost") {
    ctx.shadowBlur = 0;
    ctx.font = "22px Arial";
    ctx.textAlign = "center";
    ctx.fillText("🚀", x, y - 22);
  } else if (p.type === "special") {
    ctx.shadowBlur = 0;
    ctx.font = "14px Arial";
    ctx.textAlign = "center";
    ctx.fillStyle = "#9b30d9";
    ctx.fillText("✦", x, y - 18);
  }

  ctx.restore();
}

function drawFireworks() {
  for (const fw of fireworks) {
    if (fw.delay > 0) continue;
    ctx.save();
    const alpha = Math.max(0, fw.life / fw.maxLife);
    ctx.globalAlpha = alpha;
    ctx.fillStyle = fw.color;
    ctx.shadowColor = "#ff2e93";
    ctx.shadowBlur = 10;

    if (fw.isHeart) {
      ctx.font = `${Math.round(fw.size * 4.5)}px Arial`;
      ctx.fillText("♥", fw.x, fw.y);
    } else {
      ctx.beginPath();
      ctx.arc(fw.x, fw.y, fw.size, 0, Math.PI * 2);
      ctx.fill();
    }
    ctx.restore();
  }
}

function drawCoin(cItem) {
  const x = cItem.x;
  const y = cItem.y - cameraY + Math.sin(frameCount * 0.1 + cItem.phase) * 3.5;
  ctx.save();
  ctx.translate(x, y);

  // Hào quang vàng nhẹ
  ctx.shadowColor = "#ffd000";
  ctx.shadowBlur = 10;

  // Đồng xu vàng kawaii
  ctx.fillStyle = "#ffd93b";
  ctx.strokeStyle = "#8a5200";
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.arc(0, 0, 11.5, 0, Math.PI * 2);
  ctx.fill();
  ctx.stroke();

  ctx.shadowBlur = 0;
  // Viền trong đồng xu
  ctx.strokeStyle = "#fff59e";
  ctx.lineWidth = 1.4;
  ctx.beginPath();
  ctx.arc(0, 0, 8, 0, Math.PI * 2);
  ctx.stroke();

  // Trái tim nhỏ giữa đồng xu
  ctx.fillStyle = "#ff5ca8";
  ctx.font = "bold 10px Arial";
  ctx.textAlign = "center";
  ctx.textBaseline = "middle";
  ctx.fillText("♥", 0, 0.5);

  ctx.restore();
}

function draw() {
  drawBackground();

  for (const p of platforms) {
    if (p.type === "normal" || !p.used) {
      drawBow(p);
    }
  }

  for (const cItem of coins) {
    if (!cItem.collected) {
      drawCoin(cItem);
    }
  }

  if (player) {
    ctx.save();
    if (player.boostFlash > 0) {
      ctx.shadowColor = "#ff3b9a";
      ctx.shadowBlur = 24;
    }
    drawSanrioCharacter(
      ctx,
      selectedCharId,
      player.x,
      player.y - cameraY,
      1.05,
      player.vy,
      frameCount,
      saveData.equipped
    );
    ctx.restore();
  }

  // Hạt hiệu ứng bật nhảy
  for (const q of particles) {
    ctx.globalAlpha = Math.max(0, q.life / 44);
    if (q.cloud) {
      ctx.fillStyle = q.color;
      ctx.shadowColor = q.color;
      // Vẽ hạt đơn giản, không dùng shadowBlur cho từng hạt.
      ctx.beginPath();
      ctx.arc(q.x, q.y, q.radius || 2, 0, Math.PI * 2);
      ctx.fill();
      ctx.shadowBlur = 0;
    } else {
      ctx.font = "18px Arial";
      ctx.fillStyle = q.color || "#e84e99";
      ctx.fillText(q.symbol, q.x, q.y);
    }
  }
  ctx.globalAlpha = 1;

  // Pháo hoa hồng khi đạt mốc 500 điểm
  drawFireworks();

  // Thông báo Super Jump
  if (player && player.boostFlash > 0) {
    ctx.fillStyle = "#c83c80";
    ctx.font = "bold 19px Arial";
    ctx.textAlign = "center";
    ctx.fillText("SUPER JUMP! +100 💗", W / 2, 76);
  }

  // Thông báo chúc mừng mốc 500 điểm
  if (milestoneBanner.timer > 0) {
    ctx.save();
    ctx.globalAlpha = Math.min(1, milestoneBanner.timer / 25);
    ctx.fillStyle = "rgba(255, 255, 255, 0.92)";
    ctx.strokeStyle = "#ff4da6";
    ctx.lineWidth = 2.5;
    ctx.beginPath();
    ctx.roundRect(W / 2 - 155, 92, 310, 38, 19);
    ctx.fill();
    ctx.stroke();

    ctx.fillStyle = "#d9267e";
    ctx.font = "bold 15px Arial";
    ctx.textAlign = "center";
    ctx.fillText(milestoneBanner.text, W / 2, 116);
    ctx.restore();
  }
}

function loop() {
  if (!playing) return;
  update();
  draw();
  if (playing) requestAnimationFrame(loop);
}

function finishGame() {
  playing = false;
  audio.playGameOver();
  if (score > saveData.bestScore) {
    saveData.bestScore = score;
  }
  // Chỉ chốt xu, thành tích và kỷ lục khi lượt chơi đã kết thúc.
  persistSave();
  document.body.classList.remove("lobby-mode");

  const charObj = CHARACTERS.find(c => c.id === selectedCharId) || CHARACTERS[0];

  overlay.style.display = "flex";
  panel.innerHTML = `
    <h1>HẾT LƯỢT CHƠI 🎀</h1>
    <p class="subtitle">Người chơi: <b>${escapeHtml(saveData.playerName)}</b> (${charObj.name})</p>
    <div class="stat-row"><span>💗 Điểm lượt này:</span><b>${score}</b></div>
    <div class="stat-row"><span>🪙 Xu kiếm được:</span><b>+${sessionCoins} (Tổng: ${saveData.coins})</b></div>
    <div class="stat-row"><span>🏆 Kỷ lục cá nhân:</span><b>${saveData.bestScore}</b></div>
    <button class="main-btn" id="restartBtn">▶ CHƠI LẠI NGAY</button>
    <div class="dual-btns" style="margin-top:8px;">
      <button class="nav-btn" id="changeCharBtn">🐰 ĐỔI NHÂN VẬT</button>
      <button class="nav-btn" id="wardrobeEndBtn">👗 TRANG PHỤC</button>
    </div>
    <button class="secondary-btn" id="homeLobbyBtn">🏠 MÀN HÌNH CHỜ</button>
  `;

  document.getElementById("restartBtn").addEventListener("click", () => {
    audio.playClick();
    resetGame();
  });

  document.getElementById("changeCharBtn").addEventListener("click", () => {
    audio.playClick();
    showCharacterSelectScreen();
  });

  document.getElementById("wardrobeEndBtn").addEventListener("click", () => {
    audio.playClick();
    showWardrobeScreen("bow");
  });

  document.getElementById("homeLobbyBtn").addEventListener("click", () => {
    audio.playClick();
    showStartScreen();
  });

  draw();
}

/**
 * ============================================================================
 * 5. ĐIỀU KHIỂN ĐA NỀN TẢNG (BÀN PHÍM PC + NÚT BẤM + VUỐT/CHẠM TRÊN MOBILE)
 * ============================================================================
 */
document.addEventListener("keydown", e => {
  if (["ArrowLeft", "ArrowRight", " "].includes(e.key)) e.preventDefault();
  if (e.key === "ArrowLeft" || e.key.toLowerCase() === "a") {
    left = true;
    document.getElementById("leftBtn").classList.add("active");
  }
  if (e.key === "ArrowRight" || e.key.toLowerCase() === "d") {
    right = true;
    document.getElementById("rightBtn").classList.add("active");
  }
});

document.addEventListener("keyup", e => {
  if (e.key === "ArrowLeft" || e.key.toLowerCase() === "a") {
    left = false;
    document.getElementById("leftBtn").classList.remove("active");
  }
  if (e.key === "ArrowRight" || e.key.toLowerCase() === "d") {
    right = false;
    document.getElementById("rightBtn").classList.remove("active");
  }
});

function bindHoldButton(id, dir) {
  const btn = document.getElementById(id);
  const on = e => {
    e.preventDefault();
    audio.init();
    btn.classList.add("active");
    if (dir === "left") left = true;
    else right = true;
  };
  const off = e => {
    e.preventDefault();
    btn.classList.remove("active");
    if (dir === "left") left = false;
    else right = false;
  };
  btn.addEventListener("pointerdown", on);
  btn.addEventListener("pointerup", off);
  btn.addEventListener("pointercancel", off);
  btn.addEventListener("pointerleave", off);
}

bindHoldButton("leftBtn", "left");
bindHoldButton("rightBtn", "right");

// Hỗ trợ chạm & kéo trực tiếp trên Canvas cho điện thoại và máy tính bảng
let activeTouchId = null;
let lastTouchX = null;

canvas.addEventListener("touchstart", e => {
  if (!playing) return;
  e.preventDefault();
  audio.init();
  const touch = e.changedTouches[0];
  activeTouchId = touch.identifier;
  lastTouchX = touch.clientX;

  const rect = canvas.getBoundingClientRect();
  const relX = touch.clientX - rect.left;
  if (relX < rect.width / 2) {
    left = true;
    right = false;
  } else {
    right = true;
    left = false;
  }
}, { passive: false });

canvas.addEventListener("touchmove", e => {
  if (!playing) return;
  e.preventDefault();
  for (let i = 0; i < e.changedTouches.length; i++) {
    const touch = e.changedTouches[i];
    if (touch.identifier === activeTouchId) {
      const dx = touch.clientX - lastTouchX;
      lastTouchX = touch.clientX;
      // Di chuyển mượt theo ngón tay kéo và giữ trong biên trái/phải
      const minX = player.w / 2 + 4;
      const maxX = W - player.w / 2 - 4;
      player.x = Math.max(minX, Math.min(maxX, player.x + dx * (W / canvas.getBoundingClientRect().width) * 0.68));
      if (dx < -1.5) {
        left = true;
        right = false;
      } else if (dx > 1.5) {
        right = true;
        left = false;
      }
    }
  }
}, { passive: false });

function endCanvasTouch(e) {
  for (let i = 0; i < e.changedTouches.length; i++) {
    if (e.changedTouches[i].identifier === activeTouchId) {
      activeTouchId = null;
      left = false;
      right = false;
    }
  }
}

canvas.addEventListener("touchend", endCanvasTouch);
canvas.addEventListener("touchcancel", endCanvasTouch);

// Khởi chạy màn hình chờ khi mở trang
window.onload = function () {
  showStartScreen();
};
</script>
</body>
</html>
