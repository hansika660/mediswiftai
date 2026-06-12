<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MediSwift – Healthcare Without Borders</title>
<style>
  :root {
    --primary: #0B6E4F;
    --primary-light: #E1F5EE;
    --primary-mid: #1D9E75;
    --accent: #E24B4A;
    --accent-light: #FCEBEB;
    --blue: #185FA5;
    --blue-light: #E6F1FB;
    --amber: #BA7517;
    --amber-light: #FAEEDA;
    --text: #1a1a1a;
    --text-muted: #6b7280;
    --border: #e5e7eb;
    --bg: #f8fafb;
    --white: #ffffff;
    --radius: 12px;
    --shadow: 0 2px 12px rgba(0,0,0,0.08);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Segoe UI', system-ui, sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }
 
  /* NAV */
  nav { background: var(--white); border-bottom: 1px solid var(--border); padding: 0 24px; display: flex; align-items: center; justify-content: space-between; height: 60px; position: sticky; top: 0; z-index: 100; }
  .nav-logo { font-size: 20px; font-weight: 700; color: var(--primary); letter-spacing: -0.5px; }
  .nav-logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 6px; }
  .nav-links button { background: none; border: none; padding: 8px 14px; border-radius: 8px; cursor: pointer; font-size: 14px; color: var(--text-muted); transition: all 0.15s; }
  .nav-links button:hover, .nav-links button.active { background: var(--primary-light); color: var(--primary); font-weight: 500; }
  .nav-right { display: flex; align-items: center; gap: 10px; }
  .badge-emergency { background: var(--accent); color: white; padding: 6px 14px; border-radius: 20px; font-size: 13px; font-weight: 600; border: none; cursor: pointer; animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{box-shadow:0 0 0 0 rgba(226,75,74,0.4)} 50%{box-shadow:0 0 0 8px rgba(226,75,74,0)} }
 
  /* PAGES */
  .page { display: none; padding: 24px; max-width: 960px; margin: 0 auto; }
  .page.active { display: block; }
 
  /* HERO */
  .hero { background: linear-gradient(135deg, var(--primary) 0%, #0d8f65 100%); color: white; border-radius: 16px; padding: 40px; margin-bottom: 24px; position: relative; overflow: hidden; }
  .hero::after { content: ''; position: absolute; right: -40px; top: -40px; width: 200px; height: 200px; border-radius: 50%; background: rgba(255,255,255,0.08); }
  .hero h1 { font-size: 32px; font-weight: 700; margin-bottom: 8px; }
  .hero p { font-size: 16px; opacity: 0.85; margin-bottom: 24px; max-width: 500px; }
  .hero-btns { display: flex; gap: 12px; flex-wrap: wrap; }
  .btn-white { background: white; color: var(--primary); border: none; padding: 12px 24px; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; transition: transform 0.15s; }
  .btn-white:hover { transform: translateY(-1px); }
  .btn-outline-white { background: transparent; color: white; border: 1.5px solid rgba(255,255,255,0.6); padding: 12px 24px; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.15s; }
  .btn-outline-white:hover { background: rgba(255,255,255,0.15); }
 
  /* STATS ROW */
  .stats-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 12px; margin-bottom: 24px; }
  .stat-card { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px; text-align: center; }
  .stat-num { font-size: 24px; font-weight: 700; color: var(--primary); }
  .stat-label { font-size: 12px; color: var(--text-muted); margin-top: 2px; }
 
  /* CARDS GRID */
  .cards-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; margin-bottom: 24px; }
  .card { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 20px; box-shadow: var(--shadow); }
  .card-icon { width: 44px; height: 44px; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 22px; margin-bottom: 12px; }
  .card-title { font-size: 15px; font-weight: 600; margin-bottom: 6px; }
  .card-desc { font-size: 13px; color: var(--text-muted); line-height: 1.5; }
  .card .btn-primary { margin-top: 14px; width: 100%; }
 
  /* BUTTONS */
  .btn-primary { background: var(--primary); color: white; border: none; padding: 10px 20px; border-radius: 8px; font-size: 14px; font-weight: 500; cursor: pointer; transition: background 0.15s; }
  .btn-primary:hover { background: #095c42; }
  .btn-secondary { background: var(--primary-light); color: var(--primary); border: none; padding: 10px 20px; border-radius: 8px; font-size: 14px; font-weight: 500; cursor: pointer; }
  .btn-danger { background: var(--accent); color: white; border: none; padding: 10px 20px; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; }
 
  /* SECTION HEADER */
  .section-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px; }
  .section-title { font-size: 17px; font-weight: 600; }
 
  /* SYMPTOM CHECKER */
  .symptom-container { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 24px; }
  .symptom-container h3 { font-size: 16px; font-weight: 600; margin-bottom: 6px; }
  .symptom-container p { font-size: 13px; color: var(--text-muted); margin-bottom: 16px; }
  .body-parts { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 16px; }
  .body-chip { padding: 6px 14px; border-radius: 20px; border: 1.5px solid var(--border); background: var(--white); font-size: 13px; cursor: pointer; transition: all 0.15s; }
  .body-chip.selected { background: var(--primary-light); border-color: var(--primary); color: var(--primary); font-weight: 500; }
  .symptom-input { width: 100%; padding: 12px 16px; border: 1.5px solid var(--border); border-radius: 8px; font-size: 14px; margin-bottom: 12px; outline: none; transition: border-color 0.15s; }
  .symptom-input:focus { border-color: var(--primary); }
  .triage-result { margin-top: 16px; padding: 16px; border-radius: 10px; display: none; }
  .triage-result.mild { background: var(--primary-light); border-left: 4px solid var(--primary-mid); }
  .triage-result.moderate { background: var(--amber-light); border-left: 4px solid var(--amber); }
  .triage-result.severe { background: var(--accent-light); border-left: 4px solid var(--accent); }
  .triage-label { font-size: 13px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 6px; }
  .triage-desc { font-size: 14px; line-height: 1.5; }
  .triage-actions { display: flex; gap: 8px; margin-top: 12px; flex-wrap: wrap; }
 
  /* CHAT */
  .chat-wrapper { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; display: flex; flex-direction: column; height: 520px; }
  .chat-header { padding: 14px 20px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 12px; }
  .doctor-avatar { width: 40px; height: 40px; border-radius: 50%; background: var(--primary-light); display: flex; align-items: center; justify-content: center; font-size: 18px; }
  .doctor-info .name { font-weight: 600; font-size: 14px; }
  .doctor-info .status { font-size: 12px; color: var(--text-muted); display: flex; align-items: center; gap: 4px; }
  .online-dot { width: 7px; height: 7px; border-radius: 50%; background: #22c55e; }
  .chat-messages { flex: 1; overflow-y: auto; padding: 16px; display: flex; flex-direction: column; gap: 12px; }
  .msg { max-width: 75%; }
  .msg.user { align-self: flex-end; }
  .msg.bot { align-self: flex-start; }
  .msg-bubble { padding: 10px 14px; border-radius: 14px; font-size: 14px; line-height: 1.5; }
  .msg.user .msg-bubble { background: var(--primary); color: white; border-bottom-right-radius: 4px; }
  .msg.bot .msg-bubble { background: var(--bg); border: 1px solid var(--border); color: var(--text); border-bottom-left-radius: 4px; }
  .msg-time { font-size: 11px; color: var(--text-muted); margin-top: 4px; text-align: right; }
  .msg.bot .msg-time { text-align: left; }
  .chat-input-row { padding: 12px 16px; border-top: 1px solid var(--border); display: flex; gap: 8px; align-items: center; }
  .chat-input { flex: 1; padding: 10px 14px; border: 1.5px solid var(--border); border-radius: 20px; font-size: 14px; outline: none; transition: border-color 0.15s; }
  .chat-input:focus { border-color: var(--primary); }
  .chat-send { width: 40px; height: 40px; border-radius: 50%; background: var(--primary); color: white; border: none; cursor: pointer; font-size: 18px; display: flex; align-items: center; justify-content: center; }
  .quick-replies { display: flex; flex-wrap: wrap; gap: 6px; padding: 8px 16px; }
  .qr-btn { padding: 5px 12px; border-radius: 14px; border: 1px solid var(--primary); color: var(--primary); background: var(--white); font-size: 12px; cursor: pointer; }
  .qr-btn:hover { background: var(--primary-light); }
 
  /* APPOINTMENTS */
  .appt-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  @media(max-width:640px){ .appt-grid { grid-template-columns: 1fr; } }
  .doctor-card { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px; display: flex; gap: 12px; align-items: flex-start; }
  .doc-avatar { width: 52px; height: 52px; border-radius: 50%; background: var(--blue-light); display: flex; align-items: center; justify-content: center; font-size: 24px; flex-shrink: 0; }
  .doc-name { font-weight: 600; font-size: 14px; }
  .doc-spec { font-size: 12px; color: var(--primary); font-weight: 500; }
  .doc-country { font-size: 12px; color: var(--text-muted); margin-top: 2px; }
  .doc-rating { font-size: 12px; color: var(--amber); margin-top: 4px; }
  .doc-fee { font-size: 13px; font-weight: 600; color: var(--text); margin-top: 4px; }
  .slots { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 10px; }
  .slot { padding: 4px 10px; border: 1px solid var(--primary); border-radius: 6px; font-size: 12px; color: var(--primary); cursor: pointer; }
  .slot:hover, .slot.selected { background: var(--primary); color: white; }
  .slot.booked { border-color: var(--border); color: var(--text-muted); pointer-events: none; text-decoration: line-through; }
 
  /* MEDICINE REMINDER */
  .med-form { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 20px; margin-bottom: 16px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 12px; }
  @media(max-width:480px){ .form-row { grid-template-columns: 1fr; } }
  .form-group { display: flex; flex-direction: column; gap: 4px; }
  .form-label { font-size: 12px; font-weight: 500; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.3px; }
  .form-input { padding: 10px 12px; border: 1.5px solid var(--border); border-radius: 8px; font-size: 14px; outline: none; transition: border-color 0.15s; }
  .form-input:focus { border-color: var(--primary); }
  .med-list { display: flex; flex-direction: column; gap: 10px; }
  .med-item { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px 16px; display: flex; align-items: center; gap: 12px; }
  .med-icon { width: 40px; height: 40px; border-radius: 8px; background: var(--blue-light); display: flex; align-items: center; justify-content: center; font-size: 20px; flex-shrink: 0; }
  .med-name { font-weight: 600; font-size: 14px; }
  .med-dose { font-size: 13px; color: var(--text-muted); }
  .med-time { font-size: 12px; font-weight: 500; color: var(--primary); background: var(--primary-light); padding: 3px 10px; border-radius: 12px; margin-left: auto; }
  .med-del { background: none; border: none; color: var(--text-muted); cursor: pointer; font-size: 18px; padding: 4px; }
  .med-del:hover { color: var(--accent); }
 
  /* EMERGENCY MODAL */
  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.5); z-index: 200; align-items: center; justify-content: center; }
  .modal-overlay.open { display: flex; }
  .modal { background: var(--white); border-radius: 16px; padding: 28px; max-width: 420px; width: calc(100% - 32px); }
  .modal h2 { font-size: 20px; font-weight: 700; color: var(--accent); margin-bottom: 8px; }
  .modal p { font-size: 14px; color: var(--text-muted); line-height: 1.6; margin-bottom: 16px; }
  .emergency-actions { display: flex; flex-direction: column; gap: 10px; }
  .emergency-actions button { padding: 13px; border-radius: 10px; font-size: 15px; font-weight: 600; cursor: pointer; border: none; }
  .ea-call { background: var(--accent); color: white; }
  .ea-chat { background: var(--primary); color: white; }
  .ea-cancel { background: var(--bg); color: var(--text-muted); }
 
  /* TOAST */
  .toast { position: fixed; bottom: 24px; right: 24px; background: var(--text); color: white; padding: 12px 20px; border-radius: 10px; font-size: 14px; z-index: 300; transform: translateY(80px); opacity: 0; transition: all 0.3s; }
  .toast.show { transform: translateY(0); opacity: 1; }
 
  /* TABS for doctors filter */
  .filter-tabs { display: flex; gap: 6px; margin-bottom: 16px; flex-wrap: wrap; }
  .ftab { padding: 6px 14px; border-radius: 20px; border: 1px solid var(--border); background: var(--white); font-size: 13px; cursor: pointer; }
  .ftab.active { background: var(--primary); color: white; border-color: var(--primary); }
 
  /* PROFILE */
  .profile-card { background: var(--white); border: 1px solid var(--border); border-radius: var(--radius); padding: 24px; max-width: 500px; }
  .profile-avatar { width: 72px; height: 72px; border-radius: 50%; background: var(--primary-light); display: flex; align-items: center; justify-content: center; font-size: 32px; margin-bottom: 16px; }
  .profile-name { font-size: 20px; font-weight: 700; }
  .profile-sub { font-size: 14px; color: var(--text-muted); margin-top: 2px; }
  .profile-row { display: flex; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid var(--border); font-size: 14px; }
  .profile-row:last-child { border-bottom: none; }
  .profile-key { color: var(--text-muted); }
  .profile-val { font-weight: 500; }
 
  .tag { display: inline-block; padding: 3px 10px; border-radius: 12px; font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.3px; }
  .tag-mild { background: var(--primary-light); color: var(--primary); }
  .tag-moderate { background: var(--amber-light); color: var(--amber); }
  .tag-severe { background: var(--accent-light); color: var(--accent); }
  .tag-global { background: var(--blue-light); color: var(--blue); }
