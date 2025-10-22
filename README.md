<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Link Manager v3.4 — All Social Mini Player🚨</title>
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet" />
<style>
  :root {
    --bg: #071021;
    --card: rgba(255,255,255,0.03);
    --glass: rgba(255,255,255,0.04);
    --accent: #45e1ff;
    --muted: #9fb3bd;
    --radius: 12px;
  }
  * { box-sizing: border-box; }
  body {
    margin: 0;
    min-height: 100vh;
    font-family: Inter, 'Segoe UI', system-ui, Arial, sans-serif;
    background: linear-gradient(180deg, #031017, #071726);
    color: #eaf6f8;
    padding: 18px;
    display: flex;
    justify-content: center;
    align-items: flex-start;
  }
  .wrap {
    width: 100%;
    max-width: 980px;
  }
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
  }
  header h1 {
    font-size: 18px;
    margin: 0;
    display: flex;
    gap: 10px;
    align-items: center;
  }
  header .small {
    color: var(--muted);
    font-size: 13px;
  }
  .top {
    display: flex;
    gap: 12px;
    margin-top: 14px;
    align-items: center;
  }
  .search {
    flex: 1;
  }
  .search input {
    width: 100%;
    padding: 10px 12px;
    border-radius: 10px;
    border: 1px solid rgba(255,255,255,0.04);
    background: var(--glass);
    color: inherit;
    outline: none;
  }
  .btn {
    padding: 9px 12px;
    border-radius: 10px;
    border: none;
    background: var(--accent);
    color: #012;
    font-weight: 700;
    cursor: pointer;
    display: inline-flex;
    gap: 8px;
    align-items: center;
  }
  .btn.ghost {
    background: transparent;
    border: 1px solid rgba(255,255,255,0.04);
    color: var(--muted);
    font-weight: 600;
  }
  .panel {
    display: grid;
    grid-template-columns: 1fr 420px;
    gap: 18px;
    margin-top: 16px;
  }
  .card {
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    padding: 14px;
    border-radius: var(--radius);
    box-shadow: 0 8px 30px rgba(0,0,0,0.6);
  }
  .form-row {
    display: flex;
    gap: 8px;
  }
  .form-row input {
    flex: 1;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid rgba(255,255,255,0.03);
    background: transparent;
    color: inherit;
  }
  textarea {
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    border-radius: 10px;
    border: 1px solid rgba(255,255,255,0.03);
    background: transparent;
    color: inherit;
    min-height: 84px;
    resize: vertical;
  }
  .tabs {
    display: flex;
    gap: 8px;
    margin: 10px 0;
    flex-wrap: wrap;
  }
  .tab {
    padding: 8px 10px;
    border-radius: 8px;
    border: 1px solid rgba(255,255,255,0.03);
    color: var(--muted);
    cursor: pointer;
    font-size: 14px;
    user-select: none;
  }
  .tab.active {
    background: rgba(0,0,0,0.35);
    color: var(--accent);
    border-color: var(--accent);
  }
  .list {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 8px;
    min-height: 60px;
  }
  .item {
    display: flex;
    gap: 10px;
    align-items: center;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid rgba(255,255,255,0.02);
    background: var(--card);
    cursor: grab;
  }
  .favicon {
    width: 44px;
    height: 44px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(255,255,255,0.02);
    flex-shrink: 0;
    user-select: none;
  }
  .favicon img {
    width: 22px;
    height: 22px;
  }
  .meta {
    flex: 1;
    min-width: 0;
    user-select: none;
  }
  .meta .title {
    font-weight: 700;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .meta .url {
    font-size: 13px;
    color: var(--muted);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .actions {
    display: flex;
    gap: 6px;
    align-items: center;
  }
  .icon-btn {
    padding: 8px;
    border-radius: 8px;
    border: none;
    background: transparent;
    color: var(--muted);
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    font-size: 14px;
  }
  .icon-btn.primary {
    background: var(--accent);
    color: #012;
  }
  .small {
    font-size: 13px;
    color: var(--muted);
  }
  .toast {
    position: fixed;
    right: 18px;
    bottom: 18px;
    background: linear-gradient(90deg,#ffd36b,#ff8a00);
    color: #012;
    padding: 10px 14px;
    border-radius: 10px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    opacity: 0;
    transform: translateY(10px);
    transition: all 0.28s;
    pointer-events: none;
    user-select: none;
    z-index: 9999;
  }
  .toast.show {
    opacity: 1;
    transform: translateY(0);
  }
  /* preview player */
  .player-wrap {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .player-frame {
    width: 100%;
    height: 260px;
    border-radius: 10px;
    overflow: hidden;
    background: #000;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
  }
  .player-frame iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }
  .player-controls {
    display: flex;
    gap: 8px;
    align-items: center;
    justify-content: space-between;
  }
  .player-title {
    font-weight: 700;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .player-note {
    font-size: 13px;
    color: var(--muted);
  }
  /* Nomor urut */
  .number {
    min-width: 28px;
    text-align: right;
    color: var(--muted);
    font-weight: 700;
    user-select: none;
  }
  /* Panel Judul Belum ada */
  #noTitlePanel {
    margin-top: 20px;
  }
  #noTitlePanel > h3 {
    margin: 0 0 8px 0;
    font-weight: 700;
    color: var(--accent);
  }
  @media (max-width:900px) {
    .panel {
      grid-template-columns: 1fr;
    }
    .player-frame {
      height: 200px;
    }
  }
</style>
</head>
<!-- Lampu Rotator Polisi -->
<div class="rotator">
  <div class="lamp red"></div>
  <div class="lamp blue"></div>
</div>
<style>
  .rotator {
    position: fixed;
    top: 45px;      /* atur posisi vertikal (misalnya 20px dari atas) */
    right: 20px;    /* atur posisi horizontal (misalnya 20px dari kanan) */
    display: flex;
    gap: 8px;
    z-index: 9999;  /* biar selalu di atas elemen lain */
  }

  .lamp {
    width: 15px;
    height: 15px;
    border-radius: 50%;
    box-shadow: 0 0 20px rgba(255,255,255,0.2);
  }

  .red {
    background: red;
    animation: redFlash 0.4s infinite alternate;
  }

  .blue {
    background: blue;
    animation: blueFlash 0.4s infinite alternate;
    animation-delay: 0.2s;
  }

  @keyframes redFlash {
    0% { opacity: 2; box-shadow: 0 0 40px red; }
    100% { opacity: 0.1; box-shadow: 0 0 50px red; }
  }

  @keyframes blueFlash {
    0% { opacity: 2; box-shadow: 0 0 40px blue; }
    100% { opacity: 0.1; box-shadow: 0 0 50px blue; }
  }
</style>
<body>
<div class="wrap">
  <header>
    <h1><i class="fa-solid fa-link"></i> Link Manager v3.4</h1>
    <div class="small">All Social Mini Player — YouTube/TikTok/IG/Facebook/Spotify/Twitter     User ディッキー・(DICKY) 🧑‍🔬</div>
  </header>

  <div class="top">
    <div class="search"><input id="search" placeholder="🔥Cari(も宛ポ)judul atau url..." autocomplete="off" /></div>
    <button class="btn ghost" id="copyAllBtn"><i class="fa-solid fa-copy"></i> Salin Semua Judul & URL</button>
  </div>

  <div class="panel">
    <!-- LEFT MAIN LIST -->
    <div>
      <div class="card">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div style="font-weight:700">Tambah Link</div>
          <div class="small" id="count">Total: 0</div>
        </div>

        <div style="margin-top:12px" class="form-row">
          <input id="title" placeholder="Judul (opsional)" autocomplete="off" />
          <input id="url" placeholder="Contoh: youtube.com/watch?v=..." autocomplete="off" />
          <button class="btn" id="addBtn"><i class="fa-solid fa-plus"></i></button>
        </div>

        <textarea id="bulk" placeholder="Tambah banyak link (judul|link atau 1 link per baris)"></textarea>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button class="btn" id="bulkAdd"><i class="fa-solid fa-list"></i> Tambah Banyak</button>
          <button class="btn ghost" id="deleteAll" style="background:#c94b4b;color:#fff"><i class="fa-solid fa-trash"></i> Hapus Semua</button>
        </div>

        <div class="tabs" id="tabs" style="margin-top:12px">
          <div class="tab active" data-cat="all">Semua</div>
          <div class="tab" data-cat="tiktok">TikTok</div>
          <div class="tab" data-cat="youtube">YouTube</div>
          <div class="tab" data-cat="instagram">Instagram</div>
          <div class="tab" data-cat="facebook">Facebook</div>
          <div class="tab" data-cat="vimeo">Vimeo</div>
          <div class="tab" data-cat="soundcloud">SoundCloud</div>
          <div class="tab" data-cat="spotify">Spotify</div>
          <div class="tab" data-cat="twitter">Twitter</div>
          <div class="tab" data-cat="other">Lainnya</div>
        </div>

        <div class="list" id="list"></div>

        <!-- Panel link tanpa judul -->
        <div id="noTitlePanel" class="card" style="display:none;">
          <h3>Link belum punya judul (klik untuk tambah judul Hanya Dapat sekali saja!)</h3>
          <div class="list" id="noTitleList"></div>
        </div>
      </div>
    </div>

    <!-- RIGHT: Preview & Player -->
    <aside>
      <div class="card player-wrap">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div style="font-weight:700">Preview & Player</div>
          <div class="small">Klik "Putar" untuk embed</div>
        </div>

        <div class="player-frame" id="playerFrame">
          <div class="small" id="playerEmpty">Pilih item lalu klik tombol Putar (▶) untuk melihat/putar di sini.</div>
        </div>

        <div class="player-controls" id="playerControls" style="display:none">
          <div style="flex:1;min-width:0">
            <div class="player-title" id="playerTitle">—</div>
            <div class="player-note" id="playerNote"></div>
          </div>
          <div style="display:flex;gap:8px;align-items:center">
            <button class="btn ghost" id="openTabBtn"><i class="fa-solid fa-arrow-up-right-from-square"></i> Buka Tab</button>
            <button class="btn" id="closePlayer"><i class="fa-solid fa-xmark"></i> Tutup</button>
          </div>
        </div>
      </div>
    </aside>
  </div>
</div>

<div id="toast" class="toast">Tersalin</div>

<script src="https://cdn.jsdelivr.net/npm/sortablejs@1.15.0/Sortable.min.js"></script>
<script>
(() => {
  const KEY = 'link_manager_v3_2_' + btoa(location.pathname);
  let data = JSON.parse(localStorage.getItem(KEY) || '[]');
  let currentCat = 'all';

  // DOM helpers
  const $ = id => document.getElementById(id);
  const listEl = $('list');
  const noTitleListEl = $('noTitleList');
  const noTitlePanel = $('noTitlePanel');
  const playerFrame = $('playerFrame');
  const playerTitle = $('playerTitle');
  const playerNote = $('playerNote');
  const playerControls = $('playerControls');
  const playerEmpty = $('playerEmpty');

  function fixUrl(url) {
    if (!url) return '';
    const u = url.trim();
    if (/^https?:\/\//i.test(u)) return u;
    return 'https://' + u;
  }
  function tplFavicon(url) {
    try {
      return 'https://www.google.com/s2/favicons?domain=' + (new URL(url).hostname);
    } catch {
      return '';
    }
  }
  function showToast(msg) {
    const t = $('toast');
    t.textContent = msg;
    t.classList.add('show');
    clearTimeout(t._timer);
    t._timer = setTimeout(() => t.classList.remove('show'), 1700);
  }
  async function copyToClipboard(text) {
    try {
      await navigator.clipboard.writeText(text);
      showToast('Tersalin');
    } catch (e) {
      fallbackCopy(text);
      showToast('Tersalin (fallback)');
    }
  }
  function fallbackCopy(text) {
    const ta = document.createElement('textarea');
    ta.value = text;
    ta.style.position = 'fixed';
    ta.style.left = '-9999px';
    document.body.appendChild(ta);
    ta.select();
    document.execCommand('copy');
    ta.remove();
  }
  function validUrl(u) {
    try {
      new URL(u);
      return true;
    } catch {
      return false;
    }
  }
  function save() {
    localStorage.setItem(KEY, JSON.stringify(data));
    render();
  }

  function detectEmbed(url) {
    try {
      if (!url) return { platform: 'other', id: null, embedUrl: null, willEmbed: false };
      const pu = new URL(url);
      const hostname = pu.hostname.toLowerCase();
      const pathname = pu.pathname;
      if (hostname.includes('youtu.be') || hostname.includes('youtube.com')) {
        let id = null;
        if (hostname.includes('youtu.be')) id = pathname.slice(1);
        else {
          const v = pu.searchParams.get('v');
          if (v) id = v;
          else {
            const m = pathname.match(/\/(?:embed|shorts)\/([^\/\?]+)/i);
            if (m) id = m[1];
          }
        }
        if (id) return { platform: 'youtube', id, embedUrl: `https://www.youtube.com/embed/${id}?autoplay=1&rel=0`, willEmbed: true };
      }
      if (hostname.includes('vimeo.com') || hostname.includes('player.vimeo.com')) {
        const m = pathname.match(/\/(?:video\/)?(\d+)/);
        if (m) {
          const id = m[1];
          return { platform: 'vimeo', id, embedUrl: `https://player.vimeo.com/video/${id}?autoplay=1`, willEmbed: true };
        }
      }
      if (hostname.includes('tiktok.com')) {
        const m = pathname.match(/\/(?:@[^\/]+\/video\/|video\/|v\/)?([0-9]+)/i);
        if (m) {
          const id = m[1];
          return { platform: 'tiktok', id, embedUrl: `https://www.tiktok.com/embed/v2/${id}`, willEmbed: true };
        }
      }
      if (hostname.includes('instagram.com')) {
        const m = pathname.match(/\/(p|reel|tv)\/([^\/\?]+)/i);
        if (m) {
          const sc = m[2];
          return { platform: 'instagram', id: sc, embedUrl: `https://www.instagram.com/p/${sc}/embed/`, willEmbed: true };
        }
      }
      if (hostname.includes('soundcloud.com')) {
        return { platform: 'soundcloud', id: null, embedUrl: `https://w.soundcloud.com/player/?url=${encodeURIComponent(url)}`, willEmbed: true };
      }
      if (hostname.includes('spotify.com')) {
        return { platform: 'spotify', id: null, embedUrl: `https://open.spotify.com/embed?uri=${encodeURIComponent(url)}`, willEmbed: true };
      }
      if (hostname.includes('facebook.com') || hostname.includes('fb.watch')) {
        return { platform: 'facebook', id: null, embedUrl: `https://www.facebook.com/plugins/video.php?href=${encodeURIComponent(url)}&autoplay=1`, willEmbed: true };
      }
      if (hostname.includes('twitter.com') || hostname.includes('x.com') || hostname.includes('t.co')) {
        return { platform: 'twitter', id: null, embedUrl: null, willEmbed: false };
      }
      return { platform: 'other', id: null, embedUrl: null, willEmbed: false };
    } catch {
      return { platform: 'other', id: null, embedUrl: null, willEmbed: false };
    }
  }
  function getCategory(url) {
    if (!url) return 'other';
    const u = url.toLowerCase();
    if (u.includes('tiktok.com')) return 'tiktok';
    if (u.includes('youtube.com') || u.includes('youtu.be')) return 'youtube';
    if (u.includes('instagram.com')) return 'instagram';
    if (u.includes('facebook.com') || u.includes('fb.watch')) return 'facebook';
    if (u.includes('vimeo.com')) return 'vimeo';
    if (u.includes('soundcloud.com')) return 'soundcloud';
    if (u.includes('spotify.com')) return 'spotify';
    if (u.includes('twitter.com') || u.includes('x.com') || u.includes('t.co')) return 'twitter';
    return 'other';
  }

  function buildItem(item, idx, numbering = true) {
    const wrap = document.createElement('div');
    wrap.className = 'item';
    wrap.draggable = true;

    if (numbering) {
      const numDiv = document.createElement('div');
      numDiv.className = 'number';
      numDiv.textContent = (idx + 1) + '.';
      wrap.appendChild(numDiv);
    }

    const favicon = document.createElement('div');
    favicon.className = 'favicon';
    const favImg = document.createElement('img');
    favImg.src = tplFavicon(item.url);
    favicon.appendChild(favImg);

    const meta = document.createElement('div');
    meta.className = 'meta';

    const titleEl = document.createElement('div');
    titleEl.className = 'title';
    titleEl.textContent = item.title || item.url;

    const urlEl = document.createElement('div');
    urlEl.className = 'url';
    urlEl.textContent = item.url;

    meta.append(titleEl, urlEl);

    const actions = document.createElement('div');
    actions.className = 'actions';

    // Favorite (not implemented but icon for show)
    const fav = document.createElement('button');
    fav.className = 'icon-btn';
    fav.title = 'Favorit (coming soon)';
    fav.innerHTML = '<i class="fa-solid fa-check-circle"></i>';

    // Open new tab
    const openBtn = document.createElement('button');
    openBtn.className = 'icon-btn primary';
    openBtn.title = 'Buka di Tab Baru';
    openBtn.innerHTML = '<i class="fa-solid fa-arrow-up-right-from-square"></i>';
    openBtn.onclick = e => {
      e.stopPropagation();
      window.open(item.url, '_blank', 'noopener');
    };

    // Play embed
    const playBtn = document.createElement('button');
    playBtn.className = 'icon-btn primary';
    playBtn.title = 'Putar di Halaman';
    playBtn.innerHTML = '<i class="fa-solid fa-play"></i>';
    playBtn.onclick = e => {
      e.stopPropagation();
      playInPreview(item);
    };

    // Copy url
    const copyBtn = document.createElement('button');
    copyBtn.className = 'icon-btn';
    copyBtn.title = 'Salin URL';
    copyBtn.innerHTML = '<i class="fa-solid fa-copy"></i>';
    copyBtn.onclick = e => {
      e.stopPropagation();
      copyToClipboard(item.url);
    };

    // Delete
    const delBtn = document.createElement('button');
    delBtn.className = 'icon-btn';
    delBtn.title = 'Hapus';
    delBtn.innerHTML = '<i class="fa-solid fa-trash"></i>';
    delBtn.onclick = e => {
      e.stopPropagation();
      if (confirm('Hapus link ini?')) {
        data.splice(idx, 1);
        save();
        showToast('Link dihapus');
        clearPlayer();
      }
    };

    actions.append(fav, openBtn, playBtn, copyBtn, delBtn);

    wrap.append(favicon, meta, actions);

    // Klik item untuk edit judul sekali & show preview
    wrap.onclick = () => {
      if (!item.title) {
        let newTitle = prompt('Link ini belum punya judul. Masukkan judul sekarang (hanya bisa 1x):', '');
        if (newTitle) {
          newTitle = newTitle.trim();
          if (newTitle.length > 0) {
            data[idx].title = newTitle;
            save();
            showToast('Judul disimpan');
          }
        }
      }
      playerTitle.textContent = data[idx].title || data[idx].url;
      playerNote.textContent = getCategory(data[idx].url).toUpperCase();
    };

    return wrap;
  }

  function render() {
    $('count').textContent = 'Total: ' + data.length;
    listEl.innerHTML = '';
    noTitleListEl.innerHTML = '';

    const qv = ($('search').value || '').trim().toLowerCase();

    // Render main list
    let filteredMain = 0;
    data.forEach((d, i) => {
      const cat = getCategory(d.url);
      if (currentCat !== 'all' && cat !== currentCat) return;
      if (qv && !((d.title || '').toLowerCase().includes(qv) || (d.url || '').toLowerCase().includes(qv))) return;
      listEl.appendChild(buildItem(d, filteredMain));
      filteredMain++;
    });

    // Render no-title list
    const noTitleItems = data
      .map((d, i) => ({ d, i }))
      .filter(({ d }) => !d.title)
      .filter(({ d }) => {
        if (qv) return (d.url.toLowerCase().includes(qv));
        return true;
      });

    if (noTitleItems.length > 0) {
      noTitlePanel.style.display = 'block';
      noTitleItems.forEach(({ d, i }, idx) => {
        const item = document.createElement('div');
        item.className = 'item';
        item.style.cursor = 'pointer';

        const numDiv = document.createElement('div');
        numDiv.className = 'number';
        numDiv.textContent = (idx + 1) + '.';
        item.appendChild(numDiv);

        const favicon = document.createElement('div');
        favicon.className = 'favicon';
        const favImg = document.createElement('img');
        favImg.src = tplFavicon(d.url);
        favicon.appendChild(favImg);

        const meta = document.createElement('div');
        meta.className = 'meta';

        const titleEl = document.createElement('div');
        titleEl.className = 'title';
        titleEl.textContent = d.title || d.url;

        const urlEl = document.createElement('div');
        urlEl.className = 'url';
        urlEl.textContent = d.url;

        meta.append(titleEl, urlEl);

        item.append(favicon, meta);

        item.onclick = () => {
          if (!d.title) {
            let newTitle = prompt('Link ini belum punya judul. Masukkan judul sekarang (hanya bisa 1x):', '');
            if (newTitle) {
              newTitle = newTitle.trim();
              if (newTitle.length > 0) {
                data[i].title = newTitle;
                save();
                showToast('Judul disimpan');
              }
            }
          }
        };
        noTitleListEl.appendChild(item);
      });
    } else {
      noTitlePanel.style.display = 'none';
    }

    if (listEl._sortable) listEl._sortable.destroy();
    listEl._sortable = Sortable.create(listEl, {
      animation: 150, handle: '.favicon, .meta',
      onEnd: evt => {
        const from = evt.oldIndex, to = evt.newIndex;
        if (from === to) return;
        const moved = data.splice(from, 1)[0];
        data.splice(to, 0, moved);
        save();
        showToast('Urutan disimpan');
      }
    });

    // toggle visibilitas berdasarkan tombol
    listEl.style.display = linksVisible ? 'flex' : 'none';
  }

  function clearPlayer() {
    playerFrame.innerHTML = '<div class="small" id="playerEmpty">Pilih item lalu klik tombol Putar (▶) untuk melihat/putar di sini.</div>';
    playerControls.style.display = 'none';
    playerTitle.textContent = '—';
    playerNote.textContent = '';
  }

  function playInPreview(item) {
    if (!item || !item.url) return;
    const info = detectEmbed(item.url);
    playerFrame.innerHTML = '';
    playerTitle.textContent = item.title || item.url;
    playerNote.textContent = info.platform.toUpperCase();

    if (info.willEmbed && info.embedUrl) {
      const iframe = document.createElement('iframe');
      iframe.src = info.embedUrl;
      iframe.allow = 'autoplay; encrypted-media; fullscreen; picture-in-picture';
      iframe.loading = 'lazy';
      iframe.referrerPolicy = 'no-referrer';
      iframe.style.border = '0';
      playerFrame.appendChild(iframe);
      playerControls.style.display = 'flex';
      $('openTabBtn').onclick = () => window.open(item.url, '_blank', 'noopener');
      $('closePlayer').onclick = () => clearPlayer();

      const fallbackNotice = document.createElement('div');
      fallbackNotice.className = 'small';
      fallbackNotice.textContent = 'Jika tidak muncul, tekan "Buka Tab" untuk membuka di tab baru.';
      const fallbackTimer = setTimeout(() => {
        if (playerFrame.contains(iframe)) {
          playerFrame.appendChild(fallbackNotice);
        }
      }, 2000);
      $('closePlayer').onclick = () => {
        clearTimeout(fallbackTimer);
        clearPlayer();
      };
    } else {
      const box = document.createElement('div');
      box.style.padding = '12px';
      box.innerHTML = `<div class="small">Preview embed tidak tersedia untuk platform ini. Silakan buka di tab baru.</div>`;
      playerFrame.appendChild(box);
      playerControls.style.display = 'flex';
      $('openTabBtn').onclick = () => window.open(item.url, '_blank', 'noopener');
      $('closePlayer').onclick = () => clearPlayer();
    }
  }

  // toggle show/hide list
  let linksVisible = false; // default hidden
  function createToggleBtn() {
    const container = document.createElement('div');
    container.style.margin = '8px 0';
    const btn = document.createElement('button');
    btn.className = 'btn ghost';
    btn.id = 'toggleLinksBtn';
    btn.textContent = 'Tampilkan Link';
    btn.onclick = () => {
      linksVisible = !linksVisible;
      btn.textContent = linksVisible ? 'Sembunyikan Link' : 'Tampilkan Link';
      listEl.style.display = linksVisible ? 'flex' : 'none';
    };
    container.appendChild(btn);
    listEl.parentNode.insertBefore(container, listEl);
  }
  createToggleBtn();

  // copy all links + judul dengan nomor urut dan format nomor. judul|url
  $('copyAllBtn').onclick = () => {
    const qv = ($('search').value || '').trim().toLowerCase();
    const filtered = data.filter(d => {
      const cat = getCategory(d.url);
      if (currentCat !== 'all' && cat !== currentCat) return false;
      if (qv && !((d.title || '').toLowerCase().includes(qv) || (d.url || '').toLowerCase().includes(qv))) return false;
      return true;
    });
    if (!filtered.length) {
      showToast('Tidak ada link');
      return;
    }
    // Format: nomor. judul|url
    const textToCopy = filtered.map((d,i) => {
      const titlePart = d.title ? d.title : '';
      const separator = '|';
      // Kalau judul kosong, output nomor. |url
      return `${i+1}. ${titlePart}${separator}${d.url}`;
    }).join('\n');
    copyToClipboard(textToCopy);
  };

  // Add single link
  $('addBtn').onclick = () => {
    const title = $('title').value.trim();
    const raw = $('url').value.trim();
    if (!raw) {
      alert('Masukkan URL');
      return;
    }
    const url = fixUrl(raw);
    if (!validUrl(url)) {
      alert('URL tidak valid');
      return;
    }
    data.push({ title: title || '', url });
    save();
    $('title').value = '';
    $('url').value = '';
    showToast('Link ditambahkan');
  };

  // Add bulk links
  $('bulkAdd').onclick = () => {
    const lines = ($('bulk').value || '').split('\n').map(s => s.trim()).filter(Boolean);
    let added = 0;
    lines.forEach(ln => {
      if (ln.includes('|')) {
        const parts = ln.split('|');
        const t = parts[0].trim();
        const u = parts.slice(1).join('|').trim();
        const f = fixUrl(u);
        if (validUrl(f)) {
          data.push({ title: t || '', url: f });
          added++;
        }
      } else {
        const f = fixUrl(ln);
        if (validUrl(f)) {
          data.push({ title: '', url: f });
          added++;
        }
      }
    });
    if (added) {
      save();
      $('bulk').value = '';
      showToast(added + ' link ditambahkan');
    } else showToast('Tidak ada link valid');
  };

  // Delete all
  $('deleteAll').onclick = () => {
    if (!data.length) {
      showToast('Tidak ada data');
      return;
    }
    if (confirm('Hapus semua link?')) {
      data = [];
      save();
      showToast('Semua link dihapus');
      clearPlayer();
    }
  };

  // Search input
  $('search').addEventListener('input', () => render());

  // Tabs click
  $('tabs').addEventListener('click', (e) => {
    const t = e.target.closest('.tab');
    if (!t) return;
    document.querySelectorAll('.tab').forEach(x => x.classList.remove('active'));
    t.classList.add('active');
    currentCat = t.dataset.cat;
    render();
  });

  // Initial render
  render();
  clearPlayer();
})();
</script>
<!-- Jam Digital -->
<div id="clock" style="
    position: fixed;
    top: 10px;
    right: 10px;
    background: rgba(0, 0, 0, 0.6);
    color: #fff;
    font-family: Arial, sans-serif;
    font-size: 14px;
    font-weight: bold;
    padding: 6px 10px;
    border-radius: 6px;
    z-index: 9999;
"></div>

<script>
function updateClock() {
    const now = new Date();
    const h = String(now.getHours()).padStart(2, '0');
    const m = String(now.getMinutes()).padStart(2, '0');
    const s = String(now.getSeconds()).padStart(2, '0');
    document.getElementById('clock').textContent = h + ":" + m + ":" + s;
}
setInterval(updateClock, 1000);
updateClock();
</script>
<script>
(function () {
  // Deteksi sederhana: platform yang umumnya mendukung embed di halaman (bukan jaminan per-video)
  function isEmbeddablePlatform(url) {
    if (!url) return false;
    url = url.toLowerCase();
    return (
      url.includes('youtube.com/') || url.includes('youtu.be/') ||
      url.includes('vimeo.com') || url.includes('player.vimeo.com') ||
      url.includes('tiktok.com') ||
      url.includes('instagram.com') ||
      url.includes('soundcloud.com') ||
      url.includes('spotify.com') ||
      url.includes('facebook.com') || url.includes('fb.watch')
    );
  }

  function addDots(root) {
    var items = (root || document).querySelectorAll('#list .item, #noTitleList .item');
    items.forEach(function (item) {
      var urlEl = item.querySelector('.meta .url');
      if (!urlEl) return;
      var url = (urlEl.textContent || '').trim();
      if (!url) return;

      // Target tempat menaruh dot: pakai .actions kalau ada, kalau tidak ada taruh di ujung .item
      var target = item.querySelector('.actions') || item;

      // Hindari duplikasi
      var dot = target.querySelector(':scope > .embed-dot');
      if (!dot) {
        dot = document.createElement('span');
        dot.className = 'embed-dot';
        dot.style.display = 'inline-block';
        dot.style.width = '10px';
        dot.style.height = '10px';
        dot.style.borderRadius = '50%';
        dot.style.marginLeft = '8px';
        dot.style.boxShadow = '0 0 0 2px rgba(255,255,255,0.08) inset, 0 0 6px rgba(0,0,0,0.35)';
        dot.style.flexShrink = '0';

        if (target.classList.contains('actions')) {
          target.insertBefore(dot, target.firstChild); // letakkan paling kiri di bar aksi
        } else {
          item.appendChild(dot); // untuk panel "tanpa judul" yang tidak punya .actions
        }
      }

      var ok = isEmbeddablePlatform(url);
      dot.style.backgroundColor = ok ? '#22c55e' : '#ef4444';
      dot.title = ok
        ? 'Bisa diputar (platform mendukung embed)'
        : 'Tidak bisa diputar langsung (platform membatasi embed)';
    });
  }

  document.addEventListener('DOMContentLoaded', function () {
    // Jalankan awal
    addDots();

    // Amati perubahan daftar agar titik tetap terpasang setelah render/drag/add/delete/filter
    var list = document.getElementById('list');
    var noTitle = document.getElementById('noTitleList');
    [list, noTitle].forEach(function (el) {
      if (!el) return;
      var mo = new MutationObserver(function () {
        clearTimeout(el._dotTimer);
        el._dotTimer = setTimeout(function () {
          addDots(el);
        }, 50);
      });
      mo.observe(el, { childList: true, subtree: true });
    });
  });
})();
</script>
<!-- Tambahkan di dalam <body> -->
<div class="sidebar" id="sidebar">
  <div class="sidebar-header">
    <h2> ⎙ Download ✎ᝰ.</h2>
  </div>
  <ul class="sidebar-menu">
    <li><a href="https://fastdl.app/en" target="_blank"><i class="fab fa-instagram"></i> Instagram</a></li>
    <li><a href="https://ttsave.app/en" target="_blank"><i class="fab fa-tiktok"></i> TikTok</a></li>
    <li><a href="https://y2mate.com" target="_blank"><i class="fab fa-youtube"></i> YouTube</a></li>
    <li><a href="https://threadster.app/" target="_blank"><i class="fab fa-threads"></i> Threads</a></li>
    <!-- Tambahan Menu Download Opsi -->
<li>
  <a href="https://id.savefrom.net/252Fr/" target="_blank" class="flex items-center space-x-2 px-4 py-2 hover:bg-blue-600 rounded-md transition-colors duration-200">
    <i class="fas fa-check-circle"></i>
    <span>Download Opsi Cadangan</span>
    <li><a href="https://id.imgbb.com/" target="_blank" class="flex items-center space-x-1 px-2 py-1 hover:bg-blue-600 rounded-md transition-colors duration-200">
    <i class="fas fa-cogs"></i>
    <span>Hosting Gambar</span>
  </a>
</li><a dalam pengembangan
  </ul>
</div>

<!-- Button toggle -->
<div class="toggle-btn" onclick="toggleSidebar()">
  <i class="fas fa-bars"></i>
</div>

<!-- Style -->
<style>
  .sidebar {
    position: fixed;
    top: 80px; /* pas di bawah jam */
    right: -220px;
    width: 200px;
    height: auto;
    background: #1e293b;
    color: white;
    border-radius: 15px 0 0 15px;
    box-shadow: -3px 3px 10px rgba(0,0,0,0.3);
    transition: right 0.3s ease;
    font-family: "Poppins", sans-serif;
    z-index: 999;
  }

  .sidebar.open {
    right: 0;
  }

  .sidebar-header {
    padding: 15px;
    font-size: 18px;
    font-weight: bold;
    border-bottom: 1px solid rgba(255,255,255,0.2);
    text-align: center;
  }

  .sidebar-menu {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .sidebar-menu li {
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }

  .sidebar-menu a {
    display: flex;
    align-items: center;
    padding: 12px 15px;
    color: white;
    text-decoration: none;
    transition: background 0.3s ease, padding-left 0.3s ease;
  }

  .sidebar-menu a i {
    margin-right: 10px;
    font-size: 18px;
  }

  .sidebar-menu a:hover {
    background: #334155;
    padding-left: 25px;
  }

  .toggle-btn {
    position: fixed;
    top: 90px;
    right: 15px;
    background: #1e293b;
    color:#95e0ff;
    padding: 10px 12px;
    border-radius: 10px;
    cursor: pointer;
    box-shadow: 0 3px 6px rgba(0,0,0,0.3);
    z-index: 1000;
  }

  .toggle-btn i {
    font-size: 20px;
  }
</style>

<!-- FontAwesome -->
<script src="https://kit.fontawesome.com/4b1f1d6c2e.js" crossorigin="anonymous"></script>

<!-- Script -->
<script>
  function toggleSidebar() {
    document.getElementById("sidebar").classList.toggle("open");
  }
</script>
<!-- Fullscreen Icon -->
<style>
  #fullscreenIcon {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: #007bff;
    color: white;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    transition: background 0.3s;
    z-index: 9999;
  }
  #fullscreenIcon:hover {
    background: #0056b3;
  }
</style>

<div id="fullscreenIcon" style="display:none;">⛶</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const iframe = document.querySelector("iframe");
    const icon = document.getElementById("fullscreenIcon");

    // Jika ada embed/iframe, tampilkan icon
    if (iframe) {
      icon.style.display = "flex";
      
      icon.addEventListener("click", function() {
        if (iframe.requestFullscreen) {
          iframe.requestFullscreen();
        } else if (iframe.mozRequestFullScreen) { // Firefox
          iframe.mozRequestFullScreen();
        } else if (iframe.webkitRequestFullscreen) { // Chrome, Safari, Opera
          iframe.webkitRequestFullscreen();
        } else if (iframe.msRequestFullscreen) { // IE/Edge
          iframe.msRequestFullscreen();
        }
      });
    }
  });
