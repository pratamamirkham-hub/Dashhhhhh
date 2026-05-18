<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Premium Dashboard PISA 2022 — Matematika</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg: #09090b;          /* Latar belakang sangat gelap */
  --surface: #18181b;     /* Warna card/panel */
  --surface2: #27272a;    /* Warna elemen hover/aksen */
  --border: #3f3f46;      /* Garis pemisah */
  --text: #f4f4f5;        /* Teks utama (putih terang) */
  --muted: #a1a1aa;       /* Teks redup */
  --subtle: #71717a;      /* Teks sangat redup */
  
  /* Palet Warna Modern */
  --blue: #3b82f6; 
  --green: #10b981; 
  --pink: #ec4899; 
  --amber: #f59e0b;
  --purple: #8b5cf6; 
  --teal: #14b8a6; 
  --red: #ef4444;
  --font: 'Plus Jakarta Sans', sans-serif;
}

body{background:var(--bg);color:var(--text);font-family:var(--font);min-height:100vh;overflow-x:hidden}

/* ── Layout & Sidebar ── */
.layout{display:flex;min-height:100vh}
.sidebar{width:250px;flex-shrink:0;background:var(--bg);border-right:1px solid rgba(255,255,255,0.08);
  display:flex;flex-direction:column;padding:24px 18px;gap:24px;position:sticky;top:0;height:100vh;overflow-y:auto}
.brand-logo{font-size:24px;font-weight:800;color:var(--text);letter-spacing:-0.5px}
.brand-logo span{color:var(--blue)}
.brand-sub{font-size:11px;color:var(--muted);margin-top:4px;font-weight:500;letter-spacing:0.5px;text-transform:uppercase}
.nav-group-label{font-size:10px;text-transform:uppercase;letter-spacing:1.5px;color:var(--subtle);margin-bottom:8px;padding-left:10px;font-weight:700;margin-top:10px}
.nav-btn{width:100%;text-align:left;background:transparent;border:none;color:var(--muted);
  font-family:var(--font);font-size:13px;font-weight:500;padding:12px 14px;border-radius:10px;cursor:pointer;
  display:flex;align-items:center;gap:10px;transition:all .25s ease;margin-bottom:4px}
.nav-btn:hover{background:rgba(255,255,255,0.05);color:var(--text);transform:translateX(4px)}
.nav-btn.active{background:linear-gradient(90deg, rgba(59,130,246,0.15) 0%, transparent 100%);color:var(--blue);font-weight:600;border-left:3px solid var(--blue)}
.dot{display:inline-block;width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── Main & Topbar (Glassmorphism) ── */
.main{flex:1;display:flex;flex-direction:column;min-width:0}
.topbar{position:sticky;top:0;z-index:50;background:rgba(9,9,11,0.7);backdrop-filter:blur(16px);
  border-bottom:1px solid rgba(255,255,255,0.08);padding:16px 28px;display:flex;align-items:center;justify-content:space-between}
.topbar-title{font-weight:700;font-size:17px;letter-spacing:-0.3px}

/* ── Content Sections ── */
.content{padding:28px;flex:1;position:relative;}
.section{display:none;animation:fadeIn .4s ease-out}.section.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(15px)}to{opacity:1;transform:translateY(0)}}

/* ── Metrics & Cards (Premium Gradients) ── */
.metrics{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:18px;margin-bottom:24px}
.metric{background:linear-gradient(145deg, var(--surface), rgba(39,39,42,0.4));border:1px solid rgba(255,255,255,0.06);
  border-radius:16px;padding:22px;position:relative;overflow:hidden;box-shadow:0 10px 15px -3px rgba(0,0,0,0.2)}
.metric::before{content:'';position:absolute;top:0;left:0;width:100%;height:3px}
.metric.m-blue::before{background:var(--blue)}
.metric.m-green::before{background:var(--green)}
.metric.m-pink::before{background:var(--pink)}
.metric.m-amber::before{background:var(--amber)}
.m-lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:10px;font-weight:700}
.m-val{font-size:36px;font-weight:800;line-height:1;letter-spacing:-1px}
.m-note{font-size:12px;color:var(--subtle);margin-top:8px;font-weight:500}

.card{background:var(--surface);border:1px solid rgba(255,255,255,0.06);border-radius:16px;padding:24px;margin-bottom:24px;
  box-shadow:0 4px 6px -1px rgba(0,0,0,0.1)}
.card-hd{margin-bottom:18px}
.card-title{font-size:16px;font-weight:700;color:var(--text);letter-spacing:-0.3px}
.card-desc{font-size:12px;color:var(--muted);margin-top:6px;font-weight:500}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:24px;margin-bottom:24px}

/* ── Tables ── */
.tbl-card{background:var(--surface);border:1px solid rgba(255,255,255,0.06);border-radius:16px;overflow:hidden;margin-bottom:24px}
.tbl-hd{display:flex;align-items:center;justify-content:space-between;padding:18px 24px;border-bottom:1px solid rgba(255,255,255,0.06);background:rgba(255,255,255,0.01)}
.tbl-title{font-size:15px;font-weight:700;letter-spacing:-0.3px}
.tbl-scroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:13px}
th{padding:14px 24px;text-align:left;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:0.8px;color:var(--muted);border-bottom:1px solid rgba(255,255,255,0.06);cursor:pointer;white-space:nowrap;transition:color .2s}
th:hover{color:var(--text)}
td{padding:12px 24px;border-bottom:1px solid rgba(255,255,255,0.03);color:var(--text);font-weight:500}
tr:hover td{background:rgba(255,255,255,0.02)}
.rtag{font-size:10px;font-weight:600;padding:4px 10px;border-radius:20px;background:var(--surface2);color:var(--muted);white-space:nowrap;letter-spacing:0.5px}
.badge{font-size:11px;font-weight:600;padding:4px 10px;border-radius:20px;white-space:nowrap}
.b-above{background:rgba(16,185,129,0.15);color:var(--green)}
.b-avg{background:rgba(245,158,11,0.12);color:var(--amber)}
.b-below{background:rgba(239,68,68,0.15);color:var(--red)}