</style>
</head>
<body>
 
<nav>
  <div class="nav-logo">Medi<span>Swift</span></div>
  <div class="nav-links">
    <button class="active" onclick="showPage('home',this)">Home</button>
    <button onclick="showPage('symptom',this)">Symptom Checker</button>
    <button onclick="showPage('consult',this)">Consult Doctor</button>
    <button onclick="showPage('appointments',this)">Appointments</button>
    <button onclick="showPage('medicines',this)">Medicines</button>
  </div>
  <div class="nav-right">
    <button class="badge-emergency" onclick="openEmergency()">🚨 Emergency</button>
  </div>
</nav>
 
<!-- HOME -->
<div id="page-home" class="page active">
  <div class="hero">
    <h1>Healthcare Without Borders 🌍</h1>
    <p>AI-powered telehealth connecting Indian patients with global doctors. Emergency triage, instant consultations, cross-border care — all in one platform.</p>
    <div class="hero-btns">
      <button class="btn-white" onclick="showPage('symptom', document.querySelector('.nav-links button:nth-child(2)'))">Check Symptoms</button>
      <button class="btn-outline-white" onclick="showPage('consult', document.querySelector('.nav-links button:nth-child(3)'))">Talk to a Doctor</button>
    </div>
  </div>
 
  <div class="stats-row">
    <div class="stat-card"><div class="stat-num">500+</div><div class="stat-label">Verified Doctors</div></div>
    <div class="stat-card"><div class="stat-num">24/7</div><div class="stat-label">Emergency Support</div></div>
    <div class="stat-card"><div class="stat-num">15+</div><div class="stat-label">Countries</div></div>
    <div class="stat-card"><div class="stat-num">4.8⭐</div><div class="stat-label">Patient Rating</div></div>
  </div>
 
  <div class="section-header">
    <div class="section-title">Key Features</div>
  </div>
  <div class="cards-grid">
    <div class="card">
      <div class="card-icon" style="background:var(--primary-light)">🩺</div>
      <div class="card-title">AI Symptom Checker</div>
      <div class="card-desc">Describe your symptoms and get instant AI-powered triage — Mild, Moderate, or Severe — so you know what to do next.</div>
      <button class="btn-primary" onclick="showPage('symptom', document.querySelector('.nav-links button:nth-child(2)'))">Start Assessment</button>
    </div>
    <div class="card">
      <div class="card-icon" style="background:var(--blue-light)">💬</div>
      <div class="card-title">Doctor Consultation Chat</div>
      <div class="card-desc">Chat with verified doctors from India and abroad. Intrastate, national, and international consultations available.</div>
      <button class="btn-primary" onclick="showPage('consult', document.querySelector('.nav-links button:nth-child(3)'))">Connect Now</button>
    </div>
    <div class="card">
      <div class="card-icon" style="background:var(--amber-light)">📅</div>
      <div class="card-title">Appointment Booking</div>
      <div class="card-desc">Book specialist appointments instantly. No travel needed — access rare and complex-case doctors from anywhere.</div>
      <button class="btn-primary" onclick="showPage('appointments', document.querySelector('.nav-links button:nth-child(4)'))">Book Appointment</button>
    </div>
    <div class="card">
      <div class="card-icon" style="background:#FEF3C7)">💊</div>
      <div class="card-title">Medicine Reminder</div>
      <div class="card-desc">Set smart reminders for your medications. Never miss a dose with timely notifications.</div>
      <button class="btn-primary" onclick="showPage('medicines', document.querySelector('.nav-links button:nth-child(5)'))">Set Reminders</button>
    </div>
  </div>
 
  <div class="card" style="background:var(--accent-light);border-color:#fca5a5;">
    <div style="display:flex;gap:16px;align-items:center;flex-wrap:wrap;">
      <div style="font-size:32px">🚨</div>
      <div style="flex:1">
        <div style="font-size:15px;font-weight:700;color:var(--accent);margin-bottom:4px">Emergency? Act Immediately.</div>
        <div style="font-size:13px;color:#7f1d1d;">MediSwift's AI triage ensures faster emergency response than traditional systems. Connect with the nearest available doctor now.</div>
      </div>
      <button class="btn-danger" onclick="openEmergency()">Get Help Now</button>
    </div>
  </div>