</script>
<!-- ========================= SETTINGS MODULE (paste before </body>) ========================= -->
<style>
  /* Theme overrides (Light) */
  :root[data-theme="light"] {
    --bg: #f4f7fb;
    --card: rgba(0,0,0,0.03);
    --glass: rgba(0,0,0,0.05);
    --accent: #0ea5e9;
    --muted: #405465;
    color-scheme: light;
  }
  :root[data-theme="light"] body {
    background: linear-gradient(180deg, #eaf2fb, #dfe9f7);
    color: #082032;
  }
  :root[data-theme="light"] .card {
    background: linear-gradient(180deg, rgba(0,0,0,0.04), rgba(0,0,0,0.02));
    box-shadow: 0 8px 30px rgba(0,0,0,0.08);
  }
  :root[data-theme="light"] .btn.ghost,
  :root[data-theme="light"] .tab { border-color: rgba(0,0,0,0.08); }
  :root[data-theme="light"] .search input,
  :root[data-theme="light"] .form-row input,
  :root[data-theme="light"] textarea { border-color: rgba(0,0,0,0.08); }
  :root[data-theme="light"] .item { border-color: rgba(0,0,0,0.06); background: rgba(255,255,255,0.85); }
  :root[data-theme="light"] .favicon { background: rgba(0,0,0,0.04); }
  :root[data-theme="light"] .small { color: #557082; }
  :root[data-theme="light"] .player-frame { background:#fff; color:#111; }
  :root[data-theme="light"] #clock { background: rgba(0,0,0,0.2); }

  /* Floating gear button */
  #settingsBtn {
    position: fixed; bottom: 20px; right: 20px;
    width: 52px; height: 52px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    background: var(--accent); color:#012; font-size: 22px; cursor: pointer;
    box-shadow: 0 10px 24px rgba(0,0,0,0.35); z-index: 10001; border:0;
  }
  #settingsBtn:active { transform: translateY(1px); }

  /* Modal */
  #settingsModalBackdrop {
    position: fixed; inset: 0; background: rgba(0,0,0,0.55);
    display:none; align-items: center; justify-content: center; z-index: 10002;
  }
  #settingsModal {
    width: min(720px, 92vw);
    background: var(--card);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px; padding: 16px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.6);
    backdrop-filter: blur(8px);
  }
  #settingsModal h2 { margin:0 0 8px 0; font-size:18px; }
  #settingsModal .row { display:flex; gap:10px; align-items:center; justify-content: space-between; padding:10px 0; border-bottom:1px dashed rgba(255,255,255,0.08); }
  #settingsModal .row:last-child { border-bottom:0; }
  #settingsModal .desc { font-size:13px; opacity:.8 }
  #settingsModal .switch { display:inline-flex; gap:8px; align-items:center; }
  #settingsModal .switch input { width: 44px; height: 22px; }

  /* Editor table */
  #editorWrap { margin-top:10px; max-height: 46vh; overflow:auto; border:1px solid rgba(255,255,255,0.08); border-radius: 12px; }
  #editorTable { width:100%; border-collapse: collapse; font-size:14px; }
  #editorTable th, #editorTable td { padding:8px; border-bottom:1px solid rgba(255,255,255,0.06); vertical-align: top; }
  #editorTable th { position: sticky; top:0; background: rgba(0,0,0,0.25); backdrop-filter: blur(6px); text-align:left; }
  :root[data-theme="light"] #editorTable th { background: rgba(255,255,255,0.9); }
  #editorTable input { width:100%; padding:8px; border-radius:8px; border:1px solid rgba(255,255,255,0.12); background: transparent; color: inherit; }
  :root[data-theme="light"] #editorTable input { border-color: rgba(0,0,0,0.12); background: rgba(255,255,255,0.6); }
  #editorActions { display:flex; gap:8px; justify-content: flex-end; margin-top: 12px; }

  /* Lock overlay */
  #safeLock {
    position: fixed; inset:0; background: rgba(2,6,23,0.92);
    display:none; align-items:center; justify-content:center; z-index: 10003;
  }
  #safeLock .box {
    width:min(380px, 92vw); background: var(--card);
    border:1px solid rgba(255,255,255,0.08); border-radius: 16px; padding: 16px;
    text-align:center; box-shadow: 0 20px 60px rgba(0,0,0,0.6);
  }
  #safeLock input {
    width:100%; margin-top:10px; padding:10px; border-radius:10px; border:1px solid rgba(255,255,255,0.12); background:transparent; color:inherit;
  }