/* ── Search UI & Profile ── */
.top-actions{display:flex;justify-content:flex-end;margin-bottom:24px}
.search-container{position:relative;width:100%;max-width:380px}
.search-input{width:100%;background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.1);color:var(--text);
  padding:14px 20px;border-radius:30px;font-size:13px;font-family:var(--font);font-weight:500;outline:none;transition:all .3s ease}
.search-input:focus{border-color:var(--blue);background:rgba(255,255,255,0.06);box-shadow:0 0 0 4px rgba(59,130,246,0.15)}
.search-results{position:absolute;top:100%;left:0;right:0;background:var(--surface);border:1px solid var(--border);
  border-radius:16px;margin-top:10px;max-height:280px;overflow-y:auto;z-index:100;display:none;box-shadow:0 20px 40px -10px rgba(0,0,0,0.5)}
.search-item{padding:14px 20px;cursor:pointer;font-size:13px;font-weight:500;border-bottom:1px solid rgba(255,255,255,0.04);display:flex;justify-content:space-between;align-items:center;transition:all .2s}
.search-item:hover{background:rgba(59,130,246,0.1);color:var(--blue)}

.profile-card{background:linear-gradient(180deg, var(--surface) 0%, rgba(24,24,27,0.9) 100%);border:1px solid rgba(255,255,255,0.08);
  border-radius:24px;padding:36px;display:none;animation:fadeIn .4s ease-out;box-shadow:0 20px 40px rgba(0,0,0,0.3)}
.btn-close{float:right;background:rgba(239,68,68,0.1);color:var(--red);border:1px solid rgba(239,68,68,0.2);
  padding:10px 18px;border-radius:10px;cursor:pointer;font-family:var(--font);font-size:12px;font-weight:700;transition:all .2s}
.btn-close:hover{background:var(--red);color:#fff}
.profile-header{display:flex;align-items:center;gap:24px;margin-bottom:32px;border-bottom:1px solid rgba(255,255,255,0.06);padding-bottom:28px;clear:both}
.profile-flag{width:70px;height:70px;border-radius:50%;background:rgba(59,130,246,0.1);display:flex;align-items:center;
  justify-content:center;font-size:30px;border:2px solid var(--blue);box-shadow:0 0 20px rgba(59,130,246,0.2)}
.profile-name{font-size:32px;font-weight:800;letter-spacing:-1px}
.profile-region{font-size:12px;font-weight:700;color:var(--blue);background:rgba(59,130,246,0.15);padding:6px 14px;border-radius:20px;display:inline-block;margin-top:8px;letter-spacing:0.5px}
.p-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px}
.p-box{background:rgba(255,255,255,0.02);padding:24px;border-radius:16px;border:1px solid rgba(255,255,255,0.05)}
.p-box-title{font-size:12px;text-transform:uppercase;margin-bottom:18px;font-weight:800;letter-spacing:1px}
.p-row{display:flex;justify-content:space-between;margin-bottom:12px;font-size:14px;font-weight:500;align-items:center}
.p-highlight{font-weight:800;font-size:26px;color:var(--text);letter-spacing:-0.5px}

@media(max-width:1000px){.grid-2,.p-grid{grid-template-columns:1fr} .sidebar{width:220px}}
@media(max-width:700px){.layout{flex-direction:column} .sidebar{width:100%;height:auto;position:relative;flex-direction:row;overflow-x:auto;padding:14px} .top-actions{justify-content:center} .metric{padding:18px}}
</style>
</head>
<body>
<div class="layout">

<aside class="sidebar">
  <div class="brand">
    <div class="brand-logo">PISA<span>·22</span></div>
    <div class="brand-sub">ANALYTICS DASHBOARD</div>
  </div>
  
  <div class="nav-group">
    <div class="nav-group-label">Performa & Tren</div>
    <button class="nav-btn active" onclick="switchTab('overview',this)"><span class="dot" style="background:var(--blue)"></span> Menu Utama</button>
    <button class="nav-btn" onclick="switchTab('trend',this)"><span class="dot" style="background:var(--teal)"></span> Tren '18-'22</button>
    <button class="nav-btn" onclick="switchTab('regional',this)"><span class="dot" style="background:var(--green)"></span> Kawasan</button>
    <button class="nav-btn" onclick="switchTab('data',this)"><span class="dot" style="background:var(--amber)"></span> Tabel 81 Negara</button>
  </div>

  <div class="nav-group">
    <div class="nav-group-label">Analisis Mendalam</div>
    <button class="nav-btn" onclick="switchTab('gender',this)"><span class="dot" style="background:var(--pink)"></span> Kesenjangan Gender</button>
    <button class="nav-btn" onclick="switchTab('socio',this)"><span class="dot" style="background:var(--red)"></span> Sosial Ekonomi</button>
    <button class="nav-btn" onclick="switchTab('time',this)"><span class="dot" style="background:var(--purple)"></span> Waktu Belajar</button>
  </div>
</aside>

