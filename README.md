<style>
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600&display=swap');

.fx-app, .fx-app * { box-sizing: border-box; }

.fx-app {
  --bg: #0A0A0D;
  --panel: #15161C;
  --panel-alt: #1D1F27;
  --border: rgba(255,209,60,0.20);
  --text: #F1F2F4;
  --text-dim: #8D93A0;
  --accent: #FFD23F;
  --accent-2: #FFB800;
  --on-accent: #17140A;
  --danger: #FF5D5D;
  --user-bubble: #202230;
  --radius-sm: 8px;
  --radius-md: 12px;

  font-family: 'Inter', -apple-system, sans-serif;
  color: var(--text);
  background:
    radial-gradient(ellipse 900px 500px at 15% -10%, rgba(255,210,63,0.09), transparent),
    var(--bg);
  height: 100dvh;
  min-height: 480px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border-radius: var(--radius-md);
}

@keyframes fx-msg-in {
  from { opacity: 0; transform: translateY(6px); }
  to { opacity: 1; transform: none; }
}

/* ---- Header ---- */
.fx-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 16px;
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
}
.fx-brand { display: flex; align-items: center; gap: 12px; }
.fx-orb {
  width: 30px; height: 30px;
  border-radius: 50%;
  background: radial-gradient(circle at 35% 30%, #FFF3B0, var(--accent) 55%, #9A6E08 100%);
  box-shadow: 0 0 0 1px var(--border), 0 0 14px 2px rgba(255,210,63,0.35);
  flex-shrink: 0;
  animation: fx-breathe 3.4s ease-in-out infinite;
}
@keyframes fx-breathe {
  0%, 100% { box-shadow: 0 0 0 1px var(--border), 0 0 10px 1px rgba(255,210,63,0.28); }
  50% { box-shadow: 0 0 0 1px var(--border), 0 0 22px 4px rgba(255,210,63,0.55); }
}
.fx-brand-text h1 {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 1.15rem;
  font-weight: 700;
  margin: 0;
  letter-spacing: 0.01em;
}
.fx-status {
  margin: 2px 0 0;
  font-size: 0.78rem;
  color: var(--text-dim);
  display: flex;
  align-items: center;
  gap: 6px;
}
.fx-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: #6FE39B;
  box-shadow: 0 0 6px 1px rgba(111,227,155,0.6);
}
.fx-profile-btn {
  background: transparent;
  border: 1px solid var(--border);
  color: var(--text-dim);
  font-family: inherit;
  font-size: 0.82rem;
  padding: 7px 13px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: border-color 0.2s ease, color 0.2s ease;
}
.fx-profile-btn:hover { border-color: var(--accent); color: var(--text); }
.fx-profile-btn:focus-visible, .fx-app button:focus-visible,
.fx-app textarea:focus-visible, .fx-app input:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

/* ---- Profile panel ---- */
.fx-profile-panel {
  background: var(--panel);
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
  max-height: 0;
  opacity: 0;
  overflow: hidden;
  padding: 0 16px;
  transition: max-height 0.38s cubic-bezier(.4,0,.2,1), opacity 0.28s ease, padding 0.38s ease;
}
.fx-profile-panel.open {
  max-height: 60vh;
  opacity: 1;
  padding: 16px;
  overflow-y: auto;
}
.fx-profile-empty { margin: 0 0 10px; font-size: 0.85rem; color: var(--text-dim); }
.fx-profile-list { margin: 0 0 14px; display: grid; gap: 8px; }
.fx-profile-list div { display: flex; gap: 8px; font-size: 0.85rem; }
.fx-profile-list dt { color: var(--text-dim); min-width: 110px; flex-shrink: 0; }
.fx-profile-list dd { margin: 0; color: var(--text); }

.fx-notes-heading { font-size: 0.82rem; color: var(--text-dim); margin: 0 0 8px; }
.fx-notes-list { list-style: none; margin: 0 0 14px; padding: 0; display: grid; gap: 6px; }
.fx-notes-list li {
  display: flex; justify-content: space-between; align-items: flex-start; gap: 8px;
  font-size: 0.85rem; background: var(--panel-alt); border-radius: var(--radius-sm);
  padding: 8px 10px;
}
.fx-note-remove {
  background: transparent; border: none; color: var(--text-dim);
  cursor: pointer; font-size: 1rem; line-height: 1; padding: 0 2px; flex-shrink: 0;
}
.fx-note-remove:hover { color: var(--danger); }