</div>
 
<!-- SYMPTOM CHECKER -->
<div id="page-symptom" class="page">
  <div class="section-header">
    <div class="section-title">AI Symptom Checker</div>
    <span class="tag tag-global">Powered by MediSwift AI</span>
  </div>
  <div class="symptom-container">
    <h3>Where do you feel the symptoms?</h3>
    <p>Select all affected areas, then describe your symptoms in detail.</p>
    <div class="body-parts">
      <div class="body-chip" onclick="toggleChip(this)">Head</div>
      <div class="body-chip" onclick="toggleChip(this)">Eyes</div>
      <div class="body-chip" onclick="toggleChip(this)">Throat</div>
      <div class="body-chip" onclick="toggleChip(this)">Chest</div>
      <div class="body-chip" onclick="toggleChip(this)">Heart</div>
      <div class="body-chip" onclick="toggleChip(this)">Stomach</div>
      <div class="body-chip" onclick="toggleChip(this)">Back</div>
      <div class="body-chip" onclick="toggleChip(this)">Joints</div>
      <div class="body-chip" onclick="toggleChip(this)">Skin</div>
      <div class="body-chip" onclick="toggleChip(this)">Whole Body</div>
    </div>
 
    <div class="form-group" style="margin-bottom:12px">
      <label class="form-label">Describe your symptoms</label>
      <textarea class="symptom-input" id="symptomText" rows="3" placeholder="e.g. I have a severe headache, high fever since 2 days, and feel dizzy..."></textarea>
    </div>
 
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">Duration</label>
        <select class="form-input" id="duration">
          <option>Less than a day</option>
          <option>1–3 days</option>
          <option>4–7 days</option>
          <option>More than a week</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Pain level (1–10)</label>
        <input type="range" min="1" max="10" value="5" id="painLevel" class="form-input" style="padding:4px 0">
        <span id="painOut" style="font-size:13px;color:var(--text-muted)">Level: 5</span>
      </div>
    </div>
 
    <button class="btn-primary" style="width:100%;padding:13px;font-size:15px" onclick="analyzeSymptoms()">🔍 Analyze Symptoms</button>
 
    <div id="triageResult" class="triage-result">
      <div class="triage-label" id="triageLabel"></div>
      <div class="triage-desc" id="triageDesc"></div>
      <div class="triage-actions" id="triageActions"></div>
    </div>
  </div>