<div class="main">
  <header class="topbar">
    <div class="topbar-title" id="page-title">Menu Utama PISA 2022</div>
  </header>

  <div class="content">
    
    <div class="section active" id="sec-overview">
      
      <div class="top-actions">
        <div class="search-container">
          <input type="text" id="search-input" class="search-input" placeholder="🔍 Cari profil negara (misal: Singapura, Jepang)..." autocomplete="off">
          <div class="search-results" id="search-results"></div>
        </div>
      </div>

      <div class="profile-card" id="country-profile">
        <button class="btn-close" onclick="closeProfile()">✕ Tutup Profil</button>
        <div class="profile-header">
          <div class="profile-flag" id="p-flag">🌍</div>
          <div>
            <div class="profile-name" id="p-name">Nama Negara</div>
            <div class="profile-region" id="p-region">Kawasan</div>
          </div>
        </div>

        <div class="p-grid">
          <div class="p-box">
            <div class="p-box-title" style="color:var(--blue)">Skor Matematika (2022)</div>
            <div class="p-row">
              <span>Skor Rata-rata:</span> 
              <span class="p-highlight" id="p-math">-</span>
            </div>
            <div class="p-row" style="margin-top:24px;padding-top:18px;border-top:1px dashed rgba(255,255,255,0.1);">
              <span style="color:var(--muted)">Tren vs 2018:</span> 
              <span id="p-math-trend" style="font-weight:800; font-size:16px">-</span>
            </div>
          </div>

          <div class="p-box">
            <div class="p-box-title" style="color:var(--pink)">Kesenjangan & Kesetaraan</div>
            <div class="p-row"><span>Skor Laki-laki:</span> <span style="font-weight:700" id="p-boy">-</span></div>
            <div class="p-row"><span>Skor Perempuan:</span> <span style="font-weight:700" id="p-girl">-</span></div>
            <div class="p-row" style="margin-bottom:14px;font-size:12px;color:var(--pink);font-weight:600" id="p-gender-gap">Gap Gender: -</div>
            
            <div class="p-row" style="padding-top:14px;border-top:1px solid rgba(255,255,255,0.05)"><span>Siswa Mampu:</span> <span style="font-weight:700" id="p-adv">-</span></div>
            <div class="p-row"><span>Siswa Kurang:</span> <span style="font-weight:700" id="p-dis">-</span></div>
            <div class="p-row" style="margin-bottom:0;font-size:12px;color:var(--amber);font-weight:600" id="p-socio-gap">Gap Sosial: -</div>
          </div>

          <div class="p-box">
            <div class="p-box-title" style="color:var(--green)">Waktu & Kebiasaan (Minggu)</div>
            <div class="p-row"><span>Total Belajar:</span> <span style="font-weight:700;color:var(--text)" id="p-learn">-</span></div>
            <div class="p-row"><span>Waktu Digital:</span> <span style="font-weight:700;color:var(--text)" id="p-digital">-</span></div>
            <div class="p-row" style="padding-top:14px;border-top:1px solid rgba(255,255,255,0.05)"><span>Waktu PR (Hari):</span> <span style="font-weight:700;color:var(--text)" id="p-hw">-</span></div>
          </div>
        </div>
      </div>

      <div id="overview-content">
        <div class="metrics">
          <div class="metric m-blue"><div class="m-lbl">Negara Dianalisis</div><div class="m-val" style="color:var(--text)">81</div><div class="m-note">Populasi PISA 2022</div></div>
          <div class="metric m-amber"><div class="m-lbl">Rata-rata OECD Math</div><div class="m-val">472</div><div class="m-note">Turun dari 489 (2018)</div></div>
          <div class="metric m-pink"><div class="m-lbl">Rata-rata Gap Global</div><div class="m-val">-11</div><div class="m-note">Poin kehilangan skor (Loss)</div></div>
          <div class="metric m-green"><div class="m-lbl">Waktu Belajar (Avg)</div><div class="m-val">34.6<span style="font-size:18px;font-weight:600">j</span></div><div class="m-note">Jam per minggu</div></div>
        </div>
        
        <div class="grid-2">
          <div class="card">
            <div class="card-hd"><div class="card-title">10 Negara Tertinggi (Matematika)</div><div class="card-desc">Peringkat teratas global tahun 2022</div></div>
            <div style="height:270px"><canvas id="c-top10math"></canvas></div>
          </div>
          <div class="card">
            <div class="card-hd"><div class="card-title">10 Negara Terendah (Matematika)</div><div class="card-desc">Peringkat terbawah global tahun 2022</div></div>
            <div style="height:270px"><canvas id="c-bottom10math"></canvas></div>
          </div>
        </div>

        <div class="grid-2">
          <div class="card">
            <div class="card-hd"><div class="card-title">Tren Historis OECD (2006–2022)</div><div class="card-desc">Penurunan drastis pasca-pandemi</div></div>
            <div style="height:260px"><canvas id="c-trend"></canvas></div>
          </div>
          <div class="card">
            <div class="card-hd"><div class="card-title">Distribusi Skor Matematika 2022 (81 Negara)</div><div class="card-desc">Garis kuning = Rata-rata OECD 2022 (472)</div></div>
            <div style="height:260px"><canvas id="c-allbar"></canvas></div>
          </div>
        </div>
      </div>
    </div>

    <div class="section" id="sec-trend">
      <div class="metrics">
        <div class="metric m-green"><div class="m-lbl">Negara Meningkat</div><div class="m-val" id="t-up">0</div><div class="m-note">Skor membaik dibanding 2018</div></div>
        <div class="metric m-red"><div class="m-lbl">Negara Menurun</div><div class="m-val" id="t-down">0</div><div class="m-note">Skor memburuk dibanding 2018</div></div>
        <div class="metric m-blue"><div class="m-lbl">Peningkatan Tertinggi</div><div class="m-val" id="t-best" style="font-size:28px">0</div><div class="m-note">Lompatan poin terbesar</div></div>
      </div>
      <div class="card">
        <div class="card-hd"><div class="card-title">Perubahan Skor Matematika (2018 ke 2022)</div><div class="card-desc">Mengabaikan negara tanpa data partisipasi 2018.</div></div>
        <div style="height:360px"><canvas id="c-gap-bar"></canvas></div>
      </div>
      <div class="tbl-card">
        <div class="tbl-hd"><div class="tbl-title">Detail Perubahan Tren Matematika</div></div>
        <div class="tbl-scroll">
          <table>
            <thead><tr><th>#</th><th>Negara</th><th>Kawasan</th><th>Skor 2018</th><th>Skor 2022</th><th>Gap</th><th>Status</th></tr></thead>
            <tbody id="tbody-trend"></tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="section" id="sec-regional">
      <div class="metrics">
        <div class="metric m-blue"><div class="m-lbl">Asia Timur</div><div class="m-val">529</div><div class="m-note">Kawasan Tertinggi (Avg 2022)</div></div>
        <div class="metric m-green"><div class="m-lbl">Eropa</div><div class="m-val">462</div><div class="m-note">Kawasan Terbesar (37 Negara)</div></div>
        <div class="metric m-amber"><div class="m-lbl">Amerika</div><div class="m-val">388</div><div class="m-note">Rata-rata 2022</div></div>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-hd"><div class="card-title">Rata-rata Skor per Kawasan</div><div class="card-desc">Tahun 2018 (Biru) vs 2022 (Merah)</div></div>
          <div style="height:290px"><canvas id="c-region-bar"></canvas></div>
        </div>
        <div class="card">
          <div class="card-hd"><div class="card-title">Sebaran Skor (Scatter) 2018 vs 2022</div><div class="card-desc">Titik di bawah diagonal = Penurunan skor</div></div>
          <div style="height:290px"><canvas id="c-scatter"></canvas></div>
        </div>
      </div>
    </div>

    <div class="section" id="sec-data">
      <div class="tbl-card">
        <div class="tbl-hd">
          <div class="tbl-title">Tabel Data Lengkap PISA Matematika (81 Negara)</div>
        </div>
        <div class="tbl-scroll">
          <table>
            <thead><tr>
              <th onclick="sortFull('rank')">Rank '22 ↕</th>
              <th onclick="sortFull('name')">Negara ↕</th>
              <th>Kawasan</th>
              <th onclick="sortFull('math18')">Math 2018 ↕</th>
              <th onclick="sortFull('math22')">Math 2022 ↕</th>
              <th onclick="sortFull('gap')">Perubahan ↕</th>
            </tr></thead>
            <tbody id="tbody-full"></tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="section" id="sec-gender">
      <div class="card">
        <div class="card-hd"><div class="card-title">Kesenjangan Skor Matematika (Laki-laki vs Perempuan)</div><div class="card-desc">Berdasarkan data kuesioner spesifik. Kanan (Biru): Laki-laki unggul. Kiri (Pink): Perempuan unggul.</div></div>
        <div style="height:520px"><canvas id="c-gender-gap"></canvas></div>
      </div>
    </div>

    <div class="section" id="sec-socio">
      <div class="card">
        <div class="card-hd"><div class="card-title">Kesenjangan Sosial Ekonomi (Matematika)</div><div class="card-desc">Perbandingan siswa mampu (Kuartil Atas - Hijau) vs kurang mampu (Kuartil Bawah - Merah)</div></div>
        <div style="height:520px"><canvas id="c-socio"></canvas></div>
      </div>
    </div>

    <div class="section" id="sec-time">
      <div class="grid-2">
        <div class="card">
          <div class="card-hd"><div class="card-title">Waktu Belajar vs Hiburan Digital (Jam/Minggu)</div><div class="card-desc">Korelasi antara waktu studi total dan durasi layar/gadget.</div></div>
          <div style="height:360px"><canvas id="c-time-scatter"></canvas></div>
        </div>
        <div class="card">
          <div class="card-hd"><div class="card-title">Waktu Mengerjakan PR (Jam/Hari)</div><div class="card-desc">Rata-rata waktu harian yang dilaporkan siswa.</div></div>
          <div style="height:360px"><canvas id="c-hw"></canvas></div>
        </div>
      </div>
    </div>

  </div>