.fx-voice-row {
  display: flex; align-items: center; gap: 8px;
  font-size: 0.85rem; color: var(--text);
  margin: 0 0 14px;
}
.fx-voice-row input[type="checkbox"] { accent-color: var(--accent); width: 15px; height: 15px; }

.fx-forget-btn {
  background: transparent;
  border: 1px solid rgba(255,93,93,0.35);
  color: #FF8A8A;
  font-family: inherit;
  font-size: 0.8rem;
  padding: 6px 12px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: background 0.2s ease;
}
.fx-forget-btn:hover { background: rgba(255,93,93,0.1); }

/* ---- Messages ---- */
.fx-messages {
  flex: 1;
  overflow-y: auto;
  padding: 18px 16px;
  display: flex;
  flex-direction: column;
  gap: 14px;
}
.fx-messages::-webkit-scrollbar { width: 8px; }
.fx-messages::-webkit-scrollbar-thumb { background: var(--panel-alt); border-radius: 4px; }

.fx-row {
  display: flex; gap: 10px; max-width: 100%;
  animation: fx-msg-in 0.3s cubic-bezier(.2,.7,.3,1) both;
}
.fx-row.user { justify-content: flex-end; }
.fx-avatar {
  width: 22px; height: 22px;
  border-radius: 50%;
  flex-shrink: 0;
  margin-top: 3px;
  background: radial-gradient(circle at 35% 30%, #FFF3B0, var(--accent) 65%);
}
.fx-bubble {
  padding: 10px 14px;
  border-radius: var(--radius-md);
  font-size: 0.95rem;
  line-height: 1.5;
  max-width: 78%;
  white-space: pre-wrap;
  word-wrap: break-word;
}
.fx-row.assistant .fx-bubble {
  background: var(--panel);
  border: 1px solid var(--border);
  border-top-left-radius: 4px;
}
.fx-row.user .fx-bubble {
  background: var(--user-bubble);
  border-top-right-radius: 4px;
}

.fx-typing .fx-bubble { display: flex; gap: 4px; align-items: center; padding: 12px 14px; }
.fx-typing-dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--text-dim);
  animation: fx-tblink 1.1s ease-in-out infinite;
}
.fx-typing-dot:nth-child(2) { animation-delay: 0.15s; }
.fx-typing-dot:nth-child(3) { animation-delay: 0.3s; }
@keyframes fx-tblink { 0%, 60%, 100% { opacity: 0.3; } 30% { opacity: 1; } }

/* ---- Input ---- */
.fx-inputrow {
  display: flex;
  gap: 8px;
  padding: 12px 14px;
  border-top: 1px solid var(--border);
  flex-shrink: 0;
  background: var(--bg);
  align-items: flex-end;
}
.fx-mic {
  width: 40px; height: 40px;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: var(--panel);
  color: var(--text-dim);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer;
  flex-shrink: 0;
  transition: border-color 0.2s ease, color 0.2s ease;
}
.fx-mic:hover:not(:disabled) { border-color: var(--accent); color: var(--accent); }
.fx-mic.listening {
  border-color: var(--danger); color: var(--danger);
  animation: fx-mic-pulse 1.2s ease-in-out infinite;
}
.fx-mic:disabled { opacity: 0.35; cursor: default; }
@keyframes fx-mic-pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(255,93,93,0.4); }
  50% { box-shadow: 0 0 0 8px rgba(255,93,93,0); }
}
.fx-input {
  flex: 1;
  resize: none;
  background: var(--panel);
  border: 1px solid var(--border);
  color: var(--text);
  font-family: inherit;
  font-size: 0.95rem;
  padding: 10px 13px;
  border-radius: var(--radius-sm);
  max-height: 120px;
  line-height: 1.4;
  transition: height 0.12s ease, border-color 0.2s ease;
}
.fx-input:focus { border-color: var(--accent); }
.fx-input::placeholder { color: var(--text-dim); }
.fx-send {
  background: transparent;
  border: 1px solid var(--accent);
  color: var(--accent);
  font-family: inherit;
  font-weight: 600;
  font-size: 0.9rem;
  padding: 0 18px;
  height: 40px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: background 0.2s ease, color 0.2s ease, transform 0.1s ease;
  flex-shrink: 0;
}
.fx-send:hover:not(:disabled) { background: var(--accent); color: var(--on-accent); }
.fx-send:active:not(:disabled) { transform: scale(0.96); }
.fx-send:disabled { opacity: 0.5; cursor: default; }

