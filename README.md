<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
<title>Petualangan: Jadi Dokter Spesialis — Media Pembelajaran IPA SMP</title>
<meta name="description" content="Media pembelajaran interaktif sistem organ tubuh manusia untuk SMP. Oleh Salehuddin, Guru SMP Negeri Sinombayuga." />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@500;600;700;800&family=Plus+Jakarta+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
<style>
/* ============================================================
   TOKEN SISTEM — "Monitor Vital" / RPG Medis
   ============================================================ */
:root{
  --bg-0:#05222C;
  --bg-1:#0A3340;
  --bg-2:#0E4356;
  --panel:#0C3543;
  --panel-2:#0F3F4F;
  --paper:#F2FBFA;            /* kartu materi terang */
  --ink:#0A2730;             /* teks pada kartu terang */
  --ink-dim:#3C5A63;
  --line:rgba(120,230,235,.16);
  --line-strong:rgba(120,230,235,.34);
  --text:#E9FCFC;
  --text-dim:rgba(233,252,252,.62);
  --text-mut:rgba(233,252,252,.40);

  --cyan:#34E0E8;
  --cyan-deep:#13A7B4;
  --digest:#F6A609;          /* pencernaan */
  --circ:#FB4D63;            /* peredaran darah */
  --resp:#3FB6F5;            /* pernapasan */
  --gold:#FCD34D;
  --good:#34E3B0;
  --bad:#FF6B82;

  --font-d:'Sora',system-ui,sans-serif;
  --font-b:'Plus Jakarta Sans',system-ui,sans-serif;
  --font-m:'JetBrains Mono',ui-monospace,monospace;

  --r-s:12px; --r-m:18px; --r-l:26px;
  --shadow:0 18px 50px -22px rgba(0,0,0,.7);
  --maxw:1120px;
}

