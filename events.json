/* ============================================================
   GLOW BY CHLO — Console styles (loads after site.css)
   ============================================================ */

.admin-body{min-height:100vh;display:flex;flex-direction:column}

/* ---------- login ---------- */
.login-wrap{
  min-height:100vh;display:flex;align-items:center;justify-content:center;padding:1.5rem;
}
.login-card{width:min(420px,100%);padding:2.2rem}
.login-card .logo{display:block;margin-bottom:.4rem}
.login-card .eyebrow{margin-bottom:1.6rem}
.login-card form{display:grid;gap:1rem}
.error{color:#ff8fa8}

/* ---------- demo banner ---------- */
.demo-banner{
  background:var(--holo);color:var(--ink);
  font-family:var(--font-pixel);font-size:.72rem;letter-spacing:.1em;
  text-align:center;padding:.6rem 1rem;
}

/* ---------- header ---------- */
.admin-head{
  position:sticky;top:0;z-index:50;
  background:rgba(11,10,18,.85);backdrop-filter:blur(14px);
  border-bottom:1px solid var(--line);
}
.admin-head .wrap{display:flex;align-items:center;gap:1.2rem;padding:.75rem 0;flex-wrap:wrap}
.admin-head .logo{font-size:.95rem;margin-right:auto}
.admin-head .logo small{
  display:block;font-family:var(--font-pixel);font-size:.58rem;letter-spacing:.2em;
  color:var(--aqua);font-weight:400;
}
.admin-tabs{display:flex;gap:.35rem;flex-wrap:wrap}
.admin-tabs button{
  background:none;border:1px solid transparent;border-radius:999px;
  color:var(--muted);font-family:var(--font-body);font-weight:600;font-size:.85rem;
  padding:.5rem 1rem;cursor:pointer;transition:color .2s,border-color .2s,background .2s;
}
.admin-tabs button:hover{color:var(--white)}
.admin-tabs button.is-active{
  color:var(--ink);
  background:var(--holo);
  border-color:transparent;
}
.admin-actions{display:flex;gap:.5rem;align-items:center}
.admin-actions .btn{padding:.5rem 1rem;font-size:.82rem}

/* ---------- main ---------- */
.admin-main{padding:2.2rem 0 4rem;width:min(980px,92%);margin-inline:auto;flex:1}
.tab-title{margin-bottom:.3rem}
.tab-sub{color:var(--muted);font-size:.92rem;margin-bottom:1.8rem;max-width:56ch}

/* ---------- dashboard stats ---------- */
.stat-grid{display:grid;gap:1rem;grid-template-columns:repeat(3,1fr)}
@media (max-width:720px){.stat-grid{grid-template-columns:1fr}}
.stat{padding:1.3rem 1.4rem}
.stat .k{font-family:var(--font-pixel);font-size:.64rem;letter-spacing:.16em;color:var(--aqua);text-transform:uppercase;display:block;margin-bottom:.5rem}
.stat .v{font-family:var(--font-display);font-weight:800;font-size:1.5rem;line-height:1.1}
.stat .d{color:var(--muted);font-size:.82rem;margin:.4rem 0 0}

/* ---------- pricing grid ---------- */
.price-grid{display:grid;gap:1rem;grid-template-columns:1fr 1fr}
@media (max-width:720px){.price-grid{grid-template-columns:1fr}}
.price-field{background:var(--ink-2);border:1px solid var(--line);border-radius:16px;padding:1rem 1.1rem}
.price-field label{display:block;margin-bottom:.1rem}
.price-field .hint{font-size:.74rem;color:var(--muted);margin:.35rem 0 0}
.price-field input{margin-top:.45rem}

/* ---------- events ---------- */
.event-row{
  background:var(--ink-2);border:1px solid var(--line);border-radius:16px;
  padding:1.1rem;margin-bottom:1rem;display:grid;gap:.8rem;
}
.event-row .row-grid{display:grid;gap:.8rem;grid-template-columns:110px 1fr 1fr}
@media (max-width:720px){.event-row .row-grid{grid-template-columns:1fr}}
.event-row .row-grid-2{display:grid;gap:.8rem;grid-template-columns:1fr 120px 120px}
@media (max-width:720px){.event-row .row-grid-2{grid-template-columns:1fr}}
.event-row input,.event-row textarea{margin-top:.3rem}
.event-row textarea{min-height:64px}
.event-foot{display:flex;justify-content:space-between;align-items:center;gap:1rem;flex-wrap:wrap}
.check{display:flex;align-items:center;gap:.55rem;font-family:var(--font-body);font-size:.88rem;color:var(--white);text-transform:none;letter-spacing:0}
.check input{width:auto;margin:0;accent-color:#ff9dd6}
.btn-danger{background:none;box-shadow:inset 0 0 0 1px rgba(255,120,150,.5);color:#ff8fa8}
.btn-danger:hover{box-shadow:inset 0 0 0 1px #ff8fa8}
.btn-sm{padding:.5rem 1rem;font-size:.82rem}

/* ---------- panels + forms ---------- */
.panel{background:var(--ink-2);border:1px solid var(--line);border-radius:var(--radius);padding:1.6rem;margin-bottom:1.4rem}
.panel h3{margin-bottom:1rem}
.save-bar{display:flex;gap:.8rem;align-items:center;margin-top:1.4rem;flex-wrap:wrap}

/* ---------- settings ---------- */
.kv{display:flex;justify-content:space-between;gap:1rem;padding:.8rem .2rem;border-bottom:1px dashed var(--line);font-size:.92rem}
.kv:last-child{border-bottom:0}
.kv .k{color:var(--muted)}
.badge{font-family:var(--font-pixel);font-size:.62rem;letter-spacing:.12em;padding:.28rem .6rem;border-radius:999px;text-transform:uppercase}
.badge.on{background:var(--acid);color:var(--ink)}
.badge.off{background:var(--ink-3);color:var(--muted);border:1px solid var(--line)}

/* ---------- toast ---------- */
.toast{
  position:fixed;bottom:1.4rem;left:50%;transform:translateX(-50%);z-index:90;
  background:var(--holo);color:var(--ink);
  font-family:var(--font-body);font-weight:600;font-size:.9rem;
  padding:.75rem 1.4rem;border-radius:999px;
  box-shadow:0 12px 34px rgba(0,0,0,.5);
  animation:toast-in .25s ease;
}
@keyframes toast-in{from{opacity:0;transform:translateX(-50%) translateY(10px)}to{opacity:1;transform:translateX(-50%) translateY(0)}}
