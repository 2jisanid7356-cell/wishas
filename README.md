<!doctype html>
<html lang="en" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="https://cdn.jsdelivr.net/npm/lucide@0.263.0/dist/umd/lucide.min.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&amp;family=Playfair+Display:wght@400;700;900&amp;family=Cormorant+Garamond:wght@300;400;600&amp;display=swap" rel="stylesheet">
  <style>
    html, body { height: 100%; margin: 0; overflow: hidden; }
    * { box-sizing: border-box; }

    .night-sky {
      background: linear-gradient(180deg, #0a0a1a 0%, #0d1033 30%, #1a1040 50%, #0d1033 70%, #0a0a1a 100%);
    }

    @keyframes twinkle {
      0%, 100% { opacity: 0.3; transform: scale(0.8); }
      50% { opacity: 1; transform: scale(1.2); }
    }
    @keyframes twinkle2 {
      0%, 100% { opacity: 0.5; }
      50% { opacity: 0.15; }
    }
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-12px); }
    }
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(40px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes scaleIn {
      from { opacity: 0; transform: scale(0.5); }
      to { opacity: 1; transform: scale(1); }
    }
    @keyframes slideDown {
      from { opacity: 0; transform: translateY(-30px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes pulseGlow {
      0%, 100% { box-shadow: 0 0 20px rgba(212, 175, 55, 0.3); }
      50% { box-shadow: 0 0 40px rgba(212, 175, 55, 0.6), 0 0 80px rgba(212, 175, 55, 0.2); }
    }
    @keyframes shootingStar {
      0% { transform: translateX(0) translateY(0) rotate(-45deg); opacity: 1; }
      100% { transform: translateX(300px) translateY(300px) rotate(-45deg); opacity: 0; }
    }
    @keyframes confetti {
      0% { transform: translateY(0) rotate(0deg); opacity: 1; }
      100% { transform: translateY(400px) rotate(720deg); opacity: 0; }
    }

    .star {
      position: absolute;
      border-radius: 50%;
      background: radial-gradient(circle, #ffd700, #daa520);
      box-shadow: 0 0 10px 4px rgba(255, 215, 0, 0.6), 0 0 20px 8px rgba(255, 215, 0, 0.3);
    }

    .scroll-section {
      opacity: 0;
      transform: translateY(50px);
      transition: all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    }
    .scroll-section.visible {
      opacity: 1;
      transform: translateY(0);
    }

    .btn-enter {
      animation: pulseGlow 2s ease-in-out infinite;
      transition: all 0.3s ease;
    }
    .btn-enter:hover {
      transform: scale(1.08);
      box-shadow: 0 0 50px rgba(212, 175, 55, 0.7);
    }

    .scroll-indicator {
      animation: float 2s ease-in-out infinite;
    }

    #main-wrapper {
      scroll-behavior: smooth;
    }

    .shooting-star {
      position: absolute;
      width: 80px;
      height: 2px;
      background: linear-gradient(to right, rgba(255, 215, 0, 0.8), transparent);
      animation: shootingStar 1.5s ease-out forwards;
    }

    .confetti-piece {
      position: fixed;
      width: 8px;
      height: 8px;
      animation: confetti 3s ease-out forwards;
      z-index: 100;
    }

    .wish-button {
      transition: all 0.3s ease;
      cursor: pointer;
    }
    .wish-button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 20px rgba(212, 175, 55, 0.4);
    }
    .wish-button:active {
      transform: scale(0.98);
    }
  </style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div id="main-wrapper" class="h-full w-full overflow-auto night-sky relative">
   <!-- Stars container -->
   <div id="stars-container" class="fixed inset-0 pointer-events-none" style="z-index:0;"></div><!-- PAGE 1: Welcome -->
   <div id="page-welcome" class="relative flex items-center justify-center" style="min-height:100%; z-index:1;">
    <div class="text-center px-6">
     <div style="animation: float 3s ease-in-out infinite;">
      <p class="text-amber-200/60 tracking-[0.3em] uppercase text-sm mb-4" style="font-family:'Cormorant Garamond',serif;">A special celebration awaits</p>
      <div class="text-6xl mb-8">
       ✨🎂✨
      </div>
     </div><button id="btn-enter" onclick="showBirthdayPage()" class="btn-enter px-10 py-4 rounded-full border-2 border-amber-400/60 text-amber-100 text-lg tracking-widest uppercase cursor-pointer bg-amber-900/20 backdrop-blur-sm" style="font-family:'Playfair Display',serif; font-weight:700;"> Click Here </button>
     <p class="text-amber-300/30 mt-6 text-xs tracking-widest" style="font-family:'Cormorant Garamond',serif;">Something beautiful is waiting…</p>
    </div>
   </div><!-- PAGE 2: Birthday Content -->
   <div id="page-birthday" class="relative hidden" style="z-index:1;">
    <!-- Hero Section -->
    <div class="flex items-center justify-center px-6 py-20" style="min-height:100%;">
     <div class="text-center">
      <h1 id="title-text" class="text-amber-100 leading-tight mb-6" style="font-family:'Dancing Script',cursive; font-weight:700; font-size:clamp(2.5rem,10vw,4.5rem); animation: scaleIn 1s ease-out;">Happy Birthday!</h1>
      <p id="name-display" class="text-amber-300 tracking-[0.3em] uppercase mb-10" style="font-family:'Cormorant Garamond',serif; font-size:clamp(1.4rem,3vw,2rem); animation: fadeInUp 1s ease-out 0.2s both;">Munjerin</p><!-- Scroll Down Box -->
      <div id="scroll-box" class="mt-8 inline-block px-8 py-4 rounded-2xl border border-amber-400/30 bg-amber-900/15 backdrop-blur-sm" style="animation: slideDown 1s ease-out 1s both;">
       <div class="scroll-indicator">
        <p class="text-amber-200/70 text-sm tracking-widest mb-2 leading-relaxed" style="font-family:'Cormorant Garamond',serif; font-size:clamp(0.8rem,1.5vw,1rem);" id="moon-message">May you shine like Moon on your every aspects of life because you have the MOON Named in your name.</p><i data-lucide="chevrons-down" style="color: #d4af37; width:24px; height:24px; margin:0 auto; display:block;"></i>
       </div>
      </div>
     </div>
    </div><!-- Section 2: Message -->
    <div class="scroll-section flex items-center justify-center px-6 py-24" style="min-height:80%;">
     <div class="max-w-lg text-center">
      <div class="text-5xl mb-8">
       🌟
      </div>
      <p id="msg-text" class="text-amber-100/90 text-xl leading-relaxed mb-6" style="font-family:'Cormorant Garamond',serif; font-weight:300; font-size:clamp(1.1rem,2.5vw,1.4rem);">On your special day, I wish you endless joy, boundless dreams, and a life as radiant as your beautiful soul. May every moment bring you closer to your deepest wishes!</p>
      <div class="w-16 h-px bg-gradient-to-r from-transparent via-amber-400/50 to-transparent mx-auto"></div>
     </div>
    </div><!-- Section 3: Wishes -->
    <div class="scroll-section flex items-center justify-center px-6 py-24" style="min-height:80%;">
     <div class="max-w-md text-center">
      <div class="grid grid-cols-3 gap-4 mb-10">
       <div class="p-4 rounded-xl border border-amber-400/20 bg-amber-900/10 wish-button" onclick="launchIconRain('celebration')">
        <div class="text-3xl sm:text-4xl mb-2">
         🎉
        </div>
        <p class="text-amber-200/60 text-xs" style="font-family:'Cormorant Garamond',serif;">Joy</p>
       </div>
       <div class="p-4 rounded-xl border border-amber-400/20 bg-amber-900/10 wish-button" onclick="launchIconRain('heart')">
        <div class="text-3xl sm:text-4xl mb-2">
         💖
        </div>
        <p class="text-amber-200/60 text-xs" style="font-family:'Cormorant Garamond',serif;">Love</p>
       </div>
       <div class="p-4 rounded-xl border border-amber-400/20 bg-amber-900/10 wish-button" onclick="launchIconRain('stars')">
        <div class="text-3xl sm:text-4xl mb-2">
         ⭐
        </div>
        <p class="text-amber-200/60 text-xs" style="font-family:'Cormorant Garamond',serif;">Peace</p>
       </div>
      </div>
      <p class="text-amber-100/80 text-lg" style="font-family:'Playfair Display',serif;">Wishing you all the magic this world has to offer</p>
     </div>
    </div><!-- Section 4: Personal Words -->
    <div class="scroll-section flex items-center justify-center px-6 py-24" style="min-height:80%;">
     <div class="max-w-lg text-center">
      <div class="text-4xl mb-6">
       💌
      </div><button onclick="openPersonalWordsModal()" class="px-8 py-4 rounded-2xl border border-amber-400/40 bg-amber-900/20 text-amber-200 tracking-widest text-lg cursor-pointer hover:bg-amber-800/30 transition-all mb-4" style="font-family:'Playfair Display',serif; font-weight:700;"> Few Words of Mine </button>
      <p class="text-amber-300/60 text-sm" style="font-family:'Cormorant Garamond',serif;">Click to read my heartfelt message for you</p>
     </div>
    </div><!-- Section 5: Final -->
    <div class="scroll-section flex items-center justify-center px-6 py-24" style="min-height:80%;">
     <div class="text-center">
      <div class="text-7xl mb-6" style="animation: float 4s ease-in-out infinite;">
       🎉
      </div>
      <h2 class="text-amber-100 text-3xl mb-4" style="font-family:'Playfair Display',serif; font-weight:700;">Make a Wish!</h2>
      <p class="text-amber-300/50 text-sm tracking-widest" style="font-family:'Cormorant Garamond',serif;">Close your eyes and believe…</p><button onclick="launchConfetti()" class="mt-8 px-8 py-3 rounded-full border border-amber-400/40 bg-amber-900/20 text-amber-200 tracking-widest text-sm cursor-pointer hover:bg-amber-800/30 transition-all" style="font-family:'Cormorant Garamond',serif;"> 🎂 Blow the Candles </button>
     </div>
    </div>
    <div class="py-12 text-center">
     <p class="text-amber-400/20 text-xs tracking-[0.3em]" style="font-family:'Cormorant Garamond',serif;">Made with ♡</p>
    </div>
   </div><!-- Personal Words Modal -->
   <div id="personal-modal" class="fixed inset-0 hidden flex items-center justify-center px-4 z-50" style="background: rgba(10, 10, 26, 0.85); backdrop-filter: blur(4px);">
    <div class="max-w-2xl w-full max-h-80 bg-gradient-to-b from-amber-900/40 to-purple-900/30 rounded-2xl border border-amber-400/30 p-8 overflow-y-auto relative">
     <button onclick="closePersonalWordsModal()" class="absolute top-4 right-4 text-amber-400 hover:text-amber-300 transition" style="font-size: 24px;">×</button>
     <h3 class="text-amber-100 text-2xl mb-6 text-center" style="font-family:'Playfair Display',serif; font-weight:700;">Few Words of Mine</h3>
     <p id="personal-words-text" class="text-amber-100/90 leading-relaxed text-sm sm:text-base" style="font-family:'Cormorant Garamond',serif; line-height:1.8; color: #fef3c7;"></p>
     <div class="mt-6 text-center">
      <button onclick="closePersonalWordsModal()" class="px-6 py-2 rounded-full border border-amber-400/40 bg-amber-900/20 text-amber-200 text-sm cursor-pointer hover:bg-amber-800/30 transition" style="font-family:'Cormorant Garamond',serif;">Close</button>
     </div>
    </div>
   </div>
   <script>
    // Generate stars
    function createStars() {
      const container = document.getElementById('stars-container');
      container.innerHTML = '';
      const count = window.innerWidth < 640 ? 60 : 120;
      for (let i = 0; i < count; i++) {
        const star = document.createElement('div');
        star.className = 'star';
        const size = Math.random() * 3 + 1;
        const delay = Math.random() * 5;
        const duration = Math.random() * 3 + 2;
        star.style.cssText = `
          width:${size}px; height:${size}px;
          left:${Math.random()*100}%; top:${Math.random()*100}%;
          animation: ${Math.random()>0.5?'twinkle':'twinkle2'} ${duration}s ${delay}s infinite;
        `;
        container.appendChild(star);
      }
    }
    createStars();

    // Show birthday page
    function showBirthdayPage() {
      document.getElementById('page-welcome').style.display = 'none';
      document.getElementById('page-birthday').classList.remove('hidden');
      // Shooting star effect
      for (let i = 0; i < 3; i++) {
        setTimeout(() => {
          const s = document.createElement('div');
          s.className = 'shooting-star';
          s.style.top = Math.random()*30 + '%';
          s.style.left = Math.random()*50 + '%';
          document.getElementById('main-wrapper').appendChild(s);
          setTimeout(() => s.remove(), 1500);
        }, i * 500);
      }
      setTimeout(() => lucide.createIcons(), 50);
    }

    // Scroll reveal
    const wrapper = document.getElementById('main-wrapper');
    wrapper.addEventListener('scroll', () => {
      document.querySelectorAll('.scroll-section').forEach((el, i) => {
        const rect = el.getBoundingClientRect();
        if (rect.top < window.innerHeight * 0.85) {
          el.style.transitionDelay = '0.1s';
          el.classList.add('visible');
        }
      });
    });

    // Confetti
    function launchConfetti() {
      const colors = ['#ffd700','#ff6b6b','#a78bfa','#34d399','#f472b6','#fbbf24'];
      for (let i = 0; i < 40; i++) {
        const c = document.createElement('div');
        c.className = 'confetti-piece';
        c.style.cssText = `
          left:${Math.random()*100}%; top:-10px;
          background:${colors[Math.floor(Math.random()*colors.length)]};
          border-radius:${Math.random()>0.5?'50%':'2px'};
          animation-delay:${Math.random()*0.8}s;
          animation-duration:${2+Math.random()*2}s;
        `;
        document.body.appendChild(c);
        setTimeout(() => c.remove(), 4000);
      }
    }

    // Icon rain effect
    function launchIconRain(type) {
      const icons = {
        celebration: ['🎉', '🎊', '🎈', '🎁', '✨'],
        heart: ['💖', '💕', '💗', '💓', '💝'],
        stars: ['⭐', '✨', '🌟', '💫', '🌠']
      };
      const selectedIcons = icons[type] || icons.celebration;
      
      for (let i = 0; i < 25; i++) {
        setTimeout(() => {
          const rain = document.createElement('div');
          rain.style.cssText = `
            position: fixed;
            left: ${Math.random() * 100}%;
            top: -30px;
            font-size: ${20 + Math.random() * 20}px;
            z-index: 200;
            animation: confetti ${2 + Math.random() * 2}s ease-out forwards;
            animation-delay: ${Math.random() * 0.3}s;
            opacity: 1;
          `;
          rain.textContent = selectedIcons[Math.floor(Math.random() * selectedIcons.length)];
          document.body.appendChild(rain);
          setTimeout(() => rain.remove(), 4000);
        }, i * 50);
      }
    }

    // Personal words modal
    function openPersonalWordsModal() {
      document.getElementById('personal-modal').classList.remove('hidden');
      document.getElementById('personal-modal').style.display = 'flex';
    }

    function closePersonalWordsModal() {
      document.getElementById('personal-modal').classList.add('hidden');
      document.getElementById('personal-modal').style.display = 'none';
    }

    document.getElementById('personal-modal').addEventListener('click', (e) => {
      if (e.target.id === 'personal-modal') {
        closePersonalWordsModal();
      }
    });

    // Element SDK
    const defaultConfig = {
      name_display: 'Munjerin',
      moon_message: 'May you shine like Moon on your every aspects of life because you have the MOON Named in your name.',
      birthday_message: 'On your special day, I wish you endless joy, boundless dreams, and a life as radiant as your beautiful soul. May every moment bring you closer to your deepest wishes!',
      personal_words: 'Hey it\'s 24th April I\'m making this simple website for you . Jninh koydin aso mehman hishabe but ei 3-4 din e amr onk bala laagse. Ekta halka halka santi lagse . Bishesh kori amre aij 2 ta bosor dori je bednay eto chataise tmre koiya ektu relieve feel korsi. I thought tmi onk bodmejaji ba attitude type er .But matiya toh dekha gese khub oi simple. Koisla nni je 2 din or maator lgi apnr chowk e di paani aioy. Ela amro hoy kharap laage , afsos hoy je kne maat off kori de mnus e , but I hope tmi ela hut kori maat off kortay nay jehetu koisoin je asoin aro 4-5 mash . Pore baad dile reason toh ase ekan ami emneo bujmu .R emon o hoito paare 1 maash or smy oi amrar maat ses oijaito paare. Ami je chizz ami balay ow jani. Ek smy schl or furinte amr piche piche hatta amr loge matar lgi r ebla mattam na . R jibla mukh khulchi ses . Kunuguye doraiya matto na teh kunu guye ignore korta but I was happy cuz that time amr life kew ekjon asil r amio caisi na mattam. Jai howk okan ow koimu e pgl or maat hunar lgi Thank youuuuuuuuu. Jninh kotodin takhba but jotodin asoin takijain. And apnare ami onk trust koriya amr fmly r bishoye koisi I hope gula just amr r apnr maajei jeno takhe. And eta jita apnare disi eta just apni oi jeno dekhoin r kewre dekhaiba naa. R maajemodde hoyto ami ulta falta maati ba poreo kibaa matte pari just bujba jen amr mood swing oigese, overthinking hamaigese matat.R emneo mata kaam kore na blankout oijay . Hoyto ota furintor boddua lagse jitare ami kosto dislam . 2-3 tay toh koisil je dekio postaibay ow . Hasaw ow postairam. Jai howk once again Happy Birthday Munjerin. I might send this link to you on 7th AUGUST. Stay safe Allah Hafiz.',
      background_color: '#0a0a1a',
      surface_color: '#1a1040',
      text_color: '#fef3c7',
      primary_action_color: '#d4af37',
      secondary_action_color: '#92702a',
      font_family: 'Dancing Script',
      font_size: 16
    };

    function applyConfig(config) {
      const name = config.name_display || defaultConfig.name_display;
      const msg = config.birthday_message || defaultConfig.birthday_message;
      const moonMsg = config.moon_message || defaultConfig.moon_message;
      const personalWords = config.personal_words || defaultConfig.personal_words;
      const font = config.font_family || defaultConfig.font_family;
      const baseSize = config.font_size || defaultConfig.font_size;
      const bg = config.background_color || defaultConfig.background_color;
      const text = config.text_color || defaultConfig.text_color;
      const primary = config.primary_action_color || defaultConfig.primary_action_color;

      document.getElementById('name-display').textContent = name;
      document.getElementById('msg-text').textContent = msg;
      document.getElementById('moon-message').textContent = moonMsg;
      document.getElementById('personal-words-text').textContent = personalWords;
      document.getElementById('title-text').style.fontFamily = `${font}, cursive`;
      document.getElementById('name-display').style.fontFamily = `Cormorant Garamond, ${font}, serif`;
      document.getElementById('title-text').style.color = text;
      document.getElementById('name-display').style.color = primary;

      const btn = document.getElementById('btn-enter');
      btn.style.borderColor = primary + '99';
      btn.style.color = text;
      btn.style.fontFamily = `${font}, serif`;
    }

    window.elementSdk.init({
      defaultConfig,
      onConfigChange: async (config) => applyConfig(config),
      mapToCapabilities: (config) => ({
        recolorables: [
          { get: () => config.background_color || defaultConfig.background_color, set: (v) => { config.background_color = v; window.elementSdk.setConfig({ background_color: v }); }},
          { get: () => config.surface_color || defaultConfig.surface_color, set: (v) => { config.surface_color = v; window.elementSdk.setConfig({ surface_color: v }); }},
          { get: () => config.text_color || defaultConfig.text_color, set: (v) => { config.text_color = v; window.elementSdk.setConfig({ text_color: v }); }},
          { get: () => config.primary_action_color || defaultConfig.primary_action_color, set: (v) => { config.primary_action_color = v; window.elementSdk.setConfig({ primary_action_color: v }); }},
          { get: () => config.secondary_action_color || defaultConfig.secondary_action_color, set: (v) => { config.secondary_action_color = v; window.elementSdk.setConfig({ secondary_action_color: v }); }}
        ],
        borderables: [],
        fontEditable: {
          get: () => config.font_family || defaultConfig.font_family,
          set: (v) => { config.font_family = v; window.elementSdk.setConfig({ font_family: v }); }
        },
        fontSizeable: {
          get: () => config.font_size || defaultConfig.font_size,
          set: (v) => { config.font_size = v; window.elementSdk.setConfig({ font_size: v }); }
        }
      }),
      mapToEditPanelValues: (config) => new Map([
        ['name_display', config.name_display || defaultConfig.name_display],
        ['moon_message', config.moon_message || defaultConfig.moon_message],
        ['birthday_message', config.birthday_message || defaultConfig.birthday_message],
        ['personal_words', config.personal_words || defaultConfig.personal_words]
      ])
    });

    lucide.createIcons();
  </script>
  </div>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9fa20370b1c31645',t:'MTc3ODUxMTIwOS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