*{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%}
body{
  font-family:var(--font-b);
  color:var(--text);
  background:var(--bg-0);
  line-height:1.6;
  min-height:100vh;
  min-height:100dvh;
  overflow-x:hidden;
  position:relative;
}
/* atmosfer latar */
body::before{
  content:"";position:fixed;inset:0;z-index:-2;
  background:
    radial-gradient(1100px 700px at 82% -10%, rgba(63,182,245,.16), transparent 60%),
    radial-gradient(900px 650px at 8% 8%, rgba(52,224,232,.13), transparent 60%),
    radial-gradient(800px 600px at 60% 120%, rgba(251,77,99,.10), transparent 60%),
    linear-gradient(160deg, var(--bg-0), var(--bg-1) 55%, #07303C);
}
body::after{
  content:"";position:fixed;inset:0;z-index:-1;pointer-events:none;opacity:.5;
  background-image:linear-gradient(rgba(120,230,235,.05) 1px,transparent 1px),
                   linear-gradient(90deg,rgba(120,230,235,.05) 1px,transparent 1px);
  background-size:42px 42px;
  -webkit-mask-image:radial-gradient(circle at 50% 30%, #000 0%, transparent 78%);
          mask-image:radial-gradient(circle at 50% 30%, #000 0%, transparent 78%);
}

button{font-family:inherit;cursor:pointer;border:none;background:none;color:inherit}
input{font-family:inherit}
:focus-visible{outline:3px solid var(--cyan);outline-offset:3px;border-radius:6px}

/* ============================================================
   HEADER MONITOR
   ============================================================ */
.monitor{
  position:sticky;top:0;z-index:40;
  display:none;align-items:center;gap:16px;flex-wrap:wrap;
  padding:10px clamp(12px,3vw,26px);
  background:linear-gradient(180deg, rgba(8,40,50,.92), rgba(8,40,50,.7));
  backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);
  border-bottom:1px solid var(--line);
}
body.started .monitor{display:flex}
.monitor__brand{display:flex;align-items:center;gap:10px;min-width:0}
.monitor__logo{
  width:38px;height:38px;flex:0 0 auto;border-radius:11px;
  display:grid;place-items:center;color:#04222B;
  background:linear-gradient(135deg,var(--cyan),var(--cyan-deep));
  box-shadow:0 0 18px rgba(52,224,232,.5);
}
.monitor__logo svg{width:22px;height:22px}
.monitor__title{font-family:var(--font-d);font-weight:800;font-size:.82rem;letter-spacing:.02em;line-height:1.15}
.monitor__title b{color:var(--cyan)}
.monitor__sub{font-family:var(--font-m);font-size:.6rem;color:var(--text-mut);letter-spacing:.14em;text-transform:uppercase}

.patient{
  display:flex;align-items:center;gap:9px;margin-left:6px;
  padding:5px 12px 5px 6px;border-radius:999px;
  background:rgba(255,255,255,.05);border:1px solid var(--line);
}
.patient__dot{width:9px;height:9px;border-radius:50%;background:var(--good);box-shadow:0 0 10px var(--good);animation:blink 2.2s infinite}
.patient__name{font-weight:700;font-size:.8rem;white-space:nowrap;max-width:32vw;overflow:hidden;text-overflow:ellipsis}
.patient__name span{color:var(--cyan)}
.patient__class{font-family:var(--font-m);font-size:.62rem;color:var(--text-dim)}
@keyframes blink{0%,70%,100%{opacity:1}85%{opacity:.25}}

.vitals{display:flex;align-items:center;gap:14px;margin-left:auto;flex-wrap:wrap}
.vital{display:flex;align-items:center;gap:7px}
.vital__label{font-family:var(--font-m);font-size:.55rem;letter-spacing:.16em;color:var(--text-mut);text-transform:uppercase}
.vital__val{font-family:var(--font-m);font-weight:700;font-size:.92rem}
.hp{display:flex;gap:3px}
.hp__heart{width:18px;height:18px;color:var(--circ);transition:transform .3s, opacity .3s, filter .3s;filter:drop-shadow(0 0 5px rgba(251,77,99,.6))}
.hp__heart.lost{opacity:.22;filter:none;transform:scale(.82)}
.hp__heart.hit{animation:hpHit .5s}
@keyframes hpHit{0%{transform:scale(1.5)}60%{transform:scale(.7)}100%{transform:scale(.82)}}
.badgecount{display:flex;align-items:center;gap:6px;color:var(--gold)}
.badgecount svg{width:18px;height:18px;filter:drop-shadow(0 0 6px rgba(252,211,77,.55))}

/* ============================================================
   STAGE TRACK
   ============================================================ */
.track{
  display:none;align-items:center;gap:2px;flex-wrap:wrap;justify-content:center;
  padding:10px clamp(10px,3vw,22px);
  border-bottom:1px solid var(--line);
  background:rgba(6,32,40,.55);
  position:sticky;top:59px;z-index:35;backdrop-filter:blur(8px);
}
body.started .track{display:flex}
.track__step{
  display:flex;align-items:center;gap:8px;
  padding:6px 12px;border-radius:999px;
  font-size:.74rem;font-weight:600;color:var(--text-mut);
  border:1px solid transparent;transition:.2s;white-space:nowrap;
}
.track__step .n{
  width:21px;height:21px;border-radius:50%;display:grid;place-items:center;
  font-family:var(--font-m);font-size:.62rem;font-weight:700;
  background:rgba(255,255,255,.07);color:var(--text-dim);transition:.2s;
}
.track__step.done{color:var(--text-dim)}
.track__step.done .n{background:var(--good);color:#06302A}
.track__step.active{color:var(--text);border-color:var(--line-strong);background:rgba(52,224,232,.08)}
.track__step.active .n{background:var(--cyan);color:#04222B;box-shadow:0 0 14px rgba(52,224,232,.6)}
.track__step.locked{opacity:.5;cursor:not-allowed}
.track__step.clickable{cursor:pointer}
.track__step.clickable:hover{color:var(--text);background:rgba(255,255,255,.05)}
.track__sep{width:14px;height:1px;background:var(--line);flex:0 0 auto}
.track__lock{width:12px;height:12px;opacity:.7}

/* ============================================================
   VIEWS
   ============================================================ */
main{display:block}
.view{
  display:none;
  width:100%;max-width:var(--maxw);margin:0 auto;
  padding:clamp(20px,4vw,46px) clamp(16px,4vw,30px) 60px;
  animation:viewIn .5s cubic-bezier(.2,.7,.3,1);
}
.view.active{display:block}
@keyframes viewIn{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:none}}

.eyebrow{
  font-family:var(--font-m);font-size:.66rem;letter-spacing:.24em;text-transform:uppercase;
  color:var(--cyan);display:inline-flex;align-items:center;gap:9px;margin-bottom:14px;
}
.eyebrow::before{content:"";width:26px;height:1px;background:var(--cyan);opacity:.7}
h1.title{font-family:var(--font-d);font-weight:800;font-size:clamp(1.9rem,5.4vw,3.1rem);line-height:1.04;letter-spacing:-.02em}
h2.title{font-family:var(--font-d);font-weight:700;font-size:clamp(1.5rem,4vw,2.2rem);line-height:1.1;letter-spacing:-.01em}
.lead{color:var(--text-dim);font-size:clamp(1rem,2.4vw,1.12rem);max-width:62ch}

/* tombol umum */
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:9px;
  padding:13px 24px;border-radius:999px;font-weight:700;font-size:.95rem;
  font-family:var(--font-d);transition:transform .15s, box-shadow .2s, background .2s;
  border:1px solid transparent;
}
.btn:active{transform:translateY(1px) scale(.99)}
.btn--primary{background:linear-gradient(135deg,var(--cyan),var(--cyan-deep));color:#042027;box-shadow:0 12px 30px -10px rgba(52,224,232,.6)}
.btn--primary:hover{box-shadow:0 16px 36px -10px rgba(52,224,232,.8)}
.btn--ghost{background:rgba(255,255,255,.05);border-color:var(--line-strong);color:var(--text)}
.btn--ghost:hover{background:rgba(255,255,255,.1)}
.btn--gold{background:linear-gradient(135deg,#FFE08A,var(--gold));color:#3A2A00;box-shadow:0 12px 30px -10px rgba(252,211,77,.6)}
.btn svg{width:18px;height:18px}
.btn:disabled{opacity:.45;cursor:not-allowed;box-shadow:none}

.navbtns{display:flex;gap:12px;flex-wrap:wrap;margin-top:30px}

/* kartu terang (untuk materi & teks panjang) */
.paper{
  background:var(--paper);color:var(--ink);border-radius:var(--r-l);
  padding:clamp(20px,3.4vw,32px);box-shadow:var(--shadow);
  border:1px solid rgba(255,255,255,.5);
}
.paper h3{font-family:var(--font-d);font-weight:700;color:var(--ink);font-size:1.18rem;margin-bottom:8px}
.paper p{color:var(--ink-dim)}
.paper a{color:var(--cyan-deep);font-weight:600}

/* panel gelap kaca */
.glass{
  background:linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));
  border:1px solid var(--line);border-radius:var(--r-l);
  padding:clamp(18px,3vw,28px);backdrop-filter:blur(8px);
  box-shadow:var(--shadow);
}

/* ============================================================
   SPLASH
   ============================================================ */
#view-splash{display:none;min-height:100vh;min-height:100dvh;padding-top:clamp(28px,7vh,72px)}
#view-splash.active{display:flex;flex-direction:column;align-items:center;text-align:center;justify-content:center}
.splash__ekg{width:min(680px,92vw);height:74px;margin-bottom:8px;overflow:hidden;position:relative;-webkit-mask-image:linear-gradient(90deg,transparent,#000 12%,#000 88%,transparent);mask-image:linear-gradient(90deg,transparent,#000 12%,#000 88%,transparent)}
.ekg-track{display:flex;width:200%;height:100%;animation:ekgScroll 5.5s linear infinite}
.ekg-track svg{width:50%;height:100%;flex:0 0 50%}
.ekg-line{fill:none;stroke:var(--cyan);stroke-width:2.4;filter:drop-shadow(0 0 7px rgba(52,224,232,.85))}
@keyframes ekgScroll{from{transform:translateX(0)}to{transform:translateX(-50%)}}

.splash__crest{
  width:96px;height:96px;border-radius:28px;display:grid;place-items:center;margin:6px auto 22px;
  color:#04222B;background:
    radial-gradient(circle at 30% 25%, #8FF6FB, var(--cyan) 45%, var(--cyan-deep));
  box-shadow:0 0 0 8px rgba(52,224,232,.1), 0 24px 50px -16px rgba(52,224,232,.7);
  animation:floaty 5s ease-in-out infinite;
}
.splash__crest svg{width:54px;height:54px}
@keyframes floaty{0%,100%{transform:translateY(0)}50%{transform:translateY(-9px)}}

.splash__kicker{font-family:var(--font-m);letter-spacing:.34em;font-size:.72rem;color:var(--cyan);text-transform:uppercase;margin-bottom:10px}
.splash__title{font-family:var(--font-d);font-weight:800;font-size:clamp(2.2rem,7.4vw,4.4rem);line-height:.96;letter-spacing:-.03em}
.splash__title b{background:linear-gradient(120deg,#8FF6FB,var(--cyan),var(--resp));-webkit-background-clip:text;background-clip:text;color:transparent}
.splash__tag{color:var(--text-dim);font-size:clamp(1rem,2.6vw,1.18rem);margin:16px auto 0;max-width:46ch}

.enroll{
  margin:34px auto 0;width:min(440px,94vw);text-align:left;
  background:linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.025));
  border:1px solid var(--line-strong);border-radius:var(--r-l);
  padding:24px;box-shadow:var(--shadow);position:relative;
}
.enroll__head{font-family:var(--font-m);font-size:.62rem;letter-spacing:.2em;text-transform:uppercase;color:var(--text-mut);margin-bottom:16px;display:flex;align-items:center;gap:8px}
.enroll__head::before{content:"";width:8px;height:8px;border-radius:50%;background:var(--good);box-shadow:0 0 9px var(--good)}
.field{margin-bottom:14px}
.field label{display:block;font-size:.78rem;font-weight:600;color:var(--text-dim);margin-bottom:7px}
.field input{
  width:100%;padding:13px 15px;border-radius:var(--r-s);
  background:rgba(4,28,35,.6);border:1px solid var(--line-strong);color:var(--text);
  font-size:1rem;transition:border .2s, box-shadow .2s;
}
.field input::placeholder{color:var(--text-mut)}
.field input:focus{outline:none;border-color:var(--cyan);box-shadow:0 0 0 3px rgba(52,224,232,.18)}
.enroll .btn{width:100%;margin-top:6px}
.enroll__err{color:var(--bad);font-size:.78rem;min-height:1.1em;margin-top:4px;font-weight:600}

.splash__credit{margin-top:30px;font-size:.78rem;color:var(--text-mut);line-height:1.7}
.splash__credit b{color:var(--text-dim)}

/* ============================================================
   PETUNJUK
   ============================================================ */
.goal{
  display:flex;gap:16px;align-items:flex-start;margin-top:20px;
  background:linear-gradient(120deg, rgba(52,224,232,.12), rgba(52,224,232,.03));
  border:1px solid var(--line-strong);border-left:4px solid var(--cyan);
  border-radius:var(--r-m);padding:20px 22px;
}
.goal__ic{flex:0 0 auto;width:46px;height:46px;border-radius:13px;display:grid;place-items:center;background:rgba(52,224,232,.16);color:var(--cyan)}
.goal__ic svg{width:26px;height:26px}
.goal__k{font-family:var(--font-m);font-size:.62rem;letter-spacing:.2em;text-transform:uppercase;color:var(--cyan);margin-bottom:6px}
.goal__t{font-family:var(--font-d);font-weight:700;font-size:clamp(1.05rem,2.8vw,1.32rem);line-height:1.25}

.steps{display:grid;gap:12px;margin-top:26px}
.step{
  display:flex;gap:16px;align-items:flex-start;
  background:rgba(255,255,255,.035);border:1px solid var(--line);
  border-radius:var(--r-m);padding:16px 18px;transition:.2s;
}
.step:hover{border-color:var(--line-strong);background:rgba(255,255,255,.06)}
.step__n{
  flex:0 0 auto;width:36px;height:36px;border-radius:11px;display:grid;place-items:center;
  font-family:var(--font-m);font-weight:700;font-size:.95rem;
  background:linear-gradient(135deg,var(--cyan),var(--cyan-deep));color:#04222B;
}
.step__b strong{font-family:var(--font-d);font-weight:700;display:block;margin-bottom:2px}
.step__b span{color:var(--text-dim);font-size:.9rem}

/* ============================================================
   MATERI
   ============================================================ */
.pemantik{
  margin-top:8px;border-radius:var(--r-l);overflow:hidden;position:relative;
  background:linear-gradient(135deg, rgba(251,77,99,.16), rgba(63,182,245,.12) 60%, rgba(246,166,9,.12));
  border:1px solid var(--line-strong);padding:clamp(22px,4vw,34px);
}
.pemantik__k{font-family:var(--font-m);font-size:.66rem;letter-spacing:.22em;text-transform:uppercase;color:var(--gold);margin-bottom:12px;display:flex;align-items:center;gap:9px}
.pemantik__k svg{width:18px;height:18px}
.pemantik__q{font-family:var(--font-d);font-weight:700;font-size:clamp(1.15rem,3.2vw,1.55rem);line-height:1.3;max-width:40ch}
.pemantik__p{color:var(--text-dim);margin-top:14px;max-width:60ch}

.section-h{display:flex;align-items:center;gap:12px;margin:40px 0 18px}
.section-h h3{font-family:var(--font-d);font-weight:700;font-size:1.3rem}
.section-h .pill{font-family:var(--font-m);font-size:.6rem;letter-spacing:.14em;text-transform:uppercase;padding:4px 10px;border-radius:999px;background:rgba(255,255,255,.06);border:1px solid var(--line);color:var(--text-dim)}

.videos{display:grid;grid-template-columns:repeat(auto-fit,minmax(248px,1fr));gap:16px}
.vcard{background:rgba(255,255,255,.035);border:1px solid var(--line);border-radius:var(--r-m);overflow:hidden;transition:.2s}
.vcard:hover{border-color:var(--line-strong);transform:translateY(-3px)}
.vframe{position:relative;aspect-ratio:16/9;background:#03181E}
.vframe iframe{position:absolute;inset:0;width:100%;height:100%;border:0}
.vfallback{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;justify-content:center;gap:8px;text-align:center;padding:18px;color:var(--text-dim);font-size:.85rem}
.vfallback svg{width:30px;height:30px;color:var(--text-mut)}
.vcard.offline .vframe iframe{display:none}
.vcard.offline .vfallback{display:flex}
.vcard__b{padding:13px 15px}
.vcard__t{font-family:var(--font-d);font-weight:700;font-size:.95rem}
.vcard__s{font-size:.74rem;color:var(--text-mut);margin-top:3px}

.sys-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:16px;margin-top:6px}
.syscard{border-radius:var(--r-m);padding:20px;border:1px solid var(--line);position:relative;overflow:hidden;background:rgba(255,255,255,.03)}
.syscard::before{content:"";position:absolute;inset:0 auto 0 0;width:4px;background:var(--c)}
.syscard__ic{width:48px;height:48px;border-radius:13px;display:grid;place-items:center;margin-bottom:14px;color:var(--c);background:color-mix(in srgb, var(--c) 16%, transparent)}
.syscard__ic svg{width:28px;height:28px}
.syscard h4{font-family:var(--font-d);font-weight:700;font-size:1.08rem;margin-bottom:4px}
.syscard p{font-size:.84rem;color:var(--text-dim)}
.syscard__organs{display:flex;flex-wrap:wrap;gap:6px;margin-top:14px}
.organ-chip{font-size:.72rem;font-weight:600;padding:4px 11px;border-radius:999px;background:color-mix(in srgb, var(--c) 14%, transparent);color:var(--c);border:1px solid color-mix(in srgb, var(--c) 30%, transparent)}

/* ============================================================
   KUIS
   ============================================================ */
.quiz-wrap{max-width:720px;margin:0 auto}
.quiz-top{display:flex;align-items:center;justify-content:space-between;gap:14px;margin-bottom:18px}
.quiz-prog{flex:1;height:8px;border-radius:999px;background:rgba(255,255,255,.08);overflow:hidden}
.quiz-prog__bar{height:100%;border-radius:999px;background:linear-gradient(90deg,var(--cyan),var(--resp));transition:width .4s}
.quiz-count{font-family:var(--font-m);font-size:.78rem;color:var(--text-dim);white-space:nowrap}
.qbox{background:var(--paper);color:var(--ink);border-radius:var(--r-l);padding:clamp(22px,3.6vw,34px);box-shadow:var(--shadow)}
.qlevel{display:inline-flex;align-items:center;gap:6px;font-family:var(--font-m);font-size:.62rem;letter-spacing:.12em;text-transform:uppercase;color:var(--cyan-deep);background:rgba(19,167,180,.12);padding:4px 11px;border-radius:999px;margin-bottom:14px;font-weight:700}
.qtext{font-family:var(--font-d);font-weight:700;font-size:clamp(1.1rem,3vw,1.4rem);line-height:1.35;color:var(--ink);margin-bottom:20px}
.opts{display:grid;gap:11px}
.opt{
  display:flex;align-items:center;gap:14px;text-align:left;width:100%;
  padding:15px 17px;border-radius:var(--r-m);border:2px solid #DCEAE9;background:#fff;
  font-size:1rem;color:var(--ink);font-weight:600;transition:.16s;
}
.opt:hover:not(.locked){border-color:var(--cyan-deep);background:#F0FCFB}
.opt__key{flex:0 0 auto;width:30px;height:30px;border-radius:9px;display:grid;place-items:center;background:#EAF4F3;color:var(--ink-dim);font-family:var(--font-m);font-weight:700;font-size:.9rem;transition:.16s}
.opt.sel{border-color:var(--cyan-deep);background:#E7FBF9}
.opt.sel .opt__key{background:var(--cyan-deep);color:#fff}
.opt.correct{border-color:var(--good);background:#E4FBF2}
.opt.correct .opt__key{background:var(--good);color:#063b2c}
.opt.wrong{border-color:var(--bad);background:#FCE9EC}
.opt.wrong .opt__key{background:var(--bad);color:#fff}
.opt.locked{cursor:default}
.opt__mark{margin-left:auto;width:22px;height:22px;flex:0 0 auto}
.qfeedback{margin-top:18px;padding:14px 16px;border-radius:var(--r-m);font-size:.92rem;font-weight:600;display:none}
.qfeedback.show{display:block;animation:viewIn .3s}
.qfeedback.ok{background:#E4FBF2;color:#0B6B4E;border:1px solid #9FE9CE}
.qfeedback.no{background:#FCE9EC;color:#9A2233;border:1px solid #F4B7C0}
.qbox .navbtns{margin-top:22px}
.qbox .btn--ghost{background:#EEF6F5;border-color:#D6E6E4;color:var(--ink-dim)}
.qbox .btn--ghost:hover{background:#E2F0EE}

/* hasil kuis */
.result{text-align:center;max-width:560px;margin:0 auto}
.result__ring{
  width:170px;height:170px;margin:6px auto 18px;border-radius:50%;
  display:grid;place-items:center;position:relative;
  background:conic-gradient(var(--ring-c) calc(var(--p)*1%), rgba(255,255,255,.08) 0);
}
.result__ring::after{content:"";position:absolute;inset:12px;border-radius:50%;background:var(--bg-1);box-shadow:inset 0 0 0 1px var(--line)}
.result__score{position:relative;z-index:2;font-family:var(--font-m);font-weight:700;font-size:2.6rem;line-height:1;color:var(--ring-c)}
.result__score small{display:block;font-size:.7rem;letter-spacing:.16em;color:var(--text-mut);margin-top:6px}
.result__msg{font-family:var(--font-d);font-weight:700;font-size:1.5rem;margin-bottom:6px}
.result__detail{color:var(--text-dim)}

/* ============================================================
   GAME
   ============================================================ */
.game-head{display:flex;align-items:center;gap:14px;flex-wrap:wrap;margin-bottom:16px}
.world-badge{display:inline-flex;align-items:center;gap:9px;padding:7px 15px 7px 8px;border-radius:999px;border:1px solid color-mix(in srgb,var(--c) 36%, transparent);background:color-mix(in srgb,var(--c) 13%, transparent);color:var(--c);font-weight:700;font-size:.86rem}
.world-badge__ic{width:30px;height:30px;border-radius:9px;display:grid;place-items:center;background:color-mix(in srgb,var(--c) 22%, transparent)}
.world-badge__ic svg{width:18px;height:18px}
.world-prog{font-family:var(--font-m);font-size:.78rem;color:var(--text-dim);margin-left:auto}
.world-dots{display:flex;gap:6px}
.world-dot{width:11px;height:11px;border-radius:50%;background:rgba(255,255,255,.12);transition:.3s}
.world-dot.done{background:var(--c);box-shadow:0 0 9px var(--c)}
.world-dot.now{box-shadow:0 0 0 3px color-mix(in srgb,var(--c) 35%, transparent)}

.game{display:grid;grid-template-columns:minmax(0,1fr) minmax(300px,420px);gap:18px;align-items:stretch}
.board{
  position:relative;border-radius:var(--r-l);overflow:hidden;min-height:440px;
  background:
    radial-gradient(120% 90% at 50% -10%, color-mix(in srgb,var(--c) 16%, transparent), transparent 60%),
    linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.015));
  border:1px solid var(--line);box-shadow:var(--shadow);
  display:grid;place-items:center;padding:18px;
}
.bodymap{position:relative;width:min(330px,72vw);aspect-ratio:300/560}
.bodymap__svg{width:100%;height:100%;display:block}
.bodymap__fill{fill:url(#bodyGrad);stroke:color-mix(in srgb,var(--c) 50%, var(--line-strong));stroke-width:1.4}
.bodymap__center{stroke:color-mix(in srgb,var(--c) 30%, transparent);stroke-width:1;stroke-dasharray:3 7}
/* organ node */
.node{
  position:absolute;transform:translate(-50%,-50%);
  display:flex;flex-direction:column;align-items:center;gap:5px;
  width:auto;
}
.node__btn{
  width:54px;height:54px;border-radius:50%;display:grid;place-items:center;position:relative;
  background:rgba(8,40,50,.85);border:2px solid rgba(255,255,255,.18);color:var(--text-mut);
  transition:transform .18s, box-shadow .2s, border-color .2s;
}
.node__btn svg{width:26px;height:26px}
.node__label{font-size:.66rem;font-weight:700;color:var(--text-dim);background:rgba(6,32,40,.78);padding:2px 8px;border-radius:999px;white-space:nowrap;border:1px solid var(--line)}
.node--locked .node__btn{filter:saturate(.4)}
.node--active .node__btn{
  border-color:var(--c);color:var(--c);background:color-mix(in srgb,var(--c) 16%, #06222C);
  box-shadow:0 0 0 0 color-mix(in srgb,var(--c) 60%, transparent);
  animation:nodePulse 1.8s infinite;cursor:pointer;
}
.node--active .node__label{color:var(--c);border-color:color-mix(in srgb,var(--c) 40%, transparent)}
.node--active:hover .node__btn{transform:scale(1.1)}
@keyframes nodePulse{0%{box-shadow:0 0 0 0 color-mix(in srgb,var(--c) 55%, transparent)}70%{box-shadow:0 0 0 14px transparent}100%{box-shadow:0 0 0 0 transparent}}
.node--done .node__btn{border-color:var(--c);color:#06222C;background:var(--c);box-shadow:0 0 16px color-mix(in srgb,var(--c) 55%, transparent)}
.node--done .node__label{color:var(--c)}
.node__check{position:absolute;right:-3px;top:-3px;width:20px;height:20px;border-radius:50%;background:var(--good);color:#05332628;display:grid;place-items:center;border:2px solid var(--bg-1)}
.node__check svg{width:12px;height:12px;color:#053326}

/* panel */
.gpanel{
  border-radius:var(--r-l);border:1px solid var(--line);box-shadow:var(--shadow);
  background:linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));
  padding:clamp(18px,2.6vw,24px);display:flex;flex-direction:column;
}
.gpanel__k{font-family:var(--font-m);font-size:.6rem;letter-spacing:.18em;text-transform:uppercase;color:var(--c);margin-bottom:10px;display:flex;align-items:center;gap:8px}
.gpanel__title{font-family:var(--font-d);font-weight:700;font-size:1.18rem;line-height:1.25;margin-bottom:6px}
.gpanel__intro{color:var(--text-dim);font-size:.92rem}
.gpanel__hint{margin-top:auto;font-size:.78rem;color:var(--text-mut);padding-top:16px;display:flex;align-items:center;gap:8px}
.gpanel__hint svg{width:15px;height:15px}
.qg-text{font-family:var(--font-d);font-weight:700;font-size:1.06rem;line-height:1.4;margin:6px 0 16px}
.qg-opts{display:grid;gap:9px}
.qg-opt{
  display:flex;align-items:center;gap:11px;text-align:left;width:100%;padding:12px 14px;
  border-radius:var(--r-s);border:1.6px solid var(--line);background:rgba(255,255,255,.03);
  color:var(--text);font-size:.92rem;font-weight:600;transition:.14s;
}
.qg-opt:hover:not(.locked){border-color:var(--c);background:color-mix(in srgb,var(--c) 10%, transparent)}
.qg-opt__k{flex:0 0 auto;width:26px;height:26px;border-radius:7px;display:grid;place-items:center;background:rgba(255,255,255,.07);font-family:var(--font-m);font-weight:700;font-size:.8rem;color:var(--text-dim)}
.qg-opt.sel{border-color:var(--c)}
.qg-opt.sel .qg-opt__k{background:var(--c);color:#06222C}
.qg-opt.correct{border-color:var(--good);background:rgba(52,227,176,.12)}
.qg-opt.correct .qg-opt__k{background:var(--good);color:#05332620}
.qg-opt.wrong{border-color:var(--bad);background:rgba(255,107,130,.12)}
.qg-opt.wrong .qg-opt__k{background:var(--bad);color:#fff}
.qg-opt.locked{cursor:default}
.qg-fb{margin-top:14px;padding:12px 14px;border-radius:var(--r-s);font-size:.86rem;font-weight:600;line-height:1.5}
.qg-fb.ok{background:rgba(52,227,176,.13);color:#9DF4D6;border:1px solid rgba(52,227,176,.3)}
.qg-fb.no{background:rgba(255,107,130,.13);color:#FFB3BE;border:1px solid rgba(255,107,130,.3)}
.gpanel .btn{margin-top:16px}
.gpanel .btn--sys{background:linear-gradient(135deg,var(--c),color-mix(in srgb,var(--c) 60%, #000));color:#06222C}

.reward{text-align:center}
.reward__medal{width:120px;height:120px;margin:4px auto 14px;animation:pop .6s cubic-bezier(.2,1.4,.4,1)}
@keyframes pop{0%{transform:scale(0) rotate(-25deg);opacity:0}60%{transform:scale(1.15) rotate(6deg)}100%{transform:scale(1) rotate(0);opacity:1}}
.reward__t{font-family:var(--font-d);font-weight:800;font-size:1.5rem}
.reward__s{color:var(--text-dim);margin-top:6px}

.gameover{text-align:center;max-width:520px;margin:0 auto}
.gameover__ic{width:96px;height:96px;margin:6px auto 16px;border-radius:50%;display:grid;place-items:center;background:rgba(255,107,130,.12);color:var(--bad);border:1px solid rgba(255,107,130,.3)}
.gameover__ic svg{width:48px;height:48px}

/* ============================================================
   LAB MAYA
   ============================================================ */
.lab-tabs{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:18px}
.lab-tab{
  display:inline-flex;align-items:center;gap:9px;padding:10px 16px;border-radius:999px;
  border:1px solid var(--line);background:rgba(255,255,255,.03);color:var(--text-dim);font-weight:700;font-size:.86rem;transition:.18s;
}
.lab-tab svg{width:18px;height:18px}
.lab-tab:hover{color:var(--text);border-color:var(--line-strong)}
.lab-tab.active{color:#06222C;background:var(--c);border-color:var(--c);box-shadow:0 8px 22px -8px color-mix(in srgb,var(--c) 70%, transparent)}

.lab{display:grid;grid-template-columns:minmax(0,1fr) minmax(300px,440px);gap:18px;align-items:stretch}
.lab-stage{
  position:relative;border-radius:var(--r-l);min-height:480px;display:grid;place-items:center;padding:18px;
  border:1px solid var(--line);box-shadow:var(--shadow);
  background:
    radial-gradient(130% 100% at 50% 0%, color-mix(in srgb,var(--c) 14%, transparent), transparent 62%),
    linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.01));
}
.lab-scan{position:absolute;left:0;right:0;height:120px;pointer-events:none;background:linear-gradient(180deg, transparent, color-mix(in srgb,var(--c) 16%, transparent), transparent);animation:scan 4.5s linear infinite;opacity:.7}
@keyframes scan{0%{top:-20%}100%{top:100%}}
.lab-body{position:relative;width:min(340px,74vw);aspect-ratio:300/560}
.lab-body__svg{width:100%;height:100%}
/* node organ di peta Lab — oval dengan gambar organ realistis */
.lab-node{position:absolute;transform:translate(-50%,-50%);display:flex;flex-direction:column;align-items:center;gap:4px}
.lab-node__btn{
  width:58px;height:58px;border-radius:50%;display:grid;place-items:center;
  background:rgba(4,26,34,.82);
  border:2.5px solid color-mix(in srgb,var(--c) 55%, transparent);
  box-shadow:0 4px 14px -4px rgba(0,0,0,.6);
  transition:transform .16s, box-shadow .2s;cursor:pointer;overflow:hidden;
}
/* gambar organ (SVG berwarna) di dalam tombol */
.lab-node__btn svg{width:40px;height:40px;display:block}
.lab-node__btn:hover{transform:scale(1.13)}
.lab-node.active .lab-node__btn{
  border-color:var(--c);
  box-shadow:0 0 0 5px color-mix(in srgb,var(--c) 28%, transparent),
             0 0 24px color-mix(in srgb,var(--c) 65%, transparent);
}
.lab-node__label{font-size:.66rem;font-weight:700;color:var(--c);background:rgba(4,22,28,.85);padding:2px 8px;border-radius:999px;white-space:nowrap;border:1px solid color-mix(in srgb,var(--c) 32%, transparent);pointer-events:none}
.heartbeat{animation:beat 1.1s ease-in-out infinite}
@keyframes beat{0%,100%{transform:translate(-50%,-50%) scale(1)}14%{transform:translate(-50%,-50%) scale(1.16)}28%{transform:translate(-50%,-50%) scale(1)}42%{transform:translate(-50%,-50%) scale(1.1)}}
.breathe{animation:breathe 3.6s ease-in-out infinite}
@keyframes breathe{0%,100%{transform:translate(-50%,-50%) scale(1)}50%{transform:translate(-50%,-50%) scale(1.09)}}

/* panel info Lab — ilustrasi besar di header */
.lab-info{border-radius:var(--r-l);border:1px solid var(--line);box-shadow:var(--shadow);background:linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));padding:clamp(18px,2.6vw,26px);display:flex;flex-direction:column}
.lab-info__art{
  width:140px;height:140px;border-radius:22px;margin:0 auto 18px;
  display:grid;place-items:center;
  background:radial-gradient(circle at 34% 28%, rgba(255,255,255,.12), rgba(0,0,0,.35));
  border:1.5px solid color-mix(in srgb,var(--c) 36%, transparent);
  box-shadow:0 12px 34px -10px color-mix(in srgb,var(--c) 55%, transparent),
             inset 0 1px 0 rgba(255,255,255,.15);
  overflow:hidden;
}
.lab-info__art svg{width:110px;height:110px;display:block}
.lab-info__art img{width:110px;height:110px;object-fit:contain}
.lab-info__k{font-family:var(--font-m);font-size:.6rem;letter-spacing:.18em;text-transform:uppercase;color:var(--c);margin-bottom:6px;text-align:center}
.lab-info__name{font-family:var(--font-d);font-weight:800;font-size:1.6rem;line-height:1.1;margin-bottom:14px;text-align:center}
.lab-info__row{margin-bottom:16px}
.lab-info__lab{font-size:.72rem;font-weight:700;text-transform:uppercase;letter-spacing:.08em;color:var(--text-mut);margin-bottom:5px;display:flex;align-items:center;gap:7px}
.lab-info__lab svg{width:15px;height:15px;color:var(--c)}
.lab-info__txt{color:var(--text);font-size:.95rem;line-height:1.6}
.lab-info__fact{background:color-mix(in srgb,var(--c) 9%, transparent);border:1px solid color-mix(in srgb,var(--c) 24%, transparent);border-radius:var(--r-m);padding:14px 16px;margin-top:auto}
.lab-info__empty{margin:auto;text-align:center;color:var(--text-mut);font-size:.92rem;max-width:24ch}
.lab-info__empty svg{width:40px;height:40px;margin:0 auto 12px;opacity:.5;color:var(--c)}

/* ============================================================
   SERTIFIKAT / SELESAI
   ============================================================ */
.finale{text-align:center}
.cert{
  position:relative;max-width:760px;margin:10px auto 0;border-radius:var(--r-l);overflow:hidden;
  background:linear-gradient(160deg, #FBFEFE, #EFFAF9);color:var(--ink);
  border:1px solid rgba(255,255,255,.6);box-shadow:0 30px 70px -28px rgba(0,0,0,.7);
  padding:clamp(26px,5vw,48px);
}
.cert::before{content:"";position:absolute;inset:14px;border:2px solid rgba(19,167,180,.3);border-radius:18px;pointer-events:none}
.cert::after{content:"";position:absolute;inset:20px;border:1px solid rgba(252,211,77,.5);border-radius:14px;pointer-events:none}
.cert__seal{
  width:96px;height:96px;margin:0 auto 14px;border-radius:50%;display:grid;place-items:center;color:#3A2A00;
  background:radial-gradient(circle at 32% 26%, #FFE89B, var(--gold) 55%, #E9B824);
  box-shadow:0 12px 30px -10px rgba(233,184,36,.7);animation:pop .7s cubic-bezier(.2,1.4,.4,1)
}
.cert__seal svg{width:54px;height:54px}
.cert__k{font-family:var(--font-m);letter-spacing:.3em;text-transform:uppercase;font-size:.68rem;color:var(--cyan-deep)}
.cert__title{font-family:var(--font-d);font-weight:800;font-size:clamp(1.8rem,5vw,2.8rem);color:var(--ink);line-height:1.05;margin:8px 0 4px}
.cert__sub{color:var(--ink-dim);font-size:.95rem}
.cert__name{font-family:var(--font-d);font-weight:800;font-size:clamp(1.5rem,4.4vw,2.3rem);color:var(--cyan-deep);margin:18px 0 4px;line-height:1.1}
.cert__line{width:220px;max-width:70%;height:2px;background:linear-gradient(90deg,transparent,var(--cyan-deep),transparent);margin:6px auto 14px}
.cert__desc{color:var(--ink-dim);max-width:54ch;margin:0 auto 18px;font-size:.95rem}
.cert__badges{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin:18px 0 8px}
.cert-badge{display:flex;flex-direction:column;align-items:center;gap:7px;width:108px}
.cert-badge__m{width:58px;height:58px}
.cert-badge__t{font-size:.72rem;font-weight:700;color:var(--ink);line-height:1.2;text-align:center}
.cert__meta{display:flex;justify-content:space-between;gap:16px;flex-wrap:wrap;margin-top:22px;padding-top:18px;border-top:1px dashed rgba(19,167,180,.35);text-align:left}
.cert__meta div{font-size:.74rem;color:var(--ink-dim)}
.cert__meta b{display:block;color:var(--ink);font-family:var(--font-d);font-size:.86rem;margin-bottom:1px}

/* konfeti */
.confetti{position:fixed;inset:0;pointer-events:none;z-index:60;overflow:hidden}
.confetti i{position:absolute;top:-12px;width:9px;height:14px;opacity:.95;animation:fall linear forwards}
@keyframes fall{to{transform:translateY(108vh) rotate(720deg);opacity:.4}}

/* ============================================================
   FOOTER
   ============================================================ */
.foot{
  display:none;text-align:center;padding:26px 20px 40px;color:var(--text-mut);font-size:.76rem;line-height:1.7;
  border-top:1px solid var(--line);margin-top:10px;
}
body.started .foot{display:block}
.foot b{color:var(--text-dim)}
.foot__brand{display:inline-flex;align-items:center;gap:8px;color:var(--cyan);font-family:var(--font-d);font-weight:700;font-size:.82rem;margin-bottom:6px}
.foot__brand svg{width:16px;height:16px}

/* ============================================================
   RESPONSIVE
   ============================================================ */
@media (max-width:880px){
  .game,.lab{grid-template-columns:1fr}
  .board,.lab-stage{min-height:380px}
  .track{top:0;position:static}
  .monitor{position:static}
}
@media (max-width:560px){
  .vitals{gap:10px;width:100%;margin-left:0;justify-content:space-between}
  .patient__name{max-width:40vw}
  .track__sep{width:8px}
  .track__step{padding:5px 9px;font-size:.68rem}
  .splash__credit{font-size:.72rem}
}

/* aksesibilitas: kurangi gerak */
@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.001ms!important;animation-iteration-count:1!important;transition-duration:.001ms!important}
  .ekg-track{animation:none}
  .lab-scan{display:none}
}

/* cetak sertifikat */
@media print{
  body::before,body::after{display:none}
  .monitor,.track,.foot,.finale .navbtns,.confetti{display:none!important}
  body{background:#fff}
  .view{padding:0}
  .cert{box-shadow:none;border:1px solid #ccc;color:#000}
}
</style>
</head>
<body>
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <radialGradient id="gRed" cx="34%" cy="28%" r="78%">
      <stop offset="0" stop-color="#FF8A95"/><stop offset="55%" stop-color="#E14257"/><stop offset="100%" stop-color="#960E22"/>
    </radialGradient>
    <radialGradient id="gPink" cx="34%" cy="28%" r="78%">
      <stop offset="0" stop-color="#FFD3DD"/><stop offset="55%" stop-color="#F28DA0"/><stop offset="100%" stop-color="#C24F68"/>
    </radialGradient>
    <linearGradient id="gLiver" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0" stop-color="#B05F42"/><stop offset="100%" stop-color="#6E2E1E"/>
    </linearGradient>
    <linearGradient id="gAirway" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#FCEEEE"/><stop offset="100%" stop-color="#E3C2C2"/>
    </linearGradient>
    <radialGradient id="gVein" cx="34%" cy="28%" r="78%">
      <stop offset="0" stop-color="#9CC2F5"/><stop offset="55%" stop-color="#4D7FCB"/><stop offset="100%" stop-color="#274B85"/>
    </radialGradient>
    <linearGradient id="gTan" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#F1C99B"/><stop offset="100%" stop-color="#CE8F5C"/>
    </linearGradient>
    <linearGradient id="gSkin" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#FAD3AE"/><stop offset="100%" stop-color="#E0A372"/>
    </linearGradient>
    <linearGradient id="gSkinSide" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0" stop-color="#C98454"/><stop offset="45%" stop-color="#F0C091"/><stop offset="100%" stop-color="#C98454"/>
    </linearGradient>
  </defs>
</svg>

<!-- ===================== HEADER MONITOR ===================== -->
<header class="monitor" role="banner">
  <div class="monitor__brand">
    <div class="monitor__logo" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3v5a4 4 0 0 0 8 0V3"/><circle cx="18" cy="16" r="2.4"/><path d="M10 12v1.5a6.5 6.5 0 0 0 6.5 6.5"/></svg></div>
    <div>
      <div class="monitor__title">Dokter <b>Spesialis</b></div>
      <div class="monitor__sub">Sistem Organ Tubuh</div>
    </div>
  </div>

  <div class="patient" title="Identitas pemain">
    <span class="patient__dot" aria-hidden="true"></span>
    <div>
      <div class="patient__name">Dr. <span id="hudName">—</span></div>
      <div class="patient__class" id="hudClass">Kelas —</div>
    </div>
  </div>

  <div class="vitals" id="vitals" hidden>
    <div class="vital">
      <span class="vital__label">Nyawa</span>
      <span class="hp" id="hp" aria-label="Sisa nyawa"></span>
    </div>
    <div class="vital">
      <span class="vital__label">Skor</span>
      <span class="vital__val" id="hudScore" style="color:var(--cyan)">0</span>
    </div>
    <div class="vital">
      <span class="vital__label">Lencana</span>
      <span class="badgecount"><svg viewBox="0 0 24 24" fill="currentColor"><circle cx="12" cy="9" r="5" fill="none" stroke="currentColor" stroke-width="1.6"/><path d="M9 13l-1.6 6 4.6-2.7 4.6 2.7L15 13" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"/></svg><span class="vital__val" id="hudBadges">0</span></span>
    </div>
  </div>
</header>

<!-- ===================== STAGE TRACK ===================== -->
<nav class="track" id="track" aria-label="Tahapan pembelajaran"></nav>

<main>
  <!-- ===================== SPLASH ===================== -->
  <section class="view active" id="view-splash" aria-label="Halaman awal">
    <div class="splash__ekg" aria-hidden="true">
      <div class="ekg-track">
        <svg viewBox="0 0 600 120" preserveAspectRatio="none"><path class="ekg-line" d="M0 60 H70 q6 0 9-9 q3 9 9 9 H150 l8 -2 l7 -38 l9 70 l8 -40 l6 10 H280 q6 0 9-9 q3 9 9 9 H360 l8 -2 l7 -38 l9 70 l8 -40 l6 10 H490 q6 0 9-9 q3 9 9 9 H600"/></svg>
        <svg viewBox="0 0 600 120" preserveAspectRatio="none"><path class="ekg-line" d="M0 60 H70 q6 0 9-9 q3 9 9 9 H150 l8 -2 l7 -38 l9 70 l8 -40 l6 10 H280 q6 0 9-9 q3 9 9 9 H360 l8 -2 l7 -38 l9 70 l8 -40 l6 10 H490 q6 0 9-9 q3 9 9 9 H600"/></svg>
      </div>
    </div>

    <div class="splash__crest" aria-hidden="true">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3v5a4 4 0 0 0 8 0V3"/><circle cx="18" cy="15.5" r="2.6"/><path d="M10 12v1.5a6.5 6.5 0 0 0 6.5 6.5"/></svg>
    </div>

    <div class="splash__kicker">Media Pembelajaran IPA · SMP</div>
    <h1 class="splash__title">Petualangan<br><b>Jadi Dokter Spesialis</b></h1>
    <p class="splash__tag">Jelajahi organ-organ tubuh manusia, selesaikan misi tiap sistem organ, dan raih lencana <b>Dokter Cilik</b>.</p>

    <div class="enroll">
      <div class="enroll__head">Pendaftaran Calon Dokter</div>
      <div class="field">
        <label for="inName">Nama Lengkap</label>
        <input id="inName" type="text" placeholder="Tulis namamu di sini" autocomplete="off" maxlength="40" />
      </div>
      <div class="field">
        <label for="inClass">Kelas</label>
        <input id="inClass" type="text" placeholder="Contoh: 8A" autocomplete="off" maxlength="16" />
      </div>
      <div class="enroll__err" id="enrollErr" role="alert"></div>
      <button class="btn btn--primary" id="startBtn">Mulai Petualangan
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
      </button>
    </div>

    <div class="splash__credit">
      Dikembangkan oleh <b>Salehuddin</b> — Guru SMP Negeri Sinombayuga<br>
      Sumber materi: Ruang Murid &amp; Buku IPA SMP
    </div>
  </section>

  <!-- ===================== PETUNJUK ===================== -->
  <section class="view" id="view-petunjuk" aria-label="Petunjuk dan tujuan">
    <div class="eyebrow">Tahap 1 — Persiapan</div>
    <h1 class="title">Petunjuk &amp; Tujuan Pembelajaran</h1>
    <p class="lead" style="margin-top:14px">Sebelum bertugas, kenali dulu misi dan aturan mainnya, Dokter.</p>

    <div class="goal">
      <div class="goal__ic" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4"/><circle cx="12" cy="12" r="1"/></svg></div>
      <div>
        <div class="goal__k">Tujuan Pembelajaran</div>
        <div class="goal__t">Murid dapat menyebutkan organ utama penyusun satu sistem organ.</div>
      </div>
    </div>

    <div class="steps" id="steps"></div>

    <div class="navbtns">
      <button class="btn btn--primary" data-go="materi">Lanjut ke Materi
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
    </div>
  </section>

  <!-- ===================== MATERI ===================== -->
  <section class="view" id="view-materi" aria-label="Materi pembelajaran">
    <div class="eyebrow">Tahap 2 — Materi</div>
    <h1 class="title">Mengenal Sistem Organ</h1>

    <div class="pemantik" style="margin-top:20px">
      <div class="pemantik__k"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M9 18h6M10 22h4M12 2a7 7 0 0 0-4 12.7c.6.5 1 1.3 1 2.1V18h6v-1.2c0-.8.4-1.6 1-2.1A7 7 0 0 0 12 2Z"/></svg> Pertanyaan Pemantik</div>
      <div class="pemantik__q">Ke mana perginya nasi yang kamu makan? Bagaimana oksigen dari udara bisa sampai ke seluruh tubuhmu?</div>
      <p class="pemantik__p">Di dalam tubuhmu, banyak organ bekerja sama membentuk <b style="color:var(--text)">sistem organ</b>. Tugas seorang dokter adalah memahami organ-organ itu. Pelajari materi berikut, lalu buktikan kesiapanmu!</p>
    </div>

    <div class="section-h"><h3>Tonton &amp; Amati</h3><span class="pill">Video Pembelajaran</span></div>
    <div class="videos" id="videos"></div>
    <p style="color:var(--text-mut);font-size:.78rem;margin-top:12px">Video membutuhkan koneksi internet. Sumber: Ruang Murid. <em>Judul video dapat disesuaikan guru.</em></p>

    <div class="section-h"><h3>Tiga Sistem Organ yang Akan Kamu Telusuri</h3></div>
    <div class="sys-grid" id="sysGrid"></div>

    <div class="navbtns">
      <button class="btn btn--ghost" data-go="petunjuk">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 12H5M11 6l-6 6 6 6"/></svg> Kembali</button>
      <button class="btn btn--primary" data-go="kuis">Ke Kuis Kesiapan
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
    </div>
  </section>

  <!-- ===================== KUIS ===================== -->
  <section class="view" id="view-kuis" aria-label="Kuis kesiapan">
    <div class="eyebrow">Tahap 3 — Kuis Kesiapan</div>
    <h1 class="title">Uji Kesiapanmu</h1>
    <p class="lead" style="margin-top:12px">5 pertanyaan. Capai nilai minimal <b style="color:var(--cyan)">75</b> untuk membuka Petualangan Peta Tubuh.</p>
    <div class="quiz-wrap" id="quizWrap" style="margin-top:26px"></div>
  </section>

  <!-- ===================== GAME ===================== -->
  <section class="view" id="view-game" aria-label="Petualangan peta tubuh">
    <div class="eyebrow">Tahap 4 — Petualangan</div>
    <h1 class="title">Peta Tubuh Manusia</h1>
    <p class="lead" style="margin-top:12px">Tiap organ adalah satu level. Jawab benar untuk menyembuhkan organ, jaga nyawamu, dan kumpulkan lencana keahlian!</p>
    <div id="gameRoot" style="margin-top:24px"></div>
  </section>

  <!-- ===================== LAB ===================== -->
  <section class="view" id="view-lab" aria-label="Lab maya tubuh manusia">
    <div class="eyebrow">Tahap 5 — Eksplorasi</div>
    <h1 class="title">Lab Maya Tubuh Manusia</h1>
    <p class="lead" style="margin-top:12px">Pilih sistem organ, lalu ketuk tiap organ untuk membaca fungsi dan fakta menariknya.</p>
    <div id="labRoot" style="margin-top:24px"></div>
    <div class="navbtns">
      <button class="btn btn--ghost" data-go="game">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 12H5M11 6l-6 6 6 6"/></svg> Kembali ke Petualangan</button>
      <button class="btn btn--gold" id="toCertBtn" data-go="selesai">Lihat Sertifikat
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
    </div>
  </section>

  <!-- ===================== SELESAI / SERTIFIKAT ===================== -->
  <section class="view" id="view-selesai" aria-label="Sertifikat">
    <div class="finale" id="finaleRoot"></div>
  </section>
</main>

<footer class="foot">
  <span class="foot__brand"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3v5a4 4 0 0 0 8 0V3"/><circle cx="18" cy="16" r="2.4"/><path d="M10 12v1.5a6.5 6.5 0 0 0 6.5 6.5"/></svg> Petualangan: Jadi Dokter Spesialis</span><br>
  Dikembangkan oleh <b>Salehuddin</b> — Guru SMP Negeri Sinombayuga<br>
  Sumber: Ruang Murid &amp; Buku IPA SMP
</footer>

<script>
/* =========================================================================
   IKON ORGAN (SVG)
   ========================================================================= */
const SV='fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"';
const ICON = {
  mulut:`<path d="M4 11c3-3 13-3 16 0M4 13c3 3 13 3 16 0M8 11.5v3M12 11.5v3M16 11.5v3"/>`,
  kerongkongan:`<rect x="9" y="3.5" width="6" height="17" rx="3"/><path d="M9 8h6M9 12h6M9 16h6"/>`,
  lambung:`<path d="M10 4c-1 3-1 5 1.5 6 3 1.2 4.5 3 4.5 5.5C16 18 14 20 11 20c-2.4 0-4-1.4-4.2-3.4"/>`,
  usushalus:`<path d="M7 4c5 0 5 3 0 3s-5 3 0 3 5 3 0 3 5 3 0 3"/><path d="M17 4c0 2-2 2-2 4s2 2 2 4-2 2-2 4"/>`,
  jantung:`<path d="M12 20s-7-4.6-7-10a3.8 3.8 0 0 1 7-2.2A3.8 3.8 0 0 1 19 10c0 5.4-7 10-7 10Z"/><path d="M12 7v3M9 13l3-3 3 3" stroke-width="1.3"/>`,
  arteri:`<path d="M7 4v6a4 4 0 0 0 4 4h6"/><path d="M14 11l3 3-3 3" stroke-width="1.4"/>`,
  vena:`<path d="M17 4v6a4 4 0 0 1-4 4H7"/><path d="M10 11l-3 3 3 3" stroke-width="1.4"/>`,
  darah:`<path d="M12 3s6 7 6 11a6 6 0 0 1-12 0c0-4 6-11 6-11Z"/>`,
  hidung:`<path d="M11 4c0 4-2 6-2 8.5 0 1.4 1.2 2.5 3 2.5s3-1.1 3-2.5C15 10 13 8 13 4"/><path d="M9 14.5c.8 1 2 1.5 3 1.5s2.2-.5 3-1.5"/>`,
  trakea:`<rect x="9" y="3" width="6" height="11" rx="3"/><path d="M9 7h6M9 10.5h6"/><path d="M12 14v2M12 16l-3 4M12 16l3 4"/>`,
  bronkus:`<path d="M12 3v7M12 10l-4 4M12 10l4 4M8 14v4M16 14v4M6 18h4M14 18h4"/>`,
  paru:`<path d="M12 4v7"/><path d="M9 11c-2 1-3.5 3.4-3.5 6.5C5.5 19.4 6.4 20 8 20c1.4 0 2-.7 2-2.2V12c0-.7-.4-1-1-1Z"/><path d="M15 11c2 1 3.5 3.4 3.5 6.5C18.5 19.4 17.6 20 16 20c-1.4 0-2-.7-2-2.2V12c0-.7.4-1 1-1Z"/>`,
  hati:`<path d="M4 7h12.5A3.5 3.5 0 0 1 20 10.5C20 15 16.5 18 12 18 7 18 4 14.5 4 11.5V7Z"/><path d="M7 11c1.5 1 3 1 4 0"/>`,
  ususbesar:`<path d="M6 20V8a3 3 0 0 1 3-3h6a3 3 0 0 1 3 3v3a3 3 0 0 1-3 3h-4"/><path d="M6 20h3"/>`,
  diafragma:`<path d="M4 13c3-6 13-6 16 0"/><path d="M4 13v3M20 13v3M12 11v6"/>`,
  target:`<circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4.5"/><circle cx="12" cy="12" r="1"/>`,
  bolt:`<path d="M13 3 4 14h6l-1 7 9-11h-6l1-7Z"/>`
};
function svgIcon(key){return `<svg viewBox="0 0 24 24" ${SV}>${ICON[key]||''}</svg>`;}

/* ============================================================
   ORGAN ART — referensi file SVG di folder assets/
   ============================================================ */
const ORGAN_KEYS = ['jantung','paru','lambung','usushalus','ususbesar','hati',
                    'mulut','kerongkongan','hidung','trakea','bronkus','diafragma',
                    'darah','arteri','vena'];
function organArt(key){
  if(ORGAN_KEYS.includes(key)){
    return `<img src="assets/${key}.svg" alt="${key}" style="width:100%;height:100%;object-fit:contain;display:block">`;
  }
  return svgIcon(key);
}
function organArtLarge(key){
  if(ORGAN_KEYS.includes(key)){
    return `<img src="assets/${key}.svg" alt="${key}" style="width:110px;height:110px;object-fit:contain;display:block;margin:auto">`;
  }
  return `<div style="color:var(--c)">${svgIcon(key)}</div>`;
}

const heartSVG = `<svg class="hp__heart" viewBox="0 0 24 24" fill="currentColor"><path d="M12 21s-7.5-4.9-7.5-10.6A4.1 4.1 0 0 1 12 7.2 4.1 4.1 0 0 1 19.5 10.4C19.5 16.1 12 21 12 21Z"/></svg>`;
const checkSVG = `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5L20 7"/></svg>`;
function medalSVG(c1,c2){return `<svg viewBox="0 0 64 64" fill="none"><defs><linearGradient id="mg${c1.replace('#','')}" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="${c1}"/><stop offset="1" stop-color="${c2}"/></linearGradient></defs><path d="M22 6h20l-6 20H28L22 6Z" fill="${c1}" opacity=".5"/><circle cx="32" cy="40" r="17" fill="url(#mg${c1.replace('#','')})"/><circle cx="32" cy="40" r="17" fill="none" stroke="#fff" stroke-opacity=".5" stroke-width="1.4"/><circle cx="32" cy="40" r="11" fill="none" stroke="#fff" stroke-opacity=".7" stroke-width="1.4"/><path d="M32 33l2.3 4.7 5.2.7-3.8 3.6.9 5.1L32 45l-4.6 2.4.9-5.1-3.8-3.6 5.2-.7L32 33Z" fill="#fff" fill-opacity=".95"/></svg>`;}

/* SILUET TUBUH — game (wireframe semi-transparan) */
const BODY_SVG = `
<svg class="bodymap__svg" viewBox="0 0 300 560" preserveAspectRatio="xMidYMid meet" aria-hidden="true">
  <defs>
    <linearGradient id="bodyGrad" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="rgba(255,255,255,.10)"/>
      <stop offset="1" stop-color="rgba(255,255,255,.03)"/>
    </linearGradient>
  </defs>
  <ellipse class="bodymap__fill" cx="150" cy="56" rx="37" ry="41"/>
  <path class="bodymap__fill" d="M133 92 h34 v17 q0 8 -17 11 q-17 -3 -17 -11 z"/>
  <path class="bodymap__fill" d="M150 116 c-28 0 -47 9 -50 30 c-3 22 -1 52 4 74 c-6 26 -9 56 -9 92 l4 96 c1 13 22 13 23 0 l8 -94 q4 -16 8 0 l8 94 c1 13 22 13 23 0 l4 -96 c0 -36 -3 -66 -9 -92 c5 -22 7 -52 4 -74 c-3 -21 -22 -30 -50 -30 z"/>
  <path class="bodymap__fill" d="M104 132 c-12 2 -20 10 -24 24 l-16 78 c-2 11 16 14 19 3 l15 -72 c2 -10 6 -20 9 -25 z"/>
  <path class="bodymap__fill" d="M196 132 c12 2 20 10 24 24 l16 78 c2 11 -16 14 -19 3 l-15 -72 c-2 -10 -6 -20 -9 -25 z"/>
  <line class="bodymap__center" x1="150" y1="122" x2="150" y2="500"/>
</svg>`;

/* SILUET TUBUH — Lab Maya (gunakan file aset SVG eksternal) */
const LAB_BODY_SVG = `<img src="assets/tubuh.svg" class="lab-body__img" alt="Tubuh Manusia" style="width:100%;height:100%;object-fit:contain;display:block">`;



/* =========================================================================
   DATA
   ========================================================================= */
const VIDEOS = [
  {id:'aYnxpkMXA1s', t:'Video 1 · Pengantar Sistem Organ'},
  {id:'JW46cvbZcm4', t:'Video 2 · Organ &amp; Fungsinya'},
  {id:'Fxxr_4jXiGA', t:'Video 3 · Sistem Tubuh Manusia'}
];

const KUIS = [
  {lvl:'C1', q:'Organ utama pada sistem pernapasan yang menjadi tempat pertukaran oksigen (O₂) dan karbon dioksida (CO₂) adalah ….', opt:['Jantung','Paru-paru','Lambung','Ginjal'], a:1},
  {lvl:'C1', q:'Proses pencernaan makanan pada manusia dimulai dari organ ….', opt:['Lambung','Usus halus','Mulut','Kerongkongan'], a:2},
  {lvl:'C1', q:'Organ yang bertugas memompa darah ke seluruh tubuh adalah ….', opt:['Paru-paru','Hati','Ginjal','Jantung'], a:3},
  {lvl:'C2', q:'Perhatikan organ berikut: (1) Kerongkongan (2) Mulut (3) Lambung. Urutan jalannya makanan yang benar adalah ….', opt:['(2) → (1) → (3)','(1) → (2) → (3)','(2) → (3) → (1)','(3) → (2) → (1)'], a:0},
  {lvl:'C2', q:'Hidung, tenggorokan (trakea), dan paru-paru merupakan organ penyusun sistem ….', opt:['Pencernaan','Peredaran darah','Pernapasan','Gerak'], a:2}
];
const KUIS_LULUS = 75;

const DUNIA = [
  {
    id:'pencernaan', nama:'Sistem Pencernaan', warna:'#F6A609', icon:'lambung',
    desc:'Telusuri perjalanan makanan dari mulut hingga usus halus.',
    badge:'Ahli Pencernaan',
    organ:[
      {key:'mulut', nama:'Mulut', x:50, y:13, q:'Di dalam mulut, makanan dihancurkan menjadi bagian kecil oleh gigi. Proses ini disebut pencernaan ….', opt:['Mekanik','Kimiawi','Biologis','Mikrobiologis'], a:0, ex:'Penghancuran makanan oleh gigi termasuk pencernaan mekanik.'},
      {key:'kerongkongan', nama:'Kerongkongan', x:50, y:25, q:'Gerakan meremas dinding kerongkongan yang mendorong makanan menuju lambung disebut gerak ….', opt:['Peristaltik','Refleks','Rotasi','Lurus'], a:0, ex:'Gerak peristaltik mendorong makanan walau tubuh berbaring.'},
      {key:'lambung', nama:'Lambung', x:41, y:44, q:'Cairan yang dihasilkan lambung untuk membunuh kuman sekaligus membantu mencerna protein adalah ….', opt:['Asam lambung (HCl)','Empedu','Air liur','Insulin'], a:0, ex:'Asam lambung (HCl) membunuh kuman dan mengaktifkan enzim pencerna protein.'},
      {key:'usushalus', nama:'Usus Halus', x:53, y:57, q:'Penyerapan sari-sari makanan ke dalam pembuluh darah terjadi di organ ….', opt:['Usus halus','Usus besar','Lambung','Mulut'], a:0, ex:'Usus halus adalah tempat utama penyerapan sari makanan.'}
    ]
  },
  {
    id:'peredaran', nama:'Sistem Peredaran Darah', warna:'#FB4D63', icon:'jantung',
    desc:'Ikuti aliran darah bersama jantung dan pembuluh darah.',
    badge:'Ahli Peredaran Darah',
    organ:[
      {key:'jantung', nama:'Jantung', x:46, y:33, q:'Jumlah ruang yang dimiliki jantung manusia adalah ….', opt:['4 ruang','2 ruang','3 ruang','5 ruang'], a:0, ex:'Jantung manusia memiliki 4 ruang: 2 serambi dan 2 bilik.'},
      {key:'arteri', nama:'Arteri', x:30, y:44, q:'Pembuluh darah yang mengalirkan darah keluar dari jantung disebut ….', opt:['Arteri (pembuluh nadi)','Vena (pembuluh balik)','Kapiler limfa','Pembuluh getah bening'], a:0, ex:'Arteri membawa darah keluar dari jantung; dindingnya tebal dan elastis.'},
      {key:'vena', nama:'Vena', x:70, y:44, q:'Pembuluh darah yang membawa darah kembali menuju jantung adalah ….', opt:['Vena (pembuluh balik)','Arteri (pembuluh nadi)','Aorta','Trakea'], a:0, ex:'Vena membawa darah kembali ke jantung dan memiliki katup.'},
      {key:'darah', nama:'Darah', x:50, y:56, q:'Komponen darah yang berfungsi mengangkut oksigen ke seluruh tubuh adalah ….', opt:['Sel darah merah','Sel darah putih','Keping darah (trombosit)','Plasma darah'], a:0, ex:'Sel darah merah mengandung hemoglobin pengikat oksigen.'}
    ]
  },
  {
    id:'pernapasan', nama:'Sistem Pernapasan', warna:'#3FB6F5', icon:'paru',
    desc:'Hirup udara dari hidung sampai ke gelembung paru-paru.',
    badge:'Ahli Pernapasan',
    organ:[
      {key:'hidung', nama:'Hidung', x:50, y:12, q:'Saat bernapas, udara dari luar pertama kali masuk ke tubuh melalui ….', opt:['Hidung','Paru-paru','Lambung','Jantung'], a:0, ex:'Hidung menyaring, menghangatkan, dan melembapkan udara.'},
      {key:'trakea', nama:'Trakea', x:50, y:24, q:'Saluran berbentuk batang yang menjadi jalan udara dari tenggorokan menuju paru-paru disebut ….', opt:['Trakea (batang tenggorokan)','Kerongkongan','Esofagus','Usus'], a:0, ex:'Trakea dijaga tetap terbuka oleh cincin tulang rawan.'},
      {key:'bronkus', nama:'Bronkus', x:50, y:32, q:'Trakea bercabang dua menuju paru-paru kanan dan kiri. Percabangan ini disebut ….', opt:['Bronkus','Alveolus','Diafragma','Faring'], a:0, ex:'Bronkus terus bercabang halus menjadi bronkiolus.'},
      {key:'paru', nama:'Paru-paru', x:63, y:35, q:'Pertukaran oksigen dan karbon dioksida di paru-paru berlangsung di gelembung kecil bernama ….', opt:['Alveolus','Bronkus','Trakea','Hidung'], a:0, ex:'Alveolus adalah gelembung tempat pertukaran gas berlangsung.'}
    ]
  }
];

const LAB = {
  pencernaan:{nama:'Sistem Pencernaan', warna:'#F6A609', icon:'lambung', organ:[
    {key:'mulut', nama:'Mulut', x:50, y:13, fungsi:'Mengunyah dan menghaluskan makanan; air liur mulai mencerna karbohidrat.', fakta:'Air liur mengandung enzim amilase (ptialin) yang memecah zat tepung menjadi gula.'},
    {key:'kerongkongan', nama:'Kerongkongan', x:50, y:25, fungsi:'Menyalurkan makanan dari mulut ke lambung melalui gerak peristaltik.', fakta:'Makanan didorong oleh otot, bukan gravitasi — kamu tetap bisa menelan walau berbaring.'},
    {key:'lambung', nama:'Lambung', x:41, y:43, fungsi:'Mencerna makanan secara kimiawi dengan asam lambung dan enzim.', fakta:'Asam lambung sangat kuat, tetapi dinding lambung dilindungi lapisan lendir.'},
    {key:'hati', nama:'Hati', x:60, y:43, fungsi:'Menghasilkan empedu untuk mencerna lemak dan menyaring zat berbahaya.', fakta:'Hati adalah organ dalam terbesar dan mampu beregenerasi.'},
    {key:'usushalus', nama:'Usus Halus', x:46, y:58, fungsi:'Tempat utama penyerapan sari-sari makanan ke dalam darah.', fakta:'Bila dibentangkan, panjang usus halus dewasa sekitar 6–7 meter.'},
    {key:'ususbesar', nama:'Usus Besar', x:62, y:60, fungsi:'Menyerap air dan membentuk sisa makanan menjadi feses.', fakta:'Di usus besar hidup miliaran bakteri baik yang membantu tubuh.'}
  ]},
  peredaran:{nama:'Sistem Peredaran Darah', warna:'#FB4D63', icon:'jantung', organ:[
    {key:'jantung', nama:'Jantung', x:46, y:34, beat:true, fungsi:'Memompa darah ke seluruh tubuh tanpa henti.', fakta:'Jantung berdetak 60–100 kali per menit, lebih dari 100.000 kali sehari.'},
    {key:'arteri', nama:'Arteri', x:30, y:46, fungsi:'Membawa darah keluar dari jantung; umumnya kaya oksigen.', fakta:'Dinding arteri tebal dan elastis untuk menahan tekanan pompa jantung.'},
    {key:'vena', nama:'Vena', x:70, y:46, fungsi:'Membawa darah kembali menuju jantung.', fakta:'Vena memiliki katup agar darah tidak mengalir mundur.'},
    {key:'darah', nama:'Darah', x:50, y:60, fungsi:'Mengangkut oksigen, sari makanan, serta melawan penyakit.', fakta:'Tubuh manusia dewasa memiliki sekitar 4–5 liter darah.'}
  ]},
  pernapasan:{nama:'Sistem Pernapasan', warna:'#3FB6F5', icon:'paru', organ:[
    {key:'hidung', nama:'Hidung', x:50, y:12, fungsi:'Jalan masuk udara; menyaring, menghangatkan, dan melembapkan udara.', fakta:'Rambut dan lendir di hidung menyaring debu serta kuman.'},
    {key:'trakea', nama:'Trakea', x:50, y:24, fungsi:'Saluran udara menuju paru-paru, dijaga tetap terbuka oleh tulang rawan.', fakta:'Cincin tulang rawan berbentuk huruf C menjaga trakea tidak menutup.'},
    {key:'bronkus', nama:'Bronkus', x:50, y:32, fungsi:'Cabang saluran udara yang menuju paru-paru kanan dan kiri.', fakta:'Bronkus bercabang halus menjadi bronkiolus seperti ranting pohon.'},
    {key:'paru', nama:'Paru-paru', x:63, y:37, breathe:true, fungsi:'Tempat pertukaran O₂ dan CO₂ di dalam alveolus.', fakta:'Jumlah alveolus mencapai ratusan juta agar permukaan pertukaran gas sangat luas.'},
    {key:'diafragma', nama:'Diafragma', x:42, y:50, fungsi:'Otot di bawah paru-paru yang mengatur tarik dan embus napas.', fakta:'Saat diafragma turun, udara masuk; saat naik, udara keluar.'}
  ]}
};

/* =========================================================================
   STATE
   ========================================================================= */
const S = {
  name:'', cls:'',
  kuisIdx:0, kuisAns:Array(KUIS.length).fill(null), kuisDone:false, kuisLocked:false, kuisScore:0,
  hp:5, maxHp:5, score:0,
  gPhase:'intro', gWorld:0, gOrgan:0, gAnswered:false, gPick:null,
  completed:{}, badges:[],
  labSys:'pencernaan', labOrgan:0,
  unlocked:{petunjuk:false, materi:false, kuis:false, game:false, lab:false, selesai:false}
};

/* =========================================================================
   NAVIGASI & TRACK
   ========================================================================= */
const STAGES = [
  {id:'petunjuk', label:'Petunjuk'},
  {id:'materi',   label:'Materi'},
  {id:'kuis',     label:'Kuis'},
  {id:'game',     label:'Petualangan'},
  {id:'lab',      label:'Lab'},
  {id:'selesai',  label:'Sertifikat'}
];
let current = 'splash';

function show(id){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  const el = document.getElementById('view-'+id);
  if(el) el.classList.add('active');
  current = id;
  window.scrollTo({top:0,behavior:'smooth'});
  renderTrack();
  if(id==='kuis') renderKuis();
  if(id==='game') renderGame();
  if(id==='lab'){ renderLab(); const cb=document.getElementById('toCertBtn'); if(cb){ cb.disabled=!S.unlocked.selesai; cb.title=S.unlocked.selesai?'':'Selesaikan Petualangan untuk membuka sertifikat'; } }
  if(id==='selesai') renderFinale();
}

function renderTrack(){
  const lockSVG = `<svg class="track__lock" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="5" y="11" width="14" height="9" rx="2"/><path d="M8 11V8a4 4 0 0 1 8 0v3"/></svg>`;
  let h='';
  STAGES.forEach((st,i)=>{
    const unlocked = S.unlocked[st.id];
    const isActive = current===st.id;
    let cls='track__step';
    if(isActive) cls+=' active';
    else if(unlocked) cls+=' done clickable';
    else cls+=' locked';
    const inner = unlocked
      ? `<span class="n">${i+1}</span>`
      : `<span class="n">${lockSVG}</span>`;
    h+=`<button class="${cls}" data-stage="${st.id}" ${unlocked?'':'disabled aria-disabled="true"'}>${inner}<span>${st.label}</span></button>`;
    if(i<STAGES.length-1) h+=`<span class="track__sep"></span>`;
  });
  const t=document.getElementById('track');
  t.innerHTML=h;
  t.querySelectorAll('.clickable').forEach(b=>{
    b.addEventListener('click',()=>show(b.dataset.stage));
  });
}

function unlock(id){ S.unlocked[id]=true; }

/* tombol data-go */
document.addEventListener('click',e=>{
  const g=e.target.closest('[data-go]');
  if(g && current!=='splash'){
    const dest=g.dataset.go;
    if(S.unlocked[dest]) show(dest);
  }
});

/* =========================================================================
   SPLASH / START
   ========================================================================= */
function buildSteps(){
  const data=[
    ['Daftar','Isi nama dan kelasmu sebagai calon dokter.'],
    ['Pelajari Materi','Tonton video dan amati tiga sistem organ tubuh.'],
    ['Kuis Kesiapan','Kerjakan 5 soal — lulus jika nilaimu minimal 75.'],
    ['Petualangan Peta Tubuh','Sembuhkan tiap organ, jaga nyawa, kumpulkan lencana.'],
    ['Lab Maya','Jelajahi organ lebih dalam, lalu raih sertifikat Dokter Cilik.']
  ];
  document.getElementById('steps').innerHTML = data.map((d,i)=>
    `<div class="step"><div class="step__n">${i+1}</div><div class="step__b"><strong>${d[0]}</strong><span>${d[1]}</span></div></div>`
  ).join('');
}

function buildMateri(){
  document.getElementById('videos').innerHTML = VIDEOS.map((v,i)=>
    `<div class="vcard" id="vcard${i}"><div class="vframe">
      <iframe id="vframe${i}" src="https://www.youtube.com/embed/${v.id}" title="${v.t}" loading="lazy" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
      <div class="vfallback"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M3 3l18 18M10.7 5.1A9 9 0 0 1 21 12M6.3 6.3A9 9 0 0 0 3 12M8.5 8.5A5 5 0 0 1 16 12"/></svg>Video tidak dapat dimuat. Silakan lanjutkan mempelajari materi yang tersedia.</div>
    </div><div class="vcard__b"><div class="vcard__t">${v.t}</div><div class="vcard__s">Sumber: Ruang Murid · <a href="https://youtu.be/${v.id}" target="_blank" rel="noopener" style="color:var(--cyan)">Tonton di YouTube ↗</a></div></div></div>`
  ).join('');

  document.getElementById('sysGrid').innerHTML = DUNIA.map(d=>{
    const chips = d.organ.map(o=>`<span class="organ-chip">${o.nama}</span>`).join('');
    return `<div class="syscard" style="--c:${d.warna}"><div class="syscard__ic">${svgIcon(d.icon)}</div>
      <h4>${d.nama}</h4><p>${d.desc}</p>
      <div class="syscard__organs">${chips}</div></div>`;
  }).join('');

  // fallback hanya saat koneksi benar-benar terputus saat halaman dipakai
  // (navigator.onLine tidak dipakai sebagai gerbang awal karena sering salah/false-negative)
}

document.getElementById('startBtn').addEventListener('click',startGame);
[ 'inName','inClass' ].forEach(id=>{
  document.getElementById(id).addEventListener('keydown',e=>{ if(e.key==='Enter') startGame(); });
});

function startGame(){
  const name=document.getElementById('inName').value.trim();
  const cls=document.getElementById('inClass').value.trim();
  const err=document.getElementById('enrollErr');
  if(!name){ err.textContent='Tulis namamu dulu, ya.'; document.getElementById('inName').focus(); return; }
  if(!cls){ err.textContent='Jangan lupa isi kelasmu.'; document.getElementById('inClass').focus(); return; }
  err.textContent='';
  S.name=name; S.cls=cls;
  document.getElementById('hudName').textContent=name;
  document.getElementById('hudClass').textContent='Kelas '+cls;
  document.body.classList.add('started');
  unlock('petunjuk'); unlock('materi'); unlock('kuis');
  show('petunjuk');
}

/* =========================================================================
   VITALS HUD
   ========================================================================= */
function renderHP(){
  const wrap=document.getElementById('hp');
  let h='';
  for(let i=0;i<S.maxHp;i++){
    h+= heartSVG.replace('class="hp__heart"', 'class="hp__heart'+(i>=S.hp?' lost':'')+'"');
  }
  wrap.innerHTML=h;
}
function updateHUD(){
  document.getElementById('vitals').hidden = !S.unlocked.game;
  document.getElementById('hudScore').textContent=S.score;
  document.getElementById('hudBadges').textContent=S.badges.length;
  renderHP();
}
function loseHP(){
  S.hp=Math.max(0,S.hp-1);
  renderHP();
  const hearts=document.querySelectorAll('#hp .hp__heart');
  if(hearts[S.hp]){ hearts[S.hp].classList.add('hit'); }
}

/* =========================================================================
   KUIS
   ========================================================================= */
function renderKuis(){
  if(S.kuisDone){ renderKuisResult(); return; }
  const i=S.kuisIdx, item=KUIS[i];
  const picked=S.kuisAns[i];
  const keys=['A','B','C','D'];
  const opts=item.opt.map((o,j)=>{
    let cls='opt'+(picked===j?' sel':'');
    return `<button class="${cls}" data-opt="${j}"><span class="opt__key">${keys[j]}</span><span>${o}</span></button>`;
  }).join('');
  const pct=Math.round((i)/KUIS.length*100);
  document.getElementById('quizWrap').innerHTML=`
    <div class="quiz-top">
      <div class="quiz-prog"><div class="quiz-prog__bar" style="width:${pct}%"></div></div>
      <div class="quiz-count">Soal ${i+1}/${KUIS.length}</div>
    </div>
    <div class="qbox">
      <span class="qlevel">${svgIconMini()} Level ${item.lvl}</span>
      <div class="qtext">${item.q}</div>
      <div class="opts" id="qOpts">${opts}</div>
      <div class="navbtns">
        ${i>0?'<button class="btn btn--ghost" id="qPrev"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 12H5M11 6l-6 6 6 6"/></svg> Sebelumnya</button>':''}
        <button class="btn btn--primary" id="qNext" ${picked===null?'disabled':''}>${i===KUIS.length-1?'Lihat Hasil':'Lanjut'}
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
      </div>
    </div>`;
  document.querySelectorAll('#qOpts .opt').forEach(b=>{
    b.addEventListener('click',()=>{
      S.kuisAns[i]=parseInt(b.dataset.opt);
      document.querySelectorAll('#qOpts .opt').forEach(x=>x.classList.remove('sel'));
      b.classList.add('sel');
      document.getElementById('qNext').disabled=false;
    });
  });
  const prev=document.getElementById('qPrev');
  if(prev) prev.addEventListener('click',()=>{ S.kuisIdx--; renderKuis(); });
  document.getElementById('qNext').addEventListener('click',()=>{
    if(S.kuisAns[i]===null) return;
    if(i===KUIS.length-1){ finishKuis(); }
    else { S.kuisIdx++; renderKuis(); }
  });
}
function svgIconMini(){return `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="width:13px;height:13px"><path d="M9 18h6M10 22h4M12 2a7 7 0 0 0-4 12.7c.6.5 1 1.3 1 2.1V18h6v-1.2c0-.8.4-1.6 1-2.1A7 7 0 0 0 12 2Z"/></svg>`;}

function finishKuis(){
  let correct=0;
  KUIS.forEach((k,i)=>{ if(S.kuisAns[i]===k.a) correct++; });
  S.kuisScore=Math.round(correct/KUIS.length*100);
  S.kuisDone=true;
  renderKuisResult();
}

function renderKuisResult(){
  const lulus = S.kuisScore>=KUIS_LULUS;
  const ringC = lulus? 'var(--good)' : 'var(--bad)';
  let correct=0; KUIS.forEach((k,i)=>{ if(S.kuisAns[i]===k.a) correct++; });
  if(lulus){ unlock('game'); unlock('lab'); }
  document.getElementById('quizWrap').innerHTML=`
    <div class="result">
      <div class="result__ring" style="--p:${S.kuisScore};--ring-c:${ringC}">
        <div class="result__score">${S.kuisScore}<small>NILAI</small></div>
      </div>
      <div class="result__msg" style="color:${ringC}">${lulus?'Hebat, kamu Lulus! 🎉':'Belum Lulus'}</div>
      <p class="result__detail">Jawaban benar ${correct} dari ${KUIS.length}. ${lulus?'Petualangan Peta Tubuh kini terbuka!':'Pelajari kembali materi, lalu coba lagi. Butuh nilai minimal '+KUIS_LULUS+'.'}</p>
      <div class="navbtns" style="justify-content:center">
        ${lulus
          ? `<button class="btn btn--primary" id="goGame">Mulai Petualangan <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>`
          : `<button class="btn btn--ghost" id="reviewMat"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 12H5M11 6l-6 6 6 6"/></svg> Pelajari Materi</button>
             <button class="btn btn--primary" id="retryKuis">Ulangi Kuis</button>`
        }
      </div>
    </div>`;
  updateHUD();
  if(lulus){
    document.getElementById('goGame').addEventListener('click',()=>show('game'));
  } else {
    document.getElementById('retryKuis').addEventListener('click',()=>{
      S.kuisIdx=0; S.kuisAns=Array(KUIS.length).fill(null); S.kuisDone=false; S.kuisScore=0; renderKuis();
    });
    document.getElementById('reviewMat').addEventListener('click',()=>show('materi'));
  }
}

/* =========================================================================
   GAME / PETUALANGAN
   ========================================================================= */
function renderGame(){
  updateHUD();
  const root=document.getElementById('gameRoot');
  if(S.gPhase==='gameover'){ root.innerHTML=gameOverHTML(); bindGameOver(); return; }
  if(S.gPhase==='win'){ root.innerHTML=winHTML(); bindWin(); return; }

  const w=DUNIA[S.gWorld];
  const c=w.warna;
  const done=w.organ.filter(o=>S.completed[w.id+':'+o.key]).length;
  const dots=w.organ.map((o,i)=>{
    let cl='world-dot';
    if(S.completed[w.id+':'+o.key]) cl+=' done';
    else if(i===S.gOrgan) cl+=' now';
    return `<span class="${cl}"></span>`;
  }).join('');

  const nodes=w.organ.map((o,i)=>{
    let st='node--locked';
    const isDone=S.completed[w.id+':'+o.key];
    if(isDone) st='node--done';
    else if(i===S.gOrgan) st='node--active';
    const clickable=(i===S.gOrgan && !isDone);
    return `<div class="node ${st}" style="left:${o.x}%;top:${o.y}%">
      <button class="node__btn" ${clickable?'data-organ="'+i+'"':'disabled'} aria-label="${o.nama}">${svgIcon(o.key)}${isDone?'<span class="node__check">'+checkSVG+'</span>':''}</button>
      <span class="node__label">${o.nama}</span></div>`;
  }).join('');

  root.innerHTML=`
    <div class="game-head" style="--c:${c}">
      <span class="world-badge"><span class="world-badge__ic">${svgIcon(w.icon)}</span>${w.nama}</span>
      <span class="world-prog">Organ ${done}/${w.organ.length}</span>
      <span class="world-dots" style="margin-left:0">${dots}</span>
    </div>
    <div class="game" style="--c:${c}">
      <div class="board">
        <div class="bodymap">${BODY_SVG}${nodes}</div>
      </div>
      <div class="gpanel" id="gpanel" style="--c:${c}">${panelHTML(w)}</div>
    </div>`;

  // klik organ
  root.querySelectorAll('.node__btn[data-organ]').forEach(b=>{
    b.addEventListener('click',()=>{ openOrgan(parseInt(b.dataset.organ)); });
  });
  bindPanel(w);
}

function panelHTML(w){
  const o=w.organ[S.gOrgan];
  // belum mulai / intro organ
  if(!S.gAnswered && S.gPick===null && S.gPhase!=='question'){
    return `<div class="gpanel__k">${svgIcon(w.icon)} Misi: ${w.nama}</div>
      <div class="gpanel__title">Level ${S.gOrgan+1}: ${o?o.nama:''}</div>
      <p class="gpanel__intro">${w.desc} Ketuk organ <b style="color:var(--c)">${o?o.nama:''}</b> yang berdenyut pada peta tubuh untuk memulai pemeriksaan.</p>
      <div class="gpanel__hint"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9"/><path d="M12 8v5M12 16h.01"/></svg> Jawaban salah mengurangi 1 nyawa.</div>`;
  }
  return questionHTML(w);
}

function questionHTML(w){
  const o=w.organ[S.gOrgan];
  const keys=['A','B','C','D'];
  const opts=o.opt.map((t,j)=>{
    let cls='qg-opt';
    if(S.gAnswered){
      if(j===o.a) cls+=' correct';
      else if(j===S.gPick) cls+=' wrong';
      cls+=' locked';
    } else if(S.gPick===j) cls+=' sel';
    return `<button class="${cls}" data-qopt="${j}"><span class="qg-opt__k">${keys[j]}</span><span>${t}</span></button>`;
  }).join('');
  let fb='', btn='';
  if(S.gAnswered){
    const ok=S.gPick===o.a;
    fb=`<div class="qg-fb ${ok?'ok':'no'}">${ok?'✓ Tepat! ':'✗ Belum tepat. '}${o.ex}</div>`;
    const last = (S.gOrgan===w.organ.length-1);
    btn=`<button class="btn btn--sys" id="gNext">${last?'Selesaikan Misi':'Organ Berikutnya'}
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>`;
  } else {
    btn=`<button class="btn btn--sys" id="gAnswer" ${S.gPick===null?'disabled':''}>Periksa Jawaban</button>`;
  }
  return `<div class="gpanel__k">${svgIcon(o.key)} Pemeriksaan: ${o.nama}</div>
    <div class="qg-text">${o.q}</div>
    <div class="qg-opts" id="gOpts">${opts}</div>
    ${fb}${btn}`;
}

function openOrgan(i){
  S.gOrgan=i; S.gPhase='question'; S.gAnswered=false; S.gPick=null;
  const w=DUNIA[S.gWorld];
  const p=document.getElementById('gpanel');
  p.innerHTML=questionHTML(w);
  bindPanel(w);
}

function bindPanel(w){
  const opts=document.getElementById('gOpts');
  if(opts){
    opts.querySelectorAll('.qg-opt').forEach(b=>{
      if(S.gAnswered) return;
      b.addEventListener('click',()=>{
        S.gPick=parseInt(b.dataset.qopt);
        opts.querySelectorAll('.qg-opt').forEach(x=>x.classList.remove('sel'));
        b.classList.add('sel');
        const a=document.getElementById('gAnswer'); if(a) a.disabled=false;
      });
    });
  }
  const ans=document.getElementById('gAnswer');
  if(ans) ans.addEventListener('click',()=>answerOrgan(w));
  const nx=document.getElementById('gNext');
  if(nx) nx.addEventListener('click',()=>nextOrgan(w));
}

function answerOrgan(w){
  if(S.gPick===null) return;
  const o=w.organ[S.gOrgan];
  S.gAnswered=true;
  if(S.gPick===o.a){ S.score+=100; }
  else { S.score+=20; loseHP(); }
  S.completed[w.id+':'+o.key]=true;
  updateHUD();
  // re-render board (tandai done) + panel feedback
  renderGame();
  // jika nyawa habis → game over setelah jeda kecil tetap di feedback
  if(S.hp<=0){
    setTimeout(()=>{ S.gPhase='gameover'; renderGame(); }, 900);
  }
}

function nextOrgan(w){
  const allDone=w.organ.every(o=>S.completed[w.id+':'+o.key]);
  if(allDone){
    // beri lencana sistem
    if(!S.badges.find(b=>b.id===w.id)){
      S.badges.push({id:w.id, nama:w.badge, c:w.warna});
    }
    updateHUD();
    showWorldReward(w);
    return;
  }
  // organ berikutnya = indeks pertama yang belum selesai
  const nextIdx=w.organ.findIndex(o=>!S.completed[w.id+':'+o.key]);
  S.gOrgan=nextIdx; S.gPhase='intro'; S.gAnswered=false; S.gPick=null;
  renderGame();
}

function showWorldReward(w){
  const root=document.getElementById('gameRoot');
  const isLast=(S.gWorld===DUNIA.length-1);
  root.innerHTML=`
    <div class="board" style="--c:${w.warna};min-height:auto;padding:40px 22px">
      <div class="reward">
        <div class="reward__medal">${medalSVG(w.warna, shade(w.warna))}</div>
        <div class="reward__t">Lencana "${w.badge}" diraih!</div>
        <p class="reward__s">Kamu telah menguasai semua organ ${w.nama.replace('Sistem ','')}. ${isLast?'Tinggal satu langkah menuju gelar Dokter Cilik!':'Lanjutkan ke sistem organ berikutnya.'}</p>
        <div class="navbtns" style="justify-content:center">
          <button class="btn btn--gold" id="worldNext">${isLast?'Selesaikan Petualangan':'Sistem Berikutnya'}
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
        </div>
      </div>
    </div>`;
  document.getElementById('worldNext').addEventListener('click',()=>{
    if(isLast){ winAdventure(); }
    else { S.gWorld++; S.gOrgan=0; S.gPhase='intro'; S.gAnswered=false; S.gPick=null; renderGame(); }
  });
}

function winAdventure(){
  if(!S.badges.find(b=>b.id==='dokter')){
    S.badges.push({id:'dokter', nama:'Dokter Cilik', c:'#FCD34D'});
  }
  unlock('selesai');
  S.gPhase='win';
  updateHUD();
  renderGame();
  fireConfetti();
}

function winHTML(){
  return `<div class="board" style="--c:#FCD34D;min-height:auto;padding:40px 22px">
    <div class="reward">
      <div class="reward__medal">${medalSVG('#FCD34D','#E9B824')}</div>
      <div class="reward__t" style="font-size:1.7rem">🏅 Selamat, Dokter Cilik!</div>
      <p class="reward__s">Dr. ${S.name}, kamu berhasil menyembuhkan seluruh organ dari tiga sistem tubuh dengan skor <b style="color:var(--cyan)">${S.score}</b>.</p>
      <div class="navbtns" style="justify-content:center">
        <button class="btn btn--ghost" id="goLabFromWin"><svg viewBox="0 0 24 24" ${SV}>${ICON.target}</svg> Buka Lab Maya</button>
        <button class="btn btn--gold" id="goCertFromWin">Lihat Sertifikat
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
      </div>
    </div></div>`;
}
function bindWin(){
  document.getElementById('goLabFromWin').addEventListener('click',()=>show('lab'));
  document.getElementById('goCertFromWin').addEventListener('click',()=>show('selesai'));
}

function gameOverHTML(){
  return `<div class="gameover">
    <div class="gameover__ic"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M12 21s-7.5-4.9-7.5-10.6A4.1 4.1 0 0 1 12 7.2 4.1 4.1 0 0 1 19.5 10.4C19.5 16.1 12 21 12 21Z"/><path d="M9 11l6 0M9 11l-1.5-1.5M15 11l1.5-1.5" stroke-width="1.4"/></svg></div>
    <div class="result__msg">Nyawa Habis</div>
    <p class="result__detail">Jangan menyerah, Dokter! Setiap dokter hebat pernah gagal. Pelajari lagi materinya dan coba sekali lagi — kamu pasti bisa.</p>
    <div class="navbtns" style="justify-content:center">
      <button class="btn btn--ghost" id="goLab2"><svg viewBox="0 0 24 24" ${SV}>${ICON.target}</svg> Buka Lab Maya</button>
      <button class="btn btn--primary" id="retryGame">Coba Lagi</button>
    </div>
  </div>`;
}
function bindGameOver(){
  unlock('lab');
  renderTrack();
  document.getElementById('retryGame').addEventListener('click',resetGame);
  document.getElementById('goLab2').addEventListener('click',()=>show('lab'));
}

function resetGame(){
  S.hp=S.maxHp; S.score=0;
  S.gPhase='intro'; S.gWorld=0; S.gOrgan=0; S.gAnswered=false; S.gPick=null;
  S.completed={}; S.badges=[]; // reset lencana petualangan
  updateHUD();
  renderGame();
}

function shade(hex){
  const n=parseInt(hex.slice(1),16);
  let r=(n>>16)&255,g=(n>>8)&255,b=n&255;
  r=Math.round(r*.72);g=Math.round(g*.72);b=Math.round(b*.72);
  return '#'+((1<<24)+(r<<16)+(g<<8)+b).toString(16).slice(1);
}

/* konfeti */
function fireConfetti(){
  if(window.matchMedia('(prefers-reduced-motion: reduce)').matches) return;
  const cols=['#FCD34D','#34E0E8','#FB4D63','#3FB6F5','#34E3B0'];
  const box=document.createElement('div'); box.className='confetti';
  for(let i=0;i<40;i++){
    const s=document.createElement('i');
    s.style.left=Math.random()*100+'%';
    s.style.background=cols[i%cols.length];
    s.style.animationDuration=(2.4+Math.random()*1.8)+'s';
    s.style.animationDelay=(Math.random()*.5)+'s';
    s.style.transform='rotate('+(Math.random()*360)+'deg)';
    box.appendChild(s);
  }
  document.body.appendChild(box);
  setTimeout(()=>box.remove(),5200);
}

/* =========================================================================
   LAB MAYA
   ========================================================================= */
function renderLab(){
  const root=document.getElementById('labRoot');
  const sysKeys=Object.keys(LAB);
  const tabs=sysKeys.map(k=>{
    const s=LAB[k];
    return `<button class="lab-tab${k===S.labSys?' active':''}" data-sys="${k}" style="--c:${s.warna}">${svgIcon(s.icon)} ${s.nama.replace('Sistem ','')}</button>`;
  }).join('');
  const sys=LAB[S.labSys]; const c=sys.warna;

  const nodes=sys.organ.map((o,i)=>{
    let anim=''; if(o.beat) anim=' heartbeat'; else if(o.breathe) anim=' breathe';
    return `<div class="lab-node${i===S.labOrgan?' active':''}${anim}" style="left:${o.x}%;top:${o.y}%">
      <button class="lab-node__btn" data-organ="${i}" aria-label="${o.nama}">${organArt(o.key)}</button>
      <span class="lab-node__label">${o.nama}</span></div>`;
  }).join('');

  root.innerHTML=`
    <div class="lab-tabs">${tabs}</div>
    <div class="lab" style="--c:${c}">
      <div class="lab-stage">
        <div class="lab-scan"></div>
        <div class="lab-body">${LAB_BODY_SVG}${nodes}</div>
      </div>
      <div class="lab-info" id="labInfo" style="--c:${c}">${labInfoHTML(sys)}</div>
    </div>`;

  root.querySelectorAll('.lab-tab').forEach(b=>{
    b.addEventListener('click',()=>{ S.labSys=b.dataset.sys; S.labOrgan=0; renderLab(); });
  });
  root.querySelectorAll('.lab-node__btn').forEach(b=>{
    b.addEventListener('click',()=>{
      S.labOrgan=parseInt(b.dataset.organ);
      root.querySelectorAll('.lab-node').forEach(n=>n.classList.remove('active'));
      b.closest('.lab-node').classList.add('active');
      document.getElementById('labInfo').innerHTML=labInfoHTML(LAB[S.labSys]);
    });
  });
}

function labInfoHTML(sys){
  const o=sys.organ[S.labOrgan];
  if(!o){
    return `<div class="lab-info__empty"><svg viewBox="0 0 24 24" ${SV}>${ICON.target}</svg>Ketuk salah satu organ pada peta tubuh.</div>`;
  }
  return `<div class="lab-info__art">${organArtLarge(o.key)}</div>
    <div class="lab-info__k">${sys.nama}</div>
    <div class="lab-info__name">${o.nama}</div>
    <div class="lab-info__row">
      <div class="lab-info__lab"><svg viewBox="0 0 24 24" ${SV}><path d="M9 3v6l-5 8a2 2 0 0 0 1.8 3h12.4A2 2 0 0 0 20 17l-5-8V3"/><path d="M8 3h8"/></svg> Fungsi</div>
      <div class="lab-info__txt">${o.fungsi}</div>
    </div>
    <div class="lab-info__fact">
      <div class="lab-info__lab"><svg viewBox="0 0 24 24" ${SV}><path d="M9 18h6M10 22h4M12 2a7 7 0 0 0-4 12.7c.6.5 1 1.3 1 2.1V18h6v-1.2c0-.8.4-1.6 1-2.1A7 7 0 0 0 12 2Z"/></svg> Tahukah kamu?</div>
      <div class="lab-info__txt">${o.fakta}</div>
    </div>`;
}

/* =========================================================================
   SERTIFIKAT / SELESAI
   ========================================================================= */
function renderFinale(){
  const tgl=new Date().toLocaleDateString('id-ID',{day:'numeric',month:'long',year:'numeric'});
  const badgeCards = S.badges.map(b=>{
    const c2 = b.id==='dokter'? '#E9B824' : shade(b.c);
    return `<div class="cert-badge"><div class="cert-badge__m">${medalSVG(b.c,c2)}</div><div class="cert-badge__t">${b.nama}</div></div>`;
  }).join('');
  document.getElementById('finaleRoot').innerHTML=`
    <div class="eyebrow" style="justify-content:center">Tahap 6 — Selesai</div>
    <h1 class="title" style="text-align:center">Misi Tuntas! 🎓</h1>
    <div class="cert" id="cert">
      <div class="cert__seal"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round"><path d="M6 3v5a4 4 0 0 0 8 0V3"/><circle cx="18" cy="15.5" r="2.6"/><path d="M10 12v1.5a6.5 6.5 0 0 0 6.5 6.5"/></svg></div>
      <div class="cert__k">Sertifikat Penghargaan</div>
      <div class="cert__title">Dokter Cilik</div>
      <div class="cert__sub">dengan bangga diberikan kepada</div>
      <div class="cert__name">${S.name||'—'}</div>
      <div class="cert__line"></div>
      <div class="cert__sub">Kelas ${S.cls||'—'}</div>
      <p class="cert__desc">Telah menyelesaikan Petualangan "Jadi Dokter Spesialis" dan mampu menyebutkan organ utama penyusun sistem pencernaan, peredaran darah, dan pernapasan dengan skor akhir <b>${S.score}</b>.</p>
      <div class="cert__badges">${badgeCards}</div>
      <div class="cert__meta">
        <div><b>Pengembang</b>Salehuddin — Guru SMP Negeri Sinombayuga</div>
        <div><b>Sumber</b>Ruang Murid &amp; Buku IPA SMP</div>
        <div><b>Tanggal</b>${tgl}</div>
      </div>
    </div>
    <div class="navbtns" style="justify-content:center">
      <button class="btn btn--ghost" onclick="window.print()"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 9V3h12v6M6 18H4a2 2 0 0 1-2-2v-4a2 2 0 0 1 2-2h16a2 2 0 0 1 2 2v4a2 2 0 0 1-2 2h-2M6 14h12v7H6z"/></svg> Cetak Sertifikat</button>
      <button class="btn btn--ghost" id="goLabFromCert"><svg viewBox="0 0 24 24" ${SV}>${ICON.target}</svg> Kembali ke Lab</button>
      <button class="btn btn--primary" id="playAgain">Main Lagi dari Awal</button>
    </div>`;
  document.getElementById('playAgain').addEventListener('click',()=>location.reload());
  document.getElementById('goLabFromCert').addEventListener('click',()=>show('lab'));
}

/* =========================================================================
   INIT
   ========================================================================= */
buildSteps();
buildMateri();
renderTrack();
window.addEventListener('online',()=>document.querySelectorAll('.vcard').forEach(c=>c.classList.remove('offline')));
window.addEventListener('offline',()=>document.querySelectorAll('.vcard').forEach(c=>c.classList.add('offline')));
</script>
</body>
</html>
