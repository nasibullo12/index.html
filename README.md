<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="apple-mobile-web-app-title" content="Dars Pro">
<title>Dars Pro</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
:root{
  --bg:#000;--surface:#1c1c1e;--surface2:#2c2c2e;--surface3:#3a3a3c;
  --border:#38383a;--text:#fff;--muted:#8e8e93;
  --green:#30d158;--orange:#ff9f0a;--blue:#0a84ff;--red:#ff453a;--purple:#bf5af2;
}
body{background:var(--bg);color:var(--text);font-family:'Nunito',-apple-system,sans-serif;min-height:100vh;max-width:430px;margin:0 auto;padding-bottom:60px;}

/* HEADER */
.header{padding:52px 20px 6px;display:flex;justify-content:space-between;align-items:flex-end;}
.logo{display:flex;align-items:baseline;gap:2px;}
.logo-dars{font-size:2rem;font-weight:800;color:var(--orange);letter-spacing:-0.5px;}
.logo-pro{font-size:2rem;font-weight:800;color:var(--text);letter-spacing:-0.5px;}
.header-right{display:flex;align-items:center;gap:8px;}
.clock{font-size:0.85rem;color:var(--muted);}
.icon-btn{width:32px;height:32px;border-radius:50%;background:var(--surface2);border:none;color:var(--orange);font-size:1rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:transform 0.15s;}
.icon-btn:active{transform:scale(0.88);}

/* TABS */
.nav-tabs{display:flex;border-bottom:1px solid var(--border);}
.nav-tab{flex:1;padding:10px 4px;font-size:0.75rem;font-weight:700;border:none;background:transparent;color:var(--muted);cursor:pointer;font-family:'Nunito',sans-serif;border-bottom:2px solid transparent;transition:all 0.18s;letter-spacing:0.3px;}
.nav-tab.active{color:var(--orange);border-bottom-color:var(--orange);}

/* DAY TABS */
.day-scroll{display:flex;gap:7px;padding:10px 16px;overflow-x:auto;scrollbar-width:none;}
.day-scroll::-webkit-scrollbar{display:none;}
.day-chip{flex-shrink:0;padding:6px 13px;border-radius:20px;font-size:0.82rem;font-weight:600;border:none;cursor:pointer;background:var(--surface);color:var(--muted);font-family:'Nunito',sans-serif;transition:all 0.18s;}
.day-chip.active{background:var(--orange);color:#000;}
.day-chip.has-l{color:var(--text);}
.day-chip.today-chip{border:1px solid var(--orange);}

/* WEEK INFO */
.week-info{padding:4px 16px 6px;font-size:0.7rem;font-weight:700;color:var(--muted);letter-spacing:0.8px;text-transform:uppercase;}

/* LESSON ROWS */
.lesson-list{padding:0 16px;}
.lesson-row{display:flex;align-items:center;padding:12px 14px;background:var(--surface);border-radius:4px;margin-bottom:2px;gap:10px;position:relative;overflow:hidden;}
.lesson-row:first-child{border-radius:14px 14px 4px 4px;}
.lesson-row:last-child{border-radius:4px 4px 14px 14px;}
.lesson-row:only-child{border-radius:14px;}
.lesson-row.done-row{opacity:0.4;}
.lesson-left-bar{position:absolute;left:0;top:0;bottom:0;width:3px;border-radius:0;}
.lesson-time{font-size:1.3rem;font-weight:300;letter-spacing:-1px;min-width:50px;color:var(--text);}
.lesson-row.done-row .lesson-time{color:var(--muted);}
.lesson-info{flex:1;min-width:0;}
.lesson-name{font-size:0.95rem;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.lesson-row.done-row .lesson-name{text-decoration:line-through;color:var(--muted);}
.lesson-sub{font-size:0.7rem;color:var(--muted);margin-top:1px;}
.week-badge{display:inline-block;font-size:0.58rem;padding:1px 6px;border-radius:6px;background:rgba(10,132,255,0.15);color:var(--blue);font-weight:700;margin-left:5px;vertical-align:middle;}

.row-right{display:flex;align-items:center;gap:5px;}
.toggle-col{display:flex;flex-direction:column;align-items:center;gap:1px;}
.toggle{width:48px;height:28px;border-radius:14px;background:var(--surface2);position:relative;cursor:pointer;transition:background 0.25s;border:none;flex-shrink:0;}
.toggle.on{background:var(--green);}
.toggle-knob{position:absolute;top:2px;left:2px;width:24px;height:24px;border-radius:50%;background:#fff;box-shadow:0 2px 5px rgba(0,0,0,0.35);transition:transform 0.22s cubic-bezier(.4,0,.2,1);pointer-events:none;}
.toggle.on .toggle-knob{transform:translateX(20px);}
.toggle-lbl{font-size:0.55rem;font-weight:700;color:var(--muted);}
.toggle.on~.toggle-lbl{color:var(--green);}
.act-btn{width:24px;height:24px;border-radius:50%;border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:0.75rem;flex-shrink:0;}
.edit-btn-s{background:rgba(10,132,255,0.13);color:var(--blue);}
.del-btn-s{background:rgba(255,69,58,0.13);color:var(--red);opacity:0;transition:opacity 0.2s;}
.lesson-row:hover .del-btn-s,.lesson-row.show-del .del-btn-s{opacity:1;}

/* EMPTY */
.empty-state{text-align:center;padding:50px 20px;}
.empty-icon{font-size:2.5rem;margin-bottom:10px;}
.empty-text{color:var(--muted);font-size:0.9rem;}

/* STATS */
.stats-wrap{padding:0 16px 16px;}
.month-bar{display:flex;align-items:center;justify-content:space-between;padding:10px 0;margin-bottom:8px;}
.month-nav-btn{background:var(--surface2);border:none;color:var(--text);width:32px;height:32px;border-radius:50%;font-size:1.1rem;cursor:pointer;display:flex;align-items:center;justify-content:center;}
.month-name{font-size:0.95rem;font-weight:700;}

.sum-row{display:flex;gap:8px;margin-bottom:12px;}
.sum-c{flex:1;background:var(--surface);border-radius:14px;padding:13px 8px;text-align:center;}
.sum-v{font-size:1.4rem;font-weight:800;line-height:1;}
.sum-l{font-size:0.6rem;color:var(--muted);font-weight:700;margin-top:3px;text-transform:uppercase;letter-spacing:0.4px;}

.salary-card{background:var(--surface);border:1px solid rgba(191,90,242,0.4);border-radius:16px;padding:16px;margin-bottom:12px;}
.salary-lbl{font-size:0.7rem;font-weight:700;color:var(--purple);letter-spacing:0.8px;text-transform:uppercase;margin-bottom:6px;}
.salary-val{font-size:1.8rem;font-weight:800;color:var(--purple);line-height:1;margin-bottom:3px;}
.salary-sub{font-size:0.75rem;color:var(--muted);}

.chart-c{background:var(--surface);border-radius:16px;padding:16px;margin-bottom:12px;}
.chart-lbl{font-size:0.7rem;font-weight:700;color:var(--muted);letter-spacing:0.8px;text-transform:uppercase;margin-bottom:12px;}
.chart-wrap{position:relative;height:190px;}
.chart-wrap.sm{height:160px;}

.stu-card{background:var(--surface);border-radius:16px;padding:16px;margin-bottom:10px;}
.stu-name{font-size:1rem;font-weight:700;margin-bottom:10px;}
.stu-row{display:flex;justify-content:space-between;margin-bottom:5px;}
.stu-lbl{font-size:0.78rem;color:var(--muted);}
.stu-val{font-size:0.85rem;font-weight:700;}
.stu-div{height:1px;background:var(--border);margin:8px 0;}
.prog-bar{height:5px;background:var(--surface2);border-radius:3px;overflow:hidden;margin-top:6px;}
.prog-fill{height:100%;border-radius:3px;transition:width 0.5s ease;}

/* SETTINGS */
.settings-wrap{padding:16px;}
.set-section{font-size:0.7rem;font-weight:700;color:var(--muted);letter-spacing:0.8px;text-transform:uppercase;margin:16px 0 8px;}
.set-card{background:var(--surface);border-radius:14px;overflow:hidden;margin-bottom:10px;}
.set-row{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border);}
.set-row:last-child{border-bottom:none;}
.set-row-label{font-size:0.9rem;font-weight:600;}
.set-row-sub{font-size:0.72rem;color:var(--muted);margin-top:1px;}

.sound-item{display:flex;align-items:center;padding:12px 16px;border-bottom:1px solid var(--border);cursor:pointer;transition:background 0.15s;}
.sound-item:last-child{border-bottom:none;}
.sound-item.selected{background:rgba(255,159,10,0.06);}
.sound-icon{font-size:1.3rem;margin-right:12px;}
.sound-info{flex:1;}
.sound-name{font-size:0.9rem;font-weight:600;}
.sound-desc{font-size:0.72rem;color:var(--muted);}
.sound-check{color:var(--orange);font-weight:800;font-size:1rem;}
.play-s{background:var(--surface2);border:none;color:var(--orange);width:28px;height:28px;border-radius:50%;cursor:pointer;font-size:0.75rem;display:flex;align-items:center;justify-content:center;margin-left:8px;}

.vol-row{display:flex;align-items:center;gap:10px;padding:14px 16px;}
input[type=range]{flex:1;-webkit-appearance:none;height:4px;border-radius:2px;background:var(--surface2);outline:none;}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:20px;height:20px;border-radius:50%;background:var(--orange);cursor:pointer;}
.vol-val{font-size:0.8rem;color:var(--muted);min-width:32px;text-align:right;}

.theme-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px;}
.theme-item{background:var(--surface);border-radius:12px;padding:12px;display:flex;align-items:center;gap:8px;cursor:pointer;border:2px solid transparent;transition:all 0.18s;}
.theme-item.selected{border-color:var(--orange);}
.theme-icon{font-size:1.3rem;}
.theme-name{font-size:0.85rem;font-weight:700;}
.theme-desc{font-size:0.68rem;color:var(--muted);}