</style>

<!-- Floating Settings button -->
<button id="settingsBtn" title="Settings"><i class="fa-solid fa-gear"></i></button>

<!-- Modal -->
<div id="settingsModalBackdrop" role="dialog" aria-modal="true" aria-labelledby="settingsTitle">
  <div id="settingsModal" class="card">
    <div style="display:flex;justify-content:space-between;align-items:center;gap:8px">
      <h2 id="settingsTitle"><i class="fa-solid fa-sliders"></i> Settings</h2>
      <button class="btn ghost" id="closeSettings"><i class="fa-solid fa-xmark"></i> Tutup</button>
    </div>

    <div class="row">
      <div>
        <div><strong>Mode Gelap/Terang</strong></div>
        <div class="desc">Ubah tampilan tema. Disimpan otomatis.</div>
      </div>
      <div class="switch">
        <label for="themeSelect" class="small">Tema</label>
        <select id="themeSelect" class="btn ghost" style="padding:8px 10px">
          <option value="dark">Gelap</option>
          <option value="light">Terang</option>
          </option>
        </select>
      </div>
    </div>

    <div class="row">
      <div>
        <div><strong>Akses Edit</strong></div>
        <div class="desc">Edit semua judul & URL yang tersimpan.</div>
      </div>
      <button class="btn" id="openEditor"><i class="fa-solid fa-pen-to-square"></i> Buka Editor</button>
    </div>

    <div id="editorSection" style="display:none">
      <div id="editorWrap">
        <table id="editorTable">
          <thead>
            <tr><th style="width:56px">No</th><th>Judul</th><th>URL</th><th style="width:44px">Hapus</th></tr>
          </thead>
          <tbody id="editorBody"></tbody>
        </table>
      </div>
      <div id="editorActions">
        <button class="btn ghost" id="addRow"><i class="fa-solid fa-plus"></i> Tambah Baris</button>
        <button class="btn" id="saveEdits"><i class="fa-solid fa-floppy-disk"></i> Simpan & Muat Ulang</button>
      </div>
    </div>

    <div class="row" style="margin-top:8px">
      <div>
        <div><strong>Mode Aman (Lock)</strong></div>
        <div class="desc">Setelah Mode diaktifkan, halaman akan terkunci bahkan setelah direfresh. Buka dengan sandi yang benar<strong> *** </strong>.</div>
      </div>
      <div class="switch">
        <label class="small" for="safeToggle">Aktifkan</label>
        <input type="checkbox" id="safeToggle">
      </div>
    </div>

    <div class="row">
      <div>
        <div><strong>Ekspor Data</strong></div>
        <div class="desc">Unduh semua data link ke penyimpanan perangkat.</div>
      </div>
      <div style="display:flex;gap:8px">
        <button class="btn ghost" id="exportTxt"><i class="fa-solid fa-file-lines"></i> TXT</button>
        <button class="btn ghost" id="exportJson"><i class="fa-solid fa-file-code"></i> JSON</button>
      </div>
    </div>
  </div>
