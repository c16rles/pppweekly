# pppweekly<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WWP Tracker</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&family=DM+Mono:wght@400;500&family=Playfair+Display:wght@600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0f1117;
  --bg2: #161b26;
  --bg3: #1e2535;
  --bg4: #252d40;
  --border: rgba(255,255,255,0.07);
  --border2: rgba(255,255,255,0.12);
  --text: #e8eaf0;
  --text2: #8b92a8;
  --text3: #565e78;
  --green: #4ade9a;
  --green-bg: rgba(74,222,154,0.1);
  --green-dim: rgba(74,222,154,0.06);
  --blue: #60a5fa;
  --blue-bg: rgba(96,165,250,0.1);
  --amber: #fbbf24;
  --amber-bg: rgba(251,191,36,0.1);
  --red: #f87171;
  --red-bg: rgba(248,113,113,0.1);
  --accent: #4ade9a;
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { font-size: 15px; }
body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  line-height: 1.6;
}

/* Subtle grid texture */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.015) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.015) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
  z-index: 0;
}

.wrap { position: relative; z-index: 1; max-width: 1100px; margin: 0 auto; padding: 2rem 1.5rem; }

/* Header */
.header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 2.5rem;
  gap: 1rem;
  flex-wrap: wrap;
}
.header-left { display: flex; align-items: center; gap: 14px; }
.logo-mark {
  width: 46px; height: 46px;
  background: var(--green);
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  color: #0f1117;
  font-size: 22px;
}
.app-name {
  font-family: 'Playfair Display', serif;
  font-size: 26px;
  color: var(--text);
  letter-spacing: -0.5px;
}
.app-sub { font-size: 12px; color: var(--text3); margin-top: 2px; letter-spacing: 0.3px; }

.sync-pill {
  display: flex; align-items: center; gap: 8px;
  padding: 8px 14px;
  background: var(--bg3);
  border: 1px solid var(--border);
  border-radius: 40px;
  font-size: 12px;
  color: var(--text2);
  cursor: pointer;
  transition: all .2s;
}
.sync-pill:hover { border-color: var(--border2); color: var(--text); }
.sdot { width: 7px; height: 7px; border-radius: 50%; background: var(--green); }
.sdot.stale { background: var(--amber); }
.sdot.err { background: var(--red); }

/* Stats */
.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-bottom: 2rem;
}
.stat {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px 18px;
  transition: border-color .2s;
}
.stat:hover { border-color: var(--border2); }
.stat-label { font-size: 11px; color: var(--text3); text-transform: uppercase; letter-spacing: .7px; margin-bottom: 6px; }
.stat-num { font-size: 28px; font-weight: 500; }
.stat-num.g { color: var(--green); }
.stat-num.b { color: var(--blue); }
.stat-num.a { color: var(--amber); }

/* Nav */
.nav-wrapper {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 5px;
  display: flex;
  flex-wrap: wrap;
  gap: 3px;
  margin-bottom: 1.5rem;
}
.nav-btn {
  padding: 7px 13px;
  font-size: 12px;
  font-family: 'DM Sans', sans-serif;
  border: none;
  background: none;
  cursor: pointer;
  color: var(--text2);
  border-radius: 10px;
  transition: all .15s;
  white-space: nowrap;
}
.nav-btn:hover { color: var(--text); background: var(--bg3); }
.nav-btn.on {
  background: var(--bg4);
  color: var(--text);
  font-weight: 500;
  border: 1px solid var(--border2);
}

/* Panels */
.panel {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 1.5rem;
  margin-bottom: 1rem;
}
.panel-title {
  font-size: 13px;
  font-weight: 500;
  color: var(--text2);
  text-transform: uppercase;
  letter-spacing: .6px;
  margin-bottom: 1.25rem;
  display: flex;
  align-items: center;
  gap: 8px;
}
.panel-title .dot { width: 6px; height: 6px; border-radius: 50%; background: var(--green); }