</div>
</div>

<script>
// Setting Font Global ChartJS
Chart.defaults.font.family = "'Plus Jakarta Sans', sans-serif";
Chart.defaults.color = "#a1a1aa";

// ════ DATA MENTAH 81 NEGARA ════
const pisaRaw = [
  {name:"Australia", region:"Oseania", math18:491, math22:487},
  {name:"Austria", region:"Eropa", math18:499, math22:487},
  {name:"Belgium", region:"Eropa", math18:508, math22:489},
  {name:"Canada", region:"Amerika", math18:512, math22:497},
  {name:"Chile", region:"Amerika", math18:417, math22:412},
  {name:"Colombia", region:"Amerika", math18:391, math22:383},
  {name:"Costa Rica", region:"Amerika", math18:402, math22:385},
  {name:"Czech Republic", region:"Eropa", math18:499, math22:487},
  {name:"Denmark", region:"Eropa", math18:509, math22:489},
  {name:"Estonia", region:"Eropa", math18:523, math22:510},
  {name:"Finland", region:"Eropa", math18:507, math22:484},
  {name:"France", region:"Eropa", math18:495, math22:474},
  {name:"Germany", region:"Eropa", math18:500, math22:475},
  {name:"Greece", region:"Eropa", math18:451, math22:430},
  {name:"Hungary", region:"Eropa", math18:481, math22:473},
  {name:"Iceland", region:"Eropa", math18:495, math22:459},
  {name:"Ireland", region:"Eropa", math18:500, math22:492},
  {name:"Israel", region:"Timur Tengah & Afrika", math18:463, math22:458},
  {name:"Italy", region:"Eropa", math18:487, math22:471},
  {name:"Japan", region:"Asia Timur", math18:527, math22:536},
  {name:"Korea", region:"Asia Timur", math18:526, math22:527},
  {name:"Latvia", region:"Eropa", math18:496, math22:483},
  {name:"Lithuania", region:"Eropa", math18:481, math22:475},
  {name:"Mexico", region:"Amerika", math18:409, math22:395},
  {name:"Netherlands", region:"Eropa", math18:519, math22:493},
  {name:"New Zealand", region:"Oseania", math18:494, math22:479},
  {name:"Norway", region:"Eropa", math18:501, math22:468},
  {name:"Poland", region:"Eropa", math18:516, math22:489},
  {name:"Portugal", region:"Eropa", math18:492, math22:472},
  {name:"Slovak Republic", region:"Eropa", math18:486, math22:464},
  {name:"Slovenia", region:"Eropa", math18:509, math22:485},
  {name:"Spain", region:"Eropa", math18:481, math22:473},
  {name:"Sweden", region:"Eropa", math18:502, math22:482},
  {name:"Switzerland", region:"Eropa", math18:515, math22:508},
  {name:"Türkiye", region:"Timur Tengah & Afrika", math18:454, math22:453},
  {name:"United Kingdom", region:"Eropa", math18:502, math22:489},
  {name:"United States", region:"Amerika", math18:478, math22:465},
  {name:"Albania", region:"Eropa", math18:437, math22:368},
  {name:"Argentina", region:"Amerika", math18:379, math22:378},
  {name:"Baku (Azerbaijan)", region:"Timur Tengah & Afrika", math18:420, math22:397},
  {name:"Brazil", region:"Amerika", math18:384, math22:379},
  {name:"Brunei Darussalam", region:"Asia Tenggara", math18:430, math22:442},
  {name:"Bulgaria", region:"Eropa", math18:436, math22:417},
  {name:"Cambodia", region:"Asia Tenggara", math18:325, math22:336},
  {name:"Croatia", region:"Eropa", math18:464, math22:463},
  {name:"Cyprus", region:"Eropa", math18:451, math22:418},
  {name:"Dominican Republic", region:"Amerika", math18:325, math22:339},
  {name:"El Salvador", region:"Amerika", math18:null, math22:343},
  {name:"Georgia", region:"Timur Tengah & Afrika", math18:398, math22:390},
  {name:"Guatemala", region:"Amerika", math18:334, math22:344},
  {name:"Hong Kong (China)", region:"Asia Timur", math18:551, math22:540},
  {name:"Indonesia", region:"Asia Tenggara", math18:379, math22:366},
  {name:"Jamaica", region:"Amerika", math18:null, math22:377},
  {name:"Jordan", region:"Timur Tengah & Afrika", math18:400, math22:361},
  {name:"Kazakhstan", region:"Timur Tengah & Afrika", math18:423, math22:425},
  {name:"Kosovo", region:"Eropa", math18:366, math22:355},
  {name:"Macao (China)", region:"Asia Timur", math18:558, math22:552},
  {name:"Malaysia", region:"Asia Tenggara", math18:440, math22:409},
  {name:"Malta", region:"Eropa", math18:472, math22:466},
  {name:"Moldova", region:"Eropa", math18:421, math22:414},
  {name:"Mongolia", region:"Asia Timur", math18:null, math22:425},
  {name:"Montenegro", region:"Eropa", math18:430, math22:406},
  {name:"Morocco", region:"Timur Tengah & Afrika", math18:368, math22:365},
  {name:"North Macedonia", region:"Eropa", math18:394, math22:389},
  {name:"Palestinian Authority", region:"Timur Tengah & Afrika", math18:null, math22:366},
  {name:"Panama", region:"Amerika", math18:353, math22:357},
  {name:"Paraguay", region:"Amerika", math18:326, math22:338},
  {name:"Peru", region:"Amerika", math18:400, math22:391},
  {name:"Philippines", region:"Asia Tenggara", math18:353, math22:355},
  {name:"Qatar", region:"Timur Tengah & Afrika", math18:414, math22:414},
  {name:"Romania", region:"Eropa", math18:430, math22:428},
  {name:"Saudi Arabia", region:"Timur Tengah & Afrika", math18:373, math22:389},
  {name:"Serbia", region:"Eropa", math18:448, math22:440},
  {name:"Singapore", region:"Asia Tenggara", math18:569, math22:575},
  {name:"Chinese Taipei", region:"Asia Timur", math18:531, math22:547},
  {name:"Thailand", region:"Asia Tenggara", math18:419, math22:394},
  {name:"Ukrainian regions", region:"Eropa", math18:null, math22:441},
  {name:"United Arab Emirates", region:"Timur Tengah & Afrika", math18:435, math22:431},
  {name:"Uruguay", region:"Amerika", math18:418, math22:409},
  {name:"Uzbekistan", region:"Timur Tengah & Afrika", math18:null, math22:364},
  {name:"Viet Nam", region:"Asia Tenggara", math18:496, math22:469}
];