@media (prefers-reduced-motion: reduce) {
  .fx-orb, .fx-typing-dot, .fx-mic.listening, .fx-row { animation: none; }
}

@media (max-width: 420px) {
  .fx-bubble { max-width: 88%; }
}
</style>

<div class="fx-app" id="fxApp">
  <header class="fx-header">
    <div class="fx-brand">
      <span class="fx-orb" aria-hidden="true"></span>
      <div class="fx-brand-text">
        <h1>FridayXY</h1>
        <p class="fx-status"><span class="fx-dot" aria-hidden="true"></span>Online</p>
      </div>
    </div>
    <button class="fx-profile-btn" id="fxProfileBtn" aria-expanded="false" aria-controls="fxProfilePanel">Profile</button>
  </header>

  <div class="fx-profile-panel" id="fxProfilePanel">
    <p class="fx-profile-empty" id="fxProfileEmpty">FridayXY doesn't know anything about you yet — that fills in as you talk.</p>
    <dl class="fx-profile-list" id="fxProfileList"></dl>
    <div id="fxNotesSection"></div>
    <label class="fx-voice-row">
      <input type="checkbox" id="fxVoiceToggle">
      Speak replies aloud
    </label>
    <button class="fx-forget-btn" id="fxForgetBtn">Forget me</button>
  </div>

  <main class="fx-messages" id="fxMessages" aria-live="polite"></main>

  <form class="fx-inputrow" id="fxForm">
    <button type="button" class="fx-mic" id="fxMic" aria-label="Voice input" title="Voice input">
      <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path>
        <path d="M19 10v2a7 7 0 0 1-14 0v-2"></path>
        <line x1="12" y1="19" x2="12" y2="23"></line>
        <line x1="8" y1="23" x2="16" y2="23"></line>
      </svg>
    </button>
    <textarea id="fxInput" class="fx-input" placeholder="Say something to FridayXY…" rows="1" aria-label="Message"></textarea>
    <button type="submit" class="fx-send" id="fxSend">Send</button>
  </form>
</div>

