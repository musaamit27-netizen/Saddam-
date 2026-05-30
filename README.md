!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Radiology Association of India</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600;700&family=Outfit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;}
html,body{height:100%;font-family:'Outfit',sans-serif;background:#04091a;color:#e8f0ff;overflow:hidden;}

:root{
  --bg:#04091a;--card:rgba(8,18,40,0.92);--accent:#00b4ff;--gold:#ffcc44;
  --muted:#6a8aaa;--border:rgba(0,180,255,0.13);--danger:#ff4466;--success:#00e896;
  --white:#e8f0ff;
}

/* PARTICLE BG */
#bg-canvas{position:fixed;inset:0;z-index:0;pointer-events:none;}

/* GLOW ORBS */
.orb{position:fixed;border-radius:50%;filter:blur(80px);pointer-events:none;z-index:0;}
.orb1{width:400px;height:400px;background:radial-gradient(circle,rgba(0,100,200,0.18),transparent);top:-100px;left:-100px;animation:orbFloat1 12s ease-in-out infinite;}
.orb2{width:300px;height:300px;background:radial-gradient(circle,rgba(0,60,120,0.15),transparent);bottom:-80px;right:-80px;animation:orbFloat2 15s ease-in-out infinite;}
@keyframes orbFloat1{0%,100%{transform:translate(0,0);}50%{transform:translate(60px,40px);}}
@keyframes orbFloat2{0%,100%{transform:translate(0,0);}50%{transform:translate(-40px,-60px);}}

/* ── AUTH ── */
#auth-screen{
  position:fixed;inset:0;z-index:100;
  display:flex;align-items:center;justify-content:center;
}
.auth-box{
  background:rgba(6,14,32,0.95);
  border:1px solid var(--border);
  border-radius:24px;padding:36px 32px;
  width:92%;max-width:450px;
  box-shadow:0 32px 80px rgba(0,0,0,0.6),0 0 60px rgba(0,100,200,0.08);
  backdrop-filter:blur(20px);
  animation:fadeUp 0.6s ease;
  position:relative;z-index:2;
}
@keyframes fadeUp{from{opacity:0;transform:translateY(28px);}to{opacity:1;transform:none;}}

.logo{text-align:center;margin-bottom:28px;}
.logo-ic{
  width:72px;height:72px;margin:0 auto 14px;
  background:linear-gradient(135deg,rgba(0,140,220,0.2),rgba(0,60,140,0.35));
  border:1px solid rgba(0,180,255,0.3);border-radius:18px;
  display:flex;align-items:center;justify-content:center;font-size:30px;
  box-shadow:0 0 40px rgba(0,180,255,0.15);
  animation:pulse 3s ease-in-out infinite;
}
@keyframes pulse{0%,100%{box-shadow:0 0 40px rgba(0,180,255,0.15);}50%{box-shadow:0 0 60px rgba(0,180,255,0.35);}}
.logo h1{font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:600;line-height:1.3;}
.logo p{color:var(--muted);font-size:11px;letter-spacing:2px;text-transform:uppercase;margin-top:5px;}

.tabs{display:flex;background:rgba(255,255,255,0.04);border-radius:10px;padding:3px;margin-bottom:22px;}
.tab{flex:1;padding:9px;text-align:center;border-radius:7px;cursor:pointer;font-size:13px;font-weight:500;transition:all 0.2s;color:var(--muted);}
.tab.on{background:rgba(0,180,255,0.12);color:var(--accent);}

.fg{margin-bottom:13px;}
.fg label{display:block;font-size:10px;font-weight:600;letter-spacing:1px;text-transform:uppercase;color:var(--muted);margin-bottom:5px;}
.fg input{
  width:100%;padding:10px 13px;
  background:rgba(255,255,255,0.04);
  border:1px solid rgba(0,180,255,0.18);
  border-radius:10px;font-size:13px;
  font-family:'Outfit',sans-serif;color:var(--white);outline:none;
  transition:border-color 0.2s,box-shadow 0.2s;
}
.fg input:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(0,180,255,0.1);}
.fg input::placeholder{color:rgba(106,138,170,0.5);}
.frow{display:grid;grid-template-columns:1fr 1fr;gap:10px;}