// ════ DATA ANALISIS DETAIL (Untuk menu mendalam) ════
const pisaDetail = [
  {name: "OECD Average", boy: 477, girl: 468, adv: 520, dis: 427, learn: 34.6, digital: 20.7, hw: 1.5},
  {name: "Singapura", boy: 580, girl: 570, adv: 620, dis: 510, learn: 42.1, digital: 22.5, hw: 2.1},
  {name: "Jepang", boy: 542, girl: 529, adv: 575, dis: 495, learn: 38.5, digital: 18.2, hw: 1.4},
  {name: "Korea", boy: 532, girl: 521, adv: 580, dis: 485, learn: 45.2, digital: 19.5, hw: 1.8},
  {name: "Estonia", boy: 512, girl: 508, adv: 545, dis: 475, learn: 36.4, digital: 21.3, hw: 1.6},
  {name: "Canada", boy: 503, girl: 491, adv: 535, dis: 455, learn: 32.5, digital: 23.4, hw: 1.3},
  {name: "United Kingdom", boy: 495, girl: 483, adv: 530, dis: 445, learn: 33.2, digital: 24.1, hw: 1.5},
  {name: "Australia", boy: 493, girl: 481, adv: 532, dis: 440, learn: 32.8, digital: 23.3, hw: 1.4},
  {name: "Finland", boy: 485, girl: 483, adv: 520, dis: 450, learn: 30.5, digital: 22.0, hw: 1.1},
  {name: "Germany", boy: 481, girl: 469, adv: 525, dis: 420, learn: 34.0, digital: 21.5, hw: 1.4},
  {name: "France", boy: 479, girl: 469, adv: 525, dis: 418, learn: 35.1, digital: 19.8, hw: 1.6},
  {name: "United States", boy: 471, girl: 459, adv: 515, dis: 410, learn: 33.8, digital: 25.0, hw: 1.4},
  {name: "Türkiye", boy: 455, girl: 451, adv: 495, dis: 415, learn: 39.2, digital: 19.2, hw: 1.9},
  {name: "Brunei Darussalam", boy: 438, girl: 446, adv: 480, dis: 405, learn: 38.0, digital: 21.5, hw: 1.8},
  {name: "United Arab Emirates", boy: 428, girl: 434, adv: 475, dis: 395, learn: 42.7, digital: 23.8, hw: 2.1},
  {name: "Malaysia", boy: 405, girl: 413, adv: 450, dis: 375, learn: 39.5, digital: 22.0, hw: 1.7},
  {name: "Mexico", boy: 401, girl: 389, adv: 435, dis: 360, learn: 34.5, digital: 19.4, hw: 1.3},
  {name: "Thailand", boy: 390, girl: 398, adv: 440, dis: 355, learn: 41.2, digital: 18.5, hw: 1.6},
  {name: "Brazil", boy: 384, girl: 374, adv: 425, dis: 340, learn: 33.0, digital: 24.5, hw: 1.2},
  {name: "Argentina", boy: 383, girl: 373, adv: 420, dis: 335, learn: 42.4, digital: 25.4, hw: 1.9},
  {name: "Albania", boy: 365, girl: 371, adv: 410, dis: 330, learn: 37.5, digital: 16.8, hw: 2.3},
  {name: "Indonesia", boy: 364, girl: 368, adv: 400, dis: 340, learn: 38.5, digital: 18.0, hw: 1.5},
  {name: "Philippines", boy: 350, girl: 360, adv: 395, dis: 325, learn: 39.0, digital: 17.5, hw: 1.6},
  {name: "Viet Nam", boy: 474, girl: 464, adv: 520, dis: 440, learn: 44.0, digital: 15.5, hw: 2.4},
  {name: "Uzbekistan", boy: 366, girl: 360, adv: 390, dis: 345, learn: 36.5, digital: 14.0, hw: 1.8}
];