</div>
 
<!-- CONSULT DOCTOR -->
<div id="page-consult" class="page">
  <div class="section-header">
    <div class="section-title">Doctor Consultation Chat</div>
    <span class="tag tag-global">🌍 Global Network</span>
  </div>
  <div class="chat-wrapper">
    <div class="chat-header">
      <div class="doctor-avatar">👨‍⚕️</div>
      <div class="doctor-info">
        <div class="name">Dr. Arjun Mehta — General Physician</div>
        <div class="status"><span class="online-dot"></span> Online · India</div>
      </div>
      <button class="btn-secondary" style="margin-left:auto;font-size:12px;padding:6px 12px" onclick="showPage('appointments', document.querySelector('.nav-links button:nth-child(4)'))">Change Doctor</button>
    </div>
    <div class="quick-replies" id="quickReplies">
      <button class="qr-btn" onclick="sendQuick('I have a fever and headache')">Fever & Headache</button>
      <button class="qr-btn" onclick="sendQuick('Chest pain since morning')">Chest Pain</button>
      <button class="qr-btn" onclick="sendQuick('Need prescription renewal')">Prescription</button>
      <button class="qr-btn" onclick="sendQuick('I need a second opinion')">Second Opinion</button>
    </div>
    <div class="chat-messages" id="chatMessages">
      <div class="msg bot">
        <div class="msg-bubble">Namaste! I'm Dr. Arjun Mehta. How can I help you today? Please describe your symptoms and I'll guide you appropriately. 🙏</div>
        <div class="msg-time">Just now</div>
      </div>
    </div>
    <div class="chat-input-row">
      <input class="chat-input" id="chatInput" type="text" placeholder="Type your message..." onkeydown="if(event.key==='Enter')sendMessage()">
      <button class="chat-send" onclick="sendMessage()">➤</button>
    </div>
  </div>