.btn-main{
  width:100%;padding:12px;margin-top:4px;
  background:linear-gradient(135deg,rgba(0,160,240,0.85),rgba(0,60,160,0.9));
  border:1px solid rgba(0,180,255,0.4);
  border-radius:11px;font-size:14px;font-weight:600;
  cursor:pointer;font-family:'Outfit',sans-serif;color:white;
  transition:all 0.2s;letter-spacing:0.3px;
}
.btn-main:hover{transform:translateY(-1px);box-shadow:0 6px 24px rgba(0,180,255,0.25);}
.admin-note{text-align:center;margin-top:12px;font-size:11px;color:var(--muted);padding:8px;background:rgba(255,204,68,0.05);border-radius:8px;border:1px solid rgba(255,204,68,0.1);}

/* ── APP SHELL ── */
#app{position:fixed;inset:0;z-index:100;display:none;flex-direction:column;}

/* TOPNAV */
.tnav{
  height:58px;flex-shrink:0;
  background:rgba(4,9,26,0.9);border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
  padding:0 18px;backdrop-filter:blur(16px);
  position:relative;z-index:10;
}
.brand{display:flex;align-items:center;gap:10px;font-family:'Cormorant Garamond',serif;font-size:16px;font-weight:600;letter-spacing:0.5px;}
.brand-ic{width:34px;height:34px;background:linear-gradient(135deg,rgba(0,140,220,0.25),rgba(0,60,140,0.4));border:1px solid rgba(0,180,255,0.25);border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:15px;}
.nr{display:flex;align-items:center;gap:8px;position:relative;}
.nav-av{
  width:36px;height:36px;border-radius:50%;
  background:linear-gradient(135deg,var(--accent),#0050b4);
  display:flex;align-items:center;justify-content:center;
  font-weight:700;font-size:13px;cursor:pointer;
  border:1.5px solid rgba(0,180,255,0.3);overflow:hidden;
  transition:box-shadow 0.2s;
}
.nav-av:hover{box-shadow:0 0 20px rgba(0,180,255,0.3);}
.nav-av img{width:100%;height:100%;object-fit:cover;}
.tdot{
  width:34px;height:34px;border-radius:9px;
  background:rgba(255,255,255,0.05);border:1px solid var(--border);
  cursor:pointer;display:flex;align-items:center;justify-content:center;
  font-size:17px;color:var(--muted);transition:all 0.2s;
}
.tdot:hover{background:rgba(0,180,255,0.08);color:var(--accent);}

.dd{
  position:absolute;top:46px;right:0;
  background:rgba(5,12,30,0.98);border:1px solid var(--border);
  border-radius:14px;padding:6px;min-width:190px;
  box-shadow:0 12px 40px rgba(0,0,0,0.5);
  backdrop-filter:blur(16px);display:none;z-index:200;
}
.dd.on{display:block;animation:ddIn 0.15s ease;}
@keyframes ddIn{from{opacity:0;transform:translateY(-6px) scale(0.97);}to{opacity:1;transform:none;}}
.ddi{display:flex;align-items:center;gap:9px;padding:9px 12px;border-radius:8px;cursor:pointer;font-size:13px;color:var(--muted);transition:all 0.15s;}
.ddi:hover{background:rgba(0,180,255,0.07);color:var(--accent);}
.ddi.red{color:rgba(255,68,102,0.7);}
.ddi.red:hover{background:rgba(255,68,102,0.07);color:var(--danger);}
.ddiv{height:1px;background:var(--border);margin:5px 0;}

/* BODY AREA */
.app-body{flex:1;display:flex;overflow:hidden;min-height:0;}

/* SIDEBAR */
.sb{
  width:64px;flex-shrink:0;
  background:rgba(4,9,26,0.9);border-right:1px solid var(--border);
  display:flex;flex-direction:column;align-items:center;
  padding:16px 0;gap:4px;backdrop-filter:blur(16px);
  overflow-y:auto;
}
.sb::-webkit-scrollbar{display:none;}
.sbi{
  width:44px;height:44px;border-radius:12px;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;font-size:19px;transition:all 0.2s;
  color:var(--muted);position:relative;
}
.sbi:hover{background:rgba(0,180,255,0.08);color:var(--accent);}
.sbi.on{background:rgba(0,180,255,0.12);color:var(--accent);}
.sbi.on::before{content:'';position:absolute;left:-1px;top:10px;bottom:10px;width:3px;background:var(--accent);border-radius:0 3px 3px 0;}
.sbi-tip{
  position:absolute;left:54px;background:rgba(4,9,26,0.98);
  border:1px solid var(--border);padding:5px 10px;border-radius:7px;
  font-size:11px;font-weight:600;white-space:nowrap;
  pointer-events:none;opacity:0;transition:opacity 0.15s;color:var(--white);
  z-index:999;
}
.sbi:hover .sbi-tip{opacity:1;}

/* PAGES AREA */
.pages{flex:1;overflow-y:auto;overflow-x:hidden;padding:22px;position:relative;}
.pages::-webkit-scrollbar{width:4px;}
.pages::-webkit-scrollbar-thumb{background:rgba(0,180,255,0.15);border-radius:2px;}

/* PAGES */
.pg{display:none;}
.pg.on{display:block;animation:pgIn 0.35s ease;}
@keyframes pgIn{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:none;}}