// ════ PENGGABUNGAN DATA ════
const pisa = pisaRaw.map(r => {
  const detail = pisaDetail.find(d => d.name === r.name);
  const gap = r.math18 ? (r.math22 - r.math18) : null;
  return { ...r, ...detail, gap: gap };
});
pisa.sort((a,b)=>b.math22 - a.math22).forEach((d,i)=> d.rank = i+1);

const pisaWithOECD = [{name: "OECD Average", region: "Global", math18: 489, math22: 472, gap: -17, ...pisaDetail[0]}, ...pisa];

const regions = ['Asia Timur','Asia Tenggara','Eropa','Amerika','Oseania','Timur Tengah & Afrika'];
const regColors = {'Asia Timur':'#3b82f6','Asia Tenggara':'#14b8a6','Eropa':'#10b981','Amerika':'#f59e0b','Oseania':'#8b5cf6','Timur Tengah & Afrika':'#ec4899'};
const OECD_MATH_2022 = 472;

// ════ NAVIGASI TAB ════
const sections = ['overview','trend','regional','data','gender','socio','time'];
const titles = {
  'overview': 'Menu Utama PISA 2022',
  'trend': 'Tren PISA Matematika (2018-2022)',
  'regional': 'Analisis Antar Kawasan',
  'data': 'Database 81 Negara (Lengkap)',
  'gender': 'Analisis Kesenjangan Gender',
  'socio': 'Kesenjangan Sosial Ekonomi',
  'time': 'Waktu Belajar & Gadget'
};

function switchTab(id, btn){
  if(id === 'overview') closeProfile();
  sections.forEach(s => document.getElementById('sec-'+s).classList.remove('active'));
  document.getElementById('sec-'+id).classList.add('active');
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  if(btn) btn.classList.add('active');
  document.getElementById('page-title').innerText = titles[id];
}

// ════ TABEL 81 NEGARA ════
let fullSortKey='rank', fullSortDir='asc';
function renderFullTable(){
  let data = [...pisa];
  if(fullSortKey==='name') data.sort((a,b)=>fullSortDir==='asc'?a.name.localeCompare(b.name):b.name.localeCompare(a.name));
  else data.sort((a,b)=>fullSortDir==='asc'?(a[fullSortKey]||0)-(b[fullSortKey]||0):(b[fullSortKey]||0)-(a[fullSortKey]||0));
  
  const tb = document.getElementById('tbody-full');
  tb.innerHTML = data.map(d=>{
    const gapStr = d.gap === null ? `<span style="color:var(--muted)">N/A</span>` : (d.gap > 0 ? `<span style="color:var(--green)">+${d.gap}</span>` : d.gap < 0 ? `<span style="color:var(--red)">${d.gap}</span>` : `0`);
    const math18Str = d.math18 ? d.math18 : `<span style="color:var(--subtle)">N/A</span>`;
    return`<tr>
      <td>${d.rank}</td><td style="font-weight:700">${d.name}</td>
      <td><span class="rtag">${d.region}</span></td>
      <td style="color:var(--muted)">${math18Str}</td>
      <td style="font-weight:800;color:var(--blue);font-size:15px">${d.math22}</td>
      <td style="font-weight:700">${gapStr}</td>
    </tr>`;
  }).join('');
}
function sortFull(k){
  if(fullSortKey===k) fullSortDir=fullSortDir==='asc'?'desc':'asc';
  else{fullSortKey=k;fullSortDir='asc';}
  renderFullTable();
}

function renderTrendTable(){
  const data = pisa.filter(d=>d.gap !== null).sort((a,b)=>b.gap - a.gap);
  let up=0, down=0;
  data.forEach(d=>{ if(d.gap>0)up++; else if(d.gap<0)down++; });
  document.getElementById('t-up').innerText = up;
  document.getElementById('t-down').innerText = down;
  document.getElementById('t-best').innerText = `+${data[0].gap} (${data[0].name})`;
  
  const tb = document.getElementById('tbody-trend');
  tb.innerHTML = data.map((d,i)=>{
    const gapStr = d.gap > 0 ? `<span style="color:var(--green)">+${d.gap}</span>` : d.gap < 0 ? `<span style="color:var(--red)">${d.gap}</span>` : `0`;
    const status = d.gap > 0 ? '<span class="badge b-above">Naik</span>' : d.gap < 0 ? '<span class="badge b-below">Turun</span>' : '<span class="badge b-avg">Tetap</span>';
    return`<tr><td>${i+1}</td><td style="font-weight:600">${d.name}</td><td><span class="rtag">${d.region}</span></td><td>${d.math18}</td><td style="font-weight:700">${d.math22}</td><td style="font-weight:800;font-size:14px">${gapStr}</td><td>${status}</td></tr>`;
  }).join('');
}