/* Overview table */
.tbl-wrap { overflow-x: auto; border-radius: 10px; }
.tbl {
  width: 100%;
  border-collapse: collapse;
  font-size: 11px;
  min-width: 900px;
}
.tbl th {
  padding: 8px 5px;
  color: var(--text3);
  font-weight: 500;
  border-bottom: 1px solid var(--border);
  text-align: center;
  white-space: nowrap;
  font-size: 10.5px;
  letter-spacing: .3px;
}
.tbl th:first-child { text-align: left; padding-left: 4px; }
.tbl td {
  padding: 6px 5px;
  border-bottom: 1px solid var(--border);
  text-align: center;
  vertical-align: middle;
}
.tbl td:first-child { text-align: left; padding-left: 4px; }
.tbl tr:last-child td { border-bottom: none; }
.tbl tr:hover td { background: rgba(255,255,255,0.02); }

.pip {
  display: inline-flex; align-items: center; justify-content: center;
  width: 24px; height: 20px;
  border-radius: 5px;
  font-size: 10px;
  cursor: pointer;
  font-weight: 500;
  transition: transform .1s;
}
.pip:hover { transform: scale(1.15); }
.p-own { background: var(--green-dim); color: var(--green); border: 1px solid rgba(74,222,154,.2); }
.p-in  { background: var(--blue-bg); color: var(--blue); border: 1px solid rgba(96,165,250,.2); }
.p-used{ background: rgba(255,255,255,0.04); color: var(--text3); border: 1px solid var(--border); text-decoration: line-through; }
.p-out { background: var(--red-bg); color: var(--red); border: 1px solid rgba(248,113,113,.2); }

/* Manager grid */
.mgr-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(195px, 1fr));
  gap: 10px;
}
.mgr-card {
  background: var(--bg3);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 14px 16px;
  transition: border-color .2s;
}
.mgr-card:hover { border-color: var(--border2); }
.mgr-head { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; }
.mgr-name { display: flex; align-items: center; gap: 8px; font-size: 13px; font-weight: 500; }
.av {
  width: 28px; height: 28px;
  border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-size: 10px; font-weight: 500;
  flex-shrink: 0;
  font-family: 'DM Mono', monospace;
}
.chip {
  font-size: 10px; padding: 3px 8px; border-radius: 20px; font-weight: 500; white-space: nowrap;
}
.c-ok   { background: var(--green-dim); color: var(--green); border: 1px solid rgba(74,222,154,.2); }
.c-used { background: rgba(255,255,255,0.05); color: var(--text3); border: 1px solid var(--border); }
.c-out  { background: var(--red-bg); color: var(--red); border: 1px solid rgba(248,113,113,.2); }
.c-in   { background: var(--blue-bg); color: var(--blue); border: 1px solid rgba(96,165,250,.2); }

.player-line { font-size: 11.5px; color: var(--text2); margin-bottom: 10px; display: flex; align-items: center; gap: 5px; }
.act-row { display: flex; gap: 6px; flex-wrap: wrap; }