</div>
 
<!-- APPOINTMENTS -->
<div id="page-appointments" class="page">
  <div class="section-header">
    <div class="section-title">Book an Appointment</div>
  </div>
  <div class="filter-tabs">
    <button class="ftab active" onclick="filterDoctors('all',this)">All</button>
    <button class="ftab" onclick="filterDoctors('general',this)">General</button>
    <button class="ftab" onclick="filterDoctors('cardio',this)">Cardiology</button>
    <button class="ftab" onclick="filterDoctors('neuro',this)">Neurology</button>
    <button class="ftab" onclick="filterDoctors('international',this)">🌍 International</button>
  </div>
  <div class="appt-grid" id="doctorGrid"></div>
</div>
 
<!-- MEDICINES -->
<div id="page-medicines" class="page">
  <div class="section-header">
    <div class="section-title">Medicine Reminders</div>
  </div>
  <div class="med-form">
    <h3 style="font-size:15px;font-weight:600;margin-bottom:16px">Add New Reminder</h3>
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">Medicine Name</label>
        <input class="form-input" id="medName" placeholder="e.g. Paracetamol 500mg">
      </div>
      <div class="form-group">
        <label class="form-label">Dosage</label>
        <input class="form-input" id="medDose" placeholder="e.g. 1 tablet">
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label class="form-label">Time</label>
        <input class="form-input" id="medTime" type="time" value="08:00">
      </div>
      <div class="form-group">
        <label class="form-label">Frequency</label>
        <select class="form-input" id="medFreq">
          <option>Once daily</option>
          <option>Twice daily</option>
          <option>Three times daily</option>
          <option>Every 8 hours</option>
          <option>As needed</option>
        </select>
      </div>
    </div>
    <button class="btn-primary" onclick="addMedicine()">+ Add Reminder</button>
  </div>
  <div class="section-header">
    <div class="section-title">Today's Schedule</div>
    <span id="medCount" style="font-size:13px;color:var(--text-muted)">0 medicines</span>
  </div>
  <div class="med-list" id="medList">
    <div style="text-align:center;padding:32px;color:var(--text-muted);font-size:14px;">No reminders added yet. Add your first medicine above.</div>
  </div>