/* SECTION TITLE */
.stitle{
  font-family:'Cormorant Garamond',serif;font-size:26px;font-weight:600;
  color:var(--white);margin-bottom:20px;display:flex;align-items:center;gap:12px;
}
.stitle::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,rgba(0,180,255,0.25),transparent);}

/* GLASS CARD */
.gc{
  background:rgba(6,14,34,0.85);border:1px solid var(--border);
  border-radius:18px;padding:22px;margin-bottom:18px;
  backdrop-filter:blur(10px);
  transition:border-color 0.25s;
}
.gc:hover{border-color:rgba(0,180,255,0.22);}

/* WELCOME */
.wb{
  background:linear-gradient(135deg,rgba(0,30,70,0.9),rgba(0,10,30,0.95));
  border:1px solid rgba(0,180,255,0.18);border-radius:20px;
  padding:28px;margin-bottom:18px;position:relative;overflow:hidden;
}
.wb-glow{position:absolute;top:-30px;right:-30px;width:160px;height:160px;background:radial-gradient(circle,rgba(0,180,255,0.12),transparent 70%);border-radius:50%;animation:pulse 4s ease-in-out infinite;}
.wb-xr{position:absolute;right:22px;top:50%;transform:translateY(-50%);font-size:64px;opacity:0.07;animation:floatY 6s ease-in-out infinite;}
@keyframes floatY{0%,100%{transform:translateY(-50%);}50%{transform:translateY(-55%);}}
.wb h2{font-family:'Cormorant Garamond',serif;font-size:23px;font-weight:600;margin-bottom:6px;}
.wb p{color:var(--muted);font-size:13px;}
.wb-badge{display:inline-block;margin-top:12px;padding:4px 14px;background:rgba(0,180,255,0.1);border:1px solid rgba(0,180,255,0.22);border-radius:20px;font-size:11px;font-weight:600;color:var(--accent);letter-spacing:0.5px;}

/* STATS */
.sg{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:18px;}
.sc{background:rgba(6,14,34,0.85);border:1px solid var(--border);border-radius:16px;padding:18px;text-align:center;transition:all 0.25s;cursor:default;}
.sc:hover{border-color:rgba(0,180,255,0.3);transform:translateY(-3px);}
.sc-n{font-family:'Cormorant Garamond',serif;font-size:34px;font-weight:700;color:var(--accent);line-height:1;}
.sc-l{font-size:10px;color:var(--muted);margin-top:5px;text-transform:uppercase;letter-spacing:0.5px;}