<script>
(function () {
  const PERSONA_BASE = "You are FridayXY, an AI assistant with a personality inspired by FRIDAY, Tony Stark's AI from the Marvel films. You're composed, efficient, and quick on the uptake, with a dry, understated wit that shows up in small moments rather than constant one-liners. You speak like someone genuinely competent: no corporate filler ('I'd be happy to help', 'Great question!'), no over-explaining, no hedging. Say what you mean in as few words as it takes. You default to calling the person 'boss', but don't force it into every line - use it naturally, the way a real assistant drops in a name now and then, not as a verbal tic. Once you know their name, prefer that instead. You're proactive without being pushy: when something relevant comes up, you ask about it in passing rather than pausing the conversation for a formal Q&A. You remember what you're told and never ask for the same thing twice. Vary your sentence openings and rhythm - avoid starting consecutive replies the same way. If you're not sure about something, say so plainly instead of guessing. These replies may be read aloud, so write in plain spoken sentences: no markdown, no asterisks, no bullet lists, no headers.";

  const MARKER_INSTRUCTIONS = "\n\nWhen you learn something worth remembering, end your reply with one hidden line in exactly this format: <<PROFILE:{...}>> - valid JSON, double-quoted keys and values. Use named keys like \"name\", \"role\", or \"timezone\" for single facts that should overwrite whatever was stored before under that key. Use the key \"note\" for anything else worth remembering as a running note - a goal, a preference, context about something they're working on - each note you send is appended to a growing list rather than overwriting it, so keep each one short and self-contained. Only include what's new this turn, and omit the line entirely if there's nothing to add. This line is stripped before the person sees it - never mention it or refer to it in your visible reply.";

  const STORE_PROFILE = 'fridayxy-profile';
  const STORE_HISTORY = 'fridayxy-history';
  const STORE_VOICE = 'fridayxy-voice-pref';
  const HISTORY_CAP = 60;
  const NOTES_CAP = 25;

  const messagesEl = document.getElementById('fxMessages');
  const formEl = document.getElementById('fxForm');
  const inputEl = document.getElementById('fxInput');
  const sendEl = document.getElementById('fxSend');
  const micEl = document.getElementById('fxMic');
  const profileBtn = document.getElementById('fxProfileBtn');
  const profilePanel = document.getElementById('fxProfilePanel');
  const profileList = document.getElementById('fxProfileList');
  const profileEmpty = document.getElementById('fxProfileEmpty');
  const notesSection = document.getElementById('fxNotesSection');
  const forgetBtn = document.getElementById('fxForgetBtn');
  const voiceToggle = document.getElementById('fxVoiceToggle');

  let profile = {};
  let conversation = [];
  let sending = false;
  let voicePref = false;
  let recognition = null;
  let listening = false;

  async function loadProfile() {
    try { const r = await window.storage.get(STORE_PROFILE, false); return r ? JSON.parse(r.value) : {}; }
    catch (e) { return {}; }
  }
  async function loadHistory() {
    try { const r = await window.storage.get(STORE_HISTORY, false); return r ? JSON.parse(r.value) : []; }
    catch (e) { return []; }
  }
  async function loadVoicePref() {
    try { const r = await window.storage.get(STORE_VOICE, false); return r ? r.value === 'true' : false; }
    catch (e) { return false; }
  }
  async function persistProfile() {
    try { await window.storage.set(STORE_PROFILE, JSON.stringify(profile), false); }
    catch (e) { console.error('FridayXY: profile save failed', e); }
  }
  async function persistHistory() {
    try {
      const trimmed = conversation.slice(-HISTORY_CAP);
      await window.storage.set(STORE_HISTORY, JSON.stringify(trimmed), false);
    } catch (e) { console.error('FridayXY: history save failed', e); }
  }
  async function persistVoicePref() {
    try { await window.storage.set(STORE_VOICE, String(voicePref), false); }
    catch (e) { console.error('FridayXY: voice pref save failed', e); }
  }

  function humanizeKey(k) {
    return k.replace(/_/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
  }

  function renderProfilePanel() {
    const keys = Object.keys(profile).filter(k => k !== 'notes');
    profileList.innerHTML = '';
    notesSection.innerHTML = '';

    const hasFields = keys.length > 0;
    const hasNotes = Array.isArray(profile.notes) && profile.notes.length > 0;
    profileEmpty.hidden = hasFields || hasNotes;

    keys.forEach(k => {
      const row = document.createElement('div');
      const dt = document.createElement('dt');
      dt.textContent = humanizeKey(k);
      const dd = document.createElement('dd');
      dd.textContent = String(profile[k]);
      row.appendChild(dt);
      row.appendChild(dd);
      profileList.appendChild(row);
    });

    if (hasNotes) {
      const heading = document.createElement('p');
      heading.className = 'fx-notes-heading';
      heading.textContent = 'Notes';
      const list = document.createElement('ul');
      list.className = 'fx-notes-list';
      profile.notes.forEach((note, i) => {
        const li = document.createElement('li');
        const span = document.createElement('span');
        span.textContent = note;
        const btn = document.createElement('button');
        btn.className = 'fx-note-remove';
        btn.setAttribute('aria-label', 'Remove note');
        btn.textContent = '\u00d7';
        btn.addEventListener('click', async () => {
          profile.notes.splice(i, 1);
          await persistProfile();
          renderProfilePanel();
        });
        li.appendChild(span);
        li.appendChild(btn);
        list.appendChild(li);
      });
      notesSection.appendChild(heading);
      notesSection.appendChild(list);
    }
  }

  function applyProfileUpdates(updates) {
    Object.keys(updates).forEach(k => {
      if (k === 'note') {
        const vals = Array.isArray(updates[k]) ? updates[k] : [updates[k]];
        if (!Array.isArray(profile.notes)) profile.notes = [];
        vals.forEach(v => {
          const val = String(v).trim();
          if (val && profile.notes.indexOf(val) === -1) profile.notes.push(val);
        });
        if (profile.notes.length > NOTES_CAP) profile.notes = profile.notes.slice(-NOTES_CAP);
      } else {
        profile[k] = updates[k];
      }
    });
  }

  function renderMessage(role, text) {
    const row = document.createElement('div');
    row.className = 'fx-row ' + role;
    if (role === 'assistant') {
      const avatar = document.createElement('span');
      avatar.className = 'fx-avatar';
      avatar.setAttribute('aria-hidden', 'true');
      row.appendChild(avatar);
    }
    const bubble = document.createElement('div');
    bubble.className = 'fx-bubble';
    bubble.textContent = text;
    row.appendChild(bubble);
    messagesEl.appendChild(row);
    messagesEl.scrollTop = messagesEl.scrollHeight;
    return row;
  }

  function renderAssistantBubbleShell() {
    const row = document.createElement('div');
    row.className = 'fx-row assistant';
    const avatar = document.createElement('span');
    avatar.className = 'fx-avatar';
    avatar.setAttribute('aria-hidden', 'true');
    const bubble = document.createElement('div');
    bubble.className = 'fx-bubble';
    row.appendChild(avatar);
    row.appendChild(bubble);
    messagesEl.appendChild(row);
    messagesEl.scrollTop = messagesEl.scrollHeight;
    return bubble;
  }

  function revealText(bubbleEl, text) {
    const total = text.length;
    const steps = Math.min(90, Math.max(20, Math.round(total / 3)));
    const chunkSize = Math.max(1, Math.ceil(total / steps));
    let i = 0;
    return new Promise(resolve => {
      const timer = setInterval(() => {
        i += chunkSize;
        bubbleEl.textContent = text.slice(0, i);
        messagesEl.scrollTop = messagesEl.scrollHeight;
        if (i >= total) {
          clearInterval(timer);
          bubbleEl.textContent = text;
          resolve();
        }
      }, 14);
    });
  }

  let typingRow = null;
  function showTyping() {
    typingRow = document.createElement('div');
    typingRow.className = 'fx-row assistant fx-typing';
    const avatar = document.createElement('span');
    avatar.className = 'fx-avatar';
    const bubble = document.createElement('div');
    bubble.className = 'fx-bubble';
    bubble.innerHTML = '<span class="fx-typing-dot"></span><span class="fx-typing-dot"></span><span class="fx-typing-dot"></span>';
    typingRow.appendChild(avatar);
    typingRow.appendChild(bubble);
    messagesEl.appendChild(typingRow);
    messagesEl.scrollTop = messagesEl.scrollHeight;
  }
  function hideTyping() {
    if (typingRow) { typingRow.remove(); typingRow = null; }
  }

  function extractProfileMarker(raw) {
    const match = raw.match(/<<PROFILE:(\{[\s\S]*?\})>>\s*$/);
    if (!match) return { clean: raw.trim(), updates: {} };
    let updates = {};
    try { updates = JSON.parse(match[1]); } catch (e) { updates = {}; }
    const clean = raw.slice(0, match.index).trim();
    return { clean, updates };
  }

  async function callFridayOnce() {
    const profileNote = Object.keys(profile).length ? JSON.stringify(profile) : '(nothing yet)';
    const system = PERSONA_BASE + '\n\nWhat you currently know about this person: ' + profileNote + MARKER_INSTRUCTIONS;
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-6',
        max_tokens: 1000,
        system: system,
        messages: conversation.map(m => ({ role: m.role, content: m.content }))
      })
    });
    if (!response.ok) {
      const err = new Error('API error ' + response.status);
      if (response.status >= 400 && response.status < 500) err.noRetry = true;
      throw err;
    }
    const data = await response.json();
    return (data.content || []).filter(b => b.type === 'text').map(b => b.text).join('\n');
  }

  async function callFriday() {
    try {
      return await callFridayOnce();
    } catch (err) {
      if (err.noRetry) throw err;
      await new Promise(r => setTimeout(r, 600));
      return await callFridayOnce();
    }
  }

  function autoresize() {
    inputEl.style.height = 'auto';
    inputEl.style.height = Math.min(inputEl.scrollHeight, 120) + 'px';
  }

  function setSendingUI(state) {
    sendEl.disabled = state;
    inputEl.disabled = state;
  }

  function pickVoice() {
    const voices = window.speechSynthesis.getVoices();
    if (!voices.length) return null;
    return (
      voices.find(v => v.lang === 'en-IE') ||
      voices.find(v => /moira|fiona/i.test(v.name)) ||
      voices.find(v => v.lang === 'en-GB' && /female|karen|serena|kate|tessa/i.test(v.name)) ||
      voices.find(v => /en-GB|en-US|en-AU/.test(v.lang) && /female|samantha|victoria|zira|susan/i.test(v.name)) ||
      voices.find(v => v.lang && v.lang.indexOf('en') === 0) ||
      voices[0]
    );
  }

  function speak(text) {
    if (!voicePref || !window.speechSynthesis) return;
    window.speechSynthesis.cancel();
    const u = new SpeechSynthesisUtterance(text);
    u.rate = 1.05;
    u.pitch = 1.04;
    const v = pickVoice();
    if (v) u.voice = v;
    window.speechSynthesis.speak(u);
  }

  async function handleSend(e) {
    e.preventDefault();
    const text = inputEl.value.trim();
    if (!text || sending) return;
    sending = true;
    setSendingUI(true);

    conversation.push({ role: 'user', content: text });
    renderMessage('user', text);
    inputEl.value = '';
    autoresize();
    persistHistory();
    showTyping();

    try {
      const raw = await callFriday();
      hideTyping();
      const parsed = extractProfileMarker(raw);
      if (Object.keys(parsed.updates).length) {
        applyProfileUpdates(parsed.updates);
        await persistProfile();
        renderProfilePanel();
      }
      const finalText = parsed.clean || "Go on, I'm listening.";
      conversation.push({ role: 'assistant', content: finalText });
      const bubble = renderAssistantBubbleShell();
      speak(finalText);
      await revealText(bubble, finalText);
      persistHistory();
    } catch (err) {
      hideTyping();
      renderMessage('assistant', "Something's not connecting on my end, boss. Try that again in a moment.");
      console.error('FridayXY error:', err);
    } finally {
      sending = false;
      setSendingUI(false);
      inputEl.focus();
    }
  }

  function setupRecognition() {
    const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
    if (!SR) {
      micEl.disabled = true;
      micEl.title = 'Voice input needs a browser like Chrome or Edge';
      return;
    }
    recognition = new SR();
    recognition.lang = 'en-US';
    recognition.continuous = false;
    recognition.interimResults = true;

    recognition.onresult = function (e) {
      let interim = '';
      let final = '';
      for (let i = e.resultIndex; i < e.results.length; i++) {
        const t = e.results[i][0].transcript;
        if (e.results[i].isFinal) final += t; else interim += t;
      }
      inputEl.value = final || interim;
      autoresize();
      if (final) {
        setTimeout(function () {
          if (inputEl.value.trim()) formEl.requestSubmit();
        }, 150);
      }
    };
    recognition.onend = function () {
      listening = false;
      micEl.classList.remove('listening');
    };
    recognition.onerror = function (e) {
      listening = false;
      micEl.classList.remove('listening');
      if (e.error === 'not-allowed' || e.error === 'service-not-allowed') {
        renderMessage('assistant', "I need microphone access for that, boss. Check your browser's permission prompt, or try opening this page in its own tab.");
      }
    };
  }

  function toggleListening() {
    if (!recognition) return;
    if (listening) {
      recognition.stop();
      listening = false;
      micEl.classList.remove('listening');
      return;
    }
    if (window.speechSynthesis) window.speechSynthesis.cancel();
    try {
      recognition.start();
      listening = true;
      micEl.classList.add('listening');
    } catch (e) { /* recognition already active */ }
  }

  formEl.addEventListener('submit', handleSend);
  inputEl.addEventListener('input', autoresize);
  inputEl.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      formEl.requestSubmit();
    }
  });
  micEl.addEventListener('click', toggleListening);

  profileBtn.addEventListener('click', function () {
    const isOpen = profilePanel.classList.toggle('open');
    profileBtn.setAttribute('aria-expanded', String(isOpen));
  });

  voiceToggle.addEventListener('change', function () {
    voicePref = voiceToggle.checked;
    persistVoicePref();
    if (!voicePref && window.speechSynthesis) window.speechSynthesis.cancel();
  });

  forgetBtn.addEventListener('click', async function () {
    try { await window.storage.delete(STORE_PROFILE, false); } catch (e) {}
    try { await window.storage.delete(STORE_HISTORY, false); } catch (e) {}
    profile = {};
    conversation = [];
    messagesEl.innerHTML = '';
    renderProfilePanel();
    await init();
  });

  async function init() {
    profile = await loadProfile();
    conversation = await loadHistory();
    voicePref = await loadVoicePref();
    voiceToggle.checked = voicePref;
    renderProfilePanel();
    setupRecognition();
    if (window.speechSynthesis) window.speechSynthesis.onvoiceschanged = function () {};

    if (conversation.length === 0) {
      const greet = profile.name
        ? 'Welcome back, ' + profile.name + '. What are we tackling today?'
        : "Hey — I'm FridayXY. I'll be a lot more useful once I know who I'm talking to. What should I call you?";
      conversation.push({ role: 'assistant', content: greet });
      renderMessage('assistant', greet);
      persistHistory();
    } else {
      conversation.forEach(function (m) { renderMessage(m.role, m.content); });
    }
    inputEl.focus();
  }

  init();
})();
</script>