/* ios toggle */
.ios-toggle{width:44px;height:26px;border-radius:13px;background:var(--surface2);position:relative;cursor:pointer;transition:background 0.25s;border:none;flex-shrink:0;}
.ios-toggle.on{background:var(--green);}
.ios-toggle-knob{position:absolute;top:2px;left:2px;width:22px;height:22px;border-radius:50%;background:#fff;box-shadow:0 1px 4px rgba(0,0,0,0.3);transition:transform 0.22s;pointer-events:none;}
.ios-toggle.on .ios-toggle-knob{transform:translateX(18px);}

/* CONFIRM */
.overlay-bg{position:fixed;inset:0;background:rgba(0,0,0,0.8);backdrop-filter:blur(10px);z-index:200;display:flex;align-items:center;justify-content:center;padding:20px;opacity:0;pointer-events:none;transition:opacity 0.2s;}
.overlay-bg.open{opacity:1;pointer-events:all;}
.cf-box{background:var(--surface);border-radius:20px;padding:24px 20px;width:100%;max-width:320px;text-align:center;transform:scale(0.9);transition:transform 0.2s;}
.overlay-bg.open .cf-box{transform:scale(1);}
.cf-icon{font-size:2.4rem;margin-bottom:10px;}
.cf-title{font-size:1.05rem;font-weight:700;margin-bottom:5px;}
.cf-sub{font-size:0.82rem;color:var(--muted);margin-bottom:18px;line-height:1.4;}
.cf-btns{display:flex;flex-wrap:wrap;gap:8px;}
.cf-btn{flex:1;min-width:80px;padding:11px;border-radius:12px;border:none;font-family:'Nunito',sans-serif;font-size:0.88rem;font-weight:700;cursor:pointer;}
.cf-cancel{background:var(--surface2);color:var(--text);}
.cf-yes{background:var(--green);color:#000;}
.cf-skip{background:rgba(255,69,58,0.15);color:var(--red);}

/* MODAL */
.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.72);backdrop-filter:blur(8px);z-index:100;display:flex;align-items:flex-end;opacity:0;pointer-events:none;transition:opacity 0.22s;}
.modal-bg.open{opacity:1;pointer-events:all;}
.modal-box{width:100%;background:#1c1c1e;border-radius:20px 20px 0 0;padding:18px 20px 44px;transform:translateY(100%);transition:transform 0.28s cubic-bezier(.4,0,.2,1);max-height:92vh;overflow-y:auto;}
.modal-bg.open .modal-box{transform:translateY(0);}
.modal-handle{width:36px;height:4px;background:var(--border);border-radius:2px;margin:0 auto 18px;}
.modal-title{font-size:1.05rem;font-weight:700;margin-bottom:16px;}
.m-label{display:block;font-size:0.68rem;color:var(--muted);font-weight:700;letter-spacing:0.5px;text-transform:uppercase;margin-bottom:5px;margin-top:12px;}
.m-input{width:100%;background:var(--surface2);border:none;border-radius:10px;color:var(--text);font-family:'Nunito',sans-serif;font-size:0.95rem;padding:11px 14px;outline:none;-webkit-appearance:none;}
.m-select{width:100%;background:var(--surface2);border:none;border-radius:10px;color:var(--text);font-family:'Nunito',sans-serif;font-size:0.95rem;padding:11px 14px;outline:none;-webkit-appearance:none;}
.m-select option{background:var(--surface2);}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.three-col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;}
.rem-row{display:flex;gap:8px;margin-top:6px;}
.rem-btn{flex:1;padding:10px;border-radius:10px;border:1.5px solid var(--border);background:transparent;color:var(--muted);font-family:'Nunito',sans-serif;font-size:0.82rem;font-weight:600;cursor:pointer;transition:all 0.18s;}
.rem-btn.active{border-color:var(--orange);color:var(--orange);background:rgba(255,159,10,0.08);}
.pay-row{display:flex;gap:0;background:var(--surface2);border-radius:10px;overflow:hidden;margin-top:6px;}
.pay-btn{flex:1;padding:10px 4px;border:none;background:transparent;color:var(--muted);font-family:'Nunito',sans-serif;font-size:0.8rem;font-weight:700;cursor:pointer;transition:all 0.18s;text-align:center;}
.pay-btn.active{background:var(--orange);color:#000;border-radius:8px;margin:3px;}
.alt-box{background:var(--surface2);border-radius:12px;padding:14px;margin-top:12px;}
.alt-title{font-size:0.72rem;font-weight:700;color:var(--orange);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:10px;display:flex;justify-content:space-between;align-items:center;}
.price-input-wrap{display:flex;align-items:center;background:var(--surface2);border-radius:10px;overflow:hidden;margin-top:6px;}
.price-input-wrap input{flex:1;background:transparent;border:none;color:var(--text);font-family:'Nunito',sans-serif;font-size:0.95rem;padding:11px 14px;outline:none;}
.price-input-wrap span{padding:0 12px;color:var(--muted);font-size:0.82rem;font-weight:600;}
.save-btn-m{width:100%;padding:14px;background:var(--orange);color:#000;border:none;border-radius:13px;font-family:'Nunito',sans-serif;font-size:1rem;font-weight:700;cursor:pointer;margin-top:16px;}
.sch-row{display:flex;align-items:center;gap:8px;background:var(--surface2);border-radius:10px;padding:8px 12px;margin-top:8px;}
.sch-row select{flex:1;background:transparent;border:none;color:var(--text);font-family:'Nunito',sans-serif;font-size:0.9rem;outline:none;-webkit-appearance:none;}
.sch-time{font-size:1rem;font-weight:600;color:var(--orange);min-width:46px;cursor:pointer;}
.sch-remove{background:rgba(255,69,58,0.15);border:none;color:var(--red);width:26px;height:26px;border-radius:50%;cursor:pointer;font-size:0.85rem;display:flex;align-items:center;justify-content:center;}
.add-sch-btn{background:rgba(10,132,255,0.1);border:none;color:var(--blue);padding:8px 14px;border-radius:8px;font-family:'Nunito',sans-serif;font-size:0.82rem;font-weight:600;cursor:pointer;margin-top:8px;}

/* BANNER */
@keyframes slideDown{from{top:-80px;opacity:0}to{top:20px;opacity:1}}
.banner{position:fixed;top:20px;left:50%;transform:translateX(-50%);background:var(--surface);border:1px solid var(--border);border-left:3px solid var(--orange);border-radius:14px;padding:12px 16px;z-index:150;min-width:240px;max-width:340px;box-shadow:0 8px 30px rgba(0,0,0,0.6);animation:slideDown .3s ease;font-family:'Nunito',sans-serif;}
.banner-title{font-size:0.68rem;color:var(--orange);font-weight:800;letter-spacing:0.8px;text-transform:uppercase;margin-bottom:3px;}
.banner-name{font-size:0.95rem;font-weight:700;}
.banner-time{font-size:0.78rem;color:var(--muted);margin-top:2px;}
</style>
</head>
<body>

<div class="header">
  <div class="logo"><span class="logo-dars">Dars</span><span class="logo-pro"> Pro</span></div>
  <div class="header-right">
    <div class="clock" id="clk"></div>
    <button class="icon-btn" onclick="switchTab('settings')" title="Sozlamalar">⚙️</button>
    <button class="icon-btn" onclick="openModal()" title="Qo'shish" style="background:var(--orange);color:#000;font-size:1.3rem;">+</button>
  </div>
</div>

<div class="nav-tabs">
  <button class="nav-tab active" id="tab-jadval" onclick="switchTab('jadval')">JADVAL</button>
  <button class="nav-tab" id="tab-stat" onclick="switchTab('stat')">STATISTIKA</button>
  <button class="nav-tab" id="tab-settings" onclick="switchTab('settings')">⚙️</button>
</div>

<!-- JADVAL -->
<div id="page-jadval">
  <div class="day-scroll" id="dayScroll"></div>
  <div class="week-info" id="weekInfo"></div>
  <div id="lessonContent"></div>
</div>

<!-- STATISTIKA -->
<div id="page-stat" style="display:none">
  <div class="stats-wrap">
    <div class="month-bar">
      <button class="month-nav-btn" onclick="changeMonth(-1)">‹</button>
      <div class="month-name" id="monthName"></div>
      <button class="month-nav-btn" onclick="changeMonth(1)">›</button>
    </div>
    <div id="statsContent"></div>
  </div>
</div>

<!-- SETTINGS -->
<div id="page-settings" style="display:none">
  <div class="settings-wrap">
    <div class="set-section">🔔 BILDIRISHNOMALAR</div>
    <div class="set-card">
      <div class="set-row">
        <div><div class="set-row-label">Bildirishnomalar</div><div class="set-row-sub">Dars eslatmalari</div></div>
        <button class="ios-toggle on" id="notifToggle" onclick="toggleNotif()"><div class="ios-toggle-knob"></div></button>
      </div>
      <div class="set-row">
        <div><div class="set-row-label">Sinov bildirishnoma</div></div>
        <button onclick="testNotif()" style="background:rgba(255,159,10,0.15);color:var(--orange);border:none;padding:7px 14px;border-radius:8px;font-family:'Nunito',sans-serif;font-weight:700;font-size:0.82rem;cursor:pointer;">Sinab ko'r</button>
      </div>
    </div>

    <div class="set-section">🎵 OVOZ TANLASH</div>
    <div class="set-card" id="soundList"></div>

    <div class="set-section">🔊 OVOZ BALANDLIGI</div>
    <div class="set-card">
      <div class="vol-row">
        <span>🔈</span>
        <input type="range" id="volRange" min="0" max="1" step="0.05" value="0.7" oninput="updateVol(this)">
        <span>🔊</span>
        <span class="vol-val" id="volVal">70%</span>
      </div>
    </div>

    <div class="set-section">🎨 MAVZU</div>
    <div class="theme-grid" id="themeGrid"></div>

    <div class="set-section">ℹ️ HAQIDA</div>
    <div class="set-card">
      <div class="set-row"><span class="set-row-label">Dars Pro</span><span style="color:var(--muted);font-size:0.82rem;">v2.0</span></div>
      <div class="set-row"><span class="set-row-label">Shogirdlar</span><span id="studentCount" style="color:var(--orange);font-weight:700;">0 ta</span></div>
    </div>
  </div>
</div>

<!-- CONFIRM -->
<div class="overlay-bg" id="cfOverlay">
  <div class="cf-box">
    <div class="cf-icon" id="cfIcon"></div>
    <div class="cf-title" id="cfTitle"></div>
    <div class="cf-sub" id="cfSub"></div>
    <div class="cf-btns" id="cfBtns"></div>
  </div>
</div>

<!-- ADD/EDIT MODAL -->
<div class="modal-bg" id="modalBg" onclick="modalBgClose(event)">
  <div class="modal-box">
    <div class="modal-handle"></div>
    <div class="modal-title" id="modalTitleEl">Yangi shogird</div>

    <label class="m-label">Shogird ismi</label>
    <input class="m-input" type="text" id="mName" placeholder="Ismi">

    <label class="m-label">Dars kunlari va vaqtlari</label>
    <div id="schList"></div>
    <button class="add-sch-btn" onclick="addSchRow()">+ Kun qo'shish</button>

    <div class="alt-box">
      <div class="alt-title">
        <span>🔄 Galma-gal jadval</span>
        <button class="ios-toggle" id="altToggle" onclick="toggleAlt()"><div class="ios-toggle-knob"></div></button>
      </div>
      <div id="altContent" style="display:none">
        <div style="font-size:0.75rem;color:var(--muted);margin-bottom:8px;">Toq haftalarda boshqa vaqt</div>
        <div class="two-col">
          <select class="m-select" id="altDay">
            <option value="0">Dushanba</option><option value="1">Seshanba</option>
            <option value="2">Chorshanba</option><option value="3">Payshanba</option>
            <option value="4">Juma</option><option value="5">Shanba</option><option value="6">Yakshanba</option>
          </select>
          <input class="m-input" type="time" id="altTime" value="20:00">
        </div>
        <div style="font-size:0.7rem;color:var(--muted);margin-top:6px;">💡 Juft haftalarda oddiy vaqt ishlatiladi</div>
      </div>
    </div>

    <label class="m-label">Eslatma vaqti</label>
    <div class="rem-row" id="remRow">
      <button class="rem-btn active" data-v="5" onclick="pickRem(this)">5 daq oldin</button>
      <button class="rem-btn" data-v="10" onclick="pickRem(this)">10 daq oldin</button>
      <button class="rem-btn" data-v="15" onclick="pickRem(this)">15 daq oldin</button>
    </div>

    <label class="m-label">To'lov turi</label>
    <div class="pay-row" id="payRow">
      <button class="pay-btn active" data-v="per_lesson" onclick="pickPay(this)">Dars uchun</button>
      <button class="pay-btn" data-v="monthly" onclick="pickPay(this)">Oylik</button>
      <button class="pay-btn" data-v="both" onclick="pickPay(this)">Ikkala</button>
    </div>

    <div id="priceFields">
      <div id="perLessonField">
        <label class="m-label">Dars narxi</label>
        <div class="price-input-wrap"><input type="number" id="mPrice" placeholder="0"><span>so'm</span></div>
      </div>
      <div id="monthlyField" style="display:none">
        <label class="m-label">Oylik narx</label>
        <div class="price-input-wrap"><input type="number" id="mMonthlyPrice" placeholder="0"><span>so'm</span></div>
      </div>
    </div>

    <label class="m-label">Izoh (ixtiyoriy)</label>
    <textarea class="m-input" id="mNote" placeholder="Shogird haqida eslatma..." rows="2" style="resize:none;"></textarea>

    <button class="save-btn-m" id="saveBtnM" onclick="saveStudent()">Qo'shish</button>
  </div>
</div>

<script>
// ==================== DATA ====================
const DAYS=['Dushanba','Seshanba','Chorshanba','Payshanba','Juma','Shanba','Yakshanba'];
const DS=['Du','Se','Ch','Pa','Ju','Sh','Ya'];
const MONTHS=['Yanvar','Fevral','Mart','Aprel','May','Iyun','Iyul','Avgust','Sentabr','Oktabr','Noyabr','Dekabr'];

let students=JSON.parse(localStorage.getItem('darsproV3')||'[]');
let settings=JSON.parse(localStorage.getItem('darsproV3_set')||'{}');
settings={sound:'bell',vol:0.7,notif:true,theme:'dark',...settings};

let selDay=todayIdx();
let curTab='jadval';
let statMonth=new Date().getMonth();
let statYear=new Date().getFullYear();
let editId=null;
let altEnabled=false;
let remMin=5;
let payType='per_lesson';
let schRows=[];
let noted=new Set(JSON.parse(sessionStorage.getItem('darsproV3_noted')||'[]'));
let charts={};

function saveData(){localStorage.setItem('darsproV3',JSON.stringify(students));}
function saveSettings(){localStorage.setItem('darsproV3_set',JSON.stringify(settings));}

function todayIdx(){const d=new Date().getDay();return d===0?6:d-1;}
function nowMin(){const n=new Date();return n.getHours()*60+n.getMinutes();}
function toMin(t){const[h,m]=t.split(':').map(Number);return h*60+m;}
function todayKey(){const n=new Date();return`${n.getFullYear()}-${n.getMonth()+1}-${n.getDate()}`;}
function dateKeyFor(dayIdx){
  const now=new Date();
  const todayW=todayIdx();
  const diff=dayIdx-todayW;
  const target=new Date(now);
  target.setDate(now.getDate()+diff);
  return`${target.getFullYear()}-${target.getMonth()+1}-${target.getDate()}`;
}
function getWeekNum(date){
  const d=new Date(date);d.setHours(0,0,0,0);
  d.setDate(d.getDate()+4-(d.getDay()||7));
  const y=new Date(d.getFullYear(),0,1);
  return Math.ceil((((d-y)/86400000)+1)/7);
}
function isOddWeek(){return getWeekNum(new Date())%2===1;}

function getEffSched(s){
  const sch=s.schedule||[];
  const alt=s.altSchedule;
  if(!alt||!alt.enabled)return sch;
  if(isOddWeek()){
    const r=[...sch];
    if(r.length>0)r[0]={day:+alt.day,time:alt.time};
    return r;
  }
  return sch;
}

function getLessonsForDay(dayIdx){
  const res=[];
  students.forEach(s=>{
    getEffSched(s).forEach(sc=>{
      if(sc.day===dayIdx)res.push({s,time:sc.time});
    });
  });
  return res.sort((a,b)=>a.time.localeCompare(b.time));
}

function getStatus(s,date,time){
  const h=s.history&&s.history.find(x=>x.date===date&&x.time===time);
  return h?h.status:null;
}

function setStatus(sid,date,time,status){
  const s=students.find(x=>x.id===sid);if(!s)return;
  if(!s.history)s.history=[];
  s.history=s.history.filter(x=>!(x.date===date&&x.time===time));
  s.history.push({date,time,status});
  saveData();render();
}

function removeStatus(sid,date,time){
  const s=students.find(x=>x.id===sid);if(!s)return;
  if(!s.history)s.history=[];
  s.history=s.history.filter(x=>!(x.date===date&&x.time===time));
  saveData();render();
}

// ==================== SOUND ====================
const SOUNDS={
  bell:{icon:'🔔',name:"Qo'ng'iroq",desc:'Klassik signal'},
  chime:{icon:'🎵',name:'Chime',desc:'Yumshoq melodiya'},
  beep:{icon:'📳',name:'Beep',desc:'Oddiy signal'},
  ding:{icon:'✨',name:'Ding',desc:'Yumshoq ding'},
  alert:{icon:'🚨',name:'Alert',desc:"E'tibor tortuvchi"},
  soft:{icon:'🌙',name:'Yumshoq',desc:'Sokin ovoz'},
};

let audioCtx=null;
function getCtx(){if(!audioCtx)audioCtx=new(window.AudioContext||window.webkitAudioContext)();return audioCtx;}

function playSound(type,vol){
  try{
    const ctx=getCtx();
    const v=vol!==undefined?vol:settings.vol;
    const fns={
      bell:()=>{[523,659,784].forEach((f,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='sine';o.frequency.value=f;g.gain.setValueAtTime(v,ctx.currentTime+i*0.15);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+i*0.15+0.4);o.start(ctx.currentTime+i*0.15);o.stop(ctx.currentTime+i*0.15+0.45);});},
      chime:()=>{[523,784,1047,784,523].forEach((f,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='sine';o.frequency.value=f;g.gain.setValueAtTime(v*0.6,ctx.currentTime+i*0.12);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+i*0.12+0.3);o.start(ctx.currentTime+i*0.12);o.stop(ctx.currentTime+i*0.12+0.35);});},
      beep:()=>{[800,800,800].forEach((_,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='square';o.frequency.value=800;g.gain.setValueAtTime(v*0.3,ctx.currentTime+i*0.25);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+i*0.25+0.15);o.start(ctx.currentTime+i*0.25);o.stop(ctx.currentTime+i*0.25+0.18);});},
      ding:()=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='sine';o.frequency.setValueAtTime(1047,ctx.currentTime);o.frequency.exponentialRampToValueAtTime(800,ctx.currentTime+0.5);g.gain.setValueAtTime(v,ctx.currentTime);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+1.2);o.start(ctx.currentTime);o.stop(ctx.currentTime+1.3);},
      alert:()=>{[400,600,400,600].forEach((f,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='sawtooth';o.frequency.value=f;g.gain.setValueAtTime(v*0.4,ctx.currentTime+i*0.15);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+i*0.15+0.12);o.start(ctx.currentTime+i*0.15);o.stop(ctx.currentTime+i*0.15+0.14);});},
      soft:()=>{[392,494,587].forEach((f,i)=>{const o=ctx.createOscillator(),g=ctx.createGain();o.connect(g);g.connect(ctx.destination);o.type='sine';o.frequency.value=f;g.gain.setValueAtTime(0,ctx.currentTime+i*0.2);g.gain.linearRampToValueAtTime(v*0.4,ctx.currentTime+i*0.2+0.1);g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+i*0.2+0.6);o.start(ctx.currentTime+i*0.2);o.stop(ctx.currentTime+i*0.2+0.65);});}
    };
    if(fns[type])fns[type]();
  }catch(e){}
}