/* ACTION CARDS */
.ag{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:18px;}
.ac{border-radius:18px;padding:22px;cursor:pointer;border:1px solid transparent;position:relative;overflow:hidden;transition:all 0.25s;}
.ac:hover{transform:translateY(-4px);}
.ac.wa{background:linear-gradient(135deg,rgba(37,211,102,0.15),rgba(18,140,126,0.22));border-color:rgba(37,211,102,0.25);}
.ac.wa:hover{box-shadow:0 12px 36px rgba(37,211,102,0.15);}
.ac.jb{background:linear-gradient(135deg,rgba(0,100,200,0.15),rgba(0,50,120,0.22));border-color:rgba(0,180,255,0.22);}
.ac.jb:hover{box-shadow:0 12px 36px rgba(0,180,255,0.15);}
.ac-ic{font-size:32px;margin-bottom:8px;display:block;}
.ac-t{font-size:14px;font-weight:700;margin-bottom:3px;}
.ac-d{font-size:11px;color:var(--muted);}

/* MEMBER ROW */
.mr{display:flex;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid rgba(0,180,255,0.07);transition:padding 0.2s;}
.mr:hover{padding-left:6px;}
.mr:last-child{border-bottom:none;}
.mav{width:40px;height:40px;border-radius:50%;flex-shrink:0;background:linear-gradient(135deg,rgba(0,140,220,0.25),rgba(0,50,120,0.4));display:flex;align-items:center;justify-content:center;font-weight:700;font-size:14px;overflow:hidden;border:1px solid rgba(0,180,255,0.18);}
.mav img{width:100%;height:100%;object-fit:cover;}
.mi h4{font-size:13px;font-weight:600;}
.mi p{font-size:11px;color:var(--muted);}
.mtag{margin-left:auto;padding:3px 10px;border-radius:20px;font-size:10px;font-weight:600;background:rgba(0,180,255,0.07);color:var(--accent);border:1px solid rgba(0,180,255,0.13);white-space:nowrap;}

