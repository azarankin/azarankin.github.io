<div id="arthurcam-demo" style="background:#222; padding:1em; border-radius:10px; max-width:370px; font-family:sans-serif; color:#eee; margin-bottom:1.5em;">
  <iframe
    id="arthurcam-demo iframe"
    src="{{ site.arthurcam_video_url }}?autoplay=1&mute=1"
    style="aspect-ratio:16/9; width:100%; border-radius:8px; border:2px solid #555;"
    title="Live ArthurCam Stream"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>


  <div style="color:#e53935; font-weight:bold; margin-bottom:6px; font-size:90%; letter-spacing:1px;">
    🔴 Live Stream & Real-Time Control
  </div>

  <div id="ac-feedback" style="margin:10px 0; font-weight:bold;"></div>

  <input   
    id="ac-text" 
    type="text" 
    maxlength="10" 
    placeholder="Enter text (max 10 in English)" 
    autocomplete="off" 
    autocorrect="off" 
    autocapitalize="off" 
    spellcheck="false"
    pattern="[a-zA-Z0-9\s]*"
    title="Only English letters and numbers allowed"
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

<div style="margin-top:10px; font-size:0.97em; color:#ccc;">
  <b>Test it live:</b>
  <ul style="margin:8px 0 0 18px; padding:0;">
    <li>💡 Turn the lamp on/off</li>
    <li>🔆 Blink LEDs</li>
    <li>💬 Send a message</li>
    <li>📡 All actions update instantly on the live stream</li>
  </ul>
</div>
</div>


<script>
  window.addEventListener('DOMContentLoaded', function () {
    setTimeout(function() {
      var iframe = document.querySelector('#arthurcam-demo iframe');
      if (iframe) {
        var src = iframe.src;
        // הוספת פרמטר dummy תכריח רענון בלי קאש
        if(src.indexOf('refresh=') === -1) {
          iframe.src = src + (src.indexOf('?') > -1 ? '&' : '?') + 'refresh=' + Date.now();
        }
      }
    }, 7000); // 7 שניות אחרי הטעינה (אפשר לשנות)
    document.getElementById('ac-text').addEventListener('input', function(e) {
      // השאר רק אותיות אנגלית ומספרים
      this.value = this.value.replace(/[^a-zA-Z0-9 ]/g, '');
    });
  });

  
</script>

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
    acAction('{{ site.arthurcam_domain }}/api/arduinoIOT/' + encodeURIComponent(v));
  };

  document.getElementById('ac-led').onclick = () => acAction('{{ site.arthurcam_domain }}/api/arduinoIOT/6');
  document.getElementById('ac-lamp').onclick = () => acAction('{{ site.arthurcam_domain }}/api/arduinoIOT/2');
</script>



### ArthurCam – Real-Time Smart Home Demo

- 🟢 **Live control:** lamp, LEDs, and OLED display — direct from your browser
- 📡 **24/7 video streaming** from the Arduino-based setup
- 💬 Instantly send messages and see them appear live
- ☁️ **Cloud IoT integration** with real server-side logic


<a target="_blank" rel="noopener noreferrer" href="https://github.com/azarankin/ArthurCam.com.Project" style="display:inline-block; margin:10px 0 12px 0; color:#fff; background:#222; border:1px solid #06b6d4; border-radius:6px; padding:6px 18px; font-weight:bold; text-decoration:none;">🔗 Source Code & Docs</a>