function updateVol(input){
  settings.vol=parseFloat(input.value);
  document.getElementById('volVal').textContent=Math.round(settings.vol*100)+'%';
  saveSettings();
  playSound(settings.sound,settings.vol);
}

function testNotif(){
  showBanner('⏰ Sinov','Ahmad','15:00 — 5 daqiqada');
  playSound(settings.sound);
}

function toggleNotif(){
  settings.notif=!settings.notif;
  const btn=document.getElementById('notifToggle');
  btn.classList.toggle('on',settings.notif);
  saveSettings();
}

// ==================== THEMES ====================
const THEMES={
  dark:{icon:'🌑',name:"Qorong'u",desc:'Default',bg:'#000',surface:'#1c1c1e',orange:'#ff9f0a'},
  midnight:{icon:'🌌',name:'Midnight',desc:'Ko\'k-qora',bg:'#0a0e1a',surface:'#141826',orange:'#5e9fff'},
  forest:{icon:'🌿',name:'Forest',desc:'Yashil',bg:'#0a1a0e',surface:'#132018',orange:'#4cd97b'},
  sunset:{icon:'🌅',name:'Sunset',desc:'Issiq',bg:'#1a0e00',surface:'#261800',orange:'#ff7f0a'},
};

function applyTheme(key){
  const t=THEMES[key]||THEMES.dark;
  document.documentElement.style.setProperty('--bg',t.bg);
  document.documentElement.style.setProperty('--surface',t.surface);
  document.documentElement.style.setProperty('--orange',t.orange);
}

