Create a responsive "Play Together" Page for a web-based music game called "MelodyPlay" using HTML, CSS, and JavaScript. Without any react, tailwand or any other framework
Follow a clean, minimal, Apple-style design.
Write the code to link to this code and match them exactly:
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>MelodyPlay • Play Together</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    :root{
      --bg: #f5f7fb;
      --card: #ffffff;
      --text: #0a0a0a;
      --muted: #70757c;
      --border: #e6e8ef;
      --accent: #0a84ff; /* Apple blue-ish */
      --accent-press: #0066da;
      --shadow-soft: 0 8px 24px rgba(16, 24, 40, 0.06);
      --shadow-hover: 0 10px 28px rgba(16, 24, 40, 0.10);
      --radius-lg: 16px;
      --radius-md: 12px;
      --radius-sm: 10px;
    }
    /* Global reset-ish */
    *, *::before, *::after { box-sizing: border-box; }
    html, body { height: 100%; }
    body{
      margin:0; color: var(--text);
      background:
        radial-gradient(1200px 600px at 10% -10%, rgba(10,132,255,0.06), transparent 60%),
        linear-gradient(180deg, #f9fafc 0%, #f4f6fb 40%, #f3f5fa 100%);
      font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, "SF Pro Text", "Segoe UI", Roboto, "Helvetica Neue", Arial, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }

    /* Container */
    .container{ max-width: 1100px; margin: 0 auto; padding: 0 20px; }

    /* Nav */
    .nav{
      position: sticky; top: 0; z-index: 20;
      backdrop-filter: saturate(180%) blur(12px);
      background: rgba(255,255,255,0.75);
      border-bottom: 1px solid var(--border);
    }
    .nav-inner{ display:flex; align-items:center; justify-content:space-between; height:64px; }
    .brand{ display:flex; align-items:center; gap:12px; font-weight:700; letter-spacing:.2px; }
    .logo{
      width:36px; height:36px; border-radius:10px;
      background: linear-gradient(145deg, #a0cfff, #7db1ff);
      display:grid; place-items:center; color:#fff; box-shadow: var(--shadow-soft);
    }
    .nav-links{ display:flex; gap:12px; align-items:center; }
    .nav a{
      text-decoration: none; color: #2a2f35; padding:10px 14px; border-radius:10px; transition: all .2s ease;
    }
    .nav a:hover{ background: #f0f3f8; }
    .nav a.active{
      color: #0a59b0;
      background: #e8f2ff;
      box-shadow: inset 0 0 0 1px #d6e8ff;
    }

    /* Hero */
    .hero{
      text-align:center; padding: 40px 0 24px;
    }
    .hero h1{
      margin:0;
      font-size: clamp(28px, 4vw, 40px);
      line-height:1.1; font-weight:800; letter-spacing: -0.5px;
    }
    .hero p{
      margin:10px 0 0; color: var(--muted); font-size: clamp(14px, 2.2vw, 16px);
    }

    /* Layout */
    .grid{
      display:grid; gap:20px; align-items:start;
      grid-template-columns: 1fr;
    }
    @media (min-width: 900px){
      .grid{ grid-template-columns: 1.1fr .9fr; }
    }

    /* Cards */
    .card{
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: var(--radius-lg);
      box-shadow: var(--shadow-soft);
    }
    .card-header{
      padding: 18px 18px 10px; border-bottom: 1px solid var(--border);
    }
    .card-title{ margin:0; font-weight:700; font-size:16px; }
    .card-body{ padding: 16px; }
    .section-actions{ display:flex; gap:12px; flex-wrap:wrap; }

    /* Friend list */
    .friends{ display:flex; flex-direction:column; gap:8px; }
    .friend{
      display:flex; align-items:center; gap:12px;
      padding:10px 12px; border-radius: 12px; border: 1px solid var(--border);
      transition: box-shadow .2s ease, transform .15s ease, background .2s ease;
      background: #fff;
    }
    .friend:hover{ box-shadow: var(--shadow-soft); transform: translateY(-1px); background: #fbfdff; }
    .avatar{
      width:36px; height:36px; border-radius: 50%;
      background: linear-gradient(145deg, #edf3ff, #e6efff);
      display:grid; place-items:center; font-weight:700; color:#2f5fa6; border: 1px solid #dbe6ff;
      flex: 0 0 36px;
      user-select: none;
    }
    .friend-main{ display:flex; align-items:center; gap:8px; min-width:0; flex: 1; }
    .friend-name{ font-weight:600; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
    .friend-meta{ font-size:12px; color: var(--muted); }

    /* Buttons */
    .btn{
      appearance: none; border: none; cursor: pointer;
      font: inherit;
      padding: 10px 14px; border-radius: 999px;
      background: #f0f3f8; color:#142033;
      transition: transform .08s ease, box-shadow .2s ease, background .2s ease, color .2s ease;
      box-shadow: 0 0 0 0 rgba(0,0,0,0);
    }
    .btn:hover{ transform: translateY(-1px); box-shadow: var(--shadow-soft); }
    .btn:active{ transform: translateY(0); box-shadow: none; }
    .btn-primary{
      background: var(--accent); color: #fff;
      box-shadow: 0 6px 14px rgba(10,132,255,.25);
    }
    .btn-primary:hover{ background: #167dff; box-shadow: 0 8px 18px rgba(10,132,255,.32); }
    .btn-primary:active{ background: var(--accent-press); }
    .btn-outline{
      background: #fff; color:#0a59b0; border:1px solid #cfe2ff;
    }
    .btn-ghost{
      background: transparent; color:#2a2f35;
    }
    .btn-small{ padding: 8px 12px; font-size: 14px; }
    .btn-icon{
      display:inline-flex; align-items:center; gap:8px;
    }

    .friend .btn-invite{
      margin-left:auto;
      background: #edf3ff; color:#0a59b0; border: 1px solid #dbe6ff;
      padding: 8px 12px;
    }
    .friend .btn-invite:hover{ background: #e6f0ff; }

    .list-footer{
      padding: 10px 12px; display:flex; justify-content:center;
      border-top: 1px dashed var(--border);
    }

    /* Lobby buttons area */
    .lobby-actions{
      display:grid; gap:12px; grid-template-columns: 1fr; margin-top: 6px;
    }
    @media (min-width: 560px){
      .lobby-actions{ grid-template-columns: 1fr 1fr; }
    }

    /* Inputs */
    .field{ display:flex; flex-direction:column; gap:6px; }
    .field label{ font-size: 13px; color: #3b4151; }
    .input, .select{
      width:100%; padding: 12px 14px; border-radius: 12px;
      border: 1px solid var(--border); background:#fbfcff; color:#0f1222;
      outline: none; transition: box-shadow .2s ease, border-color .2s ease, background .2s ease;
    }
    .input:focus, .select:focus{
      border-color: #b9d6ff; box-shadow: 0 0 0 4px rgba(10,132,255,0.12);
      background: #ffffff;
    }

    /* Modal */
    .modal-backdrop{
      position: fixed; inset:0; display:none; align-items:center; justify-content:center; padding:16px;
      background: rgba(15,20,35,0.45); backdrop-filter: blur(6px);
      z-index: 50;
    }
    .modal{
      width: 100%; max-width: 560px; background: var(--card);
      border: 1px solid var(--border); border-radius: 20px; box-shadow: var(--shadow-hover);
      transform: translateY(6px); opacity: 0; transition: opacity .2s ease, transform .2s ease;
    }
    .modal.show{ transform: translateY(0); opacity: 1; }
    .modal-header{ padding: 18px 20px; border-bottom: 1px solid var(--border); display:flex; justify-content:space-between; align-items:center; }
    .modal-title{ margin:0; font-weight:700; font-size:18px; }
    .modal-body{ padding: 18px 20px; display:grid; gap:14px; }
    .modal-footer{ padding: 16px 20px; border-top: 1px solid var(--border); display:flex; gap:10px; justify-content:flex-end; }

    /* Footer */
    footer{
      margin-top: 36px; padding: 20px 0; text-align:center; color: var(--muted);
      border-top: 1px solid var(--border);
    }

    /* Toasts */
    .toast-stack{ position: fixed; right: 16px; bottom: 16px; display:flex; flex-direction:column; gap:8px; z-index: 60; }
    .toast{
      background:#ffffff; border:1px solid var(--border); border-radius: 12px; padding:10px 12px;
      box-shadow: var(--shadow-soft); font-size: 14px; color:#25405f;
      animation: toast-in .25s ease both;
    }
    @keyframes toast-in{
      from{ opacity:0; transform: translateY(6px); }
      to{ opacity:1; transform: translateY(0); }
    }

    /* Utility */
    .sr-only{ position:absolute; left:-9999px; }
  </style>
</head>
<body>
  <!-- Nav -->
  <nav class="nav">
    <div class="container nav-inner">
      <div class="brand">
        <div class="logo" aria-hidden="true">
          <!-- Simple music glyph -->
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true">
            <path d="M9 4v11.2a2.8 2.8 0 1 1-1.2-2.3V6.2l8-1.6v8.6a2.8 2.8 0 1 1-1.2-2.3V4L9 4z" fill="#fff"/>
          </svg>
        </div>
        <span>MelodyPlay</span>
      </div>
      <div class="nav-links" role="navigation" aria-label="Primary">
        <a href="#" aria-label="Home">Home</a>
        <a href="#" aria-label="Leaderboard">Leaderboard</a>
        <a href="#" class="active" aria-current="page" aria-label="Play Together">Play Together</a>
        <a href="#" aria-label="Settings">Settings</a>
      </div>
    </div>
  </nav>

  <!-- Header -->
  <header class="container hero">
    <h1>Play Together</h1>
    <p>Invite friends or join a lobby to start playing.</p>
  </header>

  <!-- Main -->
  <main class="container">
    <div class="grid">
      <!-- Friends Panel -->
      <section class="card" aria-labelledby="friends-title">
        <div class="card-header">
          <h2 class="card-title" id="friends-title">Friends</h2>
        </div>
        <div class="card-body">
          <div class="friends" id="friendsList">
            <!-- Friend rows (placeholders) -->
            <!-- Example friend item -->
          </div>
        </div>
        <div class="list-footer">
          <button class="btn btn-icon" id="addFriendBtn" aria-label="Add Friend">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" aria-hidden="true">
              <path d="M12 5v14M5 12h14" stroke="#0a59b0" stroke-width="2" stroke-linecap="round"/>
            </svg>
            <span>Add Friend</span>
          </button>
        </div>
      </section>

      <!-- Lobby Section -->
      <section class="card" aria-labelledby="lobby-title">
        <div class="card-header">
          <h2 class="card-title" id="lobby-title">Lobby</h2>
        </div>
        <div class="card-body">
          <p style="color:var(--muted); margin: 0 0 8px;">Create a new room for your group or join with a room code.</p>
          <div class="lobby-actions">
            <button class="btn btn-primary btn-icon" id="createRoomBtn">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M12 5v14M5 12h14" stroke="#fff" stroke-width="2" stroke-linecap="round"/>
              </svg>
              <span>Create Room</span>
            </button>
            <button class="btn btn-outline btn-icon" id="joinRoomBtn">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" aria-hidden="true">
                <path d="M12 5v14M5 12h14" stroke="#0a59b0" stroke-width="2" stroke-linecap="round" transform="rotate(45 12 12)"/>
              </svg>
              <span>Join Room</span>
            </button>
          </div>
        </div>
      </section>
    </div>
  </main>

  <!-- Footer -->
  <footer>
    © 2025 MelodyPlay
  </footer>

  <!-- Modal -->
  <div class="modal-backdrop" id="modalBackdrop" aria-hidden="true" aria-labelledby="modalTitle" role="dialog">
    <div class="modal" id="modalCard">
      <div class="modal-header">
        <h3 class="modal-title" id="modalTitle">Modal</h3>
        <button class="btn btn-ghost btn-small" id="modalCloseBtn" aria-label="Close">✕</button>
      </div>
      <form id="modalForm">
        <div class="modal-body" id="modalBody"><!-- dynamic fields --></div>
        <div class="modal-footer">
          <button type="button" class="btn" id="modalCancelBtn">Cancel</button>
          <button type="submit" class="btn btn-primary" id="modalConfirmBtn">Confirm</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Toasts -->
  <div class="toast-stack" id="toastStack" aria-live="polite" aria-atomic="true"></div>

  <script>
    // ----- Data: friend placeholders -----
    const FRIENDS = [
      { id: 'f1', name: 'Ava Carter' },
      { id: 'f2', name: 'Noah Kim' },
      { id: 'f3', name: 'Mia Johnson' },
      { id: 'f4', name: 'Liam Chen' },
      { id: 'f5', name: 'Zoe Patel' }
    ];

    // ----- Utilities -----
    function initials(name){
      return name.split(' ').map(s => s[0]).slice(0,2).join('').toUpperCase();
    }
    function toast(message, timeout=2200){
      const stack = document.getElementById('toastStack');
      const t = document.createElement('div');
      t.className = 'toast';
      t.textContent = message;
      stack.appendChild(t);
      setTimeout(() => {
        t.style.transition = 'opacity .25s ease, transform .25s ease';
        t.style.opacity = '0';
        t.style.transform = 'translateY(6px)';
        setTimeout(()=> t.remove(), 250);
      }, timeout);
    }

    // ----- Friends rendering -----
    function renderFriends(){
      const list = document.getElementById('friendsList');
      list.innerHTML = '';
      FRIENDS.forEach(friend => {
        const row = document.createElement('div');
        row.className = 'friend';
        row.setAttribute('data-id', friend.id);

        const av = document.createElement('div');
        av.className = 'avatar';
        av.textContent = initials(friend.name);

        const main = document.createElement('div');
        main.className = 'friend-main';
        const name = document.createElement('div');
        name.className = 'friend-name';
        name.textContent = friend.name;
        const meta = document.createElement('div');
        meta.className = 'friend-meta';
        meta.textContent = 'Online';

        const invite = document.createElement('button');
        invite.className = 'btn btn-small btn-invite';
        invite.textContent = 'Invite';
        invite.addEventListener('click', () => onInvite(friend, invite));

        main.appendChild(name);
        main.appendChild(meta);
        row.appendChild(av);
        row.appendChild(main);
        row.appendChild(invite);

        list.appendChild(row);
      });
    }

    // ----- Invite handler (placeholder) -----
    function onInvite(friend, buttonEl){
      // Visual feedback: mark as invited temporarily
      const prev = buttonEl.textContent;
      buttonEl.textContent = 'Invited ✓';
      buttonEl.style.opacity = '0.75';
      buttonEl.disabled = true;
      toast(`Invitation sent to ${friend.name}`);
      // Reset after delay to simulate placeholder behavior
      setTimeout(()=> {
        buttonEl.textContent = prev;
        buttonEl.style.opacity = '1';
        buttonEl.disabled = false;
      }, 2500);
    }

    // ----- Modal helpers -----
    const modal = {
      backdrop: document.getElementById('modalBackdrop'),
      card: document.getElementById('modalCard'),
      title: document.getElementById('modalTitle'),
      body: document.getElementById('modalBody'),
      form: document.getElementById('modalForm'),
      closeBtn: document.getElementById('modalCloseBtn'),
      cancelBtn: document.getElementById('modalCancelBtn'),
      confirmBtn: document.getElementById('modalConfirmBtn'),
      open(){ 
        this.backdrop.style.display = 'flex';
        requestAnimationFrame(()=> this.card.classList.add('show'));
        this.backdrop.setAttribute('aria-hidden', 'false');
      },
      close(){
        this.card.classList.remove('show');
        this.backdrop.setAttribute('aria-hidden', 'true');
        setTimeout(()=> { this.backdrop.style.display = 'none'; }, 180);
      }
    };

    // Build Create Room modal content
    function showCreateRoom(){
      modal.title.textContent = 'Create Room';
      modal.body.innerHTML = `
        <div class="field">
          <label for="roomName">Room Name</label>
          <input id="roomName" class="input" type="text" placeholder="e.g., Saturday Jam" required />
        </div>
        <div class="field">
          <label for="playerCount">Number of Players</label>
          <select id="playerCount" class="select">
            <option value="2">2 players</option>
            <option value="3">3 players</option>
            <option value="4" selected>4 players</option>
            <option value="5">5 players</option>
            <option value="6">6 players</option>
            <option value="8">8 players</option>
          </select>
        </div>
      `;
      modal.form.onsubmit = (e) => {
        e.preventDefault(); // prevent navigation
        const name = document.getElementById('roomName').value.trim();
        const count = document.getElementById('playerCount').value;
        if (!name){ toast('Please enter a room name.'); return; }
        toast(`Room "${name}" created for ${count} players`);
        modal.close();
      };
      modal.open();
      setTimeout(()=> document.getElementById('roomName')?.focus(), 60);
    }

    // Build Join Room modal content
    function showJoinRoom(){
      modal.title.textContent = 'Join Room';
      modal.body.innerHTML = `
        <div class="field">
          <label for="roomCode">Room Code</label>
          <input id="roomCode" class="input" type="text" placeholder="Enter code (e.g., X7K9)" required />
        </div>
      `;
      modal.form.onsubmit = (e) => {
        e.preventDefault(); // prevent navigation
        const code = document.getElementById('roomCode').value.trim().toUpperCase();
        if (!code){ toast('Please enter a room code.'); return; }
        toast(`Joining room with code ${code}...`);
        modal.close();
      };
      modal.open();
      setTimeout(()=> document.getElementById('roomCode')?.focus(), 60);
    }

    // ----- Event wiring -----
    function wireUI(){
      // Initial friends render
      renderFriends();

      // Add Friend
      document.getElementById('addFriendBtn').addEventListener('click', () => {
        // Placeholder action
        toast('Add Friend clicked');
      });

      // Lobby buttons
      document.getElementById('createRoomBtn').addEventListener('click', showCreateRoom);
      document.getElementById('joinRoomBtn').addEventListener('click', showJoinRoom);

      // Modal controls
      modal.closeBtn.addEventListener('click', ()=> modal.close());
      modal.cancelBtn.addEventListener('click', ()=> modal.close());
      modal.backdrop.addEventListener('click', (e) => {
        if (e.target === modal.backdrop){ modal.close(); }
      });
      window.addEventListener('keydown', (e) => {
        if (e.key === 'Escape' && modal.backdrop.style.display === 'flex'){ modal.close(); }
      });

      // Prevent nav links from navigating (demo)
      document.querySelectorAll('.nav a').forEach(a => {
        a.addEventListener('click', (e) => { e.preventDefault(); toast('Navigation is a demo here'); });
      });
    }

    // ----- Init -----
    (function init(){
      wireUI();
    })();
  </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9842a2a75331b26a',t:'MTc1ODcyMDYxNS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>


Requirements:

1.	Main section layout:
Title: "Play Together" (centered, large, bold).
Subtitle: "Invite friends or join a lobby to start playing."

2.	Friends List Panel:
A clean card/list view showing friend placeholders (username + small avatar).
Each friend card should have an "Invite" button (rounded, minimal).
Option at the bottom: "Add Friend" (button or + icon).

3.	Lobby Section:
Two buttons: "Create Room" and "Join Room".
"Create Room" opens a modal popup asking for room name and settings (e.g., number of players).
"Join Room" opens a modal popup asking for Room Code.
Both modals should have Cancel and Confirm buttons.

4.	Modal Popups:
Styled with rounded corners, shadows, and centered.
Simple, minimal input fields with labels.

5.	JavaScript:
Handle modal open/close for Create Room and Join Room.
Handle click on "Invite" buttons (placeholder function).
Handle "Add Friend" click (placeholder function).

6.	Styling:
Use light background, soft shadows, rounded corners.
Font: clean and modern (system-ui or SF Pro style).
Buttons should have hover effects (slight shadow or scale).
Consistent with the Home page design.

7.	Footer (minimal): "© 2025 MelodyPlay"
