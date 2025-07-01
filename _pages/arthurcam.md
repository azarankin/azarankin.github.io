---
title: "ArthurCam – Smart Home IoT Demo"
excerpt: "Minimal smart-home control system with real-time video and remote commands over WebSocket/REST."
layout: single
permalink: /arthurcam/
---


<div id="arthurcam-demo" style="background:#222; padding:1em; border-radius:10px; max-width:370px; font-family:sans-serif; color:#eee;">
  <iframe
    src="https://www.youtube.com/embed/EWZFFhwFOkA?autoplay=1&mute=1&controls=1"
    style="aspect-ratio:16/9; width:100%; border-radius:8px; border:2px solid #555;"
    title="YouTube video player"
    allow="autoplay; encrypted-media; fullscreen"
    allowfullscreen>
  </iframe>



  <div id="ac-feedback" style="margin:10px 0; font-weight:bold;"></div>

  <input   
    id="ac-text" 
    type="text" 
    maxlength="10" 
    placeholder="Enter text (max 10)" 
    autocomplete="off" 
    autocorrect="off" 
    autocapitalize="off" 
    spellcheck="false"
    style="width:100%; padding:0.5em; margin:6px 0; border:1px solid #444; background:#111; color:#fff; border-radius:5px; font-size:1em;">

  <button id="ac-send" style="width:100%; margin:8px 0; padding:0.6em; background:#008CBA; color:white; border:none; border-radius:5px; font-weight:bold; cursor:pointer;">
    ⚡ Send Text
  </button>

  <button id="ac-led" style="display:inline-block; width:48%; margin:5px 1% 5px 0; padding:0.5em; background:#4CAF50; color:white; border:none; border-radius:5px; font-weight:bold; cursor:pointer;">
    💡 LED
  </button>

  <button id="ac-lamp" style="display:inline-block; width:48%; margin:5px 0; padding:0.5em; background:#FF9800; color:white; border:none; border-radius:5px; font-weight:bold; cursor:pointer;">
    💡 Lamp
  </button>

  <div style="margin-top:10px; font-size:0.9em; color:#ccc;">
    🧪 Live control in your browser. Type a message, toggle LEDs, or control a lamp – straight from your phone.
  </div>
</div>

<script>
  function acSetMsg(msg, color = '#0f0') {
    const el = document.getElementById('ac-feedback');
    el.textContent = msg;
    el.style.color = color;
  }

  async function acAction(url) {
    const buttons = [...document.querySelectorAll('#ac-send,#ac-led,#ac-lamp')];
    buttons.forEach(b => b.disabled = true);

    acSetMsg('Please wait...', '#ff0');

    try {
      const res = await fetch(url, { method: 'GET' });
      console.log('Status:', res.status);
      await new Promise(r => setTimeout(r, 8000));
      acSetMsg('Success!', '#0f0');
    } catch (E) {
      acSetMsg('Error', '#f44');
      console.error('Fetch error:', E);
    }

    await new Promise(r => setTimeout(r, 2000));
    acSetMsg('Cooldown...', '#ccc');
    await new Promise(r => setTimeout(r, 2000));
    acSetMsg('');
    buttons.forEach(b => b.disabled = false);
  }

  document.getElementById('ac-send').onclick = () => {
    let v = document.getElementById('ac-text').value.trim().slice(0, 10);
    if (!v) return acSetMsg('Enter text!', '#f44');
    acAction('https://arthurcam.com/api/arduinoIOT/' + encodeURIComponent(v));
  };

  document.getElementById('ac-led').onclick = () => acAction('https://arthurcam.com/api/arduinoIOT/6');
  document.getElementById('ac-lamp').onclick = () => acAction('https://arthurcam.com/api/arduinoIOT/2');
</script>

---

**ArthurCam** is a lightweight, browser-accessible smart-home prototype.  
It combines live video streaming from an Arduino-based system with real-time remote control via:

- Toggling LEDs (on/off)
- Displaying messages on an OLED screen
- Controlling hardware through **WebSocket** and **REST APIs**

✅ Built using minimal web technologies, running on an embedded device  
💡 Demonstrates core IoT principles and real-time interaction

🔗 **Source Code & Docs**: [GitHub – ArthurCam Project](https://github.com/azarankin/ArthurCam.com.Project)

<img src="/assets/arthurcam.jpg" alt="ArthurCam Demo Photo" style="max-width:300px; border-radius:12px; border:2px solid #444; display:block; margin-top:1em;">