// ==================== TABS ====================
function switchTab(t){
  curTab=t;
  ['jadval','stat','settings'].forEach(x=>{
    document.getElementById('tab-'+x)?.classList.toggle('active',x===t);
    document.getElementById('page-'+x).style.display=x===t?'':'none';
  });
  if(t==='stat')renderStats();
  if(t==='settings')renderSettings();
}

// ==================== RENDER ====================
function renderDayTabs(){
  const el=document.getElementById('dayScroll');el.innerHTML='';
  const today=todayIdx();
  DS.forEach((s,d)=>{
    const cnt=getLessonsForDay(d).length;
    const btn=document.createElement('button');
    btn.className='day-chip'+(d===selDay?' active':'')+(cnt>0?' has-l':'')+(d===today&&d!==selDay?' today-chip':'');
    btn.textContent=cnt>0&&d!==selDay?`${s} ${cnt}`:s;
    btn.onclick=()=>{selDay=d;renderDayTabs();renderLessons();};
    el.appendChild(btn);
  });
  const wi=document.getElementById('weekInfo');
  const today2=todayIdx();
  const odd=isOddWeek();
  if(selDay===today2){wi.textContent=`BUGUN — ${odd?'Toq':'Juft'} hafta`;}
  else{wi.textContent=DAYS[selDay].toUpperCase();}
}