</div>
 
<!-- EMERGENCY MODAL -->
<div class="modal-overlay" id="emergencyModal">
  <div class="modal">
    <h2>🚨 Emergency Alert</h2>
    <p>MediSwift will immediately connect you with the nearest available emergency doctor. For life-threatening emergencies, always call 108 (ambulance) first.</p>
    <div class="emergency-actions">
      <button class="ea-call" onclick="callEmergency()">📞 Call 108 — Ambulance Now</button>
      <button class="ea-chat" onclick="closeEmergency();showPage('consult', document.querySelector('.nav-links button:nth-child(3)'))">💬 Connect Emergency Doctor</button>
      <button class="ea-cancel" onclick="closeEmergency()">Cancel</button>
    </div>
  </div>
</div>
 
<div class="toast" id="toast"></div>
 
<script>
const DOCTORS = [
  { name:'Dr. Arjun Mehta', spec:'General Physician', country:'🇮🇳 India', rating:'4.9 ★ (312 reviews)', fee:'₹299', emoji:'👨‍⚕️', cat:'general', slots:['9:00 AM','10:30 AM','2:00 PM','4:00 PM'] },
  { name:'Dr. Priya Sharma', spec:'Cardiologist', country:'🇮🇳 India', rating:'4.8 ★ (210 reviews)', fee:'₹599', emoji:'👩‍⚕️', cat:'cardio', slots:['11:00 AM','3:30 PM'] },
  { name:'Dr. Ravi Nair', spec:'Neurologist', country:'🇮🇳 India', rating:'4.7 ★ (185 reviews)', fee:'₹799', emoji:'👨‍⚕️', cat:'neuro', slots:['10:00 AM','1:00 PM','5:00 PM'] },
  { name:'Dr. Sarah Johnson', spec:'Internal Medicine', country:'🇺🇸 USA', rating:'4.9 ★ (408 reviews)', fee:'₹1499', emoji:'👩‍⚕️', cat:'international', slots:['6:00 PM','8:00 PM','9:30 PM'] },
  { name:'Dr. Kenji Tanaka', spec:'Oncologist', country:'🇯🇵 Japan', rating:'5.0 ★ (92 reviews)', fee:'₹1999', emoji:'👨‍⚕️', cat:'international', slots:['7:00 PM','9:00 PM'] },
  { name:'Dr. Ananya Roy', spec:'General Physician', country:'🇮🇳 India', rating:'4.6 ★ (144 reviews)', fee:'₹249', emoji:'👩‍⚕️', cat:'general', slots:['8:30 AM','12:00 PM','3:00 PM','6:00 PM'] },
];
 
function showPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-links button').forEach(b => b.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  if(btn) btn.classList.add('active');
}
 
function toggleChip(el) { el.classList.toggle('selected'); }
 
document.getElementById('painLevel').addEventListener('input', function(){
  document.getElementById('painOut').textContent = 'Level: ' + this.value;
});
 
function analyzeSymptoms() {
  const text = document.getElementById('symptomText').value.toLowerCase();
  const pain = parseInt(document.getElementById('painLevel').value);
  const duration = document.getElementById('duration').value;
  const selected = [...document.querySelectorAll('.body-chip.selected')].map(c=>c.textContent);
 
  let level = 'mild';
  let label = '🟢 Mild — Self-Care Advised';
  let desc = 'Your symptoms appear mild. Rest, stay hydrated, and monitor for any changes. Over-the-counter medication may help.';
  let actions = `<button class="btn-secondary" style="font-size:13px">💊 Home Remedies</button><button class="btn-primary" style="font-size:13px" onclick="showPage('consult',document.querySelector('.nav-links button:nth-child(3)'))">Chat with Doctor</button>`;
 
  const severeWords = ['cardiac','chest pain','breathing','difficulty','stroke','seizure','unconscious','no pulse','crush','fracture','heavy bleeding','heart attack'];
  const modWords = ['high fever','vomiting','dizziness','confusion','ear pain','moderate','persistent','joint'];
 
  if(pain >= 8 || severeWords.some(w=>text.includes(w)) || selected.includes('Heart') || selected.includes('Chest')) {
    level = 'severe';
    label = '🔴 Severe — Seek Immediate Care';
    desc = 'Your symptoms indicate a potentially serious condition. Please consult a doctor immediately or call emergency services.';
    actions = `<button class="btn-danger" onclick="openEmergency()">🚨 Emergency Help</button><button class="btn-primary" onclick="showPage('consult',document.querySelector('.nav-links button:nth-child(3)'))">Consult Doctor Now</button>`;
  } else if(pain >= 5 || modWords.some(w=>text.includes(w)) || duration.includes('4–7') || duration.includes('week')) {
    level = 'moderate';
    label = '🟡 Moderate — Doctor Consultation Advised';
    desc = 'Your symptoms need medical attention. We recommend consulting a doctor within the next few hours.';
    actions = `<button class="btn-primary" onclick="showPage('consult',document.querySelector('.nav-links button:nth-child(3)'))">Consult Doctor</button><button class="btn-secondary" onclick="showPage('appointments',document.querySelector('.nav-links button:nth-child(4)'))">Book Appointment</button>`;
  }
 
  const result = document.getElementById('triageResult');
  result.className = 'triage-result ' + level;
  result.style.display = 'block';
  document.getElementById('triageLabel').textContent = label;
  document.getElementById('triageDesc').textContent = desc;
  document.getElementById('triageActions').innerHTML = actions;
  result.scrollIntoView({behavior:'smooth', block:'nearest'});
}
 
// CHAT
const botReplies = {
  default: ["I understand your concern. Can you tell me more about when it started?", "Have you taken any medication for this?", "How would you rate the pain on a scale of 1 to 10?", "I recommend booking a full consultation. Shall I connect you with a specialist?", "Based on what you've shared, this may need in-person examination. Please visit a nearby clinic if symptoms worsen."],
  fever: ["Fever can be caused by many things. Do you have any other symptoms like cough or body ache?", "Please stay hydrated and take rest. Paracetamol 500mg can help if the fever is mild. If it exceeds 103°F, visit a doctor."],
  chest: ["Chest pain needs immediate attention. Is it sharp or dull? Does it radiate to your arm or jaw?", "Please call emergency services if the chest pain is severe. I'm alerting our emergency team."],
  headache: ["Headaches can be tension-related or migraines. Are you experiencing light sensitivity or nausea as well?"],
};
 
let chatHistory = [];
function getTime() { return new Date().toLocaleTimeString([],{hour:'2-digit',minute:'2-digit'}); }
 
function appendMsg(text, role) {
  const msgs = document.getElementById('chatMessages');
  const div = document.createElement('div');
  div.className = 'msg ' + role;
  div.innerHTML = `<div class="msg-bubble">${text}</div><div class="msg-time">${getTime()}</div>`;
  msgs.appendChild(div);
  msgs.scrollTop = msgs.scrollHeight;
}
 