// ════ RENDER CHARTS ════
const baseOpts = {
  responsive: true, maintainAspectRatio: false,
  plugins: { legend: { labels: { color: '#f4f4f5', font: {family: "'Plus Jakarta Sans', sans-serif"} } } },
  scales: { 
    x: { ticks: {color: '#a1a1aa', font: {weight: 500}}, grid: {display: false} }, 
    y: { ticks: {color: '#a1a1aa', font: {weight: 500}}, grid: {color: 'rgba(255,255,255,0.05)'} } 
  }
};

// 1. Overview (Top 10 dan Bottom 10)
const top10 = pisa.slice(0,10);
new Chart(document.getElementById('c-top10math'),{
  type:'bar',
  data:{ labels:top10.map(d=>d.name), datasets:[{ label:'Skor Math 2022', data:top10.map(d=>d.math22), backgroundColor:top10.map(d=>regColors[d.region]), borderRadius:6 }]},
  options:{...baseOpts, plugins:{legend:{display:false}}, scales:{x:{ticks:{color:'#a1a1aa',font:{size:10, weight: 600}},grid:{display:false}}, y:{min:480, ...baseOpts.scales.y}}}
});

const bottom10 = pisa.slice(-10);
new Chart(document.getElementById('c-bottom10math'),{
  type:'bar',
  data:{ labels:bottom10.map(d=>d.name), datasets:[{ label:'Skor Math 2022', data:bottom10.map(d=>d.math22), backgroundColor:bottom10.map(d=>regColors[d.region]), borderRadius:6 }]},
  options:{...baseOpts, plugins:{legend:{display:false}}, scales:{x:{ticks:{color:'#a1a1aa',font:{size:10, weight: 600},maxRotation:45},grid:{display:false}}, y:{min:300, ...baseOpts.scales.y}}}
});

new Chart(document.getElementById('c-trend'),{
  type:'line',
  data:{ labels:['2006','2009','2012','2015','2018','2022'], datasets:[{ label:'Rata-rata OECD', data:[498,496,494,490,489,472], borderColor:'#3b82f6', backgroundColor:'rgba(59,130,246,0.15)', borderWidth:3, tension:0.4, fill:true, pointRadius:6, pointBackgroundColor:'#fff', pointBorderColor:'#3b82f6', pointBorderWidth:2 }] },
  options:{...baseOpts, plugins:{legend:{display:false}}, scales:{x:baseOpts.scales.x, y:{min:460,...baseOpts.scales.y}}}
});

new Chart(document.getElementById('c-allbar'),{
  type:'bar',
  data:{ labels:pisa.map(d=>d.name), datasets:[
      {label:'Skor 2022', data:pisa.map(d=>d.math22), backgroundColor:pisa.map(d=>d.math22>=OECD_MATH_2022?'rgba(59,130,246,0.85)':'rgba(239,68,68,0.7)'), borderRadius:3},
      {label:'OECD Avg', type:'line', data:pisa.map(()=>OECD_MATH_2022), borderColor:'#f59e0b', borderDash:[5,4], borderWidth:2, pointRadius:0}
  ]},
  options:{...baseOpts, plugins:{legend:{display:false}}, scales:{x:{ticks:{display:false},grid:{display:false}}, y:{min:300,...baseOpts.scales.y}}}
});

// 2. Trend GAP
const gapSorted = pisa.filter(d=>d.gap !== null).sort((a,b)=>b.gap - a.gap);
new Chart(document.getElementById('c-gap-bar'),{
  type:'bar',
  data:{ labels:gapSorted.map(d=>d.name), datasets:[{ label:'Gap 2018-2022', data:gapSorted.map(d=>d.gap), backgroundColor:gapSorted.map(d=>d.gap>0?'#10b981':d.gap<0?'#ef4444':'#71717a'), borderRadius:4 }]},
  options:{...baseOpts, plugins:{legend:{display:false}}, scales:{x:{ticks:{color:'#a1a1aa',font:{size:9},maxRotation:90,minRotation:90}}, y:baseOpts.scales.y}}
});

// 3. Regional
new Chart(document.getElementById('c-region-bar'),{
  type:'bar',
  data:{ labels:regions, datasets:[
      {label:'2018', data:regions.map(r=>{const g=pisa.filter(d=>d.region===r && d.math18); return Math.round(g.reduce((s,d)=>s+d.math18,0)/g.length)||0}), backgroundColor:'rgba(59,130,246,0.4)', borderRadius:4},
      {label:'2022', data:regions.map(r=>{const g=pisa.filter(d=>d.region===r); return Math.round(g.reduce((s,d)=>s+d.math22,0)/g.length)||0}), backgroundColor:'#ef4444', borderRadius:4}
  ]},
  options:{...baseOpts, scales:{y:{min:350,...baseOpts.scales.y}}}
});

new Chart(document.getElementById('c-scatter'),{
  type:'scatter',
  data:{ datasets:regions.map(r=>({ label:r, data:pisa.filter(d=>d.region===r && d.math18).map(d=>({x:d.math18,y:d.math22,name:d.name})), backgroundColor:regColors[r], pointRadius:7, pointHoverRadius:9, borderColor:'rgba(255,255,255,0.2)', borderWidth:1 })) },
  options:{...baseOpts, plugins:{legend:{display:false},tooltip:{callbacks:{label:c=>`${c.raw.name} ('18: ${c.raw.x}, '22: ${c.raw.y})`}}}, scales:{x:{title:{display:true,text:'Skor 2018',color:'#a1a1aa'},...baseOpts.scales.x}, y:{title:{display:true,text:'Skor 2022',color:'#a1a1aa'},...baseOpts.scales.y}}}
});