function renderLessons(){
  const el=document.getElementById('lessonContent');
  const today=todayIdx();
  const now=nowMin();
  const dateKey=dateKeyFor(selDay);
  const items=getLessonsForDay(selDay);
  const odd=isOddWeek();

  if(!items.length){
    el.innerHTML=`<div class="empty-state"><div class="empty-icon">📭</div><div class="empty-text">${DAYS[selDay]} uchun dars yo'q</div></div>`;
    return;
  }

  el.innerHTML='';

  const active=items.filter(x=>!getStatus(x.s,dateKey,x.time));
  const done=items.filter(x=>getStatus(x.s,dateKey,x.time)==='done');
  const skipped=items.filter(x=>getStatus(x.s,dateKey,x.time)==='skipped');

  function makeGroup(arr,lbl){
    if(!arr.length)return;
    const sec=document.createElement('div');
    sec.innerHTML=`<div class="week-info" style="margin-top:8px">${lbl}</div>`;
    el.appendChild(sec);
    const list=document.createElement('div');
    list.className='lesson-list';
    arr.forEach(({s,time})=>{
      const status=getStatus(s,dateKey,time);
      const diff=toMin(time)-now;
      const isSoon=selDay===today&&!status&&diff<=(s.rem||5)&&diff>=0;
      const isDone=status==='done';
      const isSkip=status==='skipped';

      let subTxt='',subColor='var(--muted)';
      if(selDay===today&&!status){
        if(isSoon){subTxt=diff===0?'Hozir boshlanadi!':`${diff} daqiqada`;subColor='var(--orange)';}
        else if(diff>0&&diff<120){subTxt=`${diff} daqiqadan keyin`;}
        else if(diff<0&&diff>-60){subTxt='Hozir o\'tayotgan bo\'lishi mumkin';}
      }else if(isDone){
        const cnt=s.history?s.history.filter(h=>h.status==='done').length:0;
        subTxt=`✓ O'tildi • Jami: ${cnt} ta`;subColor='var(--green)';
      }else if(isSkip){subTxt='✗ Qoldirildi';subColor='var(--red)';}

      const hasAlt=s.altSchedule?.enabled;
      const barColor=isDone?'var(--green)':isSkip?'var(--red)':isSoon?'var(--orange)':'var(--blue)';

      const row=document.createElement('div');
      row.className=`lesson-row${isDone?' done-row':''}${isSkip?' done-row':''}`;
      let pt;
      row.addEventListener('touchstart',()=>{pt=setTimeout(()=>row.classList.add('show-del'),600);});
      row.addEventListener('touchend',()=>clearTimeout(pt));
      row.addEventListener('mouseleave',()=>row.classList.remove('show-del'));

      const cnt=s.history?s.history.filter(h=>h.status==='done').length:0;

      row.innerHTML=`
        <div class="lesson-left-bar" style="background:${barColor}"></div>
        <div class="lesson-time">${time}</div>
        <div class="lesson-info">
          <div class="lesson-name">${s.name}${hasAlt?`<span class="week-badge">${odd?'Toq':'Juft'}</span>`:''}</div>
          ${subTxt?`<div class="lesson-sub" style="color:${subColor}">${subTxt}</div>`:''}
        </div>
        <div class="row-right">
          <div class="toggle-col">
            <button class="toggle ${isDone?'on':''}" onclick="onToggle('${s.id}','${time}','${dateKey}','${status||''}')">
              <div class="toggle-knob"></div>
            </button>
            <div class="toggle-lbl">${isDone?"O'tildi":isSkip?"Qoldi":"O'tilmadi"}</div>
          </div>
          <button class="act-btn edit-btn-s" onclick="openModal('${s.id}')">✎</button>
          <button class="act-btn del-btn-s" onclick="delStudent('${s.id}')">✕</button>
        </div>`;
      list.appendChild(row);
    });
    el.appendChild(list);
  }

  makeGroup(active,selDay===today?'BUGUN':DAYS[selDay].toUpperCase());
  makeGroup(done,"O'TILGAN");
  makeGroup(skipped,'QOLDIRILGAN');
}

