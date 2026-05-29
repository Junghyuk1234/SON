[digital-balance-hub.html](https://github.com/user-attachments/files/28373016/digital-balance-hub.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Digital Balance Hub</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;600;700&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green-dark: #1a3c2e;
    --green-main: #2d6a4f;
    --green-mid: #40916c;
    --green-light: #52b788;
    --green-pale: #95d5b2;
    --green-bg: #d8f3dc;
    --blue-soft: #EBF3FF;
    --blue-icon: #C7DEFB;
    --orange-soft: #FFF3E8;
    --orange-icon: #FFD8B3;
    --purple-soft: #F0EDFF;
    --purple-icon: #D8D1FF;
    --teal-soft: #EAFAF2;
    --teal-icon: #B3EDD4;
    --bg: #f0f4f1;
    --surface: #ffffff;
    --text-primary: #1a2e22;
    --text-secondary: #5a7a68;
    --text-muted: #8aab97;
    --border: rgba(0,0,0,0.07);
    --shadow-sm: 0 1px 3px rgba(0,0,0,0.06), 0 1px 2px rgba(0,0,0,0.04);
    --shadow-md: 0 4px 12px rgba(0,0,0,0.08), 0 2px 4px rgba(0,0,0,0.04);
    --radius-sm: 8px;
    --radius-md: 12px;
    --radius-lg: 18px;
    --radius-xl: 24px;
  }

  html, body {
    height: 100%;
    font-family: 'Noto Sans KR', 'Plus Jakarta Sans', sans-serif;
    background: var(--bg);
    color: var(--text-primary);
    font-size: 14px;
    line-height: 1.5;
  }

  .app {
    display: flex;
    flex-direction: column;
    height: 100vh;
    max-height: 100vh;
    overflow: hidden;
  }

  /* ── HEADER ── */
  header {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 28px;
    height: 58px;
    flex-shrink: 0;
    z-index: 10;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
  }
  .logo-icon {
    width: 32px;
    height: 32px;
    background: linear-gradient(135deg, var(--green-main), var(--green-mid));
    border-radius: 9px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 2px 6px rgba(45,106,79,0.35);
  }
  .logo-icon svg { width: 18px; height: 18px; color: #fff; }
  .logo-text {
    font-size: 15px;
    font-weight: 700;
    color: var(--text-primary);
    font-family: 'Plus Jakarta Sans', sans-serif;
    letter-spacing: -0.3px;
  }

  nav {
    display: flex;
    height: 58px;
    align-items: center;
    gap: 2px;
  }
  .nav-item {
    padding: 0 16px;
    height: 58px;
    display: flex;
    align-items: center;
    font-size: 13.5px;
    font-weight: 500;
    color: var(--text-secondary);
    cursor: pointer;
    border-bottom: 2.5px solid transparent;
    transition: color 0.15s;
    user-select: none;
  }
  .nav-item:hover { color: var(--green-main); }
  .nav-item.active {
    color: var(--green-main);
    border-bottom-color: var(--green-main);
    font-weight: 600;
  }

  .user-area {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .avatar {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, #f6a192, #e07b6a);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 700;
    color: #fff;
    flex-shrink: 0;
    border: 2px solid #fff;
    box-shadow: 0 2px 6px rgba(224,123,106,0.4);
  }
  .user-info { line-height: 1.2; }
  .user-name { font-size: 13px; font-weight: 600; color: var(--text-primary); }
  .user-level { font-size: 11px; color: var(--text-muted); }
  .badge {
    width: 24px; height: 24px;
    background: linear-gradient(135deg, #ffd700, #ffb400);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 12px;
    box-shadow: 0 2px 4px rgba(255,180,0,0.4);
  }
  .bell-btn {
    width: 34px; height: 34px;
    border-radius: 50%;
    border: 1px solid var(--border);
    background: var(--surface);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer;
    transition: background 0.15s;
  }
  .bell-btn:hover { background: var(--bg); }
  .bell-btn svg { width: 17px; height: 17px; color: var(--text-secondary); }

  /* ── MAIN GRID ── */
  .main-grid {
    display: grid;
    grid-template-columns: 230px 1fr 210px;
    gap: 14px;
    padding: 14px 20px;
    flex: 1;
    overflow: hidden;
  }

  .card {
    background: var(--surface);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow-sm);
    padding: 16px;
  }

  /* ── LEFT PANEL ── */
  .left-panel { display: flex; flex-direction: column; gap: 12px; overflow: hidden; }

  .challenge-illus {
    background: linear-gradient(145deg, #e8f5e9 0%, #c8e6c9 60%, #a5d6a7 100%);
    border-radius: var(--radius-md);
    height: 120px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    position: relative;
    flex-shrink: 0;
  }
  .challenge-illus svg { width: 190px; height: 110px; }

  .challenge-badge {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    background: var(--green-bg);
    color: var(--green-main);
    font-size: 10.5px;
    font-weight: 600;
    padding: 3px 8px;
    border-radius: 20px;
    margin-bottom: 6px;
  }
  .challenge-title {
    font-size: 13.5px;
    font-weight: 700;
    color: var(--text-primary);
    line-height: 1.3;
    margin-bottom: 2px;
  }
  .challenge-sub { font-size: 11px; color: var(--text-muted); margin-bottom: 10px; }

  .progress-list { display: flex; flex-direction: column; gap: 9px; flex: 1; }
  .progress-item {}
  .pi-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 3px; }
  .pi-name { font-size: 11.5px; color: var(--text-primary); font-weight: 500; }
  .pi-meta { display: flex; gap: 8px; }
  .pi-time { font-size: 11px; color: var(--text-secondary); }
  .pi-count {
    font-size: 10px; color: var(--green-main);
    background: var(--green-bg);
    padding: 1px 6px; border-radius: 10px; font-weight: 600;
  }
  .prog-track { height: 5px; background: #e8f0eb; border-radius: 99px; overflow: hidden; }
  .prog-fill { height: 100%; border-radius: 99px; transition: width 0.6s ease; }

  .btn-join {
    width: 100%;
    padding: 11px;
    background: var(--green-dark);
    color: #fff;
    border: none;
    border-radius: var(--radius-md);
    font-size: 13.5px;
    font-weight: 600;
    cursor: pointer;
    font-family: inherit;
    letter-spacing: 0.3px;
    transition: background 0.15s, transform 0.1s;
    flex-shrink: 0;
  }
  .btn-join:hover { background: var(--green-main); }
  .btn-join:active { transform: scale(0.98); }

  /* ── CENTER PANEL ── */
  .center-panel { display: flex; flex-direction: column; gap: 12px; }

  .panel-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .panel-title { font-size: 15px; font-weight: 700; color: var(--text-primary); }
  .more-btn {
    width: 28px; height: 28px;
    border-radius: 8px;
    border: none; background: transparent;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; color: var(--text-muted);
    transition: background 0.15s;
  }
  .more-btn:hover { background: var(--bg); }

  .donut-area {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    gap: 10px;
    align-items: center;
  }
  .mini-cards-col { display: flex; flex-direction: column; gap: 8px; }

  .mini-card {
    border-radius: var(--radius-md);
    padding: 10px 12px;
    display: flex;
    align-items: center;
    gap: 9px;
    cursor: pointer;
    transition: filter 0.15s;
  }
  .mini-card:hover { filter: brightness(0.97); }
  .mc-blue { background: var(--blue-soft); }
  .mc-orange { background: var(--orange-soft); }
  .mc-purple { background: var(--purple-soft); }
  .mc-teal { background: var(--teal-soft); }

  .mc-icon {
    width: 32px; height: 32px;
    border-radius: 9px;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .mc-icon.blue { background: var(--blue-icon); }
  .mc-icon.orange { background: var(--orange-icon); }
  .mc-icon.purple { background: var(--purple-icon); }
  .mc-icon.teal { background: var(--teal-icon); }
  .mc-icon svg { width: 16px; height: 16px; }

  .mc-info {}
  .mc-label { font-size: 11px; font-weight: 600; color: var(--text-primary); margin-bottom: 1px; }
  .mc-time { font-size: 12px; color: #666; }
  .mc-link { font-size: 10px; color: var(--text-muted); cursor: pointer; margin-top: 1px; }
  .mc-link:hover { color: var(--green-main); }

  .donut-wrap {
    position: relative;
    width: 175px; height: 175px;
    flex-shrink: 0;
  }
  #donutChart { width: 175px !important; height: 175px !important; }
  .donut-label {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    pointer-events: none;
  }
  .donut-total-sm { font-size: 11px; color: var(--text-muted); margin-bottom: 1px; }
  .donut-total { font-size: 16px; font-weight: 700; color: var(--text-primary); line-height: 1.15; }
  .donut-detail { font-size: 10px; color: var(--text-muted); margin-top: 3px; line-height: 1.5; }

  .goal-section {}
  .goal-meta {
    display: flex; justify-content: space-between;
    font-size: 12px; color: var(--text-secondary);
    margin-bottom: 6px;
  }
  .goal-pct { font-weight: 700; color: var(--green-main); }
  .goal-track { height: 9px; background: #e0ede6; border-radius: 99px; overflow: hidden; }
  .goal-fill {
    height: 100%;
    border-radius: 99px;
    background: linear-gradient(90deg, var(--green-main), var(--green-pale));
    transition: width 0.8s ease;
  }

  /* ── RIGHT PANEL ── */
  .right-col { display: flex; flex-direction: column; gap: 14px; overflow: hidden; }

  .section-title { font-size: 13px; font-weight: 700; color: var(--text-primary); margin-bottom: 2px; }
  .section-sub { font-size: 11px; color: var(--text-muted); margin-bottom: 10px; }

  .app-list { display: flex; flex-direction: column; }
  .app-item {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 7px 0;
    border-bottom: 1px solid var(--border);
  }
  .app-item:last-child { border-bottom: none; padding-bottom: 0; }
  .app-icon {
    width: 24px; height: 24px;
    border-radius: 7px;
    display: flex; align-items: center; justify-content: center;
    font-size: 11px; font-weight: 700;
    flex-shrink: 0;
    overflow: hidden;
  }
  .app-name { font-size: 12px; color: var(--text-primary); font-weight: 500; flex: 1; }
  .app-time { font-size: 11px; color: var(--text-secondary); min-width: 44px; text-align: right; margin-right: 6px; }
  .mini-bar-track { width: 44px; height: 5px; background: #e0ede6; border-radius: 99px; overflow: hidden; flex-shrink: 0; }
  .mini-bar-fill { height: 100%; border-radius: 99px; }

  .bar-chart-wrap { position: relative; width: 100%; height: 140px; }

  /* ── FOOTER ── */
  footer {
    background: var(--surface);
    border-top: 1px solid var(--border);
    padding: 0 28px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
  }
  .footer-links { display: flex; gap: 16px; }
  .footer-links a { font-size: 11.5px; color: var(--text-muted); text-decoration: none; }
  .footer-links a:hover { color: var(--green-main); }
  .footer-time { font-size: 11.5px; color: var(--text-muted); }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--green-pale); border-radius: 99px; }
</style>
</head>
<body>
<div class="app">

  <!-- HEADER -->
  <header>
    <a href="#" class="logo">
      <div class="logo-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
          <rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8M12 17v4"/>
          <path d="M7 8l3 3 2-2 3 3" stroke-width="2"/>
        </svg>
      </div>
      <span class="logo-text">Digital Balance Hub</span>
    </a>

    <nav>
      <div class="nav-item active">대시보드</div>
      <div class="nav-item">보고서</div>
      <div class="nav-item">목표</div>
      <div class="nav-item">챌린지</div>
      <div class="nav-item">설정</div>
    </nav>

    <div class="user-area">
      <div class="avatar">지윤</div>
      <div class="user-info">
        <div class="user-name">지윤</div>
        <div class="user-level">Lv.12</div>
      </div>
      <div class="badge" title="왕관 뱃지">👑</div>
      <button class="bell-btn" aria-label="알림">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/>
        </svg>
      </button>
    </div>
  </header>

  <!-- MAIN -->
  <div class="main-grid">

    <!-- LEFT: 오늘의 챌린지 -->
    <div class="card left-panel">
      <div class="challenge-illus">
        <svg viewBox="0 0 190 110" xmlns="http://www.w3.org/2000/svg">
          <!-- sky blobs -->
          <ellipse cx="30" cy="25" rx="22" ry="16" fill="white" opacity="0.55"/>
          <ellipse cx="50" cy="20" rx="18" ry="12" fill="white" opacity="0.45"/>
          <ellipse cx="155" cy="30" rx="20" ry="14" fill="white" opacity="0.5"/>
          <ellipse cx="170" cy="26" rx="14" ry="10" fill="white" opacity="0.4"/>
          <!-- tightrope -->
          <line x1="8" y1="72" x2="182" y2="64" stroke="#6ab98a" stroke-width="2.5" stroke-linecap="round"/>
          <!-- stick figure walking -->
          <!-- head -->
          <circle cx="95" cy="42" r="8" fill="#4a7c59"/>
          <!-- body -->
          <line x1="95" y1="50" x2="95" y2="68" stroke="#4a7c59" stroke-width="2.8" stroke-linecap="round"/>
          <!-- balance pole -->
          <line x1="62" y1="61" x2="128" y2="59" stroke="#4a7c59" stroke-width="2.2" stroke-linecap="round"/>
          <!-- arms -->
          <line x1="95" y1="56" x2="68" y2="62" stroke="#4a7c59" stroke-width="2.2" stroke-linecap="round"/>
          <line x1="95" y1="56" x2="122" y2="60" stroke="#4a7c59" stroke-width="2.2" stroke-linecap="round"/>
          <!-- legs -->
          <line x1="95" y1="68" x2="87" y2="82" stroke="#4a7c59" stroke-width="2.2" stroke-linecap="round"/>
          <line x1="95" y1="68" x2="103" y2="80" stroke="#4a7c59" stroke-width="2.2" stroke-linecap="round"/>
          <!-- foot on rope indicator -->
          <circle cx="95" cy="68" r="2.5" fill="#6ab98a" opacity="0.7"/>
          <!-- laptop (left) -->
          <rect x="18" y="50" width="20" height="14" rx="2.5" fill="#b5d5ff" opacity="0.75"/>
          <rect x="20" y="53" width="16" height="8" rx="1" fill="#82b4f0" opacity="0.7"/>
          <rect x="15" y="64" width="26" height="2.5" rx="1.5" fill="#9ec7f8" opacity="0.6"/>
          <!-- smartphone (right) -->
          <rect x="152" y="55" width="14" height="22" rx="3" fill="#ffd5b8" opacity="0.75"/>
          <rect x="154" y="59" width="10" height="12" rx="1" fill="#ffb380" opacity="0.7"/>
          <circle cx="159" cy="74" r="1.5" fill="#ff9d6e" opacity="0.7"/>
        </svg>
      </div>

      <div>
        <div class="challenge-badge">
          <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><path d="M12 2l2.4 7.4H22l-6.2 4.5 2.4 7.4L12 17l-6.2 4.3 2.4-7.4L2 9.4h7.6z"/></svg>
          오늘의 챌린지
        </div>
        <div class="challenge-title">하루 2시간 미만 소셜 미디어</div>
        <div class="challenge-sub">알똥하는 진정의 챌린지</div>
      </div>

      <div class="progress-list">
        <div class="progress-item">
          <div class="pi-row">
            <span class="pi-name">하루 2시간 미만 소셜 미디어</span>
          </div>
          <div class="pi-row" style="margin-bottom:4px;">
            <span class="pi-time">1간 30분</span>
            <span class="pi-count">1일 9명</span>
          </div>
          <div class="prog-track">
            <div class="prog-fill" style="width:75%;background:linear-gradient(90deg,#40916c,#52b788);"></div>
          </div>
        </div>
        <div class="progress-item">
          <div class="pi-row">
            <span class="pi-name">하루 1시간 생산성 증대</span>
          </div>
          <div class="pi-row" style="margin-bottom:4px;">
            <span class="pi-time"></span>
            <span class="pi-count">1일 9명</span>
          </div>
          <div class="prog-track">
            <div class="prog-fill" style="width:55%;background:linear-gradient(90deg,#52b788,#74c69d);"></div>
          </div>
        </div>
        <div class="progress-item">
          <div class="pi-row">
            <span class="pi-name">하루 2시간 미만 쿨링 라지</span>
          </div>
          <div class="pi-row" style="margin-bottom:4px;">
            <span class="pi-time"></span>
            <span class="pi-count">1일 9명</span>
          </div>
          <div class="prog-track">
            <div class="prog-fill" style="width:38%;background:linear-gradient(90deg,#74c69d,#95d5b2);"></div>
          </div>
        </div>
      </div>

      <button class="btn-join">도전 참가하기</button>
    </div>

    <!-- CENTER: 오늘의 디지털 밸런스 -->
    <div class="card center-panel">
      <div class="panel-header">
        <span class="panel-title">오늘의 디지털 밸런스</span>
        <button class="more-btn" aria-label="더보기">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
            <circle cx="12" cy="5" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="12" cy="19" r="2"/>
          </svg>
        </button>
      </div>

      <div class="donut-area">
        <!-- Left mini cards -->
        <div class="mini-cards-col">
          <div class="mini-card mc-blue">
            <div class="mc-icon blue">
              <svg viewBox="0 0 24 24" fill="none" stroke="#2563eb" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="5" y="2" width="14" height="20" rx="2"/><line x1="12" y1="18" x2="12.01" y2="18" stroke-width="2.5"/>
              </svg>
            </div>
            <div class="mc-info">
              <div class="mc-label">소셜 미디어</div>
              <div class="mc-time">1시간 30분</div>
              <div class="mc-link">상세히 보기 ›</div>
            </div>
          </div>
          <div class="mini-card mc-purple">
            <div class="mc-icon purple">
              <svg viewBox="0 0 24 24" fill="none" stroke="#7c3aed" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <polygon points="5,3 19,12 5,21"/></svg>
            </div>
            <div class="mc-info">
              <div class="mc-label">엔터테인먼트</div>
              <div class="mc-time">1간 6분</div>
              <div class="mc-link">자세히 보기 ›</div>
            </div>
          </div>
        </div>

        <!-- Donut -->
        <div class="donut-wrap">
          <canvas id="donutChart" role="img" aria-label="도넛 차트: PC 4시간, 소셜 미디어 1시간 30분, 엔터테인먼트 1시간 6분, 기타 54분"></canvas>
          <div class="donut-label">
            <div class="donut-total-sm">Total</div>
            <div class="donut-total">6시간<br>30분</div>
            <div class="donut-detail">PC: 4시간<br>Mobile: 2시간 30분</div>
          </div>
        </div>

        <!-- Right mini cards -->
        <div class="mini-cards-col">
          <div class="mini-card mc-orange">
            <div class="mc-icon orange">
              <svg viewBox="0 0 24 24" fill="none" stroke="#d97706" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="4" width="20" height="14" rx="2"/><path d="M8 21h8M12 18v3"/>
              </svg>
            </div>
            <div class="mc-info">
              <div class="mc-label">PC</div>
              <div class="mc-time">4시간 30분</div>
              <div class="mc-link">상세 보기 ›</div>
            </div>
          </div>
          <div class="mini-card mc-teal">
            <div class="mc-icon teal">
              <svg viewBox="0 0 24 24" fill="none" stroke="#059669" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
              </svg>
            </div>
            <div class="mc-info">
              <div class="mc-label">기타</div>
              <div class="mc-time">1시간 30분</div>
              <div class="mc-link">자세히 보기 ›</div>
            </div>
          </div>
        </div>
      </div>

      <div class="goal-section">
        <div class="goal-meta">
          <span>오늘의 목표: 8시간</span>
          <span>진행률 <span class="goal-pct">81%</span></span>
        </div>
        <div class="goal-track">
          <div class="goal-fill" style="width:81%;"></div>
        </div>
      </div>
    </div>

    <!-- RIGHT COL -->
    <div class="right-col">
      <!-- Top: 앱 & 사이트 -->
      <div class="card" style="flex:1;overflow:hidden;display:flex;flex-direction:column;">
        <div class="section-title">가장 자주 사용한 앱 &amp; 사이트</div>
        <div class="app-list" style="flex:1;">
          <div class="app-item">
            <div class="app-icon" style="background:#ff3333;">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="white"><path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-2.88 2.5 2.89 2.89 0 0 1-2.89-2.89 2.89 2.89 0 0 1 2.89-2.89c.28 0 .54.04.79.1V9.01a6.33 6.33 0 0 0-.79-.05 6.34 6.34 0 0 0-6.34 6.34 6.34 6.34 0 0 0 6.34 6.34 6.34 6.34 0 0 0 6.33-6.34V8.69a8.25 8.25 0 0 0 4.84 1.56V6.79a4.85 4.85 0 0 1-1.07-.1z"/></svg>
            </div>
            <span class="app-name">Youtube</span>
            <span class="app-time">1시간 45분</span>
            <div class="mini-bar-track"><div class="mini-bar-fill" style="width:90%;background:#ff3333;"></div></div>
          </div>
          <div class="app-item">
            <div class="app-icon" style="background:linear-gradient(135deg,#f09433 0%,#e6683c 25%,#dc2743 50%,#cc2366 75%,#bc1888 100%);">
              <svg width="13" height="13" viewBox="0 0 24 24" fill="white"><rect x="2" y="2" width="20" height="20" rx="5"/><circle cx="12" cy="12" r="4" fill="none" stroke="white" stroke-width="2"/><circle cx="17.5" cy="6.5" r="1.2" fill="white"/></svg>
            </div>
            <span class="app-name">Instagram</span>
            <span class="app-time">1시간 30분</span>
            <div class="mini-bar-track"><div class="mini-bar-fill" style="width:77%;background:#e1306c;"></div></div>
          </div>
          <div class="app-item">
            <div class="app-icon" style="background:#4a154b;color:#fff;font-size:13px;font-weight:800;">#</div>
            <span class="app-name">Slack</span>
            <span class="app-time">45분</span>
            <div class="mini-bar-track"><div class="mini-bar-fill" style="width:38%;background:#4a154b;"></div></div>
          </div>
          <div class="app-item">
            <div class="app-icon" style="background:#000;color:#fff;font-size:12px;font-weight:800;letter-spacing:-1px;">N</div>
            <span class="app-name">Notion</span>
            <span class="app-time">35분</span>
            <div class="mini-bar-track"><div class="mini-bar-fill" style="width:30%;background:#444;"></div></div>
          </div>
          <div class="app-item">
            <div class="app-icon" style="background:#fff;border:1px solid #eee;overflow:hidden;">
              <svg width="16" height="16" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" fill="#4285f4"/><path d="M2 12h20M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z" fill="none" stroke="white" stroke-width="1.5"/><path d="M2.68 9h18.64M2.68 15h18.64" stroke="white" stroke-width="1.3"/></svg>
            </div>
            <span class="app-name">Chrome</span>
            <span class="app-time">30분</span>
            <div class="mini-bar-track"><div class="mini-bar-fill" style="width:25%;background:#4285f4;"></div></div>
          </div>
        </div>
      </div>

      <!-- Bottom: 장치별 사용 분석 -->
      <div class="card" style="flex:0 0 auto;">
        <div class="panel-header" style="margin-bottom:2px;">
          <span class="section-title">장치별 사용 분석</span>
          <button class="more-btn" aria-label="더보기">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
              <circle cx="12" cy="5" r="2"/><circle cx="12" cy="12" r="2"/><circle cx="12" cy="19" r="2"/>
            </svg>
          </button>
        </div>
        <div class="section-sub">장치별 사용한 vs 사용 분석</div>
        <div class="bar-chart-wrap">
          <canvas id="barChart" role="img" aria-label="PC 와 Mobile 사용 시간 비교 막대 차트"></canvas>
        </div>
      </div>
    </div>

  </div><!-- end main-grid -->

  <!-- FOOTER -->
  <footer>
    <div class="footer-links">
      <a href="#">도움말</a>
      <a href="#">이용 약관</a>
    </div>
    <div class="footer-time" id="footerTime">16:36 / 02:12:30</div>
  </footer>

</div><!-- end app -->

<script>
/* ── Clock ── */
function updateTime() {
  const now = new Date();
  const hh = String(now.getHours()).padStart(2,'0');
  const mm = String(now.getMinutes()).padStart(2,'0');
  document.getElementById('footerTime').textContent =
    hh + ':' + mm + ' / 02:12:30';
}
updateTime();
setInterval(updateTime, 60000);

/* ── Nav tabs ── */
document.querySelectorAll('.nav-item').forEach(item => {
  item.addEventListener('click', () => {
    document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
    item.classList.add('active');
  });
});

/* ── Donut Chart ── */
new Chart(document.getElementById('donutChart'), {
  type: 'doughnut',
  data: {
    labels: ['소셜 미디어', 'PC', '엔터테인먼트', '기타'],
    datasets: [{
      data: [90, 240, 66, 54],
      backgroundColor: ['#82B4F0', '#FFB380', '#C4B5FD', '#6EE7B7'],
      borderColor: '#ffffff',
      borderWidth: 3,
      hoverOffset: 6
    }]
  },
  options: {
    responsive: false,
    cutout: '64%',
    plugins: {
      legend: { display: false },
      tooltip: {
        callbacks: {
          label: (ctx) => {
            const v = ctx.raw;
            const h = Math.floor(v / 60);
            const m = v % 60;
            return ctx.label + ': ' + (h > 0 ? h + '시간 ' : '') + (m > 0 ? m + '분' : '');
          }
        }
      }
    },
    animation: { animateRotate: true, duration: 900 }
  }
});

/* ── Bar Chart ── */
new Chart(document.getElementById('barChart'), {
  type: 'bar',
  data: {
    labels: ['PC', 'Mobile', 'PC', 'Mobile'],
    datasets: [{
      label: '사용 시간(분)',
      data: [120, 80, 90, 60],
      backgroundColor: ['#82B4F0', '#6EE7B7', '#82B4F0', '#6EE7B7'],
      borderRadius: 5,
      borderWidth: 0,
      barPercentage: 0.65
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
      legend: { display: false },
      tooltip: {
        callbacks: { label: (c) => c.raw + '분' }
      }
    },
    scales: {
      x: {
        ticks: { font: { size: 10, family: 'Noto Sans KR' }, color: '#8aab97' },
        grid: { display: false },
        border: { display: false }
      },
      y: {
        min: 0, max: 130,
        ticks: {
          font: { size: 10 }, color: '#8aab97',
          stepSize: 40,
          callback: (v) => v
        },
        grid: { color: 'rgba(0,0,0,0.05)', drawTicks: false },
        border: { display: false }
      }
    },
    animation: { duration: 800 }
  }
});
</script>
</body>
</html>
