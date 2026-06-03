<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BOT FIGHT GAIN – JEAN TRADER</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&family=Exo+2:wght@300;400;600&display=swap');

  :root {
    --bg: #020b18;
    --panel: #041525;
    --panel2: #061e35;
    --border: #0a4a7a;
    --cyan: #00e5ff;
    --blue: #1565c0;
    --blue2: #42a5f5;
    --green: #00e676;
    --red: #ff1744;
    --yellow: #ffea00;
    --orange: #ff6d00;
    --text: #b0bec5;
    --glow: 0 0 12px #00e5ff88;
    --glow-green: 0 0 10px #00e67688;
    --glow-red: 0 0 10px #ff174488;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--bg);
    font-family: 'Exo 2', sans-serif;
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
    background-image:
      radial-gradient(ellipse at 20% 20%, #0a2a4a55 0%, transparent 60%),
      radial-gradient(ellipse at 80% 80%, #001a3355 0%, transparent 60%),
      repeating-linear-gradient(0deg, transparent, transparent 39px, #0a2a4a22 40px),
      repeating-linear-gradient(90deg, transparent, transparent 39px, #0a2a4a22 40px);
  }

  /* ── HEADER ── */
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 20px;
    background: linear-gradient(90deg, #020b18, #041e38, #020b18);
    border-bottom: 2px solid var(--border);
    box-shadow: 0 0 20px #00e5ff33;
  }
  .logo {
    font-family: 'Orbitron', monospace;
    font-size: 1.1rem;
    font-weight: 900;
    color: var(--cyan);
    text-shadow: var(--glow);
    letter-spacing: 2px;
    line-height: 1.2;
  }
  .logo span { color: var(--yellow); }
  .header-status {
    display: flex;
    align-items: center;
    gap: 14px;
  }
  .badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.72rem;
    padding: 3px 10px;
    border-radius: 3px;
    border: 1px solid;
    letter-spacing: 1px;
  }
  .badge.active { color: var(--green); border-color: var(--green); box-shadow: var(--glow-green); }
  .badge.inactive { color: var(--red); border-color: var(--red); }

  #btn-toggle {
    font-family: 'Orbitron', monospace;
    font-size: 0.85rem;
    font-weight: 700;
    padding: 6px 22px;
    border: 2px solid var(--green);
    background: transparent;
    color: var(--green);
    cursor: pointer;
    border-radius: 3px;
    letter-spacing: 2px;
    transition: all .2s;
    box-shadow: var(--glow-green);
  }
  #btn-toggle.off { border-color: var(--red); color: var(--red); box-shadow: var(--glow-red); }
  #btn-toggle:hover { background: #00e67622; }

  /* ── LAYOUT ── */
  .main-grid {
    display: grid;
    grid-template-columns: 320px 1fr 280px;
    gap: 10px;
    padding: 10px;
    height: calc(100vh - 60px);
  }

  /* ── PANELS ── */
  .panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }
  .panel-title {
    font-family: 'Orbitron', monospace;
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 2px;
    padding: 6px 12px;
    background: linear-gradient(90deg, var(--panel2), transparent);
    border-bottom: 1px solid var(--border);
    color: var(--cyan);
    text-shadow: var(--glow);
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .panel-title::before {
    content: '';
    display: inline-block;
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--cyan);
    box-shadow: var(--glow);
    flex-shrink: 0;
  }
  .panel-body { padding: 10px; flex: 1; overflow-y: auto; }

  /* ── STATS GRID ── */
  .stat-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 5px 0;
    border-bottom: 1px solid #0a2a4a55;
    font-size: 0.78rem;
  }
  .stat-label { color: #546e7a; font-family: 'Share Tech Mono', monospace; font-size: 0.7rem; }
  .stat-value { font-family: 'Share Tech Mono', monospace; color: var(--cyan); }
  .stat-value.red { color: var(--red); }
  .stat-value.green { color: var(--green); }
  .stat-value.yellow { color: var(--yellow); }

  /* ── EVENS/ODDS DISPLAY ── */
  .eo-display {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    padding: 14px 10px 8px;
    font-family: 'Orbitron', monospace;
  }
  .eo-box {
    flex: 1;
    text-align: center;
    padding: 10px 6px;
    border: 1px solid var(--border);
    border-radius: 4px;
    background: var(--panel2);
  }
  .eo-label { font-size: 0.6rem; letter-spacing: 2px; color: #546e7a; margin-bottom: 4px; }
  .eo-pct {
    font-size: 2.2rem;
    font-weight: 900;
    text-shadow: var(--glow);
    color: var(--cyan);
    line-height: 1;
  }
  .eo-pct.dominant { color: var(--yellow); text-shadow: 0 0 12px #ffea0088; }
  .eo-sep { font-size: 1.5rem; color: #546e7a; font-weight: 900; }

  /* ── BAR ── */
  .bar-wrap { padding: 0 10px 10px; }
  .bar-track {
    height: 8px;
    background: #0a2a4a;
    border-radius: 4px;
    overflow: hidden;
    border: 1px solid var(--border);
    position: relative;
  }
  .bar-fill {
    height: 100%;
    border-radius: 4px;
    transition: width .6s ease;
    background: linear-gradient(90deg, var(--blue), var(--cyan));
    box-shadow: var(--glow);
    position: absolute; left: 0; top: 0;
  }

  /* ── DIGIT FREQ CHART ── */
  .freq-chart {
    display: flex;
    align-items: flex-end;
    gap: 3px;
    height: 80px;
    padding: 0 4px;
    margin-top: 6px;
  }
  .freq-bar-wrap {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
    height: 100%;
    justify-content: flex-end;
  }
  .freq-bar {
    width: 100%;
    border-radius: 2px 2px 0 0;
    transition: height .5s ease;
    min-height: 2px;
  }
  .freq-bar.par { background: linear-gradient(180deg, var(--blue2), var(--blue)); }
  .freq-bar.impar { background: linear-gradient(180deg, #ab47bc, #6a1b9a); }
  .freq-bar.dominant-bar { box-shadow: 0 0 8px #ffea00aa; background: linear-gradient(180deg, var(--yellow), var(--orange)); }
  .freq-lbl { font-family: 'Share Tech Mono', monospace; font-size: 0.6rem; color: #546e7a; }
  .freq-pct { font-family: 'Share Tech Mono', monospace; font-size: 0.55rem; color: #546e7a; }

  /* ── SIGNAL BOX ── */
  .signal-box {
    margin: 10px;
    border: 2px solid var(--border);
    border-radius: 4px;
    padding: 12px;
    text-align: center;
    background: var(--panel2);
    position: relative;
    overflow: hidden;
  }
  .signal-box::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, transparent 40%, #00e5ff08);
    pointer-events: none;
  }
  .signal-label {
    font-family: 'Orbitron', monospace;
    font-size: 0.6rem;
    letter-spacing: 3px;
    color: #546e7a;
    margin-bottom: 6px;
  }
  .signal-value {
    font-family: 'Orbitron', monospace;
    font-size: 1.4rem;
    font-weight: 900;
    letter-spacing: 3px;
  }
  .signal-value.par { color: var(--blue2); text-shadow: 0 0 12px #42a5f588; }
  .signal-value.impar { color: #ab47bc; text-shadow: 0 0 12px #ab47bc88; }
  .signal-value.aguardando { color: #546e7a; font-size: 0.9rem; }
  .signal-sub {
    font-size: 0.65rem;
    color: #546e7a;
    margin-top: 4px;
    font-family: 'Share Tech Mono', monospace;
  }

  /* ── CONDITIONS ── */
  .cond-list { display: flex; flex-direction: column; gap: 5px; }
  .cond-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 0.73rem;
    padding: 5px 8px;
    border-radius: 3px;
    border: 1px solid transparent;
    background: #020b18;
    font-family: 'Share Tech Mono', monospace;
  }
  .cond-item.ok { border-color: #00e67644; color: var(--green); }
  .cond-item.fail { border-color: #ff174444; color: var(--red); }
  .cond-item.wait { border-color: #ffea0044; color: var(--yellow); }
  .cond-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .cond-item.ok .cond-dot { background: var(--green); box-shadow: var(--glow-green); }
  .cond-item.fail .cond-dot { background: var(--red); box-shadow: var(--glow-red); }
  .cond-item.wait .cond-dot { background: var(--yellow); }

  /* ── LAST DIGITS ── */
  .digit-strip {
    display: flex;
    flex-wrap: wrap;
    gap: 4px;
    padding: 8px 10px;
  }
  .dig {
    width: 28px; height: 28px;
    border-radius: 3px;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Orbitron', monospace;
    font-size: 0.8rem;
    font-weight: 700;
    border: 1px solid;
    transition: all .3s;
  }
  .dig.par { color: var(--blue2); border-color: var(--blue2); background: #1565c022; }
  .dig.impar { color: #ab47bc; border-color: #ab47bc; background: #6a1b9a22; }
  .dig.new { animation: flashDig .4s ease; }
  @keyframes flashDig { 0%{transform:scale(1.3);box-shadow:0 0 14px var(--cyan);} 100%{transform:scale(1);} }

  /* ── CONFIG PANEL ── */
  .cfg-group { margin-bottom: 12px; }
  .cfg-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    color: #546e7a;
    letter-spacing: 1px;
    margin-bottom: 4px;
    display: block;
  }
  .cfg-input, .cfg-select {
    width: 100%;
    background: #020b18;
    border: 1px solid var(--border);
    color: var(--cyan);
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    padding: 6px 10px;
    border-radius: 3px;
    outline: none;
    transition: border-color .2s;
  }
  .cfg-input:focus, .cfg-select:focus { border-color: var(--cyan); box-shadow: var(--glow); }
  .cfg-select option { background: var(--panel); }

  .cfg-row { display: flex; gap: 8px; }
  .cfg-row .cfg-group { flex: 1; }

  /* ── TOGGLE SWITCH ── */
  .toggle-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 6px 0;
    border-bottom: 1px solid #0a2a4a55;
    font-size: 0.72rem;
    font-family: 'Share Tech Mono', monospace;
    color: #78909c;
  }
  .toggle-row label { cursor: pointer; }
  .switch { position: relative; display: inline-block; width: 36px; height: 18px; }
  .switch input { opacity: 0; width: 0; height: 0; }
  .slider {
    position: absolute; cursor: pointer;
    inset: 0; background: #0a2a4a;
    border-radius: 18px; border: 1px solid var(--border);
    transition: .3s;
  }
  .slider::before {
    content: ''; position: absolute;
    width: 12px; height: 12px; left: 3px; bottom: 2px;
    background: #546e7a; border-radius: 50%; transition: .3s;
  }
  input:checked + .slider { background: #00e67622; border-color: var(--green); }
  input:checked + .slider::before { background: var(--green); transform: translateX(16px); box-shadow: var(--glow-green); }

  /* ── HISTORY TABLE ── */
  .hist-table { width: 100%; border-collapse: collapse; font-size: 0.72rem; }
  .hist-table th {
    font-family: 'Orbitron', monospace;
    font-size: 0.55rem;
    letter-spacing: 1px;
    color: #546e7a;
    padding: 5px 8px;
    border-bottom: 1px solid var(--border);
    text-align: left;
    position: sticky; top: 0;
    background: var(--panel);
  }
  .hist-table td {
    padding: 5px 8px;
    border-bottom: 1px solid #0a2a4a44;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
  }
  .hist-table tr:hover td { background: #041e3544; }
  .pl-pos { color: var(--green); }
  .pl-neg { color: var(--red); }
  .type-even { color: var(--blue2); }
  .type-odd { color: #ab47bc; }

  /* ── ACTION BUTTONS ── */
  .btn-row { display: flex; gap: 8px; padding: 10px; }
  .btn {
    flex: 1;
    padding: 9px 4px;
    border-radius: 3px;
    border: 1px solid;
    font-family: 'Orbitron', monospace;
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 1px;
    cursor: pointer;
    transition: all .2s;
    background: transparent;
  }
  .btn:hover { filter: brightness(1.3); }
  .btn:active { transform: scale(.97); }
  .btn-compra { color: var(--green); border-color: var(--green); }
  .btn-compra:hover { background: #00e67622; box-shadow: var(--glow-green); }
  .btn-venda { color: var(--red); border-color: var(--red); }
  .btn-venda:hover { background: #ff174422; box-shadow: var(--glow-red); }
  .btn-cancel { color: var(--yellow); border-color: var(--yellow); }
  .btn-cancel:hover { background: #ffea0022; }
  .btn-zerar { color: var(--orange); border-color: var(--orange); }
  .btn-zerar:hover { background: #ff6d0022; }

  /* ── TOKEN INPUT ── */
  .token-wrap {
    padding: 10px;
    border-top: 1px solid var(--border);
    background: #020b18;
  }
  .token-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.6rem;
    color: #546e7a;
    margin-bottom: 4px;
  }
  .token-row { display: flex; gap: 6px; }
  .token-input {
    flex: 1;
    background: var(--panel);
    border: 1px solid var(--border);
    color: var(--cyan);
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.72rem;
    padding: 5px 8px;
    border-radius: 3px;
    outline: none;
  }
  .token-input:focus { border-color: var(--cyan); }
  .btn-connect {
    padding: 5px 14px;
    background: var(--blue);
    border: 1px solid var(--blue2);
    color: white;
    font-family: 'Orbitron', monospace;
    font-size: 0.6rem;
    font-weight: 700;
    letter-spacing: 1px;
    border-radius: 3px;
    cursor: pointer;
    transition: all .2s;
  }
  .btn-connect:hover { background: var(--blue2); }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--panel); }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

  /* ── TICKER ── */
  .ticker-row {
    display: flex;
    gap: 6px;
    padding: 4px 10px;
    border-top: 1px solid var(--border);
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    background: #020b18;
    flex-wrap: wrap;
  }
  .ticker-item { color: #546e7a; }
  .ticker-item span { color: var(--cyan); }
  .ticker-item.profit span { color: var(--green); }
  .ticker-item.loss span { color: var(--red); }

  /* ── PULSE ANIMATION ── */
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.4} }
  .pulse { animation: pulse 1.5s ease infinite; }

  /* ── STATUS LOG ── */
  .log-area {
    flex: 1;
    overflow-y: auto;
    padding: 6px 10px;
    display: flex;
    flex-direction: column;
    gap: 3px;
  }
  .log-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    padding: 3px 6px;
    border-left: 2px solid;
    border-radius: 0 2px 2px 0;
    animation: fadeIn .3s ease;
  }
  @keyframes fadeIn { from{opacity:0;transform:translateX(-6px)} to{opacity:1;transform:none} }
  .log-line.info { border-color: var(--cyan); color: #78909c; }
  .log-line.success { border-color: var(--green); color: var(--green); }
  .log-line.error { border-color: var(--red); color: var(--red); }
  .log-line.warn { border-color: var(--yellow); color: var(--yellow); }

  /* ── PIE MINI ── */
  .pie-wrap {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 8px 10px;
  }
  svg.pie { width: 60px; height: 60px; transform: rotate(-90deg); }
  .pie-legend { display: flex; flex-direction: column; gap: 4px; }
  .pie-leg-item { display: flex; align-items: center; gap: 5px; font-size: 0.65rem; font-family: 'Share Tech Mono', monospace; }
  .pie-dot { width: 8px; height: 8px; border-radius: 50%; }

  .middle-col { display: flex; flex-direction: column; gap: 10px; }

  .right-col { display: flex; flex-direction: column; gap: 10px; }

  .panel.log-panel { flex: 1; min-height: 0; }
  .panel.hist-panel { flex: 1; min-height: 0; }

  .section-divider {
    border: none;
    border-top: 1px solid var(--border);
    margin: 6px 0;
    opacity: .4;
  }

  .gale-display {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 5px 10px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.72rem;
    background: #020b18;
    border-top: 1px solid var(--border);
  }
  .gale-label { color: #546e7a; }
  .gale-value { color: var(--yellow); font-weight: 700; }

  .mode-indicator {
    padding: 4px 10px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    text-align: center;
    background: #020b18;
    border-top: 1px solid var(--border);
  }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <div class="logo">⚡ BOT FIGHT GAIN<br><span>JEAN TRADER</span> <span style="color:var(--text);font-size:.65rem;font-weight:400">v1.0</span></div>
  <div class="header-status">
    <div class="badge" id="conn-badge" style="color:var(--red);border-color:var(--red)">DESCONECTADO</div>
    <div class="badge" id="status-badge" style="color:#546e7a;border-color:#546e7a">AGUARDANDO</div>
    <button id="btn-toggle" class="off" onclick="toggleBot()">▶ INICIAR</button>
  </div>
</header>

<!-- MAIN GRID -->
<div class="main-grid">

  <!-- LEFT COLUMN -->
  <div style="display:flex;flex-direction:column;gap:10px;overflow:hidden">

    <!-- TOKEN / CONNECT -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">CONEXÃO DERIV</div>
      <div class="token-wrap">
        <div id="oauth-area">
          <button class="btn-connect" style="width:100%;padding:10px;font-size:0.75rem;background:linear-gradient(90deg,#1565c0,#0d47a1);border-color:#42a5f5;" onclick="startOAuth()">🔐 LOGIN DERIV (OAuth2)</button>
          <div style="font-family:Share Tech Mono,monospace;font-size:0.6rem;color:#546e7a;margin-top:5px;text-align:center;">Clique para autenticar com sua conta Deriv</div>
        </div>
        <div id="token-area" style="display:none">
          <div class="token-label">AUTENTICADO ✓</div>
          <div class="token-row">
            <span class="token-input" style="flex:1;display:flex;align-items:center;color:var(--green);font-size:0.7rem;" id="auth-status">Conectando...</span>
            <button class="btn-connect" style="background:#b71c1c;border-color:#ef5350;" onclick="logout()">SAIR</button>
          </div>
        </div>
      </div>
      <div class="ticker-row" id="ticker-row">
        <div class="ticker-item">ATIVO: <span id="t-ativo">–</span></div>
        <div class="ticker-item">CONTA: <span id="t-conta">–</span></div>
        <div class="ticker-item profit">SALDO: <span id="t-saldo">–</span></div>
        <div class="ticker-item loss">P&L: <span id="t-pl">R$ 0.00</span></div>
      </div>
    </div>

    <!-- CONFIG -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">CONFIGURAÇÕES</div>
      <div class="panel-body" style="overflow:visible">
        <div class="cfg-row">
          <div class="cfg-group">
            <span class="cfg-label">ATIVO</span>
            <select class="cfg-select" id="cfg-ativo">
              <option value="R_100" selected>R_100</option>
              <option value="R_50">R_50</option>
              <option value="R_75">R_75</option>
              <option value="R_25">R_25</option>
              <option value="R_10">R_10</option>
              <option value="1HZ100V">1HZ100V</option>
              <option value="1HZ50V">1HZ50V</option>
              <option value="1HZ75V">1HZ75V</option>
            </select>
          </div>
          <div class="cfg-group">
            <span class="cfg-label">TICKS ANÁLISE</span>
            <input class="cfg-input" id="cfg-ticks" type="number" value="50" min="20" max="200">
          </div>
        </div>
        <div class="cfg-row">
          <div class="cfg-group">
            <span class="cfg-label">ENTRADA (USD)</span>
            <input class="cfg-input" id="cfg-stake" type="number" value="0.35" min="0.35" step="0.01">
          </div>
          <div class="cfg-group">
            <span class="cfg-label">META DIÁRIA</span>
            <input class="cfg-input" id="cfg-meta" type="number" value="10" step="0.1">
          </div>
        </div>
        <div class="cfg-row">
          <div class="cfg-group">
            <span class="cfg-label">STOP LOSS</span>
            <input class="cfg-input" id="cfg-stop" type="number" value="20" step="0.1">
          </div>
          <div class="cfg-group">
            <span class="cfg-label">% DOMÍNIO MÍN.</span>
            <input class="cfg-input" id="cfg-pct" type="number" value="60" min="51" max="90">
          </div>
        </div>
        <hr class="section-divider">
        <div style="font-family:'Share Tech Mono',monospace;font-size:.65rem;color:#546e7a;margin-bottom:6px;letter-spacing:1px;">MARTINGALE</div>
        <div class="cfg-row">
          <div class="cfg-group">
            <span class="cfg-label">FATOR GALE</span>
            <input class="cfg-input" id="cfg-gale" type="number" value="2.0" min="1.1" max="5" step="0.1">
          </div>
          <div class="cfg-group">
            <span class="cfg-label">MÁX. GALES</span>
            <input class="cfg-input" id="cfg-max-gale" type="number" value="2" min="0" max="5">
          </div>
        </div>
        <hr class="section-divider">
        <div class="toggle-row">
          <label for="sw-postloss">Inverter após loss</label>
          <label class="switch"><input type="checkbox" id="sw-postloss" checked><span class="slider"></span></label>
        </div>
        <div class="toggle-row">
          <label for="sw-autoinvert">Inversão automática</label>
          <label class="switch"><input type="checkbox" id="sw-autoinvert"><span class="slider"></span></label>
        </div>
        <div class="toggle-row">
          <label for="sw-regra-geral">Regra % Geral</label>
          <label class="switch"><input type="checkbox" id="sw-regra-geral" checked><span class="slider"></span></label>
        </div>
        <div class="toggle-row">
          <label for="sw-regra-ind">Regra Contagem Dig.</label>
          <label class="switch"><input type="checkbox" id="sw-regra-ind" checked><span class="slider"></span></label>
        </div>
        <div class="toggle-row">
          <label for="sw-regra-ult">Últimos 2 no grupo</label>
          <label class="switch"><input type="checkbox" id="sw-regra-ult" checked><span class="slider"></span></label>
        </div>
      </div>
    </div>

    <!-- ACTION BUTTONS -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">CONTROLE MANUAL</div>
      <div class="btn-row">
        <button class="btn btn-compra" onclick="manualBuy('DIGITEVEN')">PAR</button>
        <button class="btn btn-venda" onclick="manualBuy('DIGITODD')">ÍMPAR</button>
        <button class="btn btn-cancel" onclick="cancelAll()">CANCELAR</button>
        <button class="btn btn-zerar" onclick="zerarTudo()">ZERAR</button>
      </div>
      <div class="gale-display">
        <span class="gale-label">GALE ATUAL:</span>
        <span class="gale-value" id="gale-display">G0 – Stake: <span id="gale-stake">$0.35</span></span>
      </div>
      <div class="mode-indicator" id="mode-indicator" style="color:#546e7a">MODO: AGUARDANDO SINAL</div>
    </div>
  </div>

  <!-- MIDDLE COLUMN -->
  <div class="middle-col">

    <!-- EVENS/ODDS -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">ANÁLISE PAR × ÍMPAR</div>
      <div class="eo-display">
        <div class="eo-box">
          <div class="eo-label">EVENS (PAR)</div>
          <div class="eo-pct" id="pct-par">–</div>
        </div>
        <div class="eo-sep">:</div>
        <div class="eo-box">
          <div class="eo-label">ODDS (ÍMPAR)</div>
          <div class="eo-pct" id="pct-impar">–</div>
        </div>
      </div>
      <div class="bar-wrap">
        <div class="bar-track"><div class="bar-fill" id="bar-fill" style="width:50%"></div></div>
      </div>
      <div class="pie-wrap">
        <svg class="pie" viewBox="0 0 36 36">
          <circle cx="18" cy="18" r="15.9" fill="none" stroke="#0a2a4a" stroke-width="3.5"/>
          <circle cx="18" cy="18" r="15.9" fill="none" stroke="#42a5f5" stroke-width="3.5"
            stroke-dasharray="50 100" id="pie-par" style="transition:stroke-dasharray .6s"/>
          <circle cx="18" cy="18" r="15.9" fill="none" stroke="#ab47bc" stroke-width="3.5"
            stroke-dasharray="50 100" stroke-dashoffset="-50" id="pie-impar" style="transition:all .6s"/>
        </svg>
        <div class="pie-legend">
          <div class="pie-leg-item"><div class="pie-dot" style="background:#42a5f5"></div> PAR</div>
          <div class="pie-leg-item"><div class="pie-dot" style="background:#ab47bc"></div> ÍMPAR</div>
        </div>
        <div style="flex:1"></div>
        <div style="text-align:right">
          <div style="font-family:'Share Tech Mono',monospace;font-size:.65rem;color:#546e7a">DIG. DOMINANTE</div>
          <div style="font-family:'Orbitron',monospace;font-size:1.6rem;font-weight:900;color:var(--yellow);text-shadow:0 0 12px #ffea0088" id="dig-dom">–</div>
          <div style="font-family:'Share Tech Mono',monospace;font-size:.6rem;color:#546e7a" id="dig-dom-freq">FREQ: –</div>
        </div>
      </div>

      <!-- FREQ CHART -->
      <div style="padding:0 10px 4px;font-family:'Share Tech Mono',monospace;font-size:.6rem;color:#546e7a;letter-spacing:1px">FREQUÊNCIA POR DÍGITO</div>
      <div class="freq-chart" id="freq-chart">
        <!-- bars injected by JS -->
      </div>
      <div style="display:flex;gap:3px;padding:2px 14px 8px;justify-content:space-around">
        <span id="fc-lbl" style="display:flex;gap:14px;width:100%;justify-content:space-around"></span>
      </div>
    </div>

    <!-- CONDITIONS -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">CONDIÇÕES DE ENTRADA</div>
      <div class="panel-body">
        <div class="cond-list" id="cond-list">
          <div class="cond-item wait"><div class="cond-dot"></div>% Domínio > 60% – aguardando</div>
          <div class="cond-item wait"><div class="cond-dot"></div>Dígito dominante no grupo – aguardando</div>
          <div class="cond-item wait"><div class="cond-dot"></div>Últimos 2 ticks no grupo – aguardando</div>
        </div>
      </div>
    </div>

    <!-- SIGNAL -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">SINAL ATUAL</div>
      <div class="signal-box" id="signal-box">
        <div class="signal-label">ENTRADA RECOMENDADA</div>
        <div class="signal-value aguardando" id="signal-val">AGUARDANDO</div>
        <div class="signal-sub" id="signal-sub">Coletando dados...</div>
      </div>
      <!-- LAST DIGITS -->
      <div style="padding:4px 10px 2px;font-family:'Share Tech Mono',monospace;font-size:.6rem;color:#546e7a;letter-spacing:1px">ÚLTIMOS DÍGITOS</div>
      <div class="digit-strip" id="digit-strip"></div>
    </div>

    <!-- PL STATS -->
    <div class="panel" style="flex-shrink:0">
      <div class="panel-title">RESULTADO</div>
      <div class="panel-body">
        <div class="stat-row"><span class="stat-label">HOJE</span><span class="stat-value" id="stat-dia">0/0 (0%)</span></div>
        <div class="stat-row"><span class="stat-label">P&L DIA</span><span class="stat-value" id="stat-pl-dia">$0.00</span></div>
        <div class="stat-row"><span class="stat-label">TOTAL</span><span class="stat-value" id="stat-total">0/0 (0%)</span></div>
        <div class="stat-row"><span class="stat-label">P&L TOTAL</span><span class="stat-value" id="stat-pl-total">$0.00</span></div>
        <div class="stat-row"><span class="stat-label">MAX DD</span><span class="stat-value red" id="stat-dd">$0.00</span></div>
        <div class="stat-row"><span class="stat-label">STAKE ATUAL</span><span class="stat-value yellow" id="stat-stake">$0.35</span></div>
      </div>
    </div>
  </div>

  <!-- RIGHT COLUMN -->
  <div class="right-col">

    <!-- LOG -->
    <div class="panel log-panel">
      <div class="panel-title">LOG DE OPERAÇÕES</div>
      <div class="log-area" id="log-area"></div>
    </div>

    <!-- HISTORY -->
    <div class="panel hist-panel">
      <div class="panel-title">HISTÓRICO</div>
      <div style="flex:1;overflow-y:auto">
        <table class="hist-table">
          <thead>
            <tr>
              <th>TIPO</th>
              <th>PREÇO</th>
              <th>L/P</th>
              <th>MSG</th>
            </tr>
          </thead>
          <tbody id="hist-body"></tbody>
        </table>
      </div>
    </div>
  </div>

</div>

<script>
// ──────────────────────────────────────────────
// STATE
// ──────────────────────────────────────────────
const state = {
  ws: null,
  connected: false,
  botActive: false,
  digits: [],
  balance: 0,
  currency: 'USD',
  loginId: '',
  lastContractId: null,

  // P&L
  plDay: 0,
  plTotal: 0,
  maxDD: 0,
  winsDay: 0, lossDay: 0,
  winsTotal: 0, lossTotal: 0,

  // Gale
  baseStake: 0.35,
  currentStake: 0.35,
  galeLevel: 0,
  lastLoss: false,

  // Post-loss state machine
  postLossMode: false, // waiting for trigger sequence
  postLossStep: 0,     // 0=wait contrario, 1=wait favor
  lastDirection: null, // 'par' or 'impar'
  pendingBuy: false,

  // Trade tracking
  awaitingResult: false,
  currentContractType: null,
  currentProposal: null,
  reqIdCounter: 1,
};

// ──────────────────────────────────────────────
// Verifica callback OAuth ao carregar página
window.addEventListener('DOMContentLoaded', () => {
  if (window.location.search.includes('code=')) {
    handleOAuthCallback();
  }
});

// UTILS
// ──────────────────────────────────────────────
function lastDigit(price) {
  const s = price.toString().replace('.','');
  return parseInt(s[s.length-1]);
}
function isPar(d) { return d % 2 === 0; }
function cfg(id) { return document.getElementById(id); }
function log(msg, type='info') {
  const area = document.getElementById('log-area');
  const ts = new Date().toLocaleTimeString('pt-BR');
  const div = document.createElement('div');
  div.className = 'log-line ' + type;
  div.textContent = `[${ts}] ${msg}`;
  area.appendChild(div);
  area.scrollTop = area.scrollHeight;
}
function formatMoney(v) {
  const sign = v >= 0 ? '+' : '';
  return sign + '$' + Math.abs(v).toFixed(2);
}

// ──────────────────────────────────────────────
// OAUTH2 + PKCE + OTP — Nova API Deriv
// ──────────────────────────────────────────────
const DERIV_CLIENT_ID = '33rEVLuUFgw1FLgSt03bQ'; // App ID jeanbot3 (PAT/Native)
const DERIV_APP_ID_HEADER = '33rEVLuUFgw1FLgSt03bQ';
const DERIV_AUTH_URL = 'https://auth.deriv.com/oauth2/auth';
const DERIV_TOKEN_URL = 'https://auth.deriv.com/oauth2/token';
const DERIV_API_BASE = 'https://api.derivws.com/trading/v1';
const REDIRECT_URI = window.location.href.split('?')[0].split('#')[0];

let oauthState = { accessToken: null, accountId: null };

async function generatePKCE() {
  const array = crypto.getRandomValues(new Uint8Array(64));
  const verifier = Array.from(array)
    .map(v => 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-._~'[v % 66])
    .join('');
  const hash = await crypto.subtle.digest('SHA-256', new TextEncoder().encode(verifier));
  const challenge = btoa(String.fromCharCode(...new Uint8Array(hash)))
    .replace(/\+/g, '-').replace(/\//g, '_').replace(/=+$/, '');
  return { verifier, challenge };
}

async function startOAuth() {
  const { verifier, challenge } = await generatePKCE();
  const state = crypto.getRandomValues(new Uint8Array(16))
    .reduce((s, b) => s + b.toString(16).padStart(2, '0'), '');
  sessionStorage.setItem('pkce_verifier', verifier);
  sessionStorage.setItem('oauth_state', state);
  const params = new URLSearchParams({
    response_type: 'code',
    client_id: DERIV_CLIENT_ID,
    redirect_uri: REDIRECT_URI,
    scope: 'trade account_manage',
    state,
    code_challenge: challenge,
    code_challenge_method: 'S256'
  });
  window.location.href = DERIV_AUTH_URL + '?' + params.toString();
}

async function handleOAuthCallback() {
  const params = new URLSearchParams(window.location.search);
  const code = params.get('code');
  const retState = params.get('state');
  const savedState = sessionStorage.getItem('oauth_state');
  const verifier = sessionStorage.getItem('pkce_verifier');
  if (!code || !verifier) return;
  if (retState !== savedState) { log('Erro de segurança OAuth (state mismatch)', 'error'); return; }
  // Limpa URL
  window.history.replaceState({}, '', window.location.pathname);
  sessionStorage.removeItem('pkce_verifier');
  sessionStorage.removeItem('oauth_state');
  log('Código OAuth recebido, trocando por token...', 'info');
  try {
    const resp = await fetch(DERIV_TOKEN_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body: new URLSearchParams({
        grant_type: 'authorization_code',
        client_id: DERIV_CLIENT_ID,
        code,
        code_verifier: verifier,
        redirect_uri: REDIRECT_URI
      })
    });
    const data = await resp.json();
    if (!data.access_token) throw new Error(JSON.stringify(data));
    oauthState.accessToken = data.access_token;
    log('Token OAuth obtido! Buscando conta...', 'success');
    await fetchAccount();
  } catch(e) {
    log('Erro ao obter token: ' + e.message, 'error');
  }
}

async function fetchAccount() {
  try {
    const resp = await fetch(DERIV_API_BASE + '/options/accounts', {
      headers: {
        'Authorization': 'Bearer ' + oauthState.accessToken,
        'Deriv-App-ID': DERIV_APP_ID_HEADER
      }
    });
    const data = await resp.json();
    const accounts = data.accounts || data;
    if (!accounts || accounts.length === 0) throw new Error('Nenhuma conta encontrada');
    const acc = accounts[0];
    oauthState.accountId = acc.account_id || acc.id || acc.loginid;
    state.loginId = oauthState.accountId;
    state.balance = acc.balance || 0;
    state.currency = acc.currency || 'USD';
    document.getElementById('oauth-area').style.display = 'none';
    document.getElementById('token-area').style.display = 'block';
    document.getElementById('auth-status').textContent = oauthState.accountId + ' | ' + state.balance + ' ' + state.currency;
    updateConnBadge(false);
    updateTicker();
    log('Conta: ' + oauthState.accountId + ' | Saldo: ' + state.balance + ' ' + state.currency, 'success');
    await connectDeriv();
  } catch(e) {
    log('Erro ao buscar conta: ' + e.message, 'error');
  }
}

async function connectDeriv() {
  if (!oauthState.accessToken || !oauthState.accountId) {
    log('Faça login primeiro clicando em LOGIN DERIV', 'error');
    return;
  }
  if (state.ws) { state.ws.close(); }
  log('Obtendo OTP para WebSocket...', 'info');
  try {
    const resp = await fetch(`${DERIV_API_BASE}/options/accounts/${oauthState.accountId}/otp`, {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer ' + oauthState.accessToken,
        'Deriv-App-ID': DERIV_APP_ID_HEADER,
        'Content-Type': 'application/json'
      }
    });
    const data = await resp.json();
    if (!data.url) throw new Error(JSON.stringify(data));
    log('OTP obtido! Conectando WebSocket...', 'info');
    state.ws = new WebSocket(data.url);
    state.ws.onopen = () => { log('WebSocket conectado!', 'success'); };
    state.ws.onmessage = (e) => { const d = JSON.parse(e.data); handleMessage(d); };
    state.ws.onerror = () => { log('Erro de conexão WebSocket', 'error'); };
    state.ws.onclose = () => {
      state.connected = false;
      updateConnBadge(false);
      log('WebSocket fechado', 'warn');
      if (state.botActive) { setTimeout(connectDeriv, 3000); }
    };
    // Após conectar, buscar saldo e iniciar ticks
    setTimeout(() => {
      state.connected = true;
      updateConnBadge(true);
      subscribeBalance();
      if (state.botActive) startTicks();
    }, 1000);
  } catch(e) {
    log('Erro ao obter OTP: ' + e.message, 'error');
  }
}

function logout() {
  oauthState = { accessToken: null, accountId: null };
  if (state.ws) state.ws.close();
  state.connected = false;
  updateConnBadge(false);
  document.getElementById('oauth-area').style.display = 'block';
  document.getElementById('token-area').style.display = 'none';
  log('Desconectado', 'warn');
}

function handleMessage(d) {
  if (d.error) { log('Erro API: ' + d.error.message, 'error'); return; }
  switch(d.msg_type) {
    case 'authorize':
      state.connected = true;
      state.loginId = d.authorize.loginid;
      state.balance = d.authorize.balance;
      state.currency = d.authorize.currency;
      updateConnBadge(true);
      updateTicker();
      log(`Conectado como ${state.loginId} | Saldo: ${state.balance} ${state.currency}`, 'success');
      subscribeBalance();
      if (state.botActive) startTicks();
      break;
    case 'balance':
      state.balance = d.balance.balance;
      updateTicker();
      break;
    case 'tick':
      const dig = lastDigit(d.tick.quote);
      processTick(dig, d.tick.quote);
      break;
    case 'proposal':
      if (state.pendingBuy && d.proposal) {
        state.currentProposal = d.proposal;
        executeBuy(d.proposal.id);
      }
      break;
    case 'buy':
      if (d.buy) {
        state.lastContractId = d.buy.contract_id;
        state.awaitingResult = true;
        state.pendingBuy = false;
        log(`Contrato aberto #${d.buy.contract_id} – Stake: $${state.currentStake.toFixed(2)}`, 'info');
        subscribeContract(d.buy.contract_id);
      }
      break;
    case 'proposal_open_contract':
      handleContractUpdate(d.proposal_open_contract);
      break;
  }
}

function subscribeBalance() {
  state.ws.send(JSON.stringify({ balance: 1, account: 'current', subscribe: 1 }));
}

function subscribeContract(id) {
  state.ws.send(JSON.stringify({ proposal_open_contract: 1, contract_id: id, subscribe: 1 }));
}

function startTicks() {
  const ativo = cfg('cfg-ativo').value;
  state.ws.send(JSON.stringify({
    ticks: ativo,
    subscribe: 1
  }));
  log(`Inscrito em ticks: ${ativo}`, 'info');
  cfg('t-ativo').textContent = ativo;
}

function stopTicks() {
  state.ws.send(JSON.stringify({ forget_all: 'ticks' }));
}

// ──────────────────────────────────────────────
// TICK PROCESSING
// ──────────────────────────────────────────────
function processTick(dig, price) {
  const maxTicks = parseInt(cfg('cfg-ticks').value) || 50;
  state.digits.push(dig);
  if (state.digits.length > maxTicks) state.digits.shift();

  updateDigitStrip(dig);
  const analysis = analyze(state.digits);
  updateUI(analysis);

  if (state.botActive && !state.awaitingResult && state.connected) {
    checkEntry(analysis, dig);
  }
}

// ──────────────────────────────────────────────
// ANALYSIS
// ──────────────────────────────────────────────
function analyze(digits) {
  const total = digits.length;
  if (total < 5) return null;

  const pares = digits.filter(d => isPar(d));
  const impares = digits.filter(d => !isPar(d));
  const pctPar = pares.length / total * 100;
  const pctImpar = impares.length / total * 100;

  // Frequency
  const freq = {};
  for (let i = 0; i <= 9; i++) freq[i] = 0;
  digits.forEach(d => freq[d]++);
  const domDig = parseInt(Object.keys(freq).reduce((a,b) => freq[a] > freq[b] ? a : b));
  const domFreq = freq[domDig];

  // Dominant group
  const minPct = parseInt(cfg('cfg-pct').value) || 60;
  let grupo = null;
  if (pctPar >= minPct) grupo = 'par';
  else if (pctImpar >= minPct) grupo = 'impar';

  // Conditions
  const c1 = grupo !== null;
  const c2 = grupo ? (grupo === 'par' ? isPar(domDig) : !isPar(domDig)) : false;
  const last2ok = digits.length >= 2
    ? (grupo === 'par' ? isPar(digits.at(-1)) && isPar(digits.at(-2))
        : !isPar(digits.at(-1)) && !isPar(digits.at(-2)))
    : false;
  const c3 = c1 && last2ok;

  const allOk = c1 && c2 && c3;
  const signal = allOk ? (grupo === 'par' ? 'impar' : 'par') : null;

  return { pctPar, pctImpar, freq, domDig, domFreq, grupo, c1, c2, c3, allOk, signal, total };
}

// ──────────────────────────────────────────────
// ENTRY LOGIC
// ──────────────────────────────────────────────
function checkEntry(analysis, latestDig) {
  if (!analysis) return;

  const postLossEnabled = cfg('sw-postloss').checked;
  const autoInvert = cfg('sw-autoinvert').checked;

  if (state.postLossMode && postLossEnabled) {
    handlePostLossSequence(latestDig, analysis);
    return;
  }

  // Check stop / meta
  const stop = parseFloat(cfg('cfg-stop').value) || 10;
  const meta = parseFloat(cfg('cfg-meta').value) || 5;
  if (Math.abs(state.plDay) >= stop && state.plDay < 0) {
    log(`Stop Loss atingido: ${formatMoney(state.plDay)}`, 'error');
    toggleBot();
    return;
  }
  if (state.plDay >= meta) {
    log(`Meta diária atingida: ${formatMoney(state.plDay)}`, 'success');
    toggleBot();
    return;
  }

  if (analysis.allOk && analysis.signal) {
    enterTrade(analysis.signal, 'SINAL AUTOMÁTICO');
  }
}

function handlePostLossSequence(dig, analysis) {
  const dir = state.lastDirection; // direction we were trading
  const isContrario = dir === 'par' ? !isPar(dig) : isPar(dig);
  const isFavor = dir === 'par' ? isPar(dig) : !isPar(dig);

  if (state.postLossStep === 0 && isContrario) {
    state.postLossStep = 1;
    log('Pós-loss: dígito contrário detectado, aguardando dígito a favor...', 'warn');
    return;
  }
  if (state.postLossStep === 1 && isFavor) {
    log('Pós-loss: sequência confirmada! Entrando na mesma direção...', 'warn');
    state.postLossMode = false;
    state.postLossStep = 0;

    const autoInvert = cfg('sw-autoinvert').checked;
    const tradeDir = autoInvert ? (dir === 'par' ? 'impar' : 'par') : dir;
    enterTrade(tradeDir, `PÓS-LOSS${autoInvert ? ' INVERTIDO' : ''}`);
  }
}

function enterTrade(direction, reason) {
  if (state.awaitingResult || state.pendingBuy) return;

  const stake = state.currentStake;
  const contractType = direction === 'par' ? 'DIGITEVEN' : 'DIGITODD';
  state.currentContractType = contractType;
  state.lastDirection = direction;

  log(`${reason}: ${direction.toUpperCase()} | Stake: $${stake.toFixed(2)}`, 'warn');
  setModeIndicator(`ENTRANDO: ${direction.toUpperCase()} (${reason})`);

  requestProposal(contractType, stake);
}

function requestProposal(contractType, stake) {
  state.pendingBuy = true;
  const ativo = cfg('cfg-ativo').value;
  state.ws.send(JSON.stringify({
    proposal: 1,
    amount: stake,
    basis: 'stake',
    contract_type: contractType,
    currency: state.currency || 'USD',
    duration: 1,
    duration_unit: 't',
    symbol: ativo
  }));
}

function executeBuy(proposalId) {
  state.ws.send(JSON.stringify({
    buy: proposalId,
    price: state.currentStake
  }));
}

function manualBuy(contractType) {
  if (!state.connected) { log('Conecte-se primeiro', 'error'); return; }
  if (state.awaitingResult) { log('Aguardando resultado do contrato atual', 'warn'); return; }
  const direction = contractType === 'DIGITEVEN' ? 'par' : 'impar';
  enterTrade(direction, 'MANUAL');
}

// ──────────────────────────────────────────────
// CONTRACT RESULT
// ──────────────────────────────────────────────
function handleContractUpdate(contract) {
  if (!contract || !contract.is_settled) return;

  const pl = parseFloat(contract.profit);
  const won = pl > 0;
  const contractType = contract.contract_type;
  const price = parseFloat(contract.entry_spot);
  const payout = parseFloat(contract.payout);

  state.awaitingResult = false;

  // Update P&L
  state.plDay += pl;
  state.plTotal += pl;
  if (state.plTotal < state.maxDD) state.maxDD = state.plTotal;
  if (won) { state.winsDay++; state.winsTotal++; }
  else { state.lossDay++; state.lossTotal++; }

  addHistoryRow(contractType, price.toFixed(2), pl, '');
  updateStatsUI();
  updateTicker();

  const galeMax = parseInt(cfg('cfg-max-gale').value) || 2;
  const galeFactor = parseFloat(cfg('cfg-gale').value) || 2.0;

  if (won) {
    log(`✓ WIN +$${pl.toFixed(2)}`, 'success');
    // Reset gale
    state.galeLevel = 0;
    state.currentStake = parseFloat(cfg('cfg-stake').value) || 0.35;
    state.baseStake = state.currentStake;
    state.lastLoss = false;
    state.postLossMode = false;
    state.postLossStep = 0;
  } else {
    log(`✗ LOSS -$${Math.abs(pl).toFixed(2)}`, 'error');
    state.lastLoss = true;

    if (state.galeLevel < galeMax) {
      state.galeLevel++;
      state.currentStake = state.currentStake * galeFactor;
      log(`Martingale G${state.galeLevel}: próxima entrada $${state.currentStake.toFixed(2)}`, 'warn');
    } else {
      state.galeLevel = 0;
      state.currentStake = parseFloat(cfg('cfg-stake').value) || 0.35;
      log('Gales esgotados, resetando stake', 'warn');
      // Activate post-loss mode
      if (cfg('sw-postloss').checked) {
        state.postLossMode = true;
        state.postLossStep = 0;
        log('Modo pós-loss ativado: aguardando sequência gatilho', 'warn');
      }
    }
  }

  updateGaleDisplay();
  setModeIndicator(won ? 'WIN – AGUARDANDO PRÓXIMO SINAL' : 'LOSS – MODO PÓS-LOSS ATIVO');
}

// ──────────────────────────────────────────────
// UI UPDATES
// ──────────────────────────────────────────────
function updateUI(a) {
  if (!a) return;

  // Percentages
  const pp = a.pctPar.toFixed(1) + '%';
  const pi = a.pctImpar.toFixed(1) + '%';
  const parEl = document.getElementById('pct-par');
  const imparEl = document.getElementById('pct-impar');
  parEl.textContent = pp;
  imparEl.textContent = pi;
  parEl.className = 'eo-pct' + (a.grupo === 'par' ? ' dominant' : '');
  imparEl.className = 'eo-pct' + (a.grupo === 'impar' ? ' dominant' : '');

  // Bar
  document.getElementById('bar-fill').style.width = a.pctPar.toFixed(1) + '%';

  // Pie
  document.getElementById('pie-par').setAttribute('stroke-dasharray', `${a.pctPar.toFixed(1)} 100`);
  document.getElementById('pie-impar').setAttribute('stroke-dasharray', `${a.pctImpar.toFixed(1)} 100`);
  document.getElementById('pie-impar').setAttribute('stroke-dashoffset', `-${a.pctPar.toFixed(1)}`);

  // Dominant digit
  document.getElementById('dig-dom').textContent = a.domDig;
  document.getElementById('dig-dom-freq').textContent = `FREQ: ${(a.domFreq/a.total*100).toFixed(1)}%`;

  // Freq chart
  updateFreqChart(a.freq, a.total, a.domDig);

  // Conditions
  updateConditions(a);

  // Signal
  updateSignal(a);
}

function updateFreqChart(freq, total, domDig) {
  const chart = document.getElementById('freq-chart');
  chart.innerHTML = '';
  const maxFreq = Math.max(...Object.values(freq));

  for (let i = 0; i <= 9; i++) {
    const pct = freq[i] / total * 100;
    const h = maxFreq > 0 ? (freq[i] / maxFreq * 70) : 0;
    const isDom = i === domDig;
    const cls = isDom ? 'dominant-bar' : (isPar(i) ? 'par' : 'impar');
    const wrap = document.createElement('div');
    wrap.className = 'freq-bar-wrap';
    wrap.innerHTML = `
      <span class="freq-pct">${pct.toFixed(0)}%</span>
      <div class="freq-bar ${cls}" style="height:${h}px"></div>
      <span class="freq-lbl">${i}</span>`;
    chart.appendChild(wrap);
  }
}

function updateConditions(a) {
  const list = document.getElementById('cond-list');
  const minPct = parseInt(cfg('cfg-pct').value) || 60;
  const items = [
    [a.c1, `% Domínio > ${minPct}% – atual: ${a.grupo ? (a.grupo==='par'?a.pctPar:a.pctImpar).toFixed(1)+'% ('+a.grupo.toUpperCase()+')' : 'insuficiente'}`],
    [a.c2, `Dígito dominante (${a.domDig}) no grupo ${a.grupo||'–'} – ${a.c2?'✓ válido':'✗ inválido'}`],
    [a.c3, `Últimos 2 ticks no grupo – ${a.c3?'✓ confirmado':'✗ não confirmado'}`],
  ];
  list.innerHTML = '';
  items.forEach(([ok, txt]) => {
    const cl = ok ? 'ok' : (a.grupo ? 'fail' : 'wait');
    list.innerHTML += `<div class="cond-item ${cl}"><div class="cond-dot"></div>${txt}</div>`;
  });
}

function updateSignal(a) {
  const box = document.getElementById('signal-box');
  const val = document.getElementById('signal-val');
  const sub = document.getElementById('signal-sub');

  if (state.postLossMode) {
    val.className = 'signal-value aguardando';
    val.textContent = 'PÓS-LOSS';
    sub.textContent = `Aguardando sequência gatilho (passo ${state.postLossStep+1}/2)`;
    return;
  }

  if (a.allOk && a.signal) {
    val.className = 'signal-value ' + a.signal;
    val.textContent = a.signal === 'par' ? 'DIGIT EVEN' : 'DIGIT ODD';
    sub.textContent = `Grupo dominante: ${a.grupo.toUpperCase()} ${(a.grupo==='par'?a.pctPar:a.pctImpar).toFixed(1)}% | Dig: ${a.domDig}`;
  } else {
    val.className = 'signal-value aguardando';
    val.textContent = 'AGUARDANDO';
    sub.textContent = `Condições: ${[a.c1,a.c2,a.c3].filter(Boolean).length}/3 atendidas`;
  }
}

function updateDigitStrip(newDig) {
  const strip = document.getElementById('digit-strip');
  const show = 20;
  const arr = state.digits.slice(-show);
  strip.innerHTML = arr.map((d, i) => {
    const isNew = i === arr.length - 1;
    return `<div class="dig ${isPar(d)?'par':'impar'}${isNew?' new':''}">${d}</div>`;
  }).join('');
}

function updateConnBadge(connected) {
  const b = document.getElementById('conn-badge');
  b.textContent = connected ? 'CONECTADO' : 'DESCONECTADO';
  b.style.color = connected ? 'var(--green)' : 'var(--red)';
  b.style.borderColor = connected ? 'var(--green)' : 'var(--red)';
  if (connected) b.style.boxShadow = 'var(--glow-green)'; else b.style.boxShadow = '';
}

function updateTicker() {
  cfg('t-conta').textContent = state.loginId || '–';
  cfg('t-saldo').textContent = state.balance ? `$${parseFloat(state.balance).toFixed(2)}` : '–';
  const plEl = cfg('t-pl');
  plEl.textContent = formatMoney(state.plDay);
  plEl.style.color = state.plDay >= 0 ? 'var(--green)' : 'var(--red)';
}

function updateStatsUI() {
  const wd = state.winsDay, ld = state.lossDay, tt = wd+ld;
  const wt = state.winsTotal, lt = state.lossTotal, tot = wt+lt;
  const pctD = tt ? (wd/tt*100).toFixed(0) : 0;
  const pctT = tot ? (wt/tot*100).toFixed(0) : 0;

  function colorVal(el, v) {
    el.textContent = formatMoney(v);
    el.className = 'stat-value ' + (v >= 0 ? 'green' : 'red');
  }

  cfg('stat-dia').textContent = `${wd}/${tt} (${pctD}%)`;
  cfg('stat-dia').className = 'stat-value ' + (state.plDay>=0?'green':'red');
  colorVal(cfg('stat-pl-dia'), state.plDay);
  cfg('stat-total').textContent = `${wt}/${tot} (${pctT}%)`;
  cfg('stat-total').className = 'stat-value ' + (state.plTotal>=0?'green':'red');
  colorVal(cfg('stat-pl-total'), state.plTotal);
  cfg('stat-dd').textContent = formatMoney(state.maxDD);
  cfg('stat-stake').textContent = '$' + state.currentStake.toFixed(2);
}

function updateGaleDisplay() {
  cfg('gale-display').innerHTML = `G${state.galeLevel} – Stake: <span id="gale-stake">$${state.currentStake.toFixed(2)}</span>`;
}

function setModeIndicator(txt) {
  const el = document.getElementById('mode-indicator');
  el.textContent = 'MODO: ' + txt;
}

function addHistoryRow(tipo, preco, pl, msg) {
  const tbody = document.getElementById('hist-body');
  const tr = document.createElement('tr');
  const isEven = tipo === 'DIGITEVEN';
  const isPos = pl > 0;
  tr.innerHTML = `
    <td class="${isEven?'type-even':'type-odd'}">${tipo}</td>
    <td>${preco}</td>
    <td class="${isPos?'pl-pos':'pl-neg'}">${isPos?'+':''}${pl.toFixed(2)}</td>
    <td style="color:#546e7a;font-size:.6rem">${msg}</td>`;
  tbody.insertBefore(tr, tbody.firstChild);
  // Keep max 50 rows
  while (tbody.rows.length > 50) tbody.deleteRow(tbody.rows.length-1);
}

// ──────────────────────────────────────────────
// BOT TOGGLE
// ──────────────────────────────────────────────
function toggleBot() {
  state.botActive = !state.botActive;
  const btn = document.getElementById('btn-toggle');
  const badge = document.getElementById('status-badge');

  if (state.botActive) {
    btn.textContent = '⏹ PARAR';
    btn.className = '';
    badge.textContent = 'ATIVO';
    badge.style.color = 'var(--green)';
    badge.style.borderColor = 'var(--green)';
    badge.style.boxShadow = 'var(--glow-green)';
    log('Bot INICIADO', 'success');
    state.currentStake = parseFloat(cfg('cfg-stake').value) || 0.35;
    state.baseStake = state.currentStake;
    if (state.connected) startTicks();
  } else {
    btn.textContent = '▶ INICIAR';
    btn.className = 'off';
    badge.textContent = 'PARADO';
    badge.style.color = 'var(--red)';
    badge.style.borderColor = 'var(--red)';
    badge.style.boxShadow = '';
    log('Bot PARADO', 'warn');
    if (state.connected) stopTicks();
  }
}

function cancelAll() {
  if (!state.connected) return;
  log('Cancelando ordens abertas...', 'warn');
}

function zerarTudo() {
  state.plDay = 0; state.winsDay = 0; state.lossDay = 0;
  state.galeLevel = 0;
  state.currentStake = parseFloat(cfg('cfg-stake').value) || 0.35;
  state.postLossMode = false; state.postLossStep = 0;
  updateStatsUI(); updateGaleDisplay();
  log('Zerado manualmente', 'warn');
}

// ──────────────────────────────────────────────
// SIMULATION (demo when not connected)
// ──────────────────────────────────────────────
function runSimulation() {
  if (state.connected) return;
  setInterval(() => {
    if (!state.connected) {
      const d = Math.floor(Math.random() * 10);
      const price = 1234.5 + Math.random() * 10;
      processTick(d, price);
    }
  }, 1000);
}

// Init
log('BOT FIGHT GAIN – JEAN TRADER iniciado', 'info');
log('Configure o token de API e clique CONECTAR', 'info');
runSimulation();
</script>
</body>
</html>