function onToggle(sid,time,dateKey,cur){
  if(cur==='done'||cur==='skipped'){
    showConfirm('↺','Qaytarish',"O'tilmagan deb belgilash?",[
      {label:'Ha',cls:'cf-yes',fn:()=>removeStatus(sid,dateKey,time)}
    ]);
  }else{
    showConfirm('📚',students.find(x=>x.id===sid)?.name||'',`${time} — dars holati?`,[
      {label:"✓ O'tildi",cls:'cf-yes',fn:()=>setStatus(sid,dateKey,time,'done')},
      {label:"✗ Qoldirildi",cls:'cf-skip',fn:()=>setStatus(sid,dateKey,time,'skipped')}
    ]);
  }
}

function delStudent(sid){
  showConfirm('🗑️',"O'chirish","Barcha ma'lumotlar o'chib ketadi!",[
    {label:"O'chirish",cls:'cf-skip',fn:()=>{students=students.filter(s=>s.id!==sid);saveData();render();}}
  ]);
}

// ==================== STATS ====================
function changeMonth(dir){
  statMonth+=dir;
  if(statMonth<0){statMonth=11;statYear--;}
  if(statMonth>11){statMonth=0;statYear++;}
  renderStats();
}

function destroyCharts(){Object.values(charts).forEach(c=>{try{c.destroy();}catch(e){}});charts={};}