</div>

<!-- Safe Lock Overlay -->
<div id="safeLock">
  <div class="box card">
    <div style="font-weight:700;margin-bottom:6px"><i class="fa-solid fa-lock"></i> Situs Dikunci</div>
    <div class="small">Masukkan sandi untuk membuka.</div>
    <input id="lockPass" type="password" placeholder="Masukkan sandi..." autocomplete="off" />
    <div style="display:flex;gap:8px;justify-content:center;margin-top:10px">
      <button class="btn" id="unlockBtn"><i class="fa-solid fa-unlock-keyhole"></i> Buka</button>
    </div>
  </div>
</div>

<script>
(function(){
  // ====== Keys & helpers (selaras dengan script utama) ======
  const STORE_KEY = 'link_manager_v3_2_' + btoa(location.pathname); // sama seperti script utama
  const THEME_KEY = 'lm_theme';
  const LOCK_KEY  = 'lm_lock_enabled';
  const UNLOCK_SESSION_KEY = 'lm_lock_unlocked'; // sessionStorage

  const qs = s => document.querySelector(s);
  const ce = (t, props={}) => Object.assign(document.createElement(t), props);

  function readData(){
    try { return JSON.parse(localStorage.getItem(STORE_KEY) || '[]'); } catch { return []; }
  }
  function writeData(arr){
    localStorage.setItem(STORE_KEY, JSON.stringify(arr || []));
  }
  function downloadBlob(filename, text, type='text/plain'){
    const blob = new Blob([text], {type});
    const url = URL.createObjectURL(blob);
    const a = ce('a', {href:url, download: filename});
    document.body.appendChild(a); a.click(); a.remove();
    URL.revokeObjectURL(url);
  }

  // ====== Theme ======
  function applyTheme(t){
    const theme = (t === 'light') ? 'light' : 'dark';
    document.documentElement.setAttribute('data-theme', theme === 'light' ? 'light' : 'dark');
    localStorage.setItem(THEME_KEY, theme);
  }
  (function initTheme(){
    const saved = localStorage.getItem(THEME_KEY) || 'dark';
    applyTheme(saved);
    const sel = document.getElementById('themeSelect');
    if (sel) sel.value = (saved === 'light' ? 'light' : 'dark');
  })();

  // ====== Settings modal open/close ======
  const openBtn = document.getElementById('settingsBtn');
  const backdrop = document.getElementById('settingsModalBackdrop');
  const closeBtn = document.getElementById('closeSettings');

  openBtn.addEventListener('click', ()=> backdrop.style.display = 'flex');
  closeBtn.addEventListener('click', ()=> backdrop.style.display = 'none');
  backdrop.addEventListener('click', (e)=> { if(e.target === backdrop) backdrop.style.display='none'; });

  // Theme select
  document.getElementById('themeSelect').addEventListener('change', (e)=> applyTheme(e.target.value));

  // ====== Editor ======
  const editorSection = document.getElementById('editorSection');
  const editorBody = document.getElementById('editorBody');

  function buildEditorRows(){
    editorBody.innerHTML = '';
    const arr = readData();
    arr.forEach((it, idx)=>{
      const tr = ce('tr');
      const tdNo = ce('td', {textContent: (idx+1)+'.'});
      const tdTitle = ce('td');
      const tdUrl = ce('td');
      const tdDel = ce('td');

      const inpT = ce('input', {value: it.title || ''});
      const inpU = ce('input', {value: it.url || ''});
      const delBtn = ce('button', {className:'btn ghost', innerHTML:'<i class="fa-solid fa-trash"></i>'});
      delBtn.addEventListener('click', ()=> { tr.remove(); renumber(); });

      tdTitle.appendChild(inpT);
      tdUrl.appendChild(inpU);
      tdDel.appendChild(delBtn);

      tr.append(tdNo, tdTitle, tdUrl, tdDel);
      editorBody.appendChild(tr);
    });
    renumber();
  }
  function renumber(){
    [...editorBody.querySelectorAll('tr')].forEach((tr,i)=>{
      const td = tr.firstChild; if (td) td.textContent = (i+1) + '.';
    });
  }

  document.getElementById('openEditor').addEventListener('click', ()=>{
    editorSection.style.display = (editorSection.style.display === 'none' || editorSection.style.display === '') ? 'block' : 'none';
    if (editorSection.style.display === 'block') buildEditorRows();
  });

  document.getElementById('addRow').addEventListener('click', ()=>{
    const tr = ce('tr');
    tr.innerHTML = `
      <td></td>
      <td><input value=""></td>
      <td><input value=""></td>
      <td><button class="btn ghost"><i class="fa-solid fa-trash"></i></button></td>`;
    tr.querySelector('button').addEventListener('click', ()=> { tr.remove(); renumber(); });
    editorBody.appendChild(tr);
    renumber();
  });

  document.getElementById('saveEdits').addEventListener('click', ()=>{
    const rows = [...editorBody.querySelectorAll('tr')];
    const next = [];
    rows.forEach(r=>{
      const t = r.children[1].querySelector('input').value.trim();
      const u = r.children[2].querySelector('input').value.trim();
      if (!u) return; // skip baris tanpa URL
      // normalisasi URL
      const fixed = /^https?:\/\//i.test(u) ? u : ('https://' + u);
      try { new URL(fixed); next.push({title: t, url: fixed}); } catch {}
    });
    writeData(next);
    // reload agar UI utama ikut membaca ulang localStorage & render
    location.reload();
  });

  // ====== Safe Mode (Lock) ======
  const safeToggle = document.getElementById('safeToggle');
  function isLockedEnabled(){ return localStorage.getItem(LOCK_KEY) === '1'; }
  function isUnlockedThisSession(){ return sessionStorage.getItem(UNLOCK_SESSION_KEY) === '1'; }

  function applyLockUI(){
    const lock = document.getElementById('safeLock');
    if (isLockedEnabled() && !isUnlockedThisSession()) {
      lock.style.display = 'flex';
    } else {
      lock.style.display = 'none';
    }
  }
  // init toggle state
  safeToggle.checked = isLockedEnabled();
  safeToggle.addEventListener('change', ()=>{
    if (safeToggle.checked) {
      localStorage.setItem(LOCK_KEY, '1');
      sessionStorage.removeItem(UNLOCK_SESSION_KEY);
    } else {
      localStorage.removeItem(LOCK_KEY);
      sessionStorage.removeItem(UNLOCK_SESSION_KEY);
    }
    applyLockUI();
  });

  // Unlock handler
  document.getElementById('unlockBtn').addEventListener('click', ()=>{
    const val = (document.getElementById('lockPass').value || '').trim();
    if (val === '222') {
      sessionStorage.setItem(UNLOCK_SESSION_KEY, '1');
      applyLockUI();
    } else {
      alert('Sandi salah.');
    }
  });

  // Pada load awal, tampilkan lock bila perlu
  applyLockUI();

  // ====== Export ======
  function exportTxt(){
    const arr = readData();
    const lines = arr.map((it,i)=> `${i+1}. ${(it.title||'')}|${it.url}`).join('\n');
    const fname = `links_${new Date().toISOString().slice(0,19).replace(/[:T]/g,'-')}.txt`;
    downloadBlob(fname, lines, 'text/plain');
  }
  function exportJson(){
    const arr = readData();
    const fname = `links_${new Date().toISOString().slice(0,19).replace(/[:T]/g,'-')}.json`;
    downloadBlob(fname, JSON.stringify(arr, null, 2), 'application/json');
  }
  document.getElementById('exportTxt').addEventListener('click', exportTxt);
  document.getElementById('exportJson').addEventListener('click', exportJson);

})();
</script>
<!-- ====================== END SETTINGS MODULE ====================== -->
<!-- === STATUS ONLINE/OFFLINE (REAL SIGNAL, SMOOTH + ACTIVE PROBING) === -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
  /* === Status Badge (tetap seperti aslimu) === */
  .status-badge {
    position: fixed;
    top: 10px;
    right: 90px;
    padding: 4px 10px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-radius: 12px;
    font-size: 12px;
    font-weight: 600;
    color: white;
    backdrop-filter: blur(6px);
    box-shadow: 0 2px 6px rgba(0,0,0,0.3);
    transition: background 0.3s ease, box-shadow 0.3s ease, transform 0.2s ease, opacity 0.3s ease;
    opacity: 0;
    z-index: 99999;
  }
  .status-badge.show { opacity: 1; }
  .status-badge i { font-size: 12px; }
  .online {
    background: linear-gradient(135deg, #10b981, #059669);
    box-shadow: 0 0 8px rgba(16,185,129,0.6);
  }
  .offline {
    background: linear-gradient(135deg, #ef4444, #b91c1c);
    box-shadow: 0 0 10px rgba(239,68,68,0.8);
    animation: pulse 1s infinite;
  }
  @keyframes pulse {
    0% { box-shadow: 0 0 10px rgba(239,68,68,0.6); }
    50% { box-shadow: 0 0 15px rgba(239,68,68,1); transform: scale(1.05); }
    100% { box-shadow: 0 0 10px rgba(239,68,68,0.6); transform: scale(1); }
  }

  /* === Overlay Loading (tetap sama) === */
  .overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(4px);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 99998;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease;
  }
  .overlay.show { opacity: 1; pointer-events: auto; }
  .overlay .spinner {
    font-size: 40px;
    color: #ffffff;
    animation: spin 1.2s linear infinite;
  }
  .overlay p {
    margin-top: 10px;
    color: #ffffff;
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 1px;
  }
  @keyframes spin { 0% { transform: rotate(0deg);} 100% { transform: rotate(360deg);} }

  /* === Signal bars (baru, tapi ringan & non-intrusive) === */
  .signal-wrap { display:flex; align-items:center; gap:6px; }
  .signal-bars { display:flex; gap:4px; align-items:flex-end; height:15px; width:auto; }
  .signal-bar {
    width:6px;
    background: rgba(255,255,255,0.25);
    border-radius:2px;
    transition: height 480ms cubic-bezier(.2,.9,.2,1), background 300ms, opacity 300ms;
    opacity: 0.35;
    height: 6px;
  }
  .signal-text { font-size:12px; font-weight:700; margin-left:6px; letter-spacing:0.4px; }
</style>

<div id="statusBadge" class="status-badge">
  <div class="signal-wrap" aria-hidden="true">
    <div class="signal-bars" id="signalBars">
      <span class="signal-bar" data-index="1"></span>
      <span class="signal-bar" data-index="2"></span>
      <span class="signal-bar" data-index="3"></span>
      <span class="signal-bar" data-index="4"></span>
    </div>
    <span id="statusText" class="signal-text"><i class="fas fa-spinner fa-spin"></i> Reconnecting...</span>
  </div>
</div>

<!-- Overlay untuk offline -->
<div id="offlineOverlay" class="overlay">
  <i class="fas fa-circle-notch spinner"></i>
  <p>Masuk Mode Offline...</p>
</div>

<!-- Overlay untuk online -->
<div id="onlineOverlay" class="overlay">
  <i class="fas fa-circle-notch spinner"></i>
  <p>Menyambungkan...</p>
</div>

<script>
(function(){
  const statusBadge = document.getElementById("statusBadge");
  const statusText = document.getElementById("statusText");
  const signalBars = document.querySelectorAll('#signalBars .signal-bar');
  const offlineOverlay = document.getElementById("offlineOverlay");
  const onlineOverlay = document.getElementById("onlineOverlay");

  let smoothedScore = 1.0; // 0..1 (moving average)
  const SMOOTHING_ALPHA = 0.45; // semakin kecil => lebih halus
  const MEASURE_INTERVAL = 3000; // ms
  const SAMPLE_IMAGES = 2; // jumlah gambar probe
  const TIMEOUT_MS = 5000;

  /* helper */
  function showBadge(){ statusBadge.classList.add('show'); }
  function setOnlineStyle(){ statusBadge.classList.remove('offline'); statusBadge.classList.add('online'); }
  function setOfflineStyle(){ statusBadge.classList.remove('online'); statusBadge.classList.add('offline'); }

  function setSignalVisual(level){
    // level 1..4
    for (let i=0;i<signalBars.length;i++){
      const bar = signalBars[i];
      const idx = i+1;
      // base full heights for bars (low->high)
      const baseHeights = [6,10,14,20];
      if (idx <= level){
        // active bar: height scaled to its base
        const target = baseHeights[i] * (0.9 + 0.25 * (level/4)); // sedikit lebih tinggi untuk level tinggi
        bar.style.height = Math.round(target) + 'px';
        bar.style.opacity = '1';
        bar.style.background = 'rgba(255,255,255,1)';
      } else {
        // inactive
        bar.style.height = Math.round(baseHeights[i]*0.45) + 'px';
        bar.style.opacity = '0.28';
        bar.style.background = 'rgba(255,255,255,0.25)';
      }
    }
  }

  function updateStatusOffline(){
    setOfflineStyle();
    statusText.innerHTML = '<i class="fas fa-wifi-slash"></i> Offline';
    showBadge();
    setSignalVisual(0);
  }

  function updateStatusFromLevel(level, connLabel){
    setOnlineStyle();
    statusText.innerHTML = (connLabel ? connLabel + ' ' : '') + (level >= 3 ? 'Online' : 'Online');
    showBadge();
    setSignalVisual(level);
  }

  /* measure image load time (ms). resolves with ms or large number on fail */
  function measureImageLoad(url, timeoutMs = TIMEOUT_MS){
    return new Promise((resolve) => {
      const img = new Image();
      let done = false;
      const start = performance.now();
      const timer = setTimeout(()=> {
        if (!done){ done = true; resolve(timeoutMs); img.src = ''; }
      }, timeoutMs);

      img.onload = function(){
        if (done) return;
        done = true;
        clearTimeout(timer);
        const dt = performance.now() - start;
        resolve(Math.max(1, Math.round(dt)));
      };
      img.onerror = function(){
        if (done) return;
        done = true;
        clearTimeout(timer);
        resolve(timeoutMs);
      };
      // use picsum with unique seed to avoid cache
      img.src = url;
    });
  }

  /* main probing: combine navigator.connection.downlink (if available) + image latency */
  async function probeNetworkAndComputeScore(){
    if (!navigator.onLine){
      updateStatusOffline();
      return;
    }

    // 1) try navigator.connection.downlink
    const conn = navigator.connection || navigator.mozConnection || navigator.webkitConnection || null;
    const downlink = conn && typeof conn.downlink === 'number' ? conn.downlink : null; // Mbps

    // 2) measure image loads (SLOW if blocked) — we do SAMPLE_IMAGES sequentially
    const probes = [];
    for (let i=0;i<SAMPLE_IMAGES;i++){
      // different seed each time to avoid browser cache
      const seed = Date.now() + Math.floor(Math.random()*100000) + i;
      const url = 'https://picsum.photos/seed/' + seed + '/400/240';
      try {
        const t = await measureImageLoad(url, TIMEOUT_MS);
        probes.push(t);
        // short pause between probes
        await new Promise(r => setTimeout(r, 200));
      } catch(e){
        probes.push(TIMEOUT_MS);
      }
    }
    const avgMs = probes.reduce((a,b)=>a+b,0)/probes.length;

    // map avgMs to a 0..1 score (higher is better)
    // tuning thresholds:
    // <200ms -> excellent, <500ms -> good, <1000ms -> fair, <2000ms -> poor
    let latencyScore;
    if (avgMs < 200) latencyScore = 1.0;
    else if (avgMs < 500) latencyScore = 0.85;
    else if (avgMs < 1000) latencyScore = 0.6;
    else if (avgMs < 2000) latencyScore = 0.35;
    else latencyScore = 0.12;

    // map downlink (if exists) to 0..1
    let downlinkScore = null;
    if (downlink !== null && !isNaN(downlink)){
      // downlink thresholds (Mbps): >=25 excellent, >=5 good, >=1 fair
      if (downlink >= 25) downlinkScore = 1.0;
      else if (downlink >= 5) downlinkScore = 0.85;
      else if (downlink >= 1) downlinkScore = 0.6;
      else downlinkScore = 0.2;
    }

    // combine: if downlink present, weight it a bit more; else rely on latency
    const wDown = downlinkScore !== null ? 0.6 : 0.0;
    const wLat = 1.0 - wDown;
    const newScore = ( (downlinkScore !== null ? downlinkScore : 0) * wDown ) + (latencyScore * wLat);

    // smooth
    smoothedScore = (SMOOTHING_ALPHA * smoothedScore) + ((1 - SMOOTHING_ALPHA) * newScore);

    // convert smoothedScore to level 1..4
    let level = 1;
    if (smoothedScore >= 0.85) level = 4;
    else if (smoothedScore >= 0.6) level = 3;
    else if (smoothedScore >= 0.35) level = 2;
    else level = 1;

    // show label based on measured conditions
    let label = 'WIFI';
    if (conn && conn.type && conn.type === 'cellular') label = 'DATA';
    // fallback, try effectiveType if available
    if (conn && conn.effectiveType) label = conn.effectiveType.toUpperCase();

    updateStatusFromLevel(level, label);
  }

  /* fallback simulation if probing is impossible (to keep UI dynamic) */
  let simulateLevel = 4;
  function startSimulate(){
    // gentle random walk
    simulateLevel = simulateLevel || 4;
    simulateLevel += (Math.random() > 0.56 ? 1 : -1);
    if (simulateLevel < 1) simulateLevel = 1;
    if (simulateLevel > 4) simulateLevel = 4;
    updateStatusFromLevel(simulateLevel, 'Server');
  }

  /* orchestrator */
  let probeTimer = null;
  async function startProbingLoop(){
    // first immediate check
    if (!navigator.onLine){
      updateStatusOffline();
      return;
    }
    try {
      // attempt one probe; if it succeeds, keep probing; if exception, fallback to simulation
      await probeNetworkAndComputeScore();
      // set repeated interval
      if (probeTimer) clearInterval(probeTimer);
      probeTimer = setInterval(()=> {
        // protect: if offline, skip
        if (!navigator.onLine) { updateStatusOffline(); return; }
        probeNetworkAndComputeScore().catch(()=>{ /* ignore */ });
      }, MEASURE_INTERVAL);
    } catch (e){
      // fallback simulation
      if (probeTimer) clearInterval(probeTimer);
      probeTimer = setInterval(startSimulate, 2500);
    }
  }

  // Listeners
  window.addEventListener('online', () => {
    statusText.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Reconnecting...';
    showBadge();
    onlineOverlay.classList.add('show');
    setTimeout(()=> onlineOverlay.classList.remove('show'), 1400);
    // restart probing
    startProbingLoop();
  });
  window.addEventListener('offline', () => {
    updateStatusOffline();
    offlineOverlay.classList.add('show');
    setTimeout(()=> offlineOverlay.classList.remove('show'), 2000);
    if (probeTimer) clearInterval(probeTimer);
  });

  // network api change
  if (navigator.connection && navigator.connection.addEventListener){
    navigator.connection.addEventListener('change', () => {
      // quick immediate probe on change
      probeNetworkAndComputeScore().catch(()=>{});
    });
  }

  // init
  showBadge();
  // slight delay to let UI render then start probing
  setTimeout(()=> startProbingLoop(), 600);

  // safety: if everything fails, start simulation after a short time
  setTimeout(()=> {
    if (!probeTimer){
      // start simulation loop
      probeTimer = setInterval(startSimulate, 2600);
    }
  }, 2500);

})();
</script>
<!-- === END STATUS ONLINE/OFFLINE === -->