/* Buttons */
.btn {
  padding: 6px 12px; font-size: 11.5px;
  font-family: 'DM Sans', sans-serif;
  border: 1px solid var(--border2);
  border-radius: 8px;
  background: var(--bg4);
  cursor: pointer; color: var(--text);
  display: inline-flex; align-items: center; gap: 5px;
  transition: all .15s;
}
.btn:hover { border-color: rgba(255,255,255,.22); background: rgba(255,255,255,.07); }
.btn-green { background: var(--green); color: #0f1117; border-color: var(--green); font-weight: 500; }
.btn-green:hover { background: #6eeaaa; border-color: #6eeaaa; }
.btn-blue { background: var(--blue); color: #0f1117; border-color: var(--blue); font-weight: 500; }
.btn-blue:hover { background: #93c5fd; border-color: #93c5fd; }

/* History */
.hist-item {
  display: flex; align-items: flex-start; gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid var(--border);
}
.hist-item:last-child { border-bottom: none; }
.hist-ico {
  width: 32px; height: 32px; border-radius: 9px;
  display: flex; align-items: center; justify-content: center;
  font-size: 15px; flex-shrink: 0;
}
.hi-use   { background: var(--green-dim); color: var(--green); }
.hi-trade { background: var(--blue-bg); color: var(--blue); }
.hist-body { flex: 1; min-width: 0; }
.hist-main { font-size: 13px; color: var(--text); }
.hist-time { font-size: 11px; color: var(--text3); margin-top: 2px; }
.undo-btn {
  font-size: 11px; padding: 4px 9px;
  border: 1px solid var(--border);
  border-radius: 7px; background: none;
  cursor: pointer; color: var(--text3);
  font-family: 'DM Sans', sans-serif;
  white-space: nowrap; flex-shrink: 0;
  transition: all .15s;
}
.undo-btn:hover { border-color: var(--border2); color: var(--text); }

/* Legend */
.legend {
  display: flex; gap: 14px; flex-wrap: wrap;
  font-size: 11px; color: var(--text3); margin-bottom: 14px; align-items: center;
}
.ldot {
  width: 12px; height: 12px; border-radius: 3px;
  display: inline-block; margin-right: 5px; vertical-align: middle;
}

/* Modal */
.modal-bg {
  position: fixed; inset: 0;
  background: rgba(0,0,0,.7);
  display: flex; align-items: center; justify-content: center;
  z-index: 200; padding: 1rem;
  backdrop-filter: blur(4px);
}
.modal {
  background: var(--bg2);
  border: 1px solid var(--border2);
  border-radius: 18px;
  padding: 1.5rem;
  width: 100%; max-width: 340px;
}
.modal h3 {
  font-family: 'Playfair Display', serif;
  font-size: 18px; margin-bottom: 1.25rem;
  color: var(--text); display: flex; align-items: center; gap: 8px;
}
.fgrp { margin-bottom: 14px; }
.fgrp label {
  font-size: 11px; color: var(--text3); display: block;
  margin-bottom: 5px; text-transform: uppercase; letter-spacing: .5px;
}
.fgrp input, .fgrp select {
  width: 100%; padding: 10px 12px; font-size: 13px;
  font-family: 'DM Sans', sans-serif;
  border: 1px solid var(--border2);
  border-radius: 9px;
  background: var(--bg3); color: var(--text);
  outline: none;
  transition: border-color .15s;
}
.fgrp input:focus, .fgrp select:focus { border-color: var(--green); }
.fgrp select option { background: var(--bg2); }
.modal-actions { display: flex; gap: 8px; justify-content: flex-end; margin-top: 1.25rem; }

/* Sync panel */
.sync-info {
  background: var(--bg3); border: 1px solid var(--border);
  border-radius: 12px; padding: 14px 16px; margin-bottom: 1rem;
  font-size: 13px; color: var(--text2); line-height: 1.7;
}
.code-box {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 10px 12px;
  font-family: 'DM Mono', monospace;
  font-size: 10px;
  word-break: break-all;
  max-height: 100px;
  overflow-y: auto;
  color: var(--text3);
  margin-bottom: 10px;
}

/* Empty state */
.empty { text-align: center; padding: 3rem 1rem; color: var(--text3); font-size: 13px; }
.empty svg { display: block; margin: 0 auto 12px; opacity: .3; }

/* Avatar colors */
.av-0 { background: rgba(74,222,154,.15); color: var(--green); }
.av-1 { background: rgba(96,165,250,.15); color: var(--blue); }
.av-2 { background: rgba(251,191,36,.15); color: var(--amber); }
.av-3 { background: rgba(248,113,113,.15); color: var(--red); }
.av-4 { background: rgba(167,139,250,.15); color: #a78bfa; }
.av-5 { background: rgba(251,146,60,.15); color: #fb923c; }
.av-6 { background: rgba(34,211,238,.15); color: #22d3ee; }
.av-7 { background: rgba(232,121,249,.15); color: #e879f9; }
.av-8 { background: rgba(74,222,154,.12); color: #6ee7b7; }
.av-9 { background: rgba(96,165,250,.12); color: #93c5fd; }

@media (max-width: 600px) {
  .stats { grid-template-columns: repeat(2,1fr); }
  .header { flex-direction: column; }
  .stat-num { font-size: 22px; }
}
</style>
</head>
<body>
<div class="wrap">
  <div id="root"></div>
</div>

<script>
const MANAGERS = ['Charles','Ayden','Dario','Anthony','Nick','Kevin','Daniel','Nic','James','Alex'];
const WEEKS = Array.from({length:17},(_,i)=>i+1);
const STORAGE_KEY = 'wwp_league_v2';

/* picks structure: S.picks[weekStr][origManager] = {owner, orig, used, player} */
const initPicks = () => {
  const p = {};
  WEEKS.forEach(w => {
    p[String(w)] = {};
    MANAGERS.forEach(m => { p[String(w)][m] = {owner:m, orig:m, used:false, player:null}; });
  });
  return p;
};

let S = { picks:initPicks(), history:[], tab:'overview', week:1, modal:null, sync:'local', lastSync:null };

/* ---- persistence ---- */
const localSave = () => {
  try { localStorage.setItem(STORAGE_KEY, JSON.stringify({picks:S.picks, history:S.history})); } catch(e){}
};
const localLoad = () => {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return;
    const d = JSON.parse(raw);
    if (d && d.picks && d.picks['1'] && d.picks['1']['Charles']) {
      S.picks = d.picks; S.history = d.history || [];
    } else {
      localStorage.removeItem(STORAGE_KEY);
    }
  } catch(e) {}
};

const pushCloud = async () => {
  if (typeof window.storage === 'undefined') { S.sync='nostorage'; render(); return; }
  S.sync='syncing'; render();
  try {
    const r = await window.storage.set(STORAGE_KEY, JSON.stringify({picks:S.picks, history:S.history}), true);
    S.sync = r ? 'synced' : 'error';
    if (r) S.lastSync = new Date().toLocaleTimeString('en-US',{hour:'numeric',minute:'2-digit'});
  } catch(e) { S.sync='error'; }
  render();
};

const pullCloud = async () => {
  if (typeof window.storage === 'undefined') { S.sync='nostorage'; render(); return; }
  S.sync='syncing'; render();
  try {
    const r = await window.storage.get(STORAGE_KEY, true);
    if (r && r.value) {
      const d = JSON.parse(r.value);
      if (d && d.picks && d.picks['1']) { S.picks=d.picks; S.history=d.history||[]; localSave(); }
      S.sync='synced'; S.lastSync=new Date().toLocaleTimeString('en-US',{hour:'numeric',minute:'2-digit'});
    } else { S.sync='local'; }
  } catch(e) { S.sync='local'; }
  render();
};

/* ---- data helpers ---- */
const ts = () => new Date().toLocaleString('en-US',{month:'short',day:'numeric',hour:'numeric',minute:'2-digit'});



const weekKey = (w) => String(w);

const saveAll = async () => {
  localSave();
  try {
    await pushCloud();
  } catch (e) {
    console.error('saveAll failed', e);
  }
};

const usePick = async (mgr, w, player) => {
  const ok = doUsePick(mgr, w, player);
  if (!ok) {
    alert('Unable to use this pick.');
    return;
  }

  await saveAll();
  render();
};

const tradePick = async (from, w, to) => {
  const ok = doTrade(from, to, w);
  if (!ok) {
    alert('Unable to complete trade.');
    return;
  }

  await saveAll();
  render();
};

const undoAction = async (i) => {
  doUndo(i);
  await saveAll();
  render();
};

/* Find the pick object currently owned by `owner` in week `w` */
const findPick = (owner, w) => {
  const slot = S.picks[String(w)];
  if (!slot) return null;
  for (const key of Object.keys(slot)) {
    const p = slot[key];
    if (p.owner === owner && !p.used) return p;
  }
  return null;
};

/* ---- mutations — NO render() calls inside, caller renders ---- */
const doUsePick = (mgr, w, player) => {
  const p = findPick(mgr, w);
  if (!p) { console.warn('usePick: no pick found for', mgr, w); return false; }
  p.used = true; p.player = player;
  S.history.unshift({type:'use', manager:mgr, week:String(w), player, origM:p.orig, time:ts()});
  return true;
};

const doTrade = (from, to, w) => {
  const p = findPick(from, w);
  if (!p) { console.warn('doTrade: no pick found for', from, w, '| slot:', JSON.stringify(S.picks[String(w)])); return false; }
  p.owner = to;
  S.history.unshift({type:'trade', from, to, week:String(w), origM:p.orig, time:ts()});
  return true;
};

const doUndo = (i) => {
  const h = S.history[i];
  if (!h) return;
  const p = S.picks[String(h.week)] && S.picks[String(h.week)][h.origM];
  if (!p) return;
  if (h.type==='use') { p.used=false; p.player=null; }
  else { p.owner = h.from; }
  S.history.splice(i,1);
};

// --- Render helpers ---
const initials = m => m.slice(0,2).toUpperCase();
const avClass = m => 'av-' + (MANAGERS.indexOf(m) % 10);

const icon = (name) => {
  const icons = {
    trophy: '<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 9H4.5a2.5 2.5 0 0 1 0-5H6"/><path d="M18 9h1.5a2.5 2.5 0 0 0 0-5H18"/><path d="M4 22h16"/><path d="M10 14.66V17c0 .55-.47.98-.97 1.21C7.85 18.75 7 20.24 7 22"/><path d="M14 14.66V17c0 .55.47.98.97 1.21C16.15 18.75 17 20.24 17 22"/><path d="M18 2H6v7a6 6 0 0 0 12 0V2z"/></svg>',
    grid: '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>',
    clock: '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>',
    cloud: '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"/></svg>',
    cal: '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>',
    check: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg>',
    trade: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="17 1 21 5 17 9"/><path d="M3 11V9a4 4 0 0 1 4-4h14"/><polyline points="7 23 3 19 7 15"/><path d="M21 13v2a4 4 0 0 1-4 4H3"/></svg>',
    undo: '<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 14 4 9 9 4"/><path d="M20 20v-7a4 4 0 0 0-4-4H4"/></svg>',
    upload: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="16 16 12 12 8 16"/><line x1="12" y1="12" x2="12" y2="21"/><path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"/></svg>',
    download: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="8 17 12 21 16 17"/><line x1="12" y1="12" x2="12" y2="21"/><path d="M20.88 18.09A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.72"/></svg>',
    copy: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2" ry="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>',
    refresh: '<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 4 23 10 17 10"/><path d="M20.49 15a9 9 0 1 1-2.12-9.36L23 10"/></svg>',
    user: '<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>',
  };
  return icons[name] || '';
};

// --- Render functions ---
const renderStats = () => {
  let used=0, traded=0, avail=0;
  WEEKS.forEach(w => Object.values(S.picks[weekKey(w)]).forEach(p => {
    if (p.used) used++; else if (p.owner !== p.orig) traded++; else avail++;
  }));
  return `<div class="stats">
    <div class="stat"><div class="stat-label">Available</div><div class="stat-num g">${avail}</div></div>
    <div class="stat"><div class="stat-label">Used</div><div class="stat-num">${used}</div></div>
    <div class="stat"><div class="stat-label">Traded</div><div class="stat-num b">${traded}</div></div>
    <div class="stat"><div class="stat-label">Total picks</div><div class="stat-num a">${MANAGERS.length * WEEKS.length}</div></div>
  </div>`;
};

const renderNav = () => {
  const tabs = [
    {id:'overview', label:'Overview'},
    {id:'history', label:'History'},
    {id:'sync', label:'Sync'},
    ...WEEKS.map(w => ({id:`w${w}`, label:`Wk ${w}`, wk:w}))
  ];
  return `<div class="nav-wrapper">${tabs.map(t => {
    const active = t.wk ? S.tab==='week' && S.week===t.wk : S.tab===t.id;
    const fn = t.wk ? `ST('week',${t.wk})` : `ST('${t.id}')`;
    return `<button class="nav-btn${active?' on':''}" onclick="${fn}">${t.label}</button>`;
  }).join('')}</div>`;
};

const renderOverview = () => {
  let rows = '';
  MANAGERS.forEach(m => {
    let cells = '';
    WEEKS.forEach(w => {
      const allPicks = Object.values(S.picks[weekKey(w)]);
      const owned = allPicks.find(p => p.orig === m);
      const ownerOf = owned ? owned.owner : null;
      let cls='p-own', lbl='●', tip='Available';
      if (!owned) { cls='p-out'; lbl='?'; tip='Unknown'; }
      else if (owned.used) { cls='p-used'; lbl='✓'; tip='Used: '+owned.player; }
      else if (ownerOf === m && owned.orig !== m) { cls='p-in'; lbl='↓'; tip='Received trade'; }
      else if (ownerOf !== m) { cls='p-out'; lbl='↑'; tip='Traded to '+ownerOf; }
      cells += `<td><span class="pip ${cls}" title="${tip}" onclick="ST('week',${w})">${lbl}</span></td>`;
    });
    rows += `<tr>
      <td><span style="display:inline-flex;align-items:center;gap:7px">
        <span class="av ${avClass(m)}">${initials(m)}</span>
        <span style="font-size:12.5px">${m}</span>
      </span></td>${cells}
    </tr>`;
  });
  return `<div class="panel">
    <div class="panel-title"><span class="dot"></span>All picks at a glance</div>
    <div class="legend">
      <span><span class="ldot" style="background:rgba(74,222,154,.15);border:1px solid rgba(74,222,154,.3)"></span>Own</span>
      <span><span class="ldot" style="background:rgba(96,165,250,.15);border:1px solid rgba(96,165,250,.3)"></span>Received</span>
      <span><span class="ldot" style="background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.1)"></span>Used</span>
      <span><span class="ldot" style="background:rgba(248,113,113,.15);border:1px solid rgba(248,113,113,.3)"></span>Traded away</span>
      <span style="margin-left:auto;font-size:11px">Click any cell → jump to that week</span>
    </div>
    <div class="tbl-wrap">
      <table class="tbl">
        <thead><tr><th>Manager</th>${WEEKS.map(w=>`<th>Wk ${w}</th>`).join('')}</tr></thead>
        <tbody>${rows}</tbody>
      </table>
    </div>
  </div>`;
};

const renderWeek = () => {
  const wk = S.week;
  let cards = '';
  MANAGERS.forEach(m => {
    const owned = Object.values(S.picks[weekKey(wk)]).find(p => p.orig === m);
    const received = Object.values(S.picks[weekKey(wk)]).filter(p => p.owner === m && p.orig !== m && !p.used);
    const isOwner = owned && owned.owner === m;
    const p = owned || {used:false, player:null, owner:m, orig:m};
    let chipCls='c-ok', chipLbl='Available';
    if (p.used) { chipCls='c-used'; chipLbl='Used'; }
    else if (!isOwner) { chipCls='c-out'; chipLbl='Traded away'; }
    else if (p.orig !== m) { chipCls='c-in'; chipLbl='Received'; }
    const canUse = isOwner && !p.used;
    const canTrade = isOwner && !p.used;
    const receivedExtra = received.map(rp =>
      `<div class="player-line" style="color:var(--blue);font-size:11px">${icon('trade')} Received from ${rp.orig}</div>`
    ).join('');
    cards += `<div class="mgr-card">
      <div class="mgr-head">
        <div class="mgr-name"><span class="av ${avClass(m)}">${initials(m)}</span>${m}</div>
        <span class="chip ${chipCls}">${chipLbl}</span>
      </div>
      ${p.used && p.player ? `<div class="player-line">${icon('user')} ${p.player}</div>` : ''}
      ${!isOwner && !p.used ? `<div class="player-line" style="font-size:11px;color:var(--text3)">Owned by <strong style="color:var(--text2)">${p.owner}</strong></div>` : ''}
      ${receivedExtra}
      <div class="act-row">
        ${canUse ? `<button class="btn btn-green" onclick="OM('use','${m}',${wk})">${icon('check')} Use pick</button>` : ''}
        ${canTrade ? `<button class="btn btn-blue" onclick="OM('trade','${m}',${wk})">${icon('trade')} Trade</button>` : ''}
      </div>
    </div>`;
  });
  return `<div class="panel">
    <div class="panel-title"><span class="dot"></span>Week ${wk} — picks</div>
    <div class="mgr-grid">${cards}</div>
  </div>`;
};

const renderHistory = () => {
  if (!S.history.length) return `<div class="panel">
    <div class="empty">${icon('clock')}<br>No transactions recorded yet</div>
  </div>`;
  return `<div class="panel">
    <div class="panel-title"><span class="dot"></span>Transaction history</div>
    ${S.history.map((h,i) => {
      const body = h.type === 'use'
        ? `<strong>${h.manager}</strong> picked up <strong>${h.player}</strong> &mdash; Week ${h.week}`
        : `<strong>${h.from}</strong> traded Wk ${h.week} pick to <strong>${h.to}</strong>`;
      const icoCls = h.type==='use' ? 'hi-use' : 'hi-trade';
      const ico = h.type==='use' ? icon('check') : icon('trade');
      return `<div class="hist-item">
        <div class="hist-ico ${icoCls}">${ico}</div>
        <div class="hist-body">
          <div class="hist-main">${body}</div>
          <div class="hist-time">${h.time}</div>
        </div>
        <button class="undo-btn" onclick="UA(${i})">${icon('undo')} Undo</button>
      </div>`;
    }).join('')}
  </div>`;
};

const renderSync = () => {
  const dotCls = S.sync==='synced'?'':'stale';
  const statusTxt = {synced:'Synced'+(S.lastSync?' at '+S.lastSync:''),syncing:'Syncing…',local:'Local only — not yet synced',error:'Sync error',nostorage:'Cloud storage unavailable in this context'}[S.sync]||S.sync;
  return `<div class="panel">
    <div class="panel-title"><span class="dot"></span>Cloud sync</div>
    <div class="sync-info">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px">
        <span class="sdot ${dotCls}"></span>
        <span style="font-weight:500;font-size:13px">${statusTxt}</span>
      </div>
      All league managers share one cloud state. Push your changes so everyone sees them, or pull to get the latest.
    </div>
    <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:1.5rem">
      <button class="btn btn-green" onclick="pushCloud()">${icon('upload')} Push to cloud</button>
      <button class="btn btn-blue" onclick="pullCloud()">${icon('download')} Pull from cloud</button>
    </div>
    <div class="panel-title" style="margin-bottom:10px"><span class="dot"></span>Manual export / import</div>
    <div class="sync-info" style="font-size:12px;margin-bottom:10px">Use this to copy a snapshot and share it with someone, or to restore a backup.</div>
    <button class="btn" style="margin-bottom:8px" onclick="doExport()">${icon('copy')} Copy export code</button>
    <div class="code-box" id="exp-box">Click above to generate…</div>
    <div class="fgrp" style="margin-top:12px">
      <label>Paste import code</label>
      <input type="text" id="imp-in" placeholder="Paste JSON here…" />
    </div>
    <button class="btn btn-green" style="margin-top:8px" onclick="doImport()">${icon('upload')} Import</button>
  </div>`;
};

const renderModal = () => {
  const m = S.modal;
  if (!m) return '';
  let inner = '';
  if (m.type === 'use') {
    inner = `<h3>${icon('check')} Use pick — ${m.mgr}, Wk ${m.wk}</h3>
      <div class="fgrp"><label>Player picked up</label><input type="text" id="pi" placeholder="e.g. Justin Jefferson" /></div>
      <div class="modal-actions">
        <button class="btn" onclick="CM()">Cancel</button>
        <button class="btn btn-green" onclick="SU()">Confirm</button>
      </div>`;
  } else if (m.type === 'trade') {
    const opts = MANAGERS.filter(x=>x!==m.mgr).map(o=>`<option value="${o}">${o}</option>`).join('');
    inner = `<h3>${icon('trade')} Trade — ${m.mgr}, Wk ${m.wk}</h3>
      <div class="fgrp"><label>Trade to</label><select id="tt">${opts}</select></div>
      <div class="modal-actions">
        <button class="btn" onclick="CM()">Cancel</button>
        <button class="btn btn-blue" onclick="STrade()">Confirm trade</button>
      </div>`;
  }
  return `<div class="modal-bg" onclick="if(event.target===this)CM()"><div class="modal">${inner}</div></div>`;
};

const render = () => {
  const syncDotCls = S.sync==='synced'?'':'stale';
  const syncLbl = S.sync==='syncing'?'Syncing…':S.sync==='synced'?'Synced'+(S.lastSync?' '+S.lastSync:''):'Local only';
  let content = '';
  if (S.tab==='overview') content = renderOverview();
  else if (S.tab==='week') content = renderWeek();
  else if (S.tab==='history') content = renderHistory();
  else if (S.tab==='sync') content = renderSync();

  document.getElementById('root').innerHTML = `
    <div class="header">
      <div class="header-left">
        <div class="logo-mark">${icon('trophy')}</div>
        <div>
          <div class="app-name">WWP Tracker</div>
          <div class="app-sub">Waiver Wire Picks &nbsp;·&nbsp; 10 managers &nbsp;·&nbsp; 17 weeks</div>
        </div>
      </div>
      <button class="sync-pill" onclick="pullCloud()">
        <span class="sdot ${syncDotCls}"></span>
        ${syncLbl}
        ${icon('refresh')}
      </button>
    </div>
    ${renderStats()}
    ${renderNav()}
    ${content}
    ${renderModal()}
  `;

  if (S.modal?.type === 'use') {
    const inp = document.getElementById('pi');
    if (inp) { inp.focus(); inp.onkeydown = e => { if (e.key==='Enter') SU(); }; }
  }
};

// Global handlers
window.ST = (tab, wk) => { S.tab=tab; if(wk) S.week=wk; S.modal=null; render(); };
window.OM = (type, mgr, wk) => { S.modal={type,mgr,wk}; render(); };
window.CM = () => { S.modal=null; render(); };
window.UA = (i) => undoAction(i);
window.SU = () => {
  const v = document.getElementById('pi')?.value?.trim();
  if (!v) return;
  usePick(S.modal.mgr, S.modal.wk, v);
  S.modal = null;
};
window.STrade = () => {
  const v = document.getElementById('tt')?.value;
  if (!v) return;
  tradePick(S.modal.mgr, S.modal.wk, v);
  S.modal = null;
};
window.doExport = () => {
  const s = JSON.stringify({picks:S.picks, history:S.history});
  const el = document.getElementById('exp-box');
  if (el) el.textContent = s;
  try { navigator.clipboard.writeText(s); } catch(e) {}
};
window.doImport = () => {
  const s = document.getElementById('imp-in')?.value?.trim();
  if (!s) return;
  try {
    const d = JSON.parse(s);
    S.picks = d.picks || initPicks();
    S.history = d.history || [];
    saveAll();
    alert('Import successful!');
    render();
  } catch(e) { alert('Invalid data — make sure you pasted the full export code.'); }
};

// Boot
localLoad();
render();
pullCloud();
</script>
</body>
</html>