function renderStats(){
  destroyCharts();
  document.getElementById('monthName').textContent=`${MONTHS[statMonth]} ${statYear}`;
  const el=document.getElementById('statsContent');
  if(!students.length){el.innerHTML=`<div class="empty-state"><div class="empty-icon">📊</div><div class="empty-text">Hali shogird yo'q</div></div>`;return;}
  el.innerHTML='';

  const nowD=new Date();
  const daysInMonth=new Date(statYear,statMonth+1,0).getDate();
  const upTo=statYear===nowD.getFullYear()&&statMonth===nowD.getMonth()?nowD.getDate():daysInMonth;

  let totalDone=0,totalSkipped=0,totalEarned=0;
  const monthlyDone=new Array(daysInMonth).fill(0);

  students.forEach(s=>{
    (s.history||[]).forEach(h=>{
      const[y,m,d]=h.date.split('-').map(Number);
      if(y===statYear&&m===statMonth+1){
        if(h.status==='done'){totalDone++;if(d>=1&&d<=daysInMonth)monthlyDone[d-1]++;totalEarned+=s.pricePerLesson||0;}
        if(h.status==='skipped')totalSkipped++;
      }
    });
  });

  // Summary
  const sr=document.createElement('div');sr.className='sum-row';
  sr.innerHTML=`
    <div class="sum-c"><div class="sum-v" style="color:var(--green)">${totalDone}</div><div class="sum-l">O'tildi</div></div>
    <div class="sum-c"><div class="sum-v" style="color:var(--red)">${totalSkipped}</div><div class="sum-l">Qoldirildi</div></div>
    <div class="sum-c"><div class="sum-v" style="color:var(--purple)">${students.length}</div><div class="sum-l">Shogird</div></div>`;
  el.appendChild(sr);

  // Salary
  if(totalEarned>0){
    const sal=document.createElement('div');sal.className='salary-card';
    sal.innerHTML=`<div class="salary-lbl">💰 ${MONTHS[statMonth]} — Oylik maosh</div><div class="salary-val">${totalEarned.toLocaleString()} so'm</div><div class="salary-sub">${totalDone} ta dars o'tildi • ${totalSkipped} ta qoldirildi</div>`;
    el.appendChild(sal);
  }

  // Line chart
  if(totalDone>0){
    const lc=document.createElement('div');lc.className='chart-c';
    lc.innerHTML=`<div class="chart-lbl">📈 OYLIK DINAMIKA</div><div class="chart-wrap"><canvas id="lChart"></canvas></div>`;
    el.appendChild(lc);
    setTimeout(()=>{
      const ctx=document.getElementById('lChart');if(!ctx)return;
      const labels=[],data=[];let cum=0;
      for(let i=0;i<upTo;i++){labels.push(`${i+1}`);cum+=monthlyDone[i];data.push(cum);}
      charts.line=new Chart(ctx,{type:'line',data:{labels,datasets:[{data,borderColor:'#30d158',backgroundColor:'rgba(48,209,88,0.08)',fill:true,tension:0.4,pointRadius:0,borderWidth:2}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{ticks:{color:'#8e8e93',font:{size:9}},grid:{color:'#38383a'}},y:{ticks:{color:'#8e8e93',font:{size:9}},grid:{color:'#38383a'},beginAtZero:true}}}});
    },100);
  }

  // Bar chart
  if(students.length>0){
    const bc=document.createElement('div');bc.className='chart-c';
    bc.innerHTML=`<div class="chart-lbl">📊 SHOGIRDLAR FAOLLIGI</div><div class="chart-wrap"><canvas id="bChart"></canvas></div>`;
    el.appendChild(bc);
    setTimeout(()=>{
      const ctx=document.getElementById('bChart');if(!ctx)return;
      const names=students.map(s=>s.name.split(' ')[0]);
      const dc=students.map(s=>(s.history||[]).filter(h=>{const[y,m]=h.date.split('-').map(Number);return y===statYear&&m===statMonth+1&&h.status==='done';}).length);
      const sc=students.map(s=>(s.history||[]).filter(h=>{const[y,m]=h.date.split('-').map(Number);return y===statYear&&m===statMonth+1&&h.status==='skipped';}).length);
      charts.bar=new Chart(ctx,{type:'bar',data:{labels:names,datasets:[{label:"O'tildi",data:dc,backgroundColor:'rgba(48,209,88,0.7)',borderRadius:5},{label:'Qoldirildi',data:sc,backgroundColor:'rgba(255,69,58,0.5)',borderRadius:5}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#8e8e93',font:{size:9},boxWidth:10}}},scales:{x:{ticks:{color:'#8e8e93',font:{size:9}},grid:{display:false}},y:{ticks:{color:'#8e8e93',font:{size:9}},grid:{color:'#38383a'},beginAtZero:true}}}});
    },200);
  }

  // Donut
  if(totalDone+totalSkipped>0){
    const dc=document.createElement('div');dc.className='chart-c';
    dc.innerHTML=`<div class="chart-lbl">🍩 NISBAT</div><div class="chart-wrap sm"><canvas id="dChart"></canvas></div>`;
    el.appendChild(dc);
    setTimeout(()=>{
      const ctx=document.getElementById('dChart');if(!ctx)return;
      charts.donut=new Chart(ctx,{type:'doughnut',data:{labels:["O'tildi",'Qoldirildi'],datasets:[{data:[totalDone,totalSkipped],backgroundColor:['rgba(48,209,88,0.8)','rgba(255,69,58,0.6)'],borderColor:['#1c1c1e'],borderWidth:2}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{labels:{color:'#8e8e93',font:{size:11},boxWidth:12}}}}});
    },300);
  }

  // Student cards
  students.forEach(s=>{
    const mh=(s.history||[]).filter(h=>{const[y,m]=h.date.split('-').map(Number);return y===statYear&&m===statMonth+1;});
    const done=mh.filter(h=>h.status==='done').length;
    const skipped=mh.filter(h=>h.status==='skipped').length;
    let planned=0;
    for(let d=1;d<=upTo;d++){
      const date=new Date(statYear,statMonth,d);
      const di=date.getDay()===0?6:date.getDay()-1;
      (s.schedule||[]).forEach(sc=>{if(sc.day===di)planned++;});
    }
    const pct=planned>0?Math.round(done/planned*100):0;
    const earnedPer=done*(s.pricePerLesson||0);
    const earnedMonthly=s.monthlyPrice||0;

    const card=document.createElement('div');card.className='stu-card';
    let payHtml='';
    if(s.pricePerLesson&&(s.paymentType==='per_lesson'||s.paymentType==='both')){
      payHtml+=`<div class="stu-row"><span class="stu-lbl">Dars to'lovi</span><span class="stu-val" style="color:var(--purple)">${earnedPer.toLocaleString()} so'm</span></div>`;
    }
    if(earnedMonthly&&(s.paymentType==='monthly'||s.paymentType==='both')){
      payHtml+=`<div class="stu-row"><span class="stu-lbl">Oylik to'lov</span><span class="stu-val" style="color:var(--purple)">${earnedMonthly.toLocaleString()} so'm</span></div>`;
    }
    card.innerHTML=`
      <div class="stu-name">${s.name}</div>
      <div class="stu-row"><span class="stu-lbl">O'tilgan</span><span class="stu-val" style="color:var(--green)">${done} ta</span></div>
      <div class="stu-row"><span class="stu-lbl">Qoldirilgan</span><span class="stu-val" style="color:var(--red)">${skipped} ta</span></div>
      <div class="stu-row"><span class="stu-lbl">Davomat</span><span class="stu-val" style="color:var(--orange)">${pct}%</span></div>
      <div class="prog-bar"><div class="prog-fill" style="width:${pct}%;background:${pct>=80?'var(--green)':pct>=50?'var(--orange)':'var(--red)'}"></div></div>
      ${payHtml?`<div class="stu-div"></div>${payHtml}`:''}`;
    el.appendChild(card);
  });
}

// ==================== SETTINGS ====================
function renderSettings(){
  // Sound list
  const sl=document.getElementById('soundList');sl.innerHTML='';
  Object.entries(SOUNDS).forEach(([key,s])=>{
    const item=document.createElement('div');
    item.className='sound-item'+(key===settings.sound?' selected':'');
    item.innerHTML=`<span class="sound-icon">${s.icon}</span><div class="sound-info"><div class="sound-name">${s.name}</div><div class="sound-desc">${s.desc}</div></div>${key===settings.sound?'<span class="sound-check">✓</span>':''}<button class="play-s" onclick="event.stopPropagation();playSound('${key}')">▶</button>`;
    item.onclick=()=>{settings.sound=key;saveSettings();renderSettings();playSound(key);};
    sl.appendChild(item);
  });

  // Volume
  document.getElementById('volRange').value=settings.vol;
  document.getElementById('volVal').textContent=Math.round(settings.vol*100)+'%';

  // Notif toggle
  document.getElementById('notifToggle').classList.toggle('on',settings.notif);

  // Themes
  const tg=document.getElementById('themeGrid');tg.innerHTML='';
  Object.entries(THEMES).forEach(([key,t])=>{
    const item=document.createElement('div');
    item.className='theme-item'+(key===settings.theme?' selected':'');
    item.innerHTML=`<span class="theme-icon">${t.icon}</span><div><div class="theme-name">${t.name}</div><div class="theme-desc">${t.desc}</div></div>`;
    item.onclick=()=>{settings.theme=key;saveSettings();applyTheme(key);renderSettings();};
    tg.appendChild(item);
  });

  document.getElementById('studentCount').textContent=students.length+' ta';
}

// ==================== MODAL ====================
function openModal(id){
  editId=id||null;
  altEnabled=false;
  schRows=[];
  remMin=5;
  payType='per_lesson';

  document.getElementById('modalTitleEl').textContent=id?'Tahrirlash':'Yangi shogird';
  document.getElementById('saveBtnM').textContent=id?'Saqlash':"Qo'shish";
  document.getElementById('mNote').value='';
  document.getElementById('mPrice').value='';
  document.getElementById('mMonthlyPrice').value='';
  document.getElementById('altContent').style.display='none';
  document.getElementById('altToggle').classList.remove('on');

  if(id){
    const s=students.find(x=>x.id===id);if(!s)return;
    document.getElementById('mName').value=s.name;
    document.getElementById('mNote').value=s.note||'';
    document.getElementById('mPrice').value=s.pricePerLesson||'';
    document.getElementById('mMonthlyPrice').value=s.monthlyPrice||'';
    remMin=s.rem||5;
    payType=s.paymentType||'per_lesson';
    schRows=(s.schedule||[]).map(sc=>({day:sc.day,time:sc.time}));
    if(s.altSchedule?.enabled){
      altEnabled=true;
      document.getElementById('altContent').style.display='';
      document.getElementById('altToggle').classList.add('on');
      document.getElementById('altDay').value=s.altSchedule.day;
      document.getElementById('altTime').value=s.altSchedule.time;
    }
  }else{
    document.getElementById('mName').value='';
    schRows=[{day:0,time:'09:00'}];
  }

  renderSchRows();
  updateRemBtns();
  updatePayBtns();
  updatePayFields();
  document.getElementById('modalBg').classList.add('open');
}

function closeModal(){document.getElementById('modalBg').classList.remove('open');editId=null;}
function modalBgClose(e){if(e.target===document.getElementById('modalBg'))closeModal();}

function addSchRow(){
  schRows.push({day:0,time:'09:00'});
  renderSchRows();
}

function renderSchRows(){
  const el=document.getElementById('schList');el.innerHTML='';
  schRows.forEach((sc,i)=>{
    const row=document.createElement('div');row.className='sch-row';
    row.innerHTML=`
      <select onchange="schRows[${i}].day=+this.value">
        ${DAYS.map((d,di)=>`<option value="${di}"${sc.day===di?' selected':''}>${d}</option>`).join('')}
      </select>
      <input type="time" class="m-input" style="width:90px;padding:6px 8px;" value="${sc.time}" oninput="schRows[${i}].time=this.value">
      ${schRows.length>1?`<button class="sch-remove" onclick="schRows.splice(${i},1);renderSchRows()">✕</button>`:''}`;
    el.appendChild(row);
  });
}

function toggleAlt(){
  altEnabled=!altEnabled;
  document.getElementById('altToggle').classList.toggle('on',altEnabled);
  document.getElementById('altContent').style.display=altEnabled?'':'none';
}

function pickRem(btn){
  document.querySelectorAll('.rem-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');remMin=+btn.dataset.v;
}

function updateRemBtns(){
  document.querySelectorAll('.rem-btn').forEach(b=>b.classList.toggle('active',+b.dataset.v===remMin));
}

function pickPay(btn){
  document.querySelectorAll('.pay-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');payType=btn.dataset.v;
  updatePayFields();
}

function updatePayBtns(){
  document.querySelectorAll('.pay-btn').forEach(b=>b.classList.toggle('active',b.dataset.v===payType));
  updatePayFields();
}

function updatePayFields(){
  document.getElementById('perLessonField').style.display=(payType==='per_lesson'||payType==='both')?'':'none';
  document.getElementById('monthlyField').style.display=(payType==='monthly'||payType==='both')?'':'none';
}

function saveStudent(){
  const name=document.getElementById('mName').value.trim();
  if(!name)return;
  if(!schRows.length){alert("Kamida 1 ta dars kuni!");return;}
  const schedule=schRows.map(r=>({day:+r.day,time:r.time}));
  const alt=altEnabled?{enabled:true,day:+document.getElementById('altDay').value,time:document.getElementById('altTime').value}:{enabled:false,day:0,time:'20:00'};
  const price=+document.getElementById('mPrice').value||0;
  const monthly=+document.getElementById('mMonthlyPrice').value||0;
  const note=document.getElementById('mNote').value.trim();

  if(editId){
    const s=students.find(x=>x.id===editId);
    if(s){s.name=name;s.schedule=schedule;s.altSchedule=alt;s.rem=remMin;s.pricePerLesson=price;s.monthlyPrice=monthly||null;s.paymentType=payType;s.note=note||null;}
  }else{
    students.push({id:Date.now().toString(),name,schedule,altSchedule:alt,rem:remMin,pricePerLesson:price,monthlyPrice:monthly||null,paymentType:payType,note:note||null,history:[]});
  }
  saveData();closeModal();render();
}

// ==================== CONFIRM ====================
function showConfirm(icon,title,sub,btns){
  document.getElementById('cfIcon').textContent=icon;
  document.getElementById('cfTitle').textContent=title;
  document.getElementById('cfSub').textContent=sub;
  const bc=document.getElementById('cfBtns');bc.innerHTML='';
  const cancel=document.createElement('button');
  cancel.className='cf-btn cf-cancel';cancel.textContent='Bekor';
  cancel.onclick=closeConfirm;bc.appendChild(cancel);
  btns.forEach(b=>{
    const btn=document.createElement('button');
    btn.className=`cf-btn ${b.cls}`;btn.textContent=b.label;
    btn.onclick=()=>{closeConfirm();b.fn();};
    bc.appendChild(btn);
  });
  document.getElementById('cfOverlay').classList.add('open');
}
function closeConfirm(){document.getElementById('cfOverlay').classList.remove('open');}

// ==================== NOTIFICATIONS ====================
function checkReminders(){
  if(!settings.notif)return;
  const today=todayIdx();const now=nowMin();const dateKey=todayKey();
  students.forEach(s=>{
    getEffSched(s).filter(sc=>sc.day===today).forEach(sc=>{
      const diff=toMin(sc.time)-now;
      const status=getStatus(s,dateKey,sc.time);

      // Before reminder
      const bk=`b_${s.id}_${sc.time}_${dateKey}`;
      if(diff<=(s.rem||5)&&diff>=0&&!noted.has(bk)&&!status){
        noted.add(bk);sessionStorage.setItem('darsproV3_noted',JSON.stringify([...noted]));
        playSound(settings.sound);
        showBanner('⏰ Dars eslatmasi',s.name,`${sc.time} — ${diff===0?'Hozir!':diff+' daqiqada'}`);
        if('Notification'in window&&Notification.permission==='granted')
          new Notification('⏰ Dars eslatmasi',{body:`${s.name} — ${sc.time}`});
      }

      // After 45 min
      const ak=`a_${s.id}_${sc.time}_${dateKey}`;
      if(diff<=-45&&diff>=-90&&!noted.has(ak)&&!status){
        noted.add(ak);sessionStorage.setItem('darsproV3_noted',JSON.stringify([...noted]));
        playSound('ding');
        showConfirm('📚',s.name,`${sc.time} — dars o'tdimi?`,[
          {label:"✓ O'tildi",cls:'cf-yes',fn:()=>setStatus(s.id,dateKey,sc.time,'done')},
          {label:"✗ Qoldirildi",cls:'cf-skip',fn:()=>setStatus(s.id,dateKey,sc.time,'skipped')}
        ]);
      }
    });
  });
}

function showBanner(title,name,time){
  const b=document.createElement('div');b.className='banner';
  b.innerHTML=`<div class="banner-title">${title}</div><div class="banner-name">${name}</div><div class="banner-time">${time}</div>`;
  document.body.appendChild(b);
  setTimeout(()=>b.remove(),7000);
}

// ==================== CLOCK ====================
function updateClock(){
  const n=new Date();
  const el=document.getElementById('clk');
  if(el)el.textContent=`${n.getHours().toString().padStart(2,'0')}:${n.getMinutes().toString().padStart(2,'0')}`;
}

// ==================== RENDER ALL ====================
function render(){
  renderDayTabs();
  renderLessons();
  if(curTab==='stat')renderStats();
  if(curTab==='settings')renderSettings();
}

// ==================== INIT ====================
if('Notification'in window&&Notification.permission==='default')Notification.requestPermission();
applyTheme(settings.theme);
render();
updateClock();
setInterval(updateClock,1000);
setInterval(()=>{checkReminders();if(curTab==='jadval')renderLessons();},60000);
checkReminders();
</script>
</body>
</html>
