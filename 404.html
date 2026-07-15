/* ============================================================
   GLOW BY CHLO — admin.js (Studio Console)
   Two modes, same interface:
   • DEMO  — no Supabase keys in config.js → localStorage,
             perfect for pitching the console with zero backend.
   • LIVE  — Supabase configured → email/password auth + RLS.
   ============================================================ */
(function () {
  "use strict";

  var CFG = window.GBC_CONFIG || {};
  var LIVE = !!(CFG.SUPABASE_URL && CFG.SUPABASE_ANON_KEY);
  var TOKEN_KEY = "gbc_console_token";

  /* ---------- editable price keys (must match data-cms attrs) ---------- */
  var PRICE_FIELDS = [
    { key: "price-single",     label: "Single Swarovski crystal",  def: "$55",      hint: "Shown on Home, Collections, FAQ" },
    { key: "price-additional", label: "Additional crystals",       def: "+$20 ea",  hint: "Shown on Home, Collections, FAQ" },
    { key: "price-shaped",     label: "Shaped gems",               def: "from $70", hint: "Butterflies, stars, hearts" },
    { key: "price-custom",     label: "Custom design session",     def: "from $150",hint: "Shown on Home + Collections" },
    { key: "price-removal",    label: "Gentle removal",            def: "$20",      hint: "Shown on Home, Collections, FAQ" },
    { key: "price-travel",     label: "Mobile travel fee",         def: "+$25",     hint: "Shown on Collections + Policies" },
    { key: "price-lagoon",     label: "Electric Lagoon collection",def: "$185",     hint: "Set price" },
    { key: "price-candy",      label: "Cosmic Candy collection",   def: "$225",     hint: "Set price" },
    { key: "price-bikini",     label: "Bikini Bottom collection",  def: "$265",     hint: "Set price" },
    { key: "price-party",      label: "Party rate (per guest)",    def: "$45",      hint: "Shown on Parties page" }
  ];

  var DEFAULT_EVENTS = [
    { id: "demo-1", date_label: "AUG 2",  title: "Pop-Up: Midtown Sacramento", location: "Midtown Farmers Market", description: "Walk-ups welcome, singles + minis only. First come, first sparkled.", published: true, sort: 1 },
    { id: "demo-2", date_label: "AUG 16", title: "Pop-Up: Downtown Roseville", location: "Vernon Street", description: "Full collections available — book a slot to skip the line.", published: true, sort: 2 }
  ];
  var DEFAULT_ANNOUNCE = {
    message: "✦ Summer pop-up season is live — mobile appointments now booking across Sacramento",
    link_url: "book.html",
    link_label: "Book now →",
    active: true
  };

  /* ---------- tiny helpers ---------- */
  function $(s, r) { return (r || document).querySelector(s); }
  function $all(s, r) { return Array.prototype.slice.call((r || document).querySelectorAll(s)); }
  function esc(v) {
    return String(v == null ? "" : v).replace(/[&<>"']/g, function (c) {
      return { "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;" }[c];
    });
  }
  var toastTimer = null;
  function toast(msg) {
    var t = $("#toast");
    t.textContent = msg;
    t.hidden = false;
    clearTimeout(toastTimer);
    toastTimer = setTimeout(function () { t.hidden = true; }, 2600);
  }

  /* ============================================================
     STORAGE ADAPTERS — same promise API for both modes
     ============================================================ */

  /* ---------- DEMO (localStorage) ---------- */
  var demoStore = {
    _get: function (k, fallback) {
      try {
        var raw = localStorage.getItem(k);
        return raw ? JSON.parse(raw) : JSON.parse(JSON.stringify(fallback));
      } catch (e) { return JSON.parse(JSON.stringify(fallback)); }
    },
    _set: function (k, v) { localStorage.setItem(k, JSON.stringify(v)); },

    getContent: function () {
      var map = {};
      PRICE_FIELDS.forEach(function (f) { map[f.key] = f.def; });
      return Promise.resolve(this._get("gbc_demo_content", map));
    },
    saveContent: function (map) {
      this._set("gbc_demo_content", map);
      return Promise.resolve();
    },
    getEvents: function () {
      var list = this._get("gbc_demo_events", DEFAULT_EVENTS);
      list.sort(function (a, b) { return (a.sort || 0) - (b.sort || 0); });
      return Promise.resolve(list);
    },
    addEvent: function (e) {
      var list = this._get("gbc_demo_events", DEFAULT_EVENTS);
      e.id = "demo-" + Date.now();
      list.push(e);
      this._set("gbc_demo_events", list);
      return Promise.resolve();
    },
    updateEvent: function (id, patch) {
      var list = this._get("gbc_demo_events", DEFAULT_EVENTS);
      list.forEach(function (e) { if (e.id === id) Object.assign(e, patch); });
      this._set("gbc_demo_events", list);
      return Promise.resolve();
    },
    deleteEvent: function (id) {
      var list = this._get("gbc_demo_events", DEFAULT_EVENTS).filter(function (e) { return e.id !== id; });
      this._set("gbc_demo_events", list);
      return Promise.resolve();
    },
    getAnnouncement: function () {
      return Promise.resolve(this._get("gbc_demo_announce", DEFAULT_ANNOUNCE));
    },
    saveAnnouncement: function (a) {
      this._set("gbc_demo_announce", a);
      return Promise.resolve();
    },
    reset: function () {
      ["gbc_demo_content", "gbc_demo_events", "gbc_demo_announce"].forEach(function (k) {
        localStorage.removeItem(k);
      });
      return Promise.resolve();
    }
  };

  /* ---------- LIVE (Supabase REST, RLS-enforced) ---------- */
  var liveStore = {
    token: sessionStorage.getItem(TOKEN_KEY) || "",

    _headers: function (extra) {
      var h = {
        apikey: CFG.SUPABASE_ANON_KEY,
        Authorization: "Bearer " + (this.token || CFG.SUPABASE_ANON_KEY),
        "Content-Type": "application/json"
      };
      if (extra) Object.keys(extra).forEach(function (k) { h[k] = extra[k]; });
      return h;
    },
    _req: function (path, opts) {
      opts = opts || {};
      opts.headers = this._headers(opts.headers);
      return fetch(CFG.SUPABASE_URL + path, opts).then(function (r) {
        if (r.status === 401 || r.status === 403) {
          liveStore.signOut();
          showLogin("Session expired — sign in again.");
          throw new Error("auth " + r.status);
        }
        if (!r.ok) {
          return r.text().then(function (t) { throw new Error("supabase " + r.status + " " + t); });
        }
        return r.status === 204 ? null : r.json();
      });
    },

    signIn: function (email, password) {
      return fetch(CFG.SUPABASE_URL + "/auth/v1/token?grant_type=password", {
        method: "POST",
        headers: { apikey: CFG.SUPABASE_ANON_KEY, "Content-Type": "application/json" },
        body: JSON.stringify({ email: email, password: password })
      }).then(function (r) { return r.json().then(function (j) { return { ok: r.ok, j: j }; }); })
        .then(function (res) {
          if (!res.ok || !res.j.access_token) {
            throw new Error(res.j.error_description || res.j.msg || "Sign-in failed");
          }
          liveStore.token = res.j.access_token;
          sessionStorage.setItem(TOKEN_KEY, liveStore.token);
        });
    },
    signOut: function () {
      this.token = "";
      sessionStorage.removeItem(TOKEN_KEY);
    },

    getContent: function () {
      return this._req("/rest/v1/site_content?select=key,value").then(function (rows) {
        var map = {};
        PRICE_FIELDS.forEach(function (f) { map[f.key] = f.def; });
        (rows || []).forEach(function (r) { if (r.value) map[r.key] = r.value; });
        return map;
      });
    },
    saveContent: function (map) {
      var rows = Object.keys(map).map(function (k) { return { key: k, value: map[k] }; });
      return this._req("/rest/v1/site_content", {
        method: "POST",
        headers: { Prefer: "resolution=merge-duplicates,return=minimal" },
        body: JSON.stringify(rows)
      });
    },
    getEvents: function () {
      return this._req("/rest/v1/events?select=*&order=sort.asc");
    },
    addEvent: function (e) {
      return this._req("/rest/v1/events", {
        method: "POST",
        headers: { Prefer: "return=minimal" },
        body: JSON.stringify(e)
      });
    },
    updateEvent: function (id, patch) {
      return this._req("/rest/v1/events?id=eq." + encodeURIComponent(id), {
        method: "PATCH",
        headers: { Prefer: "return=minimal" },
        body: JSON.stringify(patch)
      });
    },
    deleteEvent: function (id) {
      return this._req("/rest/v1/events?id=eq." + encodeURIComponent(id), { method: "DELETE" });
    },
    getAnnouncement: function () {
      return this._req("/rest/v1/announcements?select=*&limit=1").then(function (rows) {
        return (rows && rows[0]) || Object.assign({ id: null }, DEFAULT_ANNOUNCE, { active: false, message: "" });
      });
    },
    saveAnnouncement: function (a) {
      if (a.id) {
        var id = a.id; delete a.id;
        return this._req("/rest/v1/announcements?id=eq." + encodeURIComponent(id), {
          method: "PATCH",
          headers: { Prefer: "return=minimal" },
          body: JSON.stringify(a)
        });
      }
      delete a.id;
      return this._req("/rest/v1/announcements", {
        method: "POST",
        headers: { Prefer: "return=minimal" },
        body: JSON.stringify(a)
      });
    }
  };

  var store = LIVE ? liveStore : demoStore;

  /* ============================================================
     VIEWS
     ============================================================ */
  function showLogin(msg) {
    $("#view-app").hidden = true;
    $("#view-login").hidden = false;
    var err = $("#login-error");
    if (msg) { err.textContent = msg; err.hidden = false; }
  }
  function showApp() {
    $("#view-login").hidden = true;
    $("#view-app").hidden = false;
    $("#demo-banner").hidden = LIVE;
    $("#signout-btn").hidden = !LIVE;
    $("#demo-tools").hidden = LIVE;
    renderDashboard();
    renderPricing();
    renderEvents();
    renderAnnouncement();
    renderSettings();
  }

  /* ---------- tabs ---------- */
  $("#admin-tabs").addEventListener("click", function (e) {
    var btn = e.target.closest("button[data-tab]");
    if (!btn) return;
    $all("#admin-tabs button").forEach(function (b) { b.classList.toggle("is-active", b === btn); });
    $all(".tab").forEach(function (t) { t.hidden = t.id !== "tab-" + btn.getAttribute("data-tab"); });
  });

  /* ---------- dashboard ---------- */
  function renderDashboard() {
    Promise.all([store.getEvents(), store.getAnnouncement()]).then(function (res) {
      var events = res[0] || [], ann = res[1] || {};
      var published = events.filter(function (e) { return e.published !== false; }).length;
      $("#dash-stats").innerHTML =
        '<div class="card stat"><span class="k">Mode</span><span class="v">' + (LIVE ? "Live" : "Demo") + '</span><p class="d">' + (LIVE ? "Connected to Supabase" : "Sample data — this browser only") + '</p></div>' +
        '<div class="card stat"><span class="k">Pop-ups live</span><span class="v">' + published + '</span><p class="d">' + events.length + ' total (' + (events.length - published) + ' hidden)</p></div>' +
        '<div class="card stat"><span class="k">Announcement</span><span class="v">' + (ann.active ? "On" : "Off") + '</span><p class="d">' + (ann.active ? esc((ann.message || "").slice(0, 42)) + "…" : "Bar is hidden on the site") + "</p></div>";
    });
  }

  /* ---------- pricing ---------- */
  function renderPricing() {
    store.getContent().then(function (map) {
      $("#pricing-fields").innerHTML = PRICE_FIELDS.map(function (f) {
        return (
          '<div class="price-field">' +
          '<label for="pf-' + f.key + '">' + esc(f.label) + "</label>" +
          '<input id="pf-' + f.key + '" data-key="' + f.key + '" value="' + esc(map[f.key] || f.def) + '">' +
          '<p class="hint">' + esc(f.hint) + "</p>" +
          "</div>"
        );
      }).join("");
    });
  }
  $("#save-pricing").addEventListener("click", function () {
    var map = {};
    $all("#pricing-fields input").forEach(function (i) { map[i.getAttribute("data-key")] = i.value.trim(); });
    store.saveContent(map).then(function () { toast("Pricing saved ✦"); renderDashboard(); })
      .catch(function () { toast("Couldn't save — check connection"); });
  });

  /* ---------- events ---------- */
  function renderEvents() {
    store.getEvents().then(function (list) {
      var mount = $("#events-list");
      if (!list || !list.length) {
        mount.innerHTML = '<div class="panel"><p class="form-note" style="margin:0">No pop-ups yet — add your first one below.</p></div>';
        return;
      }
      mount.innerHTML = list.map(function (e) {
        return (
          '<div class="event-row" data-id="' + esc(e.id) + '">' +
          '<div class="row-grid">' +
          '<div><label>Date label</label><input data-f="date_label" value="' + esc(e.date_label) + '"></div>' +
          '<div><label>Title</label><input data-f="title" value="' + esc(e.title) + '"></div>' +
          '<div><label>Location</label><input data-f="location" value="' + esc(e.location) + '"></div>' +
          "</div>" +
          '<div><label>Description</label><input data-f="description" value="' + esc(e.description) + '"></div>' +
          '<div class="event-foot">' +
          '<label class="check"><input type="checkbox" data-f="published"' + (e.published !== false ? " checked" : "") + "> Published</label>" +
          '<div style="display:flex;gap:.6rem;align-items:center">' +
          '<label class="check">Sort <input type="number" data-f="sort" value="' + (e.sort || 0) + '" style="width:74px"></label>' +
          '<button class="btn btn-primary btn-sm" data-act="save">Save</button>' +
          '<button class="btn btn-danger btn-sm" data-act="delete">Delete</button>' +
          "</div></div></div>"
        );
      }).join("");
    });
  }
  $("#events-list").addEventListener("click", function (e) {
    var btn = e.target.closest("button[data-act]");
    if (!btn) return;
    var row = btn.closest(".event-row");
    var id = row.getAttribute("data-id");
    if (btn.getAttribute("data-act") === "delete") {
      if (!confirm("Delete this pop-up? This can't be undone.")) return;
      store.deleteEvent(id).then(function () { toast("Pop-up deleted"); renderEvents(); renderDashboard(); })
        .catch(function () { toast("Couldn't delete — check connection"); });
      return;
    }
    var patch = {};
    $all("input[data-f]", row).forEach(function (i) {
      var f = i.getAttribute("data-f");
      if (f === "published") patch[f] = i.checked;
      else if (f === "sort") patch[f] = parseInt(i.value, 10) || 0;
      else patch[f] = i.value.trim();
    });
    store.updateEvent(id, patch).then(function () { toast("Pop-up saved ✦"); renderEvents(); renderDashboard(); })
      .catch(function () { toast("Couldn't save — check connection"); });
  });
  $("#event-add").addEventListener("submit", function (e) {
    e.preventDefault();
    var ev = {
      date_label: $("#new-date").value.trim(),
      title: $("#new-title").value.trim(),
      location: $("#new-location").value.trim(),
      description: $("#new-desc").value.trim(),
      published: true,
      sort: 99
    };
    store.addEvent(ev).then(function () {
      e.target.reset();
      toast("Pop-up added ✦");
      renderEvents(); renderDashboard();
    }).catch(function () { toast("Couldn't add — check connection"); });
  });

  /* ---------- announcement ---------- */
  var annId = null;
  function renderAnnouncement() {
    store.getAnnouncement().then(function (a) {
      annId = a.id || null;
      $("#an-message").value = a.message || "";
      $("#an-url").value = a.link_url || "";
      $("#an-label").value = a.link_label || "";
      $("#an-active").checked = !!a.active;
    });
  }
  $("#announce-form").addEventListener("submit", function (e) {
    e.preventDefault();
    var a = {
      id: annId,
      message: $("#an-message").value.trim(),
      link_url: $("#an-url").value.trim(),
      link_label: $("#an-label").value.trim(),
      active: $("#an-active").checked
    };
    store.saveAnnouncement(a).then(function () { toast("Announcement saved ✦"); renderAnnouncement(); renderDashboard(); })
      .catch(function () { toast("Couldn't save — check connection"); });
  });

  /* ---------- settings ---------- */
  function badge(on, onText, offText) {
    return '<span class="badge ' + (on ? "on" : "off") + '">' + (on ? onText : offText) + "</span>";
  }
  function renderSettings() {
    $("#settings-status").innerHTML =
      '<div class="kv"><span class="k">Supabase (console + live content)</span>' + badge(LIVE, "Connected", "Not configured") + "</div>" +
      '<div class="kv"><span class="k">Square booking embed</span>' + badge(!!CFG.SQUARE_BOOKING_URL, "Connected", "Fallback active") + "</div>" +
      '<div class="kv"><span class="k">Instagram</span><span>' + esc(CFG.INSTAGRAM_HANDLE || "—") + "</span></div>";
  }
  var resetBtn = $("#reset-demo");
  if (resetBtn) resetBtn.addEventListener("click", function () {
    if (!confirm("Reset all demo edits back to sample content?")) return;
    demoStore.reset().then(function () { toast("Demo data reset"); showApp(); });
  });

  /* ---------- auth wiring ---------- */
  $("#login-form").addEventListener("submit", function (e) {
    e.preventDefault();
    var err = $("#login-error");
    err.hidden = true;
    liveStore.signIn($("#login-email").value.trim(), $("#login-pass").value)
      .then(function () { showApp(); })
      .catch(function (ex) {
        err.textContent = ex.message || "Sign-in failed";
        err.hidden = false;
      });
  });
  $("#signout-btn").addEventListener("click", function () {
    liveStore.signOut();
    showLogin();
  });

  /* ---------- boot ---------- */
  if (!LIVE) {
    showApp();                       // demo mode — straight in, banner on
  } else if (liveStore.token) {
    showApp();                       // existing session; 401s bounce to login
  } else {
    showLogin();
  }
})();