// 4. Gender & Socio
const genderData = pisa.filter(d=>d.boy).sort((a,b)=> (b.boy - b.girl) - (a.boy - a.girl));
new Chart(document.getElementById('c-gender-gap'), {
  type: 'bar',
  data: { labels: genderData.map(d=>d.name), datasets: [{ label: 'Selisih Laki-laki - Perempuan', data: genderData.map(d => d.boy - d.girl), backgroundColor: genderData.map(d => (d.boy - d.girl) > 0 ? '#3b82f6' : '#ec4899'), borderRadius: 4 }] },
  options: { ...baseOpts, indexAxis: 'y', plugins: {legend: {display: false}} }
});

const socioData = pisa.filter(d=>d.adv).sort((a,b)=>b.math22-a.math22);
new Chart(document.getElementById('c-socio'), {
  type: 'bar',
  data: { labels: socioData.map(d=>d.name), datasets: [
      { label: 'Siswa Mampu', data: socioData.map(d=>d.adv), backgroundColor: '#10b981', borderRadius:4 },
      { label: 'Siswa Kurang Mampu', data: socioData.map(d=>d.dis), backgroundColor: '#ef4444', borderRadius:4 }
  ]},
  options: { ...baseOpts, scales: { y: { min: 300, ...baseOpts.scales.y } } }
});

// 5. Time 
new Chart(document.getElementById('c-time-scatter'), {
  type: 'scatter',
  data: { datasets: [{ label: 'Negara', data: pisa.filter(d=>d.learn).map(d=>({x: d.learn, y: d.digital, name: d.name})), backgroundColor: '#8b5cf6', pointRadius: 7, pointHoverRadius:9 }] },
  options: { ...baseOpts, plugins: { tooltip: { callbacks: { label: c => `${c.raw.name}: Belajar ${c.raw.x}j, Gadget ${c.raw.y}j` } } }, scales: { x: { title: {display:true, text:'Waktu Belajar Total (Jam/Minggu)'}, ...baseOpts.scales.x }, y: { title: {display:true, text:'Waktu Luang Digital (Jam/Minggu)'}, ...baseOpts.scales.y } } }
});

const hwData = pisa.filter(d=>d.hw).sort((a,b)=>b.hw-a.hw);
new Chart(document.getElementById('c-hw'), {
  type: 'bar',
  data: { labels: hwData.map(d=>d.name), datasets: [{ label: 'Waktu Mengerjakan PR (Jam/Hari)', data: hwData.map(d=>d.hw), backgroundColor: '#f59e0b', borderRadius: 5 }] },
  options: baseOpts
});

// ════ SEARCH LOGIC ════
const searchInput = document.getElementById('search-input');
const searchResults = document.getElementById('search-results');
const profileCard = document.getElementById('country-profile');
const overviewContent = document.getElementById('overview-content');

searchInput.addEventListener('input', function() {
  const val = this.value.toLowerCase();
  searchResults.innerHTML = '';
  if(!val) { searchResults.style.display = 'none'; return; }

  const matches = pisaWithOECD.filter(d => d.name.toLowerCase().includes(val));
  if(matches.length > 0) {
    searchResults.style.display = 'block';
    matches.forEach(m => {
      const div = document.createElement('div');
      div.className = 'search-item';
      div.innerHTML = `<span>${m.name}</span> <span style="font-size:10px;color:var(--muted);background:rgba(255,255,255,0.05);padding:2px 8px;border-radius:12px">${m.region}</span>`;
      div.onclick = () => selectCountry(m);
      searchResults.appendChild(div);
    });
  } else { searchResults.style.display = 'none'; }
});

function valStr(v, suffix=""){ return v !== undefined && v !== null ? v + suffix : '<span style="color:var(--subtle);font-weight:400;font-size:12px">N/A</span>'; }

function selectCountry(data) {
  searchInput.value = '';
  searchResults.style.display = 'none';
  overviewContent.style.display = 'none';
  profileCard.style.display = 'block';

  document.getElementById('p-name').innerText = data.name;
  document.getElementById('p-region').innerText = data.region;
  document.getElementById('p-flag').innerText = data.name === "OECD Average" ? "🌐" : "📍";
  
  document.getElementById('p-math').innerHTML = data.math22 + (data.rank ? `<span style="font-size:13px;color:var(--muted); font-weight:600;"> (Peringkat ${data.rank})</span>` : '');
  
  const trendStr = (data.gap !== null && data.gap !== undefined) ? (data.gap > 0 ? `+${data.gap} (Naik)` : data.gap < 0 ? `${data.gap} (Turun)` : "0 (Tetap)") : '<span style="color:var(--muted);font-size:13px;font-weight:500">Tidak Berpartisipasi di 2018</span>';
  document.getElementById('p-math-trend').innerHTML = trendStr;
  if(data.gap !== null) document.getElementById('p-math-trend').style.color = data.gap > 0 ? 'var(--green)' : data.gap < 0 ? 'var(--red)' : 'var(--muted)';

  document.getElementById('p-boy').innerHTML = valStr(data.boy);
  document.getElementById('p-girl').innerHTML = valStr(data.girl);
  document.getElementById('p-gender-gap').innerHTML = data.boy ? `Selisih: ${Math.abs(data.boy - data.girl)} poin (Unggul ${data.boy > data.girl ? 'Laki-laki' : 'Perempuan'})` : 'Data spesifik tidak tersedia';

  document.getElementById('p-adv').innerHTML = valStr(data.adv);
  document.getElementById('p-dis').innerHTML = valStr(data.dis);
  document.getElementById('p-socio-gap').innerHTML = data.adv ? `Kesenjangan Ekonomi: ${data.adv - data.dis} poin` : 'Data spesifik tidak tersedia';

  document.getElementById('p-learn').innerHTML = valStr(data.learn, " jam");
  document.getElementById('p-digital').innerHTML = valStr(data.digital, " jam");
  document.getElementById('p-hw').innerHTML = valStr(data.hw, " jam");
}

function closeProfile() {
  profileCard.style.display = 'none';
  overviewContent.style.display = 'block';
}

// Init
renderFullTable();
renderTrendTable();
</script>
</body>
</html>