/* PROFILE */
.ph{background:linear-gradient(135deg,rgba(0,24,60,0.92),rgba(0,8,26,0.96));border:1px solid rgba(0,180,255,0.18);border-radius:20px;padding:30px;text-align:center;margin-bottom:18px;position:relative;overflow:hidden;}
.ph-ring{position:absolute;top:50%;left:50%;width:260px;height:260px;transform:translate(-50%,-50%);border-radius:50%;border:1px solid rgba(0,180,255,0.06);animation:pulse 4s ease-in-out infinite;}
.pw{position:relative;width:100px;height:100px;margin:0 auto 16px;}
.pp{width:100px;height:100px;border-radius:50%;background:linear-gradient(135deg,rgba(0,140,220,0.2),rgba(0,50,120,0.4));display:flex;align-items:center;justify-content:center;font-size:36px;font-weight:700;border:2px solid rgba(0,180,255,0.25);overflow:hidden;cursor:pointer;box-shadow:0 0 28px rgba(0,180,255,0.15);transition:box-shadow 0.2s;position:relative;z-index:1;}
.pp:hover{box-shadow:0 0 44px rgba(0,180,255,0.3);}
.pp img{width:100%;height:100%;object-fit:cover;}
.pe{position:absolute;bottom:3px;right:3px;width:28px;height:28px;background:var(--gold);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;cursor:pointer;border:2px solid #04091a;z-index:2;}
.pname{font-family:'Cormorant Garamond',serif;font-size:22px;font-weight:600;margin-bottom:3px;}
.psub{color:var(--muted);font-size:12px;}
.apill{display:inline-block;margin-top:8px;padding:3px 12px;background:rgba(255,204,68,0.12);border:1px solid rgba(255,204,68,0.25);border-radius:20px;font-size:10px;font-weight:700;color:var(--gold);letter-spacing:1px;text-transform:uppercase;}

.dg{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.db{background:rgba(0,180,255,0.04);border:1px solid var(--border);border-radius:12px;padding:12px;}
.db label{font-size:9px;text-transform:uppercase;letter-spacing:1px;color:var(--muted);font-weight:600;}
.db p{font-size:14px;font-weight:500;color:var(--white);margin-top:3px;}

/* JOB CARD */
.jc{background:rgba(6,14,34,0.85);border:1px solid var(--border);border-radius:16px;padding:20px;margin-bottom:12px;position:relative;overflow:hidden;transition:all 0.25s;}
.jc::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:linear-gradient(180deg,var(--accent),transparent);}
.jc:hover{border-color:rgba(0,180,255,0.28);transform:translateX(3px);}
.jt{font-size:15px;font-weight:700;margin-bottom:3px;}
.jh{font-size:12px;color:var(--accent);font-weight:500;margin-bottom:8px;}
.jtags{display:flex;gap:7px;flex-wrap:wrap;}
.jtag{background:rgba(0,180,255,0.06);border:1px solid rgba(0,180,255,0.12);color:var(--muted);font-size:10px;padding:3px 9px;border-radius:20px;font-weight:500;}

/* BUTTONS */
.btn{padding:9px 18px;border-radius:10px;font-size:12px;font-weight:600;cursor:pointer;font-family:'Outfit',sans-serif;transition:all 0.2s;display:inline-flex;align-items:center;gap:5px;letter-spacing:0.3px;border:none;}
.btn-gl{background:linear-gradient(135deg,rgba(0,160,240,0.7),rgba(0,60,160,0.85));border:1px solid rgba(0,180,255,0.35);color:white;}
.btn-gl:hover{transform:translateY(-1px);box-shadow:0 6px 20px rgba(0,180,255,0.2);}
.btn-ol{background:transparent;border:1px solid rgba(0,180,255,0.25);color:var(--accent);}
.btn-ol:hover{background:rgba(0,180,255,0.07);}
.btn-gd{background:linear-gradient(135deg,rgba(255,204,68,0.8),rgba(200,130,10,0.9));border:1px solid rgba(255,204,68,0.35);color:#04091a;}
.btn-gd:hover{box-shadow:0 6px 20px rgba(255,204,68,0.18);}
.btn-rd{background:rgba(255,68,102,0.12);border:1px solid rgba(255,68,102,0.25);color:var(--danger);}
.btn-rd:hover{background:rgba(255,68,102,0.2);}
.btn-fw{width:100%;justify-content:center;padding:12px;}

/* GALLERY */
.gg{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:10px;}
.gi{aspect-ratio:1;border-radius:12px;background:rgba(6,14,34,0.85);border:1px solid var(--border);overflow:hidden;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;color:var(--muted);font-size:11px;transition:all 0.25s;position:relative;}
.gi:hover{border-color:rgba(0,180,255,0.35);transform:scale(1.03);}
.gi img{width:100%;height:100%;object-fit:cover;position:absolute;inset:0;}

/* SOCIAL */
.socg{display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:10px;}
.socb{border-radius:14px;padding:18px 8px;text-align:center;cursor:pointer;font-weight:600;font-size:11px;transition:all 0.22s;border:1px solid rgba(255,255,255,0.08);display:flex;flex-direction:column;align-items:center;gap:7px;letter-spacing:0.3px;}
.socb:hover{transform:translateY(-3px);}
.socb .si{font-size:24px;}

/* ADMIN TABLE */
.at{width:100%;border-collapse:collapse;font-size:11px;}
.at th{background:rgba(0,180,255,0.07);color:var(--muted);padding:10px;text-align:left;font-size:9px;text-transform:uppercase;letter-spacing:0.8px;border-bottom:1px solid var(--border);}
.at td{padding:10px;border-bottom:1px solid rgba(0,180,255,0.05);color:var(--white);}
.at tr:hover td{background:rgba(0,180,255,0.03);}

/* MODAL */
.mo{display:none;position:fixed;inset:0;z-index:500;background:rgba(2,5,15,0.82);backdrop-filter:blur(6px);align-items:center;justify-content:center;}
.mo.on{display:flex;animation:moIn 0.18s ease;}
@keyframes moIn{from{opacity:0;}to{opacity:1;}}
.md{background:rgba(5,12,30,0.98);border:1px solid var(--border);border-radius:22px;padding:28px;width:92%;max-width:480px;max-height:88vh;overflow-y:auto;box-shadow:0 28px 70px rgba(0,0,0,0.55);animation:mdIn 0.28s cubic-bezier(0.16,1,0.3,1);}
@keyframes mdIn{from{opacity:0;transform:scale(0.93) translateY(18px);}to{opacity:1;transform:none;}}
.md h3{font-family:'Cormorant Garamond',serif;font-size:20px;color:var(--white);margin-bottom:18px;}
.mc{float:right;cursor:pointer;font-size:19px;color:var(--muted);transition:color 0.15s;line-height:1;}
.mc:hover{color:var(--accent);}
.md::-webkit-scrollbar{width:3px;}
.md::-webkit-scrollbar-thumb{background:rgba(0,180,255,0.18);}
.md textarea{width:100%;padding:10px 13px;background:rgba(255,255,255,0.04);border:1px solid rgba(0,180,255,0.18);border-radius:10px;font-size:13px;font-family:'Outfit',sans-serif;color:var(--white);outline:none;resize:vertical;}
.md textarea:focus{border-color:var(--accent);}

/* TOAST */
.toast{position:fixed;bottom:22px;right:22px;z-index:9999;background:rgba(5,12,30,0.97);border:1px solid var(--border);color:var(--white);padding:12px 20px;border-radius:12px;font-size:13px;display:none;box-shadow:0 8px 28px rgba(0,0,0,0.35);backdrop-filter:blur(12px);}
.toast.on{display:block;animation:fadeUp 0.25s ease;}

/* ABOUT */
.abt{font-size:13px;line-height:2;color:rgba(232,240,255,0.8);white-space:pre-wrap;}

/* HIDDEN */
.hidden{display:none!important;}
input[type="file"]{display:none;}

@media(max-width:580px){
  .sg{grid-template-columns:1fr 1fr;}
  .ag{grid-template-columns:1fr;}
  .frow,.dg{grid-template-columns:1fr;}
  .sb{width:52px;}
  .pages{padding:14px;}
}
</style>
</head>
<body>

<!-- BG ORBS -->
<div class="orb orb1"></div>
<div class="orb orb2"></div>

<!-- CANVAS BG -->
<canvas id="bg-canvas"></canvas>

<!-- ═══ AUTH ═══ -->
<div id="auth-screen">
  <div class="auth-box">
    <div class="logo">
      <div class="logo-ic">🩻</div>
      <h1>Radiology Association<br>of India</h1>
      <p>Professional Medical Network</p>
    </div>
    <div class="tabs">
      <div class="tab on" onclick="swTab('login')">Login</div>
      <div class="tab" onclick="swTab('reg')">Register</div>
    </div>

    <div id="lf">
      <div class="fg"><label>Mobile Number</label><input type="tel" id="lm" placeholder="Mobile number" maxlength="10"></div>
      <div class="fg"><label>Password</label><input type="password" id="lp" placeholder="Password"></div>
      <button class="btn-main" onclick="doLogin()">Access Portal</button>
      <div class="admin-note">Admin → mobile: <strong>admin</strong> | pass: <strong>admin123</strong></div>
    </div>

    <div id="rf" class="hidden">
      <div class="fg"><label>Full Name</label><input type="text" id="rn" placeholder="Dr. Full Name"></div>
      <div class="frow">
        <div class="fg"><label>Age</label><input type="number" id="ra" placeholder="Age" min="