function getBotReply(text) {
  const t = text.toLowerCase();
  if(t.includes('chest') || t.includes('heart')) return botReplies.chest[Math.floor(Math.random()*botReplies.chest.length)];
  if(t.includes('fever') || t.includes('temperature')) return botReplies.fever[Math.floor(Math.random()*botReplies.fever.length)];
  if(t.includes('headache') || t.includes('head')) return botReplies.headache[0];
  return botReplies.default[Math.floor(Math.random()*botReplies.default.length)];
}
 
function sendMessage() {
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if(!text) return;
  appendMsg(text, 'user');
  input.value = '';
  document.getElementById('quickReplies').style.display = 'none';
  setTimeout(()=>{ appendMsg(getBotReply(text),'bot'); }, 900);
}
 
function sendQuick(text) {
  document.getElementById('chatInput').value = text;
  sendMessage();
}
 
// APPOINTMENTS
function renderDoctors(filter='all') {
  const grid = document.getElementById('doctorGrid');
  const docs = filter === 'all' ? DOCTORS : DOCTORS.filter(d=>d.cat===filter);
  grid.innerHTML = docs.map((d,i) => `
    <div class="doctor-card" style="flex-direction:column">
      <div style="display:flex;gap:12px;width:100%">
        <div class="doc-avatar">${d.emoji}</div>
        <div style="flex:1">
          <div class="doc-name">${d.name}</div>
          <div class="doc-spec">${d.spec}</div>
          <div class="doc-country">${d.country}</div>
          <div class="doc-rating">${d.rating}</div>
          <div class="doc-fee">Consultation: ${d.fee}</div>
        </div>
      </div>
      <div style="width:100%;margin-top:10px">
        <div style="font-size:12px;color:var(--text-muted);margin-bottom:6px">Available slots today:</div>
        <div class="slots">
          ${d.slots.map((s,j)=>`<div class="slot" onclick="bookSlot(this,'${d.name}','${s}')">${s}</div>`).join('')}
        </div>
      </div>
    </div>`).join('');
}
 
function filterDoctors(cat, btn) {
  document.querySelectorAll('.ftab').forEach(t=>t.classList.remove('active'));
  btn.classList.add('active');
  renderDoctors(cat);
}
 
function bookSlot(el, name, time) {
  el.classList.add('selected');
  setTimeout(()=>{
    el.classList.remove('selected');
    el.classList.add('booked');
    el.textContent = '✓ Booked';
    showToast(`Appointment booked with ${name} at ${time}`);
  }, 600);
}
 
renderDoctors();
 
// MEDICINES
let medicines = [];
const medIcons = ['💊','💉','🩺','🧴','🌡️'];
 
function addMedicine() {
  const name = document.getElementById('medName').value.trim();
  const dose = document.getElementById('medDose').value.trim();
  const time = document.getElementById('medTime').value;
  const freq = document.getElementById('medFreq').value;
  if(!name) { showToast('Please enter medicine name'); return; }
  const med = { id: Date.now(), name, dose: dose||'1 tablet', time, freq, icon: medIcons[medicines.length % medIcons.length] };
  medicines.push(med);
  document.getElementById('medName').value = '';
  document.getElementById('medDose').value = '';
  renderMedicines();
  showToast('Reminder added for ' + name);
}
 
function deleteMed(id) {
  medicines = medicines.filter(m=>m.id!==id);
  renderMedicines();
}
 
function renderMedicines() {
  const list = document.getElementById('medList');
  document.getElementById('medCount').textContent = medicines.length + ' medicine' + (medicines.length!==1?'s':'');
  if(!medicines.length) { list.innerHTML = '<div style="text-align:center;padding:32px;color:var(--text-muted);font-size:14px;">No reminders added yet. Add your first medicine above.</div>'; return; }
  list.innerHTML = medicines.map(m=>`
    <div class="med-item">
      <div class="med-icon">${m.icon}</div>
      <div style="flex:1">
        <div class="med-name">${m.name}</div>
        <div class="med-dose">${m.dose} · ${m.freq}</div>
      </div>
      <div class="med-time">${m.time}</div>
      <button class="med-del" onclick="deleteMed(${m.id})">✕</button>
    </div>`).join('');
}
 
// EMERGENCY
function openEmergency() { document.getElementById('emergencyModal').classList.add('open'); }
function closeEmergency() { document.getElementById('emergencyModal').classList.remove('open'); }
function callEmergency() { showToast('Calling 108 — Emergency Services'); closeEmergency(); }
 
// TOAST
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 3000);
}
 
document.getElementById('emergencyModal').addEventListener('click', function(e){ if(e.target===this) closeEmergency(); });
</script>
</body>
</html>
