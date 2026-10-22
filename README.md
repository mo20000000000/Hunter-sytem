<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hunter Life System</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { background-color: #08090d; color: #e2e8f0; font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace; }
    .neon-cyan { border: 1px solid #00e5ff; box-shadow: 0 0 12px rgba(0, 229, 255, 0.2); }
    .neon-red { border: 1px solid #ff3333; box-shadow: 0 0 12px rgba(255, 51, 51, 0.3); }
    .card-bg { background-color: #12151f; }
    .glow-cyan { text-shadow: 0 0 8px rgba(0, 229, 255, 0.7); }
    .glow-red { text-shadow: 0 0 8px rgba(255, 51, 51, 0.7); }
    .wheel-container { position: relative; width: 240px; height: 240px; margin: 0 auto; }
    .wheel-pointer { position: absolute; top: -10px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 12px solid transparent; border-right: 12px solid transparent; border-top: 20px solid #ef4444; z-index: 10; }
    @keyframes popfx { 0%{opacity:0;transform:translate(-50%,0) scale(.6)} 20%{opacity:1;transform:translate(-50%,-10px) scale(1.15)} 100%{opacity:0;transform:translate(-50%,-60px) scale(1)} }
    .fx-pop { position: fixed; z-index: 9999; pointer-events: none; font-weight: 700; font-size: 14px; color: #fde047; text-shadow: 0 0 8px rgba(250,204,21,.8); animation: popfx .9s ease-out forwards; }
  </style>
</head>
<body class="p-4 pb-24 min-h-screen flex flex-col items-center select-none text-right max-w-md mx-auto space-y-4">

  <header class="w-full flex justify-between items-center p-3.5 card-bg rounded-2xl neon-cyan">
    <div class="flex items-center gap-2.5 cursor-pointer" onclick="showView('home')">
      <span class="text-2xl">⚡</span>
      <div>
        <h1 class="text-xs font-bold text-cyan-400 glow-cyan font-mono">HUNTER LIFE SYSTEM</h1>
        <p class="text-[10px] text-gray-400" id="top-user-name">Mostafa Abdelrahman</p>
      </div>
    </div>
    <button onclick="showView('home')" class="px-3 py-1.5 text-xs bg-gray-900 border border-cyan-500/50 hover:bg-cyan-950 rounded-xl text-cyan-400 font-bold transition">🏠 الرئيسية</button>
  </header>

  <main class="w-full space-y-4">

    <!-- الصفحة الرئيسية -->
    <section id="view-home" class="space-y-4">
      <div class="card-bg p-5 rounded-2xl border border-gray-800 text-center relative shadow-lg">
        <div class="absolute top-3 left-3 flex gap-1.5">
          <button onclick="toggleHomeOrderMode()" id="home-order-btn" class="text-[10px] bg-gray-900 border border-gray-700 hover:border-cyan-500 text-cyan-400 px-2.5 py-1 rounded-lg">↕ ترتيب</button>
          <button onclick="toggleHomeEditMode()" id="home-edit-btn" class="text-[10px] bg-gray-900 border border-gray-700 hover:border-cyan-500 text-cyan-400 px-2.5 py-1 rounded-lg">⚙️ تعديل</button>
        </div>
        <h2 class="text-base font-bold text-gray-100 mb-1">لوحة قيادة البطل ⚔️</h2>
        <p class="text-xs text-gray-400">اختر البوابة المطلوبة لمواصلة التطوير والتعافي:</p>
      </div>

      <div id="today-card" class="card-bg p-4 rounded-2xl border border-cyan-500/40 space-y-3"></div>

      <div id="home-buttons-container" class="space-y-3">

        <div data-home-key="workouts" class="p-4 rounded-2xl card-bg border border-cyan-500/40 hover:border-cyan-400 flex items-center justify-between transition hover:scale-[1.01] relative cursor-pointer shadow" onclick="if(!isHomeEditing && !isHomeOrdering) showView('workouts')">
          <div class="flex items-center gap-3.5">
            <span class="text-2xl p-2.5 rounded-xl bg-cyan-950/60 border border-cyan-500/50 hb-icon">⚔️</span>
            <div>
              <h3 class="text-sm font-bold text-cyan-400 hb-title">نظام تمارين Hunter</h3>
              <p class="text-xs text-gray-400 hb-desc">Day 1 / Day 2، الرتب، السجل الشهري والمتوسط الأسبوعي</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <div class="order-arrows hidden flex gap-1">
              <button class="px-2 py-1 bg-gray-800 border border-cyan-400 text-cyan-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('workouts', -1)">▲</button>
              <button class="px-2 py-1 bg-gray-800 border border-cyan-400 text-cyan-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('workouts', 1)">▼</button>
            </div>
            <button class="edit-btn hidden text-[10px] bg-cyan-950 border border-cyan-400 text-cyan-300 px-2 py-1 rounded z-10" onclick="event.stopPropagation(); editHomeItem('workouts')">تعديل</button>
            <span class="text-cyan-400 text-sm arrow-icon">◀</span>
          </div>
        </div>

        <div data-home-key="dayTracker" class="p-4 rounded-2xl card-bg border border-sky-500/40 hover:border-sky-400 flex items-center justify-between transition hover:scale-[1.01] relative cursor-pointer shadow" onclick="if(!isHomeEditing && !isHomeOrdering) openDayTrackerFromHome()">
          <div class="flex items-center gap-3.5">
            <span class="text-2xl p-2.5 rounded-xl bg-sky-950/60 border border-sky-500/50 hb-icon">📅</span>
            <div>
              <h3 class="text-sm font-bold text-sky-400 hb-title">تراكينج النوم والعادات</h3>
              <p class="text-xs text-gray-400 hb-desc">العادات، تايم بلوكينج، وتسجيل النوم والاستيقاظ والسعرات</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <div class="order-arrows hidden flex gap-1">
              <button class="px-2 py-1 bg-gray-800 border border-sky-400 text-sky-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('dayTracker', -1)">▲</button>
              <button class="px-2 py-1 bg-gray-800 border border-sky-400 text-sky-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('dayTracker', 1)">▼</button>
            </div>
            <button class="edit-btn hidden text-[10px] bg-sky-950 border border-sky-400 text-sky-300 px-2 py-1 rounded z-10" onclick="event.stopPropagation(); editHomeItem('dayTracker')">تعديل</button>
            <span class="text-sky-400 text-sm arrow-icon">◀</span>
          </div>
        </div>

        <div data-home-key="recoveryCounter" class="p-4 rounded-2xl card-bg border border-orange-500/40 hover:border-orange-400 flex justify-between items-center relative cursor-pointer transition hover:scale-[1.01] shadow" onclick="if(!isHomeEditing && !isHomeOrdering) showView('recoveryCounterView')">
          <div class="flex items-center gap-3.5">
            <div class="w-12 h-12 rounded-xl bg-orange-950/60 border border-orange-500/50 flex items-center justify-center text-2xl hb-icon">✊🔥</div>
            <div>
              <h3 class="text-sm font-bold text-orange-400 hb-title">شكل المقاومة (عداد التعافي)</h3>
              <p class="text-xs text-gray-400 hb-desc">دورة الـ 90 يوم، الأوسمة، والدروع والأيام</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <div class="order-arrows hidden flex gap-1" onclick="event.stopPropagation()">
              <button class="px-2 py-1 bg-gray-800 border border-orange-400 text-orange-300 rounded text-xs" onclick="moveHomeItem('recoveryCounter', -1)">▲</button>
              <button class="px-2 py-1 bg-gray-800 border border-orange-400 text-orange-300 rounded text-xs" onclick="moveHomeItem('recoveryCounter', 1)">▼</button>
            </div>
            <button class="edit-btn hidden text-[10px] bg-orange-950 border border-orange-400 text-orange-300 px-2 py-1 rounded z-10" onclick="event.stopPropagation(); editHomeItem('recoveryCounter')">تعديل</button>
            <span class="text-orange-400 text-sm arrow-icon">◀</span>
          </div>
        </div>

        <div data-home-key="recovery" class="p-4 rounded-2xl card-bg border border-emerald-500/40 hover:border-emerald-400 flex items-center justify-between transition hover:scale-[1.01] relative cursor-pointer shadow" onclick="if(!isHomeEditing && !isHomeOrdering) showView('recovery')">
          <div class="flex items-center gap-3.5">
            <span class="text-2xl p-2.5 rounded-xl bg-emerald-950/60 border border-emerald-500/50 hb-icon">🌱</span>
            <div>
              <h3 class="text-sm font-bold text-emerald-400 hb-title">ركن التعافي</h3>
              <p class="text-xs text-gray-400 hb-desc">الأذكار، المعتقدات، الدعاء والتثبيت، واليوميات</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <div class="order-arrows hidden flex gap-1">
              <button class="px-2 py-1 bg-gray-800 border border-emerald-400 text-emerald-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('recovery', -1)">▲</button>
              <button class="px-2 py-1 bg-gray-800 border border-emerald-400 text-emerald-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('recovery', 1)">▼</button>
            </div>
            <button class="edit-btn hidden text-[10px] bg-emerald-950 border border-emerald-400 text-emerald-300 px-2 py-1 rounded z-10" onclick="event.stopPropagation(); editHomeItem('recovery')">تعديل</button>
            <span class="text-emerald-400 text-sm arrow-icon">◀</span>
          </div>
        </div>

        <div data-home-key="wheel" class="p-4 rounded-2xl card-bg border border-red-500/50 hover:border-red-400 flex items-center justify-between transition hover:scale-[1.01] bg-red-950/10 relative cursor-pointer shadow" onclick="if(!isHomeEditing && !isHomeOrdering) showView('wheel')">
          <div class="flex items-center gap-3.5">
            <span class="text-2xl p-2.5 rounded-xl bg-red-950/80 border border-red-500/70 hb-icon">🎡</span>
            <div>
              <h3 class="text-sm font-bold text-red-400 glow-red hb-title">عجلة الطوارئ (وقت الخطر)</h3>
              <p class="text-xs text-gray-400 hb-desc">تعديل المهام، خطط الهروب، وكسر الرغبة فوراً</p>
            </div>
          </div>
          <div class="flex items-center gap-2">
            <div class="order-arrows hidden flex gap-1">
              <button class="px-2 py-1 bg-gray-800 border border-red-400 text-red-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('wheel', -1)">▲</button>
              <button class="px-2 py-1 bg-gray-800 border border-red-400 text-red-300 rounded text-xs" onclick="event.stopPropagation(); moveHomeItem('wheel', 1)">▼</button>
            </div>
            <button class="edit-btn hidden text-[10px] bg-red-950 border border-red-400 text-red-300 px-2 py-1 rounded z-10" onclick="event.stopPropagation(); editHomeItem('wheel')">تعديل</button>
            <span class="text-red-400 text-sm arrow-icon">◀</span>
          </div>
        </div>

      </div>

      <div class="card-bg p-4 rounded-2xl border border-sky-500/40 space-y-3">
        <div class="flex items-center justify-between gap-2">
          <div>
            <h3 class="text-sm font-bold text-sky-300">☁️ النسخ الاحتياطي</h3>
            <p id="backup-status" class="text-[11px] text-gray-400">لسه مفيش نسخة احتياطية</p>
          </div>
          <div class="flex gap-2">
            <button onclick="backupToTelegram(true, event)" class="text-[11px] bg-sky-950 border border-sky-500 px-3 py-1.5 rounded-xl text-sky-300 font-bold">☁️ انسخ الآن</button>
            <button onclick="document.getElementById('import-file').click()" class="text-[11px] bg-gray-900 border border-gray-700 px-3 py-1.5 rounded-xl text-gray-300">📂 استرجاع</button>
          </div>
        </div>
      </div>
    </section>

    <!-- واجهة شكل المقاومة -->
    <section id="view-recoveryCounterView" class="hidden space-y-4">
      <div class="card-bg p-5 rounded-2xl border border-orange-500/40 space-y-4 text-center relative shadow-lg">

        <div class="flex justify-between items-center">
          <button onclick="reportRecoverySlip()" class="text-[10px] text-red-400 border border-red-500/40 px-2.5 py-1.5 rounded-xl hover:bg-red-950 transition">سجلت زلة (-1)</button>
          <div class="text-left bg-black/40 px-3 py-1.5 rounded-xl border border-gray-800">
            <span class="text-[9px] text-gray-400 block">البداية</span>
            <input type="date" id="recovery-start-input" onchange="updateRecoveryStart()" class="text-xs bg-transparent text-orange-400 font-bold outline-none cursor-pointer">
          </div>
        </div>

        <div class="py-2 flex flex-col items-center justify-center">
          <div class="w-32 h-32 rounded-3xl bg-orange-950/40 border border-orange-500/50 flex items-center justify-center text-6xl shadow-[0_0_20px_rgba(249,115,22,0.25)] relative">
            ✊🔥
          </div>
        </div>

        <div class="space-y-1">
          <div class="text-[11px] text-gray-400">يوم</div>
          <div class="text-4xl font-extrabold text-orange-400 font-mono tracking-wider" id="rc-days-fraction">0/90</div>
          <div class="text-[10px] text-orange-300 font-mono" id="rc-cycle-text">الدورة 1</div>
        </div>

        <div class="grid grid-cols-3 gap-2.5 pt-2">
          <div class="bg-black/50 p-3 rounded-2xl border border-gray-800 text-center font-mono">
            <div class="text-lg font-bold text-orange-300" id="rc-hours">00</div>
            <div class="text-[10px] text-gray-400">ساعة</div>
          </div>
          <div class="bg-black/50 p-3 rounded-2xl border border-gray-800 text-center font-mono">
            <div class="text-lg font-bold text-orange-300" id="rc-mins">00</div>
            <div class="text-[10px] text-gray-400">دقيقة</div>
          </div>
          <div class="bg-black/50 p-3 rounded-2xl border border-gray-800 text-center font-mono">
            <div class="text-lg font-bold text-orange-300" id="rc-secs">00</div>
            <div class="text-[10px] text-gray-400">ثانية</div>
          </div>
        </div>

      </div>

      <div class="grid grid-cols-4 gap-1.5">
        <button id="btab-badges" onclick="badgeTab('badges')" class="py-2.5 rounded-xl text-xs font-bold transition border bg-orange-500 text-black border-orange-400">الأوسمة</button>
        <button id="btab-shields" onclick="badgeTab('shields')" class="py-2.5 rounded-xl text-xs font-bold transition border bg-gray-900 text-gray-300 border-gray-800">الدروع</button>
        <button id="btab-cups" onclick="badgeTab('cups')" class="py-2.5 rounded-xl text-xs font-bold transition border bg-gray-900 text-gray-300 border-gray-800">الكؤوس</button>
        <button id="btab-certs" onclick="badgeTab('certs')" class="py-2.5 rounded-xl text-xs font-bold transition border bg-gray-900 text-gray-300 border-gray-800">الشهادات</button>
      </div>

      <div id="badges-content" class="grid grid-cols-2 gap-3"></div>
    </section>

    <!-- أقسام التمارين -->
    <section id="view-workouts" class="hidden space-y-4">
      <div class="card-bg p-5 rounded-2xl neon-cyan space-y-3">
        <div class="flex items-center justify-between">
          <div>
            <h2 id="hunter-name" class="text-lg font-bold text-cyan-400 glow-cyan cursor-pointer" onclick="editName()">Mostafa Abdelrahman ✏️</h2>
            <p id="hunter-rank-level" class="text-xs text-gray-400 mt-1">E-RANK HUNTER | LEVEL 1</p>
          </div>
          <div class="text-left">
            <span class="text-[10px] text-gray-400 block">TIME LEFT</span>
            <span id="countdown" class="text-xs font-bold text-cyan-400 font-mono">00:00:00</span>
          </div>
        </div>
        <div class="pt-3 border-t border-gray-800 space-y-1.5">
          <div class="flex justify-between text-xs">
            <span class="text-gray-300">Streak: <strong id="streak-count" class="text-cyan-400">0</strong> Days</span>
            <span id="weekly-status-text" class="text-gray-400">Level Progress</span>
          </div>
          <div class="w-full bg-gray-800 rounded-full h-2 overflow-hidden">
            <div id="streak-bar" class="bg-cyan-400 h-2 transition-all duration-300" style="width: 0%"></div>
          </div>
        </div>
      </div>

      <div class="card-bg p-4 rounded-2xl border border-orange-500/40 flex items-center justify-between">
        <div>
          <div class="text-[10px] text-gray-400">⏱ وقت التمرين</div>
          <div id="wt-display" class="text-2xl font-bold text-orange-400 font-mono">00:00:00</div>
          <div id="wt-info" class="text-[10px] text-gray-400 mt-0.5"></div>
        </div>
        <button id="wt-btn" onclick="toggleWorkoutTimer(event)" class="px-4 py-2.5 rounded-xl text-xs font-bold bg-orange-600 hover:bg-orange-500 text-white transition shadow">▶ ابدأ التمرين</button>
      </div>

      <div class="flex justify-between items-center text-xs px-1">
        <div class="flex gap-2">
          <button onclick="exportData()" class="px-2.5 py-1.5 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded-xl">💾 Export</button>
          <button onclick="document.getElementById('import-file').click()" class="px-2.5 py-1.5 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded-xl">📂 Import</button>
          <input type="file" id="import-file" accept=".json" class="hidden" onchange="importData(event)">
        </div>
        <button id="rest-toggle-btn" onclick="toggleTodayRest()" class="px-3 py-1.5 bg-gray-900 border border-green-700 text-green-400 rounded-xl font-semibold">🌿 Rest Day</button>
      </div>

      <div class="card-bg p-4 rounded-2xl border border-gray-800 space-y-2">
        <div class="flex justify-between items-center px-1">
          <span id="calendar-month-title" class="text-xs font-bold text-cyan-400">📅 MONTH LOG</span>
          <span class="text-[10px] text-gray-400">اضغط لتبديل حالة اليوم</span>
        </div>
        <div class="grid grid-cols-7 gap-1 text-center text-[10px] text-gray-500 font-semibold mb-1">
          <span>S</span><span>M</span><span>T</span><span>W</span><span>T</span><span>F</span><span>S</span>
        </div>
        <div id="calendar-days" class="grid grid-cols-7 gap-1.5 text-center"></div>
      </div>

      <div id="rest-day-banner" class="p-4 rounded-2xl bg-emerald-950/40 border border-emerald-500/50 hidden">
        <p class="text-xs text-emerald-300 font-bold">🌿 يوم استشفاء مفعل: أنت معفي اليوم من التمارين والعقوبات.</p>
      </div>

      <div id="penalty-card" class="p-4 rounded-2xl bg-red-950/30 border border-red-500 hidden space-y-2.5">
        <div class="flex justify-between items-center">
          <h4 class="text-xs font-bold text-red-400">⚠️ PENALTY QUEST ACTIVE</h4>
          <button onclick="editPenaltyText()" class="text-[10px] text-red-400 border border-red-500 px-2 py-0.5 rounded-lg">تعديل</button>
        </div>
        <p id="penalty-task-text" class="text-xs text-gray-200">1000 استغفار</p>
        <button onclick="confirmPenaltyDone()" class="w-full py-2 rounded-xl bg-red-600 font-bold text-xs">إتمام العقوبة وفتح النظام</button>
      </div>

      <div class="flex justify-between items-center">
        <div class="flex gap-2">
          <button id="tab-day1" onclick="switchRoutine('day1')" class="px-3.5 py-2 rounded-xl text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400">⚡ DAY 1</button>
          <button id="tab-day2" onclick="switchRoutine('day2')" class="px-3.5 py-2 rounded-xl text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400">🔥 DAY 2</button>
        </div>
        <button onclick="openAddQuestModal()" class="text-xs border border-cyan-500 text-cyan-400 px-3 py-2 rounded-xl hover:bg-cyan-950 transition">+ إضافة تمرين</button>
      </div>

      <div id="quest-list" class="space-y-3"></div>

      <button id="complete-day-btn" onclick="completeDay(event)" class="w-full py-3.5 rounded-2xl font-bold text-xs uppercase border border-cyan-500 text-cyan-400 hover:bg-cyan-950 transition shadow">COMPLETE DAY</button>
    </section>

    <!-- ركن التعافي -->
    <section id="view-recovery" class="hidden space-y-4">
      <div class="card-bg p-4 rounded-2xl border border-emerald-500/40">
        <h2 class="text-sm font-bold text-emerald-400">🌱 ركن التعافي</h2>
        <p class="text-[11px] text-gray-400 mt-0.5">الأذكار، المعتقدات، الدعاء والتثبيت، واليوميات</p>
      </div>
      <div class="grid grid-cols-4 gap-1.5">
        <button id="rtab-adhkar" onclick="recTab('adhkar')" class="py-2.5 rounded-xl border text-[11px] font-bold transition bg-emerald-950 border-emerald-400 text-emerald-300">📿 الأذكار</button>
        <button id="rtab-beliefs" onclick="recTab('beliefs')" class="py-2.5 rounded-xl border text-[11px] font-bold transition bg-gray-900 border-gray-800 text-gray-400">🧠 المعتقدات</button>
        <button id="rtab-duaa" onclick="recTab('duaa')" class="py-2.5 rounded-xl border text-[11px] font-bold transition bg-gray-900 border-gray-800 text-gray-400">🤲 الدعاء</button>
        <button id="rtab-journal" onclick="recTab('journal')" class="py-2.5 rounded-xl border text-[11px] font-bold transition bg-gray-900 border-gray-800 text-gray-400">🎙️ اليوميات</button>
      </div>

      <div id="pane-adhkar" class="space-y-3">
        <div class="card-bg p-4 rounded-2xl border border-emerald-500/40 flex justify-between items-center">
          <div>
            <h2 class="text-sm font-bold text-emerald-400">📿 أذكار المساء والتحصين</h2>
            <p class="text-[11px] text-gray-400">تعديل وترتيب أذكارك الخاصة</p>
          </div>
          <div class="flex gap-2">
            <button onclick="resetAzkarCounters()" class="text-[10px] bg-gray-900 border border-emerald-500/50 px-2.5 py-1.5 rounded-xl text-emerald-400">🔄 تصفير</button>
            <button onclick="openAddZekrPrompt()" class="text-[10px] bg-emerald-950 border border-emerald-500 px-3 py-1.5 rounded-xl text-emerald-300 font-bold">+ ذكر جديد</button>
          </div>
        </div>
        <div id="azkarList" class="space-y-3"></div>
      </div>

      <div id="pane-beliefs" class="hidden space-y-3"></div>

      <div id="pane-duaa" class="hidden space-y-3">
        <div class="card-bg p-4 rounded-2xl border border-blue-500/40 flex justify-between items-center">
          <div>
            <h2 class="text-sm font-bold text-blue-400">🤲 أدعية الثبات والاستعاذة</h2>
            <p class="text-[11px] text-gray-400">اضغط ✔ لتسجيل قراءة الدعاء</p>
          </div>
          <div class="flex gap-2">
            <button onclick="resetDuaaChecks()" class="text-[10px] bg-gray-900 border border-blue-500/50 px-2.5 py-1.5 rounded-xl text-blue-400">🔄 تصفير</button>
            <button onclick="openAddDuaaPrompt()" class="text-[10px] bg-blue-950 border border-blue-500 px-3 py-1.5 rounded-xl text-blue-300 font-bold">+ دعاء جديد</button>
          </div>
        </div>
        <div id="duaaList" class="space-y-3"></div>
      </div>

      <div id="pane-journal" class="hidden space-y-3">
        <div class="card-bg p-5 rounded-2xl border border-purple-500/40 space-y-3">
          <div class="flex justify-between items-start">
            <div>
              <h2 class="text-sm font-bold text-purple-400">🎙️ ركن اليوميات الصوتية والتوثيق</h2>
              <p class="text-[11px] text-gray-400">يتم إرسال الفويس والصور لتليجرام</p>
            </div>
            <button onclick="setupTelegram()" class="text-[10px] border border-purple-500/50 text-purple-300 px-2.5 py-1.5 rounded-xl">⚙️ تليجرام</button>
          </div>
          <div class="p-3.5 bg-black/40 rounded-xl border border-gray-800 flex items-center justify-between">
            <div class="flex items-center gap-3">
              <button id="recBtn" onclick="toggleRecord()" class="px-4 py-2 rounded-xl bg-blue-600 hover:bg-blue-500 text-white font-bold text-xs transition">بدء التسجيل ⏺</button>
              <span id="rec-status" class="text-xs text-gray-400">جاهز للتسجيل</span>
            </div>
          </div>
          <div id="audioList" class="space-y-2"></div>
          <div class="pt-3 border-t border-gray-800 space-y-2">
            <p class="text-xs text-gray-300">📸 توثيق بالصور (إرسال لتليجرام):</p>
            <label class="w-full block text-center py-3 px-3 rounded-xl bg-gray-900 border border-purple-500/60 text-purple-300 hover:bg-purple-950/40 text-xs font-bold cursor-pointer transition">
              📷 اختيار أو التقاط صورة
              <input type="file" id="photoInput" accept="image/*" class="hidden" onchange="sendPhotoToTelegram(this)">
            </label>
            <div id="photoStatus" class="text-[11px] text-cyan-400 text-center mt-1"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- عجلة الطوارئ -->
    <section id="view-wheel" class="hidden space-y-4 text-center">
      <div class="card-bg p-4 rounded-2xl neon-red space-y-1">
        <h2 class="text-sm font-bold text-red-400 glow-red">🚨 عجلة الطوارئ وكسر الرغبة</h2>
        <p class="text-xs text-gray-300">لف العجلة واهرب فوراً لتنفيذ المهمة!</p>
      </div>
      <div class="wheel-container">
        <div class="wheel-pointer"></div>
        <canvas id="wheelCanvas" width="500" height="500" class="w-full h-full rounded-full shadow-[0_0_15px_rgba(255,51,51,0.4)]"></canvas>
      </div>
      <div id="spinResult" class="text-xs font-bold text-yellow-300 min-h-[24px]">اضغط على الزر واهرب فوراً</div>
      <button id="spinBtn" onclick="spinWheel()" class="w-full py-3.5 rounded-2xl bg-red-600 hover:bg-red-500 text-white font-bold text-xs uppercase shadow transition">🎯 لف العجلة الآن</button>
      <div class="text-right">
        <button onclick="toggleTaskManager()" class="text-xs text-gray-400 hover:text-cyan-400 flex items-center gap-1.5 border border-gray-800 px-3 py-2 rounded-xl bg-gray-900">⚙️ تعديل وإضافة مهام العجلة</button>
        <div id="taskManager" class="mt-2 card-bg p-4 rounded-2xl border border-gray-800 hidden space-y-2.5">
          <div id="taskList" class="space-y-2 max-h-48 overflow-y-auto pr-1"></div>
          <div class="flex gap-2 pt-2 border-t border-gray-800">
            <input type="text" id="newTaskInput" placeholder="مهمة هروب جديدة..." class="flex-1 text-xs bg-gray-900 border border-gray-700 rounded-xl px-3 py-2 text-gray-200">
            <button onclick="addTask()" class="text-xs px-4 py-2 bg-cyan-600 text-white rounded-xl font-bold">إضافة</button>
          </div>
        </div>
      </div>
    </section>

  </main>

<script>
// ================= CONFIG =================
const CONFIG = {
  get TELEGRAM_BOT_TOKEN() { return localStorage.getItem("tg_token") || ""; },
  get TELEGRAM_CHAT_ID() { return localStorage.getItem("tg_chat") || ""; },
  STORAGE_KEY: "hunter_ultimate_v7",
  OLD_STORAGE_KEY: "hunter_ultimate_v6",
  RANKS: ["E-Rank", "D-Rank", "C-Rank", "B-Rank", "A-Rank", "S-Rank"]
};

// ================= STATE =================
function getFormattedDate(d) {
  return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}-${String(d.getDate()).padStart(2, '0')}`;
}
function getTodayKey() { return getFormattedDate(new Date()); }

const escH = s => String(s == null ? '' : s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));

const defaultAzkar = [
  { id: 1, text: "آية الكرسي: ﴿اللَّهُ لَا إِلَٰهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ...﴾", total: 1, current: 1 },
  { id: 2, text: "سورة الإخلاص + المعوذتين (الفلق والناس)", total: 3, current: 3 },
  { id: 3, text: "بِسْمِ اللَّهِ الَّذِي لَا يَضُرُّ مَعَ اسْمِهِ شَيْءٌ فِي الْأَرْضِ وَلَا فِي السَّمَاءِ وَهُوَ السَّمِيعُ الْعَلِيمُ", total: 3, current: 3 },
  { id: 4, text: "أَعُوذُ بِكَلِمَاتِ اللَّهِ التَّامَّاتِ مِنْ شَرِّ مَا خَلَقَ", total: 3, current: 3 },
  { id: 5, text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ أَنْ أُشْرِكَ بِكَ وَأَنَا أَعْلَمُ، وَأَسْتَغْفِرُكَ لِمَا لَا أَعْلَمُ", total: 3, current: 3 },
  { id: 6, text: "يَا حَيُّ يَا قَيُّومُ بِرَحْمَتِكَ أَسْتَغِيثُ أَصْلِحْ لِي شَأْنِي كُلَّهُ وَلَا تَكِلْنِي إِلَى نَفْسِي طَرْفَةَ عَيْنٍ", total: 1, current: 1 },
  { id: 7, text: "سيد الاستغفار: اللَّهُمَّ أَنْتَ رَبِّي لا إِلَهَ إِلا أَنْتَ، خَلَقْتَنِي وَأَنَا عَبْدُكَ...", total: 1, current: 1 },
  { id: 8, text: "حَسْبِـيَ اللّهُ لا إلهَ إلّا هُوَ عَلَـيهِ تَوَكَّـلتُ وَهُوَ رَبُّ العَرْشِ العَظـيم", total: 7, current: 7 },
  { id: 9, text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ الْهَمِّ وَالْحَزَنِ، وَأَعُوذُ بِكَ مِنْ الْعَجْزِ وَالْكَسَلِ...", total: 3, current: 3 }
];

const defaultDuas = [
  { id: 1, text: "«اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ شَرِّ سَمْعِي، وَمِنْ شَرِّ بَصَرِي، وَمِنْ شَرِّ لِسَانِي، وَمِنْ شَرِّ قَلْبِي، وَمِنْ شَرِّ مَنِيِّي»", done: false },
  { id: 2, text: "«اللهم إنك تعلم بحالي، وتعلم ما يصلح حالي، اللهم إنك تعلم من ضرني وتعلم ما يصلح ويذهب ضري، اللهم إني أكل إليك أمري»", done: false },
  { id: 3, text: "«اللَّهُمَّ إِنِّي أَسْأَلُكَ الْهُدَى وَالتُّقَى وَالْعَفَافَ وَالْغِنَى»", done: false },
  { id: 4, text: "«اللَّهُمَّ إِنِّي أَسْأَلُكَ مِنْ فَضْلِكَ وَرَحْمَتِكَ فَإِنَّهُ لا يَمْلِكُهَا إِلا أَنْتَ»", done: false },
  { id: 5, text: "«لَا إِلَهَ إِلَّا أَنْتَ سُبْحَانَكَ إِنِّي كُنْتُ مِنَ الظَّالِمِينَ»", done: false }
];

const defaultWheelPlans = [
  "اغسل وشك بماية مثلجة فوراً 🧊",
  "انزل اتمشى ربع ساعة 🚶‍♂️",
  "اتصل بصديق ثقة احكيله 📞",
  "اعمل 15 عدة ضغط حالاً 💪",
  "اتوضى وصلّي ركعتين 🤲",
  "تمارين تنفس 3 دقائق 🧘"
];

let state = {
  name: "Mostafa Abdelrahman",
  level: 1,
  streak: 0,
  penaltyText: "1000 استغفار",
  penaltyActive: false,
  lastActiveDate: getTodayKey(),
  activeRoutine: "day1",
  history: {},
  questHistory: {},
  recoveryStart: getFormattedDate(new Date()),
  recoveryPenaltyDays: 0,
  routines: {
    day1: [
      { id: 101, name: "Push-ups", current: 0, target: 100 },
      { id: 102, name: "Sit-ups", current: 0, target: 100 },
      { id: 103, name: "Squats", current: 0, target: 100 }
    ],
    day2: [
      { id: 201, name: "Pull-ups", current: 0, target: 30 },
      { id: 202, name: "Plank (sec)", current: 0, target: 120 },
      { id: 203, name: "Lunges", current: 0, target: 60 }
    ]
  },
  azkar: defaultAzkar,
  duas: defaultDuas,
  wheelPlans: defaultWheelPlans,
  homeOrder: ['workouts', 'dayTracker', 'recoveryCounter', 'recovery', 'wheel'],
  homeCustom: {}
};

function loadData() {
  const saved = localStorage.getItem(CONFIG.STORAGE_KEY);
  if (saved) {
    try { state = Object.assign(state, JSON.parse(saved)); } catch (e) {}
  } else {
    const v2 = localStorage.getItem(CONFIG.OLD_STORAGE_KEY);
    if (v2) { try { state = Object.assign(state, JSON.parse(v2)); } catch (e) {} }
  }
  checkDayTransition();
  recalculateStreakAndLevel();
  calculateRecoveryTime();
  renderAll();
  applyHomeCustom();
  applyHomeOrder();
}

function saveData() { localStorage.setItem(CONFIG.STORAGE_KEY, JSON.stringify(state)); }

function renderAll() {
  renderWorkouts(); renderAzkar(); renderDuas(); renderTasks(); drawWheel(); calculateRecoveryTime(); renderBadges();
  if (typeof renderHabitsView === 'function') renderHabitsView();
  if (typeof renderToday === 'function') renderToday();
}

// ================= تأثيرات التفاعل =================
function fx(e, text) {
  if (navigator.vibrate) navigator.vibrate(30);
  const t = e && e.target ? e.target : null;
  const r = t && t.getBoundingClientRect ? t.getBoundingClientRect() : { left: window.innerWidth / 2, top: window.innerHeight / 2, width: 0 };
  const el = document.createElement('div');
  el.className = 'fx-pop';
  el.textContent = text || '✨';
  el.style.left = (r.left + r.width / 2) + 'px';
  el.style.top = r.top + 'px';
  document.body.appendChild(el);
  setTimeout(() => el.remove(), 950);
}

// ================= التنقل =================
function showToast(msg) {
  const t = document.createElement('div');
  t.className = 'fixed bottom-5 left-1/2 -translate-x-1/2 bg-amber-500 text-black px-4 py-2 rounded-xl font-bold text-xs shadow-lg z-50 animate-bounce';
  t.innerText = msg;
  document.body.appendChild(t);
  setTimeout(() => t.remove(), 3000);
}

function showView(view) {
  ['home', 'workouts', 'recovery', 'wheel', 'habits', 'recoveryCounterView'].forEach(v => {
    const el = document.getElementById(`view-${v}`);
    if (el) el.classList.add('hidden');
  });
  const target = document.getElementById(`view-${view}`);
  if (target) target.classList.remove('hidden');
  if (view === 'wheel') drawWheel();
  if (view === 'home' && typeof renderToday === 'function') renderToday();
  if (view === 'recovery') { renderAzkar(); renderDuas(); }
  if (view === 'workouts') renderWorkouts();
  if (view === 'habits' && typeof renderHabitsView === 'function') renderHabitsView();
  if (view === 'recoveryCounterView') calculateRecoveryTime();
}

function openDayTrackerFromHome() {
  showView('habits');
  if (typeof setMainTab === 'function') setMainTab('day');
}

// ================= الأوسمة ودورة الـ 90 يوم =================
const badgesData = {
  badges: [
    { title: "وسام الأمل", days: 3, icon: "🔑", desc: "بداية الانطلاقة الحقيقية" },
    { title: "وسام القرار", days: 7, icon: "💎", desc: "أسبوع من الصمود الكامل" },
    { title: "وسام التقدم", days: 14, icon: "⚔️", desc: "أسبوعين من الثبات" },
    { title: "وسام الصبر", days: 21, icon: "⏳", desc: "21 يوم لتكوين العادة" },
    { title: "وسام البناء", days: 30, icon: "🛡️", desc: "شهر كامل من البناء" },
    { title: "وسام النور", days: 50, icon: "🦅", desc: "منتصف الطريق العظيم" },
    { title: "وسام البشائر", days: 75, icon: "🎖️", desc: "75 يوم من الانتصار" },
    { title: "وسام الحكمة", days: 100, icon: "👑", desc: "المائة يوم الأسطورية" }
  ],
  shields: [
    { title: "درع النصر", days: 100, icon: "🛡️", desc: "قوة لا تُقهر" },
    { title: "درع الثبات", days: 200, icon: "🛡️", desc: "صمود أمام كل العواصف" },
    { title: "درع الحرية", days: 300, icon: "⚔️", desc: "الحرية من القيود" },
    { title: "درع الملوك", days: 400, icon: "👑", desc: "رتبة الملوك الأبطال" }
  ],
  cups: [
    { title: "كأس برونزي", days: 30, icon: "🥉", desc: "إنجاز الـ 30 يوم" },
    { title: "كأس فضي", days: 60, icon: "🥈", desc: "إنجاز الشهرين" },
    { title: "كأس ذهبي", days: 90, icon: "🥇", desc: "إنجاز الثلاثة أشهر" },
    { title: "كأس كريستالي", days: 180, icon: "🏆", desc: "نصف سنة كاملة" },
    { title: "كأس ناري", days: 270, icon: "🔥", desc: "شجاعة وإصرار متواصل" },
    { title: "كأس ألماس", days: 365, icon: "💎", desc: "سنة كاملة من المجد" }
  ],
  certs: [
    { title: "شهادة 30 يوم", days: 30, icon: "📜", desc: "توثيق أول شهر" },
    { title: "شهادة 60 يوم", days: 60, icon: "📜", desc: "توثيق شهرين تعافي" },
    { title: "شهادة 90 يوم", days: 90, icon: "📜", desc: "توثيق 3 أشهر" },
    { title: "شهادة 180 يوم", days: 180, icon: "📜", desc: "توثيق نصف سنة" },
    { title: "شهادة 270 يوم", days: 270, icon: "📜", desc: "توثيق 9 أشهر" },
    { title: "شهادة 365 يوم", days: 365, icon: "📜", desc: "توثيق سنة كاملة أسطورية" }
  ]
};

let currentBadgeTab = 'badges';

function badgeTab(tab) {
  currentBadgeTab = tab;
  ['badges', 'shields', 'cups', 'certs'].forEach(t => {
    const btn = document.getElementById('btab-' + t);
    if (!btn) return;
    const active = t === tab;
    btn.className = `py-2.5 rounded-xl text-xs font-bold transition border ${active ? 'bg-orange-500 text-black border-orange-400' : 'bg-gray-900 text-gray-300 border-gray-800'}`;
  });
  renderBadges();
}

function getRecoveryTotalHours() {
  if (!state.recoveryStart) state.recoveryStart = getFormattedDate(new Date());
  const start = new Date(state.recoveryStart + 'T00:00:00');
  const now = new Date();
  const diffMs = now - start;
  const totalHours = Math.max(0, diffMs / 3600000) - ((state.recoveryPenaltyDays || 0) * 24);
  return Math.max(0, totalHours);
}

function calculateRecoveryTime() {
  if (!state.recoveryStart) state.recoveryStart = getFormattedDate(new Date());
  const inputEl = document.getElementById("recovery-start-input");
  if (inputEl) inputEl.value = state.recoveryStart;

  const totalH = getRecoveryTotalHours();
  const totalDays = Math.floor(totalH / 24);
  const hours = Math.floor(totalH % 24);
  const mins = Math.floor(((totalH * 60) % 60));
  const secs = Math.floor(((totalH * 3600) % 60));

  const cycleDay = (totalDays % 90) || (totalDays > 0 && totalDays % 90 === 0 ? 90 : 0);
  const cycleNum = Math.floor(totalDays / 90) + 1;

  const fracEl = document.getElementById("rc-days-fraction");
  if (fracEl) fracEl.innerText = `${cycleDay}/90`;

  const cycleText = document.getElementById("rc-cycle-text");
  if (cycleText) cycleText.innerText = `الدورة ${cycleNum} (إجمالي الأيام: ${totalDays})`;

  const hEl = document.getElementById("rc-hours");
  const mEl = document.getElementById("rc-mins");
  const sEl = document.getElementById("rc-secs");
  if (hEl) hEl.innerText = String(hours).padStart(2, '0');
  if (mEl) mEl.innerText = String(mins).padStart(2, '0');
  if (sEl) sEl.innerText = String(secs).padStart(2, '0');
}

function updateRecoveryStart() {
  const inputEl = document.getElementById("recovery-start-input");
  if (inputEl) {
    state.recoveryStart = inputEl.value;
    state.recoveryPenaltyDays = 0;
    saveData();
    calculateRecoveryTime();
    renderBadges();
  }
}

function reportRecoverySlip() {
  if (confirm("الزلة مش نهاية المطاف، كمل بكل قوتك! نخصم يوم؟")) {
    state.recoveryPenaltyDays = (state.recoveryPenaltyDays || 0) + 1;
    saveData();
    calculateRecoveryTime();
    renderBadges();
  }
}

function renderBadges() {
  const container = document.getElementById('badges-content');
  const totalH = getRecoveryTotalHours();
  const curDays = Math.floor(totalH / 24);
  if (!container) return;

  container.innerHTML = '';
  const list = badgesData[currentBadgeTab] || [];

  list.forEach(item => {
    const unlocked = curDays >= item.days;
    const card = document.createElement('div');
    card.className = `p-3.5 rounded-2xl border flex flex-col items-center text-center transition ${unlocked ? 'card-bg border-orange-500/60 shadow-[0_0_10px_rgba(249,115,22,0.2)]' : 'bg-gray-900/30 border-gray-800 opacity-50 grayscale'}`;
    card.innerHTML = `
      <div class="text-3xl mb-1.5 p-2 rounded-2xl ${unlocked ? 'bg-orange-950/80 border border-orange-500/50' : 'bg-gray-800'}">${item.icon}</div>
      <h3 class="text-xs font-bold ${unlocked ? 'text-orange-300' : 'text-gray-400'}">${item.title}</h3>
      <p class="text-[10px] text-gray-400 mt-0.5">${item.desc}</p>
      <div class="mt-2.5 text-[10px] px-2.5 py-0.5 rounded-xl border font-mono ${unlocked ? 'bg-orange-950 text-orange-300 border-orange-500/40' : 'bg-gray-800 text-gray-500 border-gray-700'}">
        ${unlocked ? '✔ تم الفتح' : `متبقي ${item.days - curDays} يوم`}
      </div>
    `;
    container.appendChild(card);
  });
}

// ================= ترتيب وتعديل الرئيسية =================
let isHomeOrdering = false;
let isHomeEditing = false;

function toggleHomeOrderMode() {
  if (isHomeEditing) toggleHomeEditMode();
  isHomeOrdering = !isHomeOrdering;
  const btn = document.getElementById('home-order-btn');
  btn.innerText = isHomeOrdering ? '✔ تم' : '↕ ترتيب';
  document.querySelectorAll('#home-buttons-container [data-home-key]').forEach(card => {
    const arrows = card.querySelector('.order-arrows');
    if (arrows) arrows.classList.toggle('hidden', !isHomeOrdering);
  });
}

function toggleHomeEditMode() {
  if (isHomeOrdering) toggleHomeOrderMode();
  isHomeEditing = !isHomeEditing;
  const btn = document.getElementById('home-edit-btn');
  btn.innerText = isHomeEditing ? '✔ تم' : '⚙️ تعديل';
  document.querySelectorAll('#home-buttons-container [data-home-key]').forEach(card => {
    const editBtn = card.querySelector('.edit-btn');
    if (editBtn) editBtn.classList.toggle('hidden', !isHomeEditing);
  });
}

function moveHomeItem(key, dir) {
  if (!state.homeOrder) state.homeOrder = ['workouts', 'dayTracker', 'recoveryCounter', 'recovery', 'wheel'];
  const idx = state.homeOrder.indexOf(key);
  const targetIdx = idx + dir;
  if (targetIdx < 0 || targetIdx >= state.homeOrder.length) return;
  [state.homeOrder[idx], state.homeOrder[targetIdx]] = [state.homeOrder[targetIdx], state.homeOrder[idx]];
  saveData();
  applyHomeOrder();
}

function applyHomeOrder() {
  const container = document.getElementById('home-buttons-container');
  if (!container || !state.homeOrder) return;
  state.homeOrder.forEach(key => {
    const card = container.querySelector(`[data-home-key="${key}"]`);
    if (card) container.appendChild(card);
  });
}

function editHomeItem(key) {
  if (!state.homeCustom) state.homeCustom = {};
  const current = state.homeCustom[key] || {};
  const card = document.querySelector(`[data-home-key="${key}"]`);
  const defaultTitle = card.querySelector('.hb-title').innerText;
  const defaultDesc = card.querySelector('.hb-desc') ? card.querySelector('.hb-desc').innerText : '';
  const defaultIcon = card.querySelector('.hb-icon') ? card.querySelector('.hb-icon').innerText : '';

  const newIcon = prompt("أدخل الأيقونة (إيموجي):", current.icon || defaultIcon);
  if (newIcon === null) return;
  const newTitle = prompt("أدخل العنوان الجديد:", current.title || defaultTitle);
  if (newTitle === null) return;
  const newDesc = prompt("أدخل الوصف الجديد:", current.desc || defaultDesc);
  if (newDesc === null) return;

  state.homeCustom[key] = { icon: newIcon.trim(), title: newTitle.trim(), desc: newDesc.trim() };
  saveData();
  applyHomeCustom();
}

function applyHomeCustom() {
  if (!state.homeCustom) return;
  Object.keys(state.homeCustom).forEach(key => {
    const card = document.querySelector(`[data-home-key="${key}"]`);
    if (!card) return;
    const c = state.homeCustom[key];
    const iconEl = card.querySelector('.hb-icon');
    const titleEl = card.querySelector('.hb-title');
    const descEl = card.querySelector('.hb-desc');
    if (iconEl && c.icon) iconEl.innerText = c.icon;
    if (titleEl && c.title) titleEl.innerText = c.title;
    if (descEl && c.desc) descEl.innerText = c.desc;
  });
}

function recTab(name) {
  ['adhkar', 'beliefs', 'duaa', 'journal'].forEach(n => {
    document.getElementById('pane-' + n).classList.toggle('hidden', n !== name);
    document.getElementById('rtab-' + n).className = 'py-2.5 rounded-xl border text-[11px] font-bold transition ' +
      (n === name ? 'bg-emerald-950 border-emerald-400 text-emerald-300' : 'bg-gray-900 border-gray-800 text-gray-400');
  });
}
// ================= WORKOUTS =================
function calculateWeeklyAverage(questId) {
  let totalReps = 0, daysDone = 0;
  const today = new Date();
  for (let i = 0; i < 7; i++) {
    const d = new Date(); d.setDate(today.getDate() - i);
    const key = getFormattedDate(d);
    const reps = state.questHistory && state.questHistory[key] ? state.questHistory[key][questId] : 0;
    if (reps > 0) { totalReps += reps; daysDone++; }
  }
  return { avg: daysDone ? (totalReps / daysDone).toFixed(1) : "0", days: daysDone };
}

function checkDayTransition() {
  const today = getTodayKey();
  if (!state.lastActiveDate) { state.lastActiveDate = today; saveData(); return false; }
  if (state.lastActiveDate === today) return false;
  const d = new Date(state.lastActiveDate + 'T12:00:00');
  const end = new Date(today + 'T12:00:00');
  for (; d < end; d.setDate(d.getDate() + 1)) {
    const s = state.history[getFormattedDate(d)];
    if (!(s === 'completed' || s === 'rest' || s === true)) { state.penaltyActive = true; state.streak = 0; break; }
  }
  Object.values(state.routines || {}).forEach(r => r.forEach(q => { q.current = 0; q.sets = []; }));
  (state.azkar || []).forEach(z => z.current = z.total);
  (state.duas || []).forEach(x => x.done = false);
  state.lastActiveDate = today;
  saveData();
  return true;
}

function recalculateStreakAndLevel() {
  let currentStreak = 0;
  const checkDate = new Date();
  if (state.history[getFormattedDate(checkDate)]) currentStreak++;
  checkDate.setDate(checkDate.getDate() - 1);
  while (true) {
    const key = getFormattedDate(checkDate);
    if (state.history[key]) { currentStreak++; checkDate.setDate(checkDate.getDate() - 1); }
    else break;
  }
  state.streak = currentStreak;
  state.level = 1 + Math.floor(state.streak / 7);
}

function isTodayRest() { return state.history[getTodayKey()] === 'rest'; }
function toggleTodayRest() {
  const k = getTodayKey();
  if (!state.questHistory) state.questHistory = {};
  if (state.history[k] === 'rest') {
    delete state.history[k];
    delete state.questHistory[k];
    Object.values(state.routines).forEach(r => r.forEach(q => { q.current = 0; q.sets = []; }));
  } else {
    state.history[k] = 'rest';
    state.penaltyActive = false;
  }
  recalculateStreakAndLevel(); saveData(); renderWorkouts();
}

function switchRoutine(r) { state.activeRoutine = r; saveData(); renderWorkouts(); }

function fmtHMS(s) {
  s = Math.max(0, Math.floor(s));
  return [Math.floor(s / 3600), Math.floor((s % 3600) / 60), s % 60].map(n => String(n).padStart(2, '0')).join(':');
}
function workoutElapsed() { return state.workoutTimer ? (Date.now() - state.workoutTimer.start) / 1000 : 0; }

function toggleWorkoutTimer(e) { if (state.workoutTimer) stopWorkout(e); else startWorkout(e); }
function startWorkout(e) { state.workoutTimer = { start: Date.now() }; fx(e, '▶ يلا!'); saveData(); renderWorkoutTimer(); }
function stopWorkout(e, silent) {
  if (!state.workoutTimer) return 0;
  const sec = Math.round(workoutElapsed());
  const k = getTodayKey();
  if (!state.workoutTimes) state.workoutTimes = {};
  state.workoutTimes[k] = (state.workoutTimes[k] || 0) + sec;
  state.workoutTimer = null;
  if (!silent) fx(e, '⏱ ' + fmtHMS(sec));
  saveData(); renderWorkoutTimer(); return sec;
}

function renderWorkoutTimer() {
  const disp = document.getElementById('wt-display');
  if (!disp) return;
  const btn = document.getElementById('wt-btn'), info = document.getElementById('wt-info');
  const times = state.workoutTimes || {};
  const todayTotal = times[getTodayKey()] || 0;
  const running = !!state.workoutTimer;
  disp.innerText = fmtHMS(running ? workoutElapsed() : todayTotal);
  const vals = [];
  for (let i = 0; i < 7; i++) {
    const d = new Date(); d.setDate(d.getDate() - i);
    const v = times[getFormattedDate(d)];
    if (v) vals.push(v);
  }
  const avg = vals.length ? Math.round(vals.reduce((a, b) => a + b, 0) / vals.length / 60) : 0;
  info.innerText = `إجمالي اليوم: ${fmtHMS(todayTotal)} • متوسط 7 أيام: ${avg} دقيقة`;
  if (running) {
    btn.className = "px-4 py-2.5 rounded-xl text-xs font-bold bg-red-600 hover:bg-red-500 text-white animate-pulse";
    btn.innerText = "⏹ إنهاء التمرين";
  } else {
    btn.className = "px-4 py-2.5 rounded-xl text-xs font-bold bg-orange-600 hover:bg-orange-500 text-white";
    btn.innerText = "▶ ابدأ التمرين";
  }
}

function tickWorkoutTimer() {
  if (!state.workoutTimer) return;
  const disp = document.getElementById('wt-display');
  if (disp) disp.innerText = fmtHMS(workoutElapsed());
}

function setsHTML(q, dis) {
  const prevSets = getPreviousQuestSets(q.id);
  const cols = "grid grid-cols-[28px_1fr_70px_36px_20px] gap-1.5 items-center";
  const rows = (q.sets || []).map((s, i) => {
    const prevVal = prevSets[i] != null ? prevSets[i] : '—';
    return `
      <div class="${cols} text-xs">
        <span class="text-gray-400 text-center">${i + 1}</span>
        <span class="text-gray-500 text-center font-mono">${prevVal}</span>
        <input type="number" inputmode="numeric" min="0" value="${s.reps}" ${dis} onchange="setReps(${q.id}, ${i}, this.value)" class="w-full text-center bg-gray-800 border border-gray-700 rounded-xl py-1 text-gray-100 disabled:opacity-40">
        <button onclick="toggleSet(${q.id}, ${i}, event)" ${dis} class="py-1 rounded-xl transition ${s.done ? 'bg-cyan-500 text-black font-bold' : 'bg-gray-800 text-gray-400 border border-gray-700'} disabled:opacity-40">✔</button>
        <button onclick="delSet(${q.id}, ${i})" ${dis} class="text-gray-600 hover:text-red-400 text-xs disabled:opacity-40">✕</button>
      </div>`;
  }).join('');
  return `
    <div class="mt-2.5 pt-2.5 border-t border-gray-800 space-y-2">
      <div class="${cols} text-[10px] text-gray-500 text-center"><span>SET</span><span>PREV</span><span>REPS</span><span>✔</span><span></span></div>
      ${rows}
      <button onclick="addSet(${q.id})" ${dis} class="w-full text-xs text-cyan-400 py-1.5 rounded-xl bg-cyan-950/40 border border-cyan-500/30 disabled:opacity-40">+ ADD SET</button>
    </div>`;
}

function getPreviousQuestSets(questId) {
  const today = getTodayKey();
  const rec = state.lastSetsRecord || {};
  const keys = Object.keys(rec).filter(k => k < today).sort().reverse();
  for (const k of keys) if (rec[k][questId]) return rec[k][questId];
  return (state.lastSets && state.lastSets[questId]) || [];
}

function addSet(id) {
  const q = findQuest(id); if (!q) return;
  if (!q.sets) q.sets = [];
  const prev = getPreviousQuestSets(id);
  const i = q.sets.length;
  const reps = prev[i] != null ? prev[i] : (i ? q.sets[i - 1].reps : 10);
  q.sets.push({ reps, done: false });
  saveData(); renderWorkouts();
}

function setReps(id, i, v) {
  const q = findQuest(id); if (!q || !q.sets || !q.sets[i]) return;
  const s = q.sets[i];
  const n = Math.max(0, parseInt(v, 10) || 0);
  if (s.done) q.current = Math.max(0, q.current + n - s.reps);
  s.reps = n; saveData(); renderWorkouts();
}

function toggleSet(id, i, e) {
  if (state.penaltyActive || isTodayRest()) return;
  const q = findQuest(id); if (!q || !q.sets || !q.sets[i]) return;
  const s = q.sets[i]; s.done = !s.done;
  if (s.done) { fx(e, '💪 +' + s.reps); q.current += s.reps; }
  else q.current = Math.max(0, q.current - s.reps);
  saveData(); renderWorkouts();
}

function delSet(id, i) {
  const q = findQuest(id); if (!q || !q.sets || !q.sets[i]) return;
  if (q.sets[i].done) q.current = Math.max(0, q.current - q.sets[i].reps);
  q.sets.splice(i, 1); saveData(); renderWorkouts();
}

function renderWorkouts() {
  document.getElementById("hunter-name").innerText = state.name + " ✏";
  document.getElementById("top-user-name").innerText = state.name;
  const rankIndex = Math.min(Math.floor((state.level - 1) / 2), CONFIG.RANKS.length - 1);
  document.getElementById("hunter-rank-level").innerText = `${CONFIG.RANKS[rankIndex].toUpperCase()} HUNTER | LEVEL ${state.level}`;
  document.getElementById("streak-count").innerText = state.streak;

  const dayInWeek = (state.streak % 7) + 1;
  document.getElementById("streak-bar").style.width = `${Math.min(100, Math.floor(((state.streak % 7) / 7) * 100))}%`;

  const restActive = isTodayRest();
  const statusText = document.getElementById("weekly-status-text");
  if (restActive) statusText.innerHTML = `<span class="text-green-400 font-bold">RECOVERY DAY 🌿</span>`;
  else statusText.innerText = `Day ${dayInWeek} of 7 (Level Progress)`;

  const restBanner = document.getElementById("rest-day-banner");
  const restBtn = document.getElementById("rest-toggle-btn");
  if (restActive) {
    restBanner.classList.remove("hidden");
    restBtn.className = "px-3 py-1.5 bg-green-950 border border-green-400 text-green-300 rounded-xl font-semibold text-xs";
    restBtn.innerText = "🌿 Rest Active";
  } else {
    restBanner.classList.add("hidden");
    restBtn.className = "px-3 py-1.5 bg-gray-900 border border-green-700 text-green-400 rounded-xl font-semibold text-xs";
    restBtn.innerText = "🌿 Rest Day";
  }

  const on = "px-3.5 py-2 rounded-xl text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400";
  const off = "px-3.5 py-2 rounded-xl text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400";
  document.getElementById("tab-day1").className = state.activeRoutine === 'day1' ? on : off;
  document.getElementById("tab-day2").className = state.activeRoutine === 'day1' ? off : on;

  document.getElementById("penalty-task-text").innerText = state.penaltyText;
  const penaltyEl = document.getElementById("penalty-card");
  if (state.penaltyActive && !restActive) penaltyEl.classList.remove("hidden");
  else penaltyEl.classList.add("hidden");

  renderCalendar(); renderWorkoutTimer();

  const listEl = document.getElementById("quest-list");
  listEl.innerHTML = "";
  const todayKey = getTodayKey();
  const doneToday = state.history[todayKey] === 'completed' || state.history[todayKey] === true;
  const quests = state.routines[state.activeRoutine] || [];
  const dis = state.penaltyActive || doneToday || restActive ? 'disabled' : '';

  quests.forEach((q, index) => {
    const pct = Math.min(100, Math.floor((q.current / q.target) * 100));
    const wa = calculateWeeklyAverage(q.id);
    const card = document.createElement("div");
    card.className = `card-bg p-4 rounded-2xl border transition ${pct >= 100 ? "border-cyan-500/70" : "border-gray-800"}`;
    card.innerHTML = `
      <div class="flex justify-between items-center mb-1.5">
        <div class="flex items-center gap-2">
          <span class="font-bold text-xs text-gray-200">${escH(q.name)}</span>
          <button onclick="editQuestName(${q.id})" class="text-[10px] text-gray-400 hover:text-cyan-400">✏️</button>
        </div>
        <div class="flex items-center gap-1.5">
          <button onclick="moveQuest(${index}, -1)" class="text-xs px-1.5 py-0.5 bg-gray-800 text-gray-400 rounded-lg">▲</button>
          <button onclick="moveQuest(${index}, 1)" class="text-xs px-1.5 py-0.5 bg-gray-800 text-gray-400 rounded-lg">▼</button>
          <button onclick="deleteQuest(${q.id})" class="text-xs text-gray-500 hover:text-red-400 px-1">✕</button>
        </div>
      </div>
      <div class="flex justify-between items-center text-xs text-gray-400 mb-1.5">
        <span>Progress: ${q.current} / <strong onclick="editTarget(${q.id})" class="text-cyan-400 underline cursor-pointer">${q.target}</strong></span>
        <span class="text-cyan-400 font-semibold">${pct}%</span>
      </div>
      <div class="text-[10px] text-gray-400 mb-2 flex justify-between">
        <span class="text-cyan-300 font-mono">📈 متوسط أسبوعي: <strong>${wa.avg}</strong> (في ${wa.days} أيام)</span>
      </div>
      <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden mb-2.5">
        <div class="bg-cyan-400 h-2 transition-all duration-200" style="width: ${pct}%"></div>
      </div>
      <div class="flex justify-end gap-2 text-xs">
        <button onclick="updateQuest(${q.id}, -1)" ${dis} class="px-3 py-1 bg-gray-800 rounded-xl hover:bg-gray-700 text-gray-300 disabled:opacity-30">-1</button>
        <button onclick="updateQuest(${q.id}, 1)" ${dis} class="px-3.5 py-1 bg-gray-800 rounded-xl hover:bg-cyan-900 text-cyan-400 disabled:opacity-30">+1</button>
      </div>
      ${setsHTML(q, dis)}
    `;
    listEl.appendChild(card);
  });

  const btn = document.getElementById("complete-day-btn");
  if (restActive) {
    btn.className = "w-full py-4 rounded-2xl font-bold text-xs uppercase border border-green-500 bg-green-950/40 text-green-400 cursor-not-allowed";
    btn.innerText = "🌿 REST DAY ACTIVE (PROTECTED)";
  } else if (doneToday) {
    btn.className = "w-full py-4 rounded-2xl font-bold text-xs uppercase border border-cyan-700 bg-cyan-950/40 text-cyan-400 cursor-not-allowed opacity-80";
    btn.innerText = "✅ TODAY ALREADY COMPLETED";
  } else if (state.penaltyActive) {
    btn.className = "w-full py-4 rounded-2xl font-bold text-xs uppercase border border-red-900 bg-red-950/30 text-red-400 cursor-not-allowed";
    btn.innerText = "LOCKED (PENALTY ACTIVE)";
  } else {
    btn.className = "w-full py-4 rounded-2xl font-bold text-xs uppercase border border-cyan-400 bg-cyan-500/20 text-cyan-400 hover:bg-cyan-500/30 transition shadow cursor-pointer";
    btn.innerText = "COMPLETE DAY";
  }
  if (typeof renderToday === 'function') renderToday();
}

function renderCalendar() {
  const calEl = document.getElementById("calendar-days");
  calEl.innerHTML = "";
  const now = new Date();
  const year = now.getFullYear(), month = now.getMonth();
  document.getElementById("calendar-month-title").innerText = `📅 ${now.toLocaleString('en-US', { month: 'short', year: 'numeric' }).toUpperCase()}`;
  const firstDay = new Date(year, month, 1).getDay();
  const days = new Date(year, month + 1, 0).getDate();

  for (let i = 0; i < firstDay; i++) calEl.appendChild(document.createElement("div"));
  for (let day = 1; day <= days; day++) {
    const key = getFormattedDate(new Date(year, month, day));
    const status = state.history[key];
    const box = document.createElement("div");
    box.onclick = () => toggleDayStatus(key);
    let borderClass = "border-gray-800 bg-gray-900/40 text-gray-500";
    let icon = "✖";
    if (status === 'rest') { borderClass = "border-green-600/70 bg-green-950/40 text-green-400"; icon = "🌿"; }
    else if (status === 'completed' || status === true) { borderClass = "border-cyan-500 bg-cyan-950/50 text-cyan-400"; icon = "✔"; }
    if (key === getTodayKey()) borderClass += " ring-1 ring-cyan-400";
    box.className = `p-2 rounded-xl cursor-pointer border transition flex flex-col items-center justify-center ${borderClass}`;
    box.innerHTML = `<span class="text-[10px] font-bold">${day}</span><span class="text-[9px] mt-0.5">${icon}</span>`;
    calEl.appendChild(box);
  }
}

function toggleDayStatus(k) {
  if (k > getTodayKey()) return;
  if (!state.questHistory) state.questHistory = {};
  if (!state.history[k]) {
    state.history[k] = 'completed';
  } else if (state.history[k] === 'completed' || state.history[k] === true) {
    state.history[k] = 'rest';
  } else {
    delete state.history[k];
  }
  recalculateStreakAndLevel(); saveData(); renderWorkouts();
}

function findQuest(id) { return state.routines[state.activeRoutine].find(x => x.id === id); }
function updateQuest(id, amt) {
  if (state.penaltyActive || isTodayRest()) return;
  const q = findQuest(id); if (!q) return;
  q.current = Math.max(0, q.current + amt); saveData(); renderWorkouts();
}
function editTarget(id) {
  const q = findQuest(id); if (!q) return;
  const t = prompt("Target:", q.target);
  if (t && parseInt(t) > 0) { q.target = parseInt(t); saveData(); renderWorkouts(); }
}
function editQuestName(id) {
  const q = findQuest(id); if (!q) return;
  const n = prompt("Quest Name:", q.name);
  if (n && n.trim()) { q.name = n.trim(); saveData(); renderWorkouts(); }
}
function moveQuest(index, dir) {
  const list = state.routines[state.activeRoutine];
  const t = index + dir;
  if (t < 0 || t >= list.length) return;
  [list[index], list[t]] = [list[t], list[index]];
  saveData(); renderWorkouts();
}
function openAddQuestModal() {
  const n = prompt(`Enter Quest Name for ${state.activeRoutine.toUpperCase()}:`);
  if (!n) return;
  const t = parseInt(prompt("Enter Target Count:", "100"), 10) || 100;
  state.routines[state.activeRoutine].push({ id: Date.now(), name: n.trim(), current: 0, target: t, sets: [] });
  saveData(); renderWorkouts();
}
function deleteQuest(id) {
  if (confirm("Delete this quest?")) {
    state.routines[state.activeRoutine] = state.routines[state.activeRoutine].filter(x => x.id !== id);
    saveData(); renderWorkouts();
  }
}
function completeDay(e) {
  const todayKey = getTodayKey();
  if (state.history[todayKey] === 'completed') { alert("You already completed your quests for today!"); return; }
  if (isTodayRest()) { alert("Today is a Rest Day!"); return; }
  if (state.routines[state.activeRoutine].some(q => q.current < q.target)) { alert("⚠️ لم تنهِ كل التمارين المطلوبة بعد!"); return; }

  fx(e, '🎉 يوم مكتمل!');
  if (state.workoutTimer) stopWorkout(null, true);

  if (!state.questHistory) state.questHistory = {};
  state.questHistory[todayKey] = {};
  if (!state.lastSetsRecord) state.lastSetsRecord = {};
  state.lastSetsRecord[todayKey] = {};

  state.routines[state.activeRoutine].forEach(q => {
    state.questHistory[todayKey][q.id] = q.current;
    const doneReps = (q.sets || []).map(s => s.reps);
    if (doneReps.length) state.lastSetsRecord[todayKey][q.id] = doneReps;
  });

  state.history[todayKey] = 'completed';
  const prevLevel = state.level;
  recalculateStreakAndLevel(); saveData(); renderWorkouts();

  const wt = (state.workoutTimes && state.workoutTimes[todayKey]) || 0;
  const timeMsg = wt ? `\n⏱ مدة التمرين: ${fmtHMS(wt)}` : '';
  if (state.level > prevLevel) alert(`🔥 [LEVEL UP] وصلت إلى LEVEL ${state.level}!${timeMsg}`);
  else alert(`✅ تم تسجيل اليوم بنجاح! الستريك: ${state.streak} يوم.${timeMsg}`);
}

function editPenaltyText() {
  const t = prompt("تعديل مهمة العقوبة:", state.penaltyText);
  if (t) { state.penaltyText = t; saveData(); renderWorkouts(); }
}
function confirmPenaltyDone() {
  if (confirm("هل أتممت مهمة العقوبة؟")) { state.penaltyActive = false; saveData(); renderWorkouts(); }
}
function editName() {
  const n = prompt("Enter Hunter Name:", state.name);
  if (n && n.trim()) { state.name = n.trim(); saveData(); renderWorkouts(); }
}

// ================= ADHKAR =================
function renderAzkar() {
  const container = document.getElementById("azkarList");
  if (!container) return;
  container.innerHTML = "";
  state.azkar.forEach((item, index) => {
    const isDone = item.current <= 0;
    const div = document.createElement("div");
    div.className = `card-bg p-4 rounded-2xl border transition ${isDone ? 'border-emerald-500/70 bg-emerald-950/25' : 'border-gray-800'}`;
    div.innerHTML = `
      <div class="text-xs text-gray-200 leading-relaxed mb-3">${escH(item.text)}</div>
      <div class="flex justify-between items-center pt-2.5 border-t border-gray-800">
        <button onclick="decrementZekr(${index})" class="px-3.5 py-1.5 rounded-xl text-xs font-bold transition ${isDone ? 'bg-emerald-500 text-black' : 'bg-emerald-950 border border-emerald-500/60 text-emerald-400'}">
          ${isDone ? 'تم الاكتفاء ✔️' : `متبقي: ${item.current} /${item.total}`}
        </button>
        <div class="flex items-center gap-1.5">
          <button onclick="moveZekr(${index}, -1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▲</button>
          <button onclick="moveZekr(${index}, 1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▼</button>
          <button onclick="editZekr(${index})" class="px-2 py-1 bg-gray-800 text-cyan-400 rounded-xl text-xs">✏️</button>
          <button onclick="deleteZekr(${index})" class="px-2 py-1 bg-gray-800 text-red-400 rounded-xl text-xs">✕</button>
        </div>
      </div>
    `;
    container.appendChild(div);
  });
  if (typeof renderToday === 'function') renderToday();
}
function decrementZekr(i) {
  if (state.azkar[i].current > 0) {
    state.azkar[i].current -= 1;
    if (navigator.vibrate) navigator.vibrate(30);
    saveData(); renderAzkar();
  }
}
function resetAzkarCounters() { state.azkar.forEach(x => x.current = x.total); saveData(); renderAzkar(); }
function openAddZekrPrompt() {
  const text = prompt("اكتب نص الذكر الجديد:");
  if (!text || !text.trim()) return;
  const total = parseInt(prompt("عدد التكرار:", "1"), 10) || 1;
  state.azkar.push({ id: Date.now(), text: text.trim(), total, current: total });
  saveData(); renderAzkar();
}
function editZekr(i) {
  const item = state.azkar[i];
  const newText = prompt("تعديل نص الذكر:", item.text);
  if (newText && newText.trim()) {
    const newTotal = parseInt(prompt("تعديل التكرار:", item.total), 10) || 1;
    item.text = newText.trim(); item.total = newTotal; item.current = newTotal;
    saveData(); renderAzkar();
  }
}
function deleteZekr(i) {
  if (confirm("هل تريد حذف هذا الذكر؟")) { state.azkar.splice(i, 1); saveData(); renderAzkar(); }
}
function moveZekr(i, dir) {
  const t = i + dir;
  if (t < 0 || t >= state.azkar.length) return;
  [state.azkar[i], state.azkar[t]] = [state.azkar[t], state.azkar[i]];
  saveData(); renderAzkar();
}

// ================= DUAS =================
function renderDuas() {
  const container = document.getElementById("duaaList");
  if (!container) return;
  container.innerHTML = "";
  state.duas.forEach((d, index) => {
    const div = document.createElement("div");
    div.className = `card-bg p-4 rounded-2xl border transition ${d.done ? 'border-blue-500/80 bg-blue-950/25' : 'border-gray-800'}`;
    div.innerHTML = `
      <div class="text-xs text-blue-100 leading-relaxed mb-3">${escH(d.text)}</div>
      <div class="flex justify-between items-center pt-2.5 border-t border-gray-800">
        <button onclick="toggleDuaCheck(${index})" class="px-3.5 py-1.5 rounded-xl text-xs font-bold transition ${d.done ? 'bg-blue-500 text-black' : 'bg-gray-800 text-blue-300 border border-blue-500/40'}">
          ${d.done ? '✔ تم الدعاء' : 'وضع علامة صح ✔'}
        </button>
        <div class="flex items-center gap-1.5">
          <button onclick="moveDua(${index}, -1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▲</button>
          <button onclick="moveDua(${index}, 1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▼</button>
          <button onclick="editDua(${index})" class="px-2 py-1 bg-gray-800 text-cyan-400 rounded-xl text-xs">✏️</button>
          <button onclick="deleteDua(${index})" class="px-2 py-1 bg-gray-800 text-red-400 rounded-xl text-xs">✕</button>
        </div>
      </div>
    `;
    container.appendChild(div);
  });
  if (typeof renderToday === 'function') renderToday();
}
function toggleDuaCheck(i) {
  state.duas[i].done = !state.duas[i].done;
  if (state.duas[i].done && navigator.vibrate) navigator.vibrate(30);
  saveData(); renderDuas();
}
function resetDuaaChecks() { state.duas.forEach(d => d.done = false); saveData(); renderDuas(); }
function openAddDuaaPrompt() {
  const text = prompt("أدخل نص الدعاء الجديد:");
  if (text && text.trim()) { state.duas.push({ id: Date.now(), text: text.trim(), done: false }); saveData(); renderDuas(); }
}
function editDua(i) {
  const t = prompt("تعديل نص الدعاء:", state.duas[i].text);
  if (t && t.trim()) { state.duas[i].text = t.trim(); saveData(); renderDuas(); }
}
function deleteDua(i) {
  if (confirm("هل تريد حذف هذا الدعاء؟")) { state.duas.splice(i, 1); saveData(); renderDuas(); }
}
function moveDua(i, dir) {
  const t = i + dir;
  if (t < 0 || t >= state.duas.length) return;
  [state.duas[i], state.duas[t]] = [state.duas[t], state.duas[i]];
  saveData(); renderDuas();
}

// ================= WHEEL =================
const wheelColors = ["#0284c7", "#16a34a", "#d97706", "#dc2626", "#7c3aed", "#059669", "#ea580c", "#4f46e5"];
let currentWheelAngle = 0;
let isWheelSpinning = false;

function drawWheel() {
  const canvas = document.getElementById("wheelCanvas");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  const n = state.wheelPlans.length;
  if (n === 0) return;
  const seg = (2 * Math.PI) / n;
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.lineWidth = 1; ctx.strokeStyle = "#0f172a";

  for (let i = 0; i < n; i++) {
    const start = i * seg + currentWheelAngle;
    ctx.beginPath();
    ctx.moveTo(250, 250);
    ctx.arc(250, 250, 240, start, start + seg);
    ctx.fillStyle = wheelColors[i % wheelColors.length];
    ctx.fill(); ctx.stroke();

    ctx.save();
    ctx.translate(250, 250);
    ctx.rotate(start + seg / 2);
    ctx.textAlign = "right";
    ctx.fillStyle = "#fff";
    ctx.font = "bold 18px system-ui";
    const t = state.wheelPlans[i];
    ctx.fillText(t.length > 18 ? t.substring(0, 16) + "..." : t, 220, 6);
    ctx.restore();
  }

  ctx.beginPath();
  ctx.arc(250, 250, 25, 0, 2 * Math.PI);
  ctx.fillStyle = "#0f172a";
  ctx.fill(); ctx.strokeStyle = "#fff"; ctx.lineWidth = 3; ctx.stroke();
}

function spinWheel() {
  if (isWheelSpinning || state.wheelPlans.length === 0) return;
  isWheelSpinning = true;
  document.getElementById('spinBtn').disabled = true;
  document.getElementById('spinResult').innerText = "العجلة تدور بأقصى سرعة...";

  const duration = 3500;
  const start = performance.now();
  const rounds = (Math.PI * 2) * (5 + Math.random() * 3);
  const startAngle = currentWheelAngle;

  function animate(time) {
    const p = Math.min(1, (time - start) / duration);
    currentWheelAngle = startAngle + rounds * (1 - Math.pow(1 - p, 3));
    drawWheel();
    if (p < 1) requestAnimationFrame(animate);
    else {
      isWheelSpinning = false;
      document.getElementById('spinBtn').disabled = false;
      determineWinner();
    }
  }
  requestAnimationFrame(animate);
}

function determineWinner() {
  const n = state.wheelPlans.length;
  const seg = (2 * Math.PI) / n;
  const a = (1.5 * Math.PI - (currentWheelAngle % (2 * Math.PI)) + (2 * Math.PI)) % (2 * Math.PI);
  document.getElementById('spinResult').innerText = "المهمة: " + state.wheelPlans[Math.floor(a / seg)];
  if (navigator.vibrate) navigator.vibrate([100, 50, 100]);
}

function toggleTaskManager() { document.getElementById("taskManager").classList.toggle("hidden"); }

function renderTasks() {
  const list = document.getElementById("taskList");
  if (!list) return;
  list.innerHTML = "";
  state.wheelPlans.forEach((task, idx) => {
    const div = document.createElement("div");
    div.className = "flex justify-between items-center bg-gray-900 border border-gray-800 p-2.5 rounded-xl text-xs";
    div.innerHTML = `
      <span class="text-gray-200">${escH(task)}</span>
      <div class="flex gap-1.5">
        <button onclick="editTask(${idx})" class="px-2 py-1 bg-gray-800 text-cyan-400 rounded-lg">✏️</button>
        <button onclick="removeTask(${idx})" class="px-2 py-1 bg-red-950 text-red-400 rounded-lg">✕</button>
      </div>
    `;
    list.appendChild(div);
  });
}
function addTask() {
  const input = document.getElementById("newTaskInput");
  const val = input.value.trim();
  if (val) { state.wheelPlans.push(val); input.value = ""; saveData(); renderTasks(); drawWheel(); }
}
function editTask(idx) {
  const t = prompt("تعديل مهمة الهروب:", state.wheelPlans[idx]);
  if (t && t.trim()) { state.wheelPlans[idx] = t.trim(); saveData(); renderTasks(); drawWheel(); }
}
function removeTask(idx) {
  if (state.wheelPlans.length <= 2) { alert("يجب بقاء خيارين على الأقل في العجلة!"); return; }
  state.wheelPlans.splice(idx, 1); saveData(); renderTasks(); drawWheel();
}
// ================= TELEGRAM =================
let mediaRecorder = null;
let audioChunks = [];
let isRecording = false;

const TG_API = () => `https://api.telegram.org/bot${CONFIG.TELEGRAM_BOT_TOKEN}`;

function setupTelegram() {
  const t = prompt("Bot Token:", CONFIG.TELEGRAM_BOT_TOKEN);
  if (t === null) return;
  const c = prompt("Chat ID:", CONFIG.TELEGRAM_CHAT_ID);
  if (c === null) return;
  localStorage.setItem("tg_token", t.trim());
  localStorage.setItem("tg_chat", c.trim());
  alert("✅ تم الحفظ على جهازك");
}

function hasTelegramConfig() {
  if (CONFIG.TELEGRAM_BOT_TOKEN && CONFIG.TELEGRAM_CHAT_ID) return true;
  alert("اضغط ⚙️ إعداد تليجرام الأول وحط التوكن والـ chat id.");
  return false;
}

async function toggleRecord() {
  const btn = document.getElementById('recBtn');
  const status = document.getElementById('rec-status');

  if (!isRecording) {
    if (!hasTelegramConfig()) return;
    try {
      const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
      mediaRecorder = new MediaRecorder(stream);
      audioChunks = [];
      mediaRecorder.ondataavailable = e => audioChunks.push(e.data);

      mediaRecorder.onstop = async () => {
        stream.getTracks().forEach(t => t.stop());
        const mime = mediaRecorder.mimeType || 'audio/webm';
        const blob = new Blob(audioChunks, { type: mime });
        const audio = document.createElement('audio');
        audio.controls = true;
        audio.src = URL.createObjectURL(blob);
        audio.className = "w-full h-8 mt-1";
        document.getElementById('audioList').prepend(audio);

        status.innerText = "⏳ جاري الإرسال لتليجرام...";
        await sendAudioToTelegram(blob, mime);
        status.innerText = "جاهز للتسجيل";
        btn.innerText = "بدء التسجيل ⏺";
        btn.className = "px-4 py-2 rounded-xl bg-blue-600 hover:bg-blue-500 text-white font-bold text-xs transition";
      };

      mediaRecorder.start();
      isRecording = true;
      btn.innerText = "⏹ إيقاف وإرسال";
      btn.className = "px-4 py-2 rounded-xl bg-red-600 hover:bg-red-500 text-white font-bold text-xs transition animate-pulse";
      status.innerText = "جارِ تسجيل صوتك...";
    } catch (err) {
      alert("يرجى منح إذن المايكروفون من إعدادات المتصفح أو تطبيق الموبايل.");
    }
  } else {
    mediaRecorder.stop();
    isRecording = false;
  }
}

async function sendAudioToTelegram(blob, mime) {
  let method, field, filename;
  if (mime.includes("ogg")) { method = "sendVoice"; field = "voice"; filename = "journal.ogg"; }
  else if (mime.includes("mp4")) { method = "sendAudio"; field = "audio"; filename = "journal.m4a"; }
  else { method = "sendDocument"; field = "document"; filename = "journal.webm"; }

  const fd = new FormData();
  fd.append("chat_id", CONFIG.TELEGRAM_CHAT_ID);
  fd.append(field, blob, filename);
  fd.append("caption", "🎙️ يوميات صوتية جديدة: " + new Date().toLocaleDateString('ar-EG'));
  try {
    const res = await fetch(`${TG_API()}/${method}`, { method: "POST", body: fd });
    const data = await res.json();
    if (data.ok) alert("🚀 تم إرسال التسجيل لتليجرام بنجاح!");
    else alert("خطأ تليجرام: " + data.description);
  } catch (e) {
    alert("تعذر الاتصال بتليجرام، تأكد من اتصال الإنترنت.");
  }
}

async function sendPhotoToTelegram(fileInput) {
  const file = fileInput.files[0];
  if (!file) return;
  if (!hasTelegramConfig()) { fileInput.value = ""; return; }
  const status = document.getElementById('photoStatus');
  status.innerText = "⏳ جاري رفع وإرسال الصورة لتليجرام...";

  const fd = new FormData();
  fd.append("chat_id", CONFIG.TELEGRAM_CHAT_ID);
  fd.append("photo", file);
  fd.append("caption", "📸 توثيق وإنجاز جديد: " + new Date().toLocaleDateString('ar-EG'));
  try {
    const res = await fetch(`${TG_API()}/sendPhoto`, { method: "POST", body: fd });
    const data = await res.json();
    if (data.ok) {
      status.innerText = "✔️ تم إرسال الصورة بنجاح لتليجرام!";
      setTimeout(() => { status.innerText = ""; }, 4000);
    } else {
      status.innerText = "❌ خطأ تليجرام: " + data.description;
    }
  } catch (err) {
    status.innerText = "❌ تعذر الاتصال بالإنترنت.";
  }
  fileInput.value = "";
}

// ================= EXPORT / IMPORT =================
function exportData() {
  const a = document.createElement('a');
  a.href = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(state, null, 2));
  a.download = `hunter_ultimate_backup_${getTodayKey()}.json`;
  a.click();
}
function importData(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    try {
      state = Object.assign(state, JSON.parse(ev.target.result));
      saveData();
      alert("✅ تم استيراد كل بياناتك بنجاح!");
      location.reload();
    } catch (err) { alert("خطأ في قراءة ملف النسخة الاحتياطية."); }
  };
  reader.readAsText(file);
  e.target.value = "";
}

// ================= TIMER + START =================
function updateTimer() {
  const now = new Date();
  const midnight = new Date(now); midnight.setHours(24, 0, 0, 0);
  const diff = midnight - now;
  if (checkDayTransition()) { recalculateStreakAndLevel(); renderAll(); }
  if (typeof tickWorkoutTimer === 'function') tickWorkoutTimer();
  if (typeof calculateRecoveryTime === 'function') calculateRecoveryTime();

  const h = String(Math.floor((diff / 3600000) % 24)).padStart(2, '0');
  const m = String(Math.floor((diff / 60000) % 60)).padStart(2, '0');
  const s = String(Math.floor((diff / 1000) % 60)).padStart(2, '0');
  const el = document.getElementById("countdown");
  if (el) el.innerText = `${h}:${m}:${s}`;
}

if (navigator.storage && navigator.storage.persist) navigator.storage.persist();
setInterval(updateTimer, 1000);
updateTimer();
loadData();

// ===== المعتقدات =====
(function () {
  if (!state.beliefs) {
    state.beliefs = [
      { id: 1, text: "مهمتك 24 ساعة بس" },
      { id: 2, text: "أنت بتبطّل عشان ربنا، مش عشان أي حاجة تانية" },
      { id: 3, text: "الله يراني، الله مطّلع عليّ" },
      { id: 4, text: "الالتزام = التعافي" },
      { id: 5, text: "عدم الالتزام = عدم التعافي" },
      { id: 6, text: "زلّة ساعة = تدمير 4 أيام" }
    ];
    saveData();
  }
  const esc = s => String(s).replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));

  const old = document.getElementById('beliefsBox'); if (old) old.remove();
  const box = document.createElement('div');
  box.id = 'beliefsBox';
  box.className = 'card-bg p-4 rounded-2xl border border-indigo-500/40 space-y-2.5';
  box.innerHTML = `
    <div class="flex justify-between items-center">
      <h2 class="text-sm font-bold text-indigo-300">🧠 معتقداتي</h2>
      <button onclick="blAdd()" class="text-[10px] bg-indigo-950 border border-indigo-500 px-3 py-1.5 rounded-xl text-indigo-300 font-bold">+ معتقد جديد</button>
    </div>
    <div id="beliefsList" class="space-y-2"></div>`;
  document.getElementById('pane-beliefs').appendChild(box);

  function render() {
    const list = document.getElementById('beliefsList');
    list.innerHTML = '';
    state.beliefs.forEach((b, i) => {
      const row = document.createElement('div');
      row.className = 'flex justify-between items-center gap-2 bg-gray-900/60 border border-gray-800 rounded-xl p-3';
      row.innerHTML = `
        <span class="text-xs text-indigo-100 leading-relaxed flex-1">${esc(b.text)}</span>
        <div class="flex items-center gap-1.5 shrink-0">
          <button onclick="blMove(${i},-1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▲</button>
          <button onclick="blMove(${i},1)" class="px-2 py-1 bg-gray-800 text-gray-300 rounded-xl text-xs">▼</button>
          <button onclick="blEdit(${b.id})" class="px-2 py-1 bg-gray-800 text-cyan-400 rounded-xl text-xs">✏️</button>
          <button onclick="blDel(${b.id})" class="px-2 py-1 bg-gray-800 text-red-400 rounded-xl text-xs">✕</button>
        </div>`;
      list.appendChild(row);
    });
  }

  window.blAdd = () => {
    const t = prompt("اكتب المعتقد الجديد:");
    if (t && t.trim()) { state.beliefs.push({ id: Date.now(), text: t.trim() }); saveData(); render(); }
  };
  window.blEdit = id => {
    const b = state.beliefs.find(x => x.id === id);
    const t = prompt("تعديل المعتقد:", b.text);
    if (t && t.trim()) { b.text = t.trim(); saveData(); render(); }
  };
  window.blDel = id => {
    if (confirm("هل تريد حذف هذا المعتقد؟")) { state.beliefs = state.beliefs.filter(x => x.id !== id); saveData(); render(); }
  };
  window.blMove = (i, dir) => {
    const t = i + dir;
    if (t < 0 || t >= state.beliefs.length) return;
    [state.beliefs[i], state.beliefs[t]] = [state.beliefs[t], state.beliefs[i]];
    saveData(); render();
  };
  render();
})();

// ===== وحدة التراكينج (العادات / تايم بلوكينج / تراكينج النوم / السعرات) =====
(function () {
  const WEEK_START = 6;
  const DAYS = ['الأحد', 'الإثنين', 'الثلاثاء', 'الأربعاء', 'الخميس', 'الجمعة', 'السبت'];
  const SHORT = ['أحد', 'اثنين', 'ثلاثاء', 'أربعاء', 'خميس', 'جمعة', 'سبت'];
  const BADGE_NAMES = { 1: ['صقر الفجر', '🦅'], 2: ['عقل الصقر', '🧠'], 3: ['حارس الورد', '📖'], 4: ['الحديد', '🏋️'], 5: ['درع التعافي', '🛡️'], 6: ['فارس الليل', '🌙'] };
  const TIERS = [7, 14, 30];
  const DEFAULT_BLOCKS = [
    { id: 1, label: '7 – 10 صباحًا' }, { id: 2, label: '10 صباحًا – الظهر' }, { id: 3, label: 'الظهر – العصر' },
    { id: 4, label: 'العصر – المغرب' }, { id: 5, label: 'العشاء – 12' }, { id: 6, label: '12 – 3' }
  ];

  // بلوكات العادات
  const HB = [
    { id: 'prayer', name: '🕌 بلوك الصلاة' },
    { id: 'taahud', name: '📖 بلوك التعاهد' },
    { id: 'career', name: '💼 بلوك المهنة' },
    { id: 'recovery', name: '🌱 بلوك التعافي' }
  ];
  const DEFAULT_BLOCK_MAP = { 1: 'prayer', 6: 'prayer', 3: 'taahud', 2: 'career', 4: 'recovery', 5: 'recovery' };
  const blockOf = h => HB.some(b => b.id === h.block) ? h.block : 'career';

  // لو التراكينج فاضي تمامًا (مثلاً بعد استيراد ملف فاضي) نرجّع الافتراضي
  if (state.habits && Array.isArray(state.habits.list) && !state.habits.list.length
      && !Object.keys(state.habits.log || {}).length
      && !Object.keys(state.habits.sleep || {}).length
      && !Object.keys(state.habits.calories || {}).length) {
    state.habits = null;
  }

  let dirty = false;
  if (!state.habits) {
    state.habits = {
      list: [
        { id: 1, name: "الفجر", type: "check", block: "prayer" },
        { id: 6, name: "قيام الليل", type: "check", block: "prayer" },
        { id: 3, name: "ورد المراجعة", type: "check", block: "taahud" },
        { id: 2, name: "المذاكرة / الحفظ", type: "time", block: "career" },
        { id: 4, name: "التمرين", type: "check", auto: "workout", block: "recovery" },
        { id: 5, name: "التعافي (اليوميات والأذكار)", type: "check", block: "recovery" }
      ],
      log: {}
    };
    dirty = true;
  }
  if (!state.habits.log) { state.habits.log = {}; dirty = true; }
  if (!state.habits.reviews) { state.habits.reviews = {}; dirty = true; }
  if (!state.habits.blockTpl) { state.habits.blockTpl = DEFAULT_BLOCKS.map(b => Object.assign({}, b)); dirty = true; }
  if (!state.habits.blockText) { state.habits.blockText = {}; dirty = true; }
  if (!state.habits.sleep) { state.habits.sleep = {}; dirty = true; }
  if (!state.habits.calories) { state.habits.calories = {}; dirty = true; }
  // ترقية العادات القديمة: إسناد بلوك لكل عادة ليس لها بلوك
  state.habits.list.forEach(h => {
    if (!h.block) { h.block = DEFAULT_BLOCK_MAP[h.id] || 'career'; dirty = true; }
  });
  if (dirty) saveData();

  const oldSec = document.getElementById('view-habits'); if (oldSec) oldSec.remove();

  const H = () => state.habits;
  const esc = s => String(s == null ? '' : s).replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c]));
  const fmt = m => m >= 60 ? `${Math.floor(m / 60)}س ${m % 60}د` : `${m}د`;
  const keyToDate = k => new Date(k + 'T12:00:00');
  const isFri = k => keyToDate(k).getDay() === 5;
  const weekKeysOf = k => {
    const d = keyToDate(k);
    d.setDate(d.getDate() - ((d.getDay() - WEEK_START + 7) % 7));
    return Array.from({ length: 7 }, (_, i) => { const x = new Date(d); x.setDate(d.getDate() + i); return getFormattedDate(x); });
  };
  const entry = (h, k) => (H().log[k] || {})[h.id];
  const isDone = (h, k) => {
    const e = entry(h, k);
    if (h.type === 'time') return !!(e && e.min > 0);
    if (e === true) return true;
    if (e === false) return false;
    return h.auto === 'workout' && (state.history[k] === 'completed' || state.history[k] === true);
  };
  const setE = (id, k, v) => { (H().log[k] = H().log[k] || {})[id] = v; saveData(); render(); if (typeof renderToday === 'function') renderToday(); };
  const find = id => H().list.find(h => h.id === id);

  const toMin = t => { if (!t) return null; const p = t.split(':'); return (+p[0]) * 60 + (+p[1]); };
  const durMin = (a, b) => { const x = toMin(a), y = toMin(b); if (x == null || y == null) return 0; let d = y - x; if (d < 0) d += 1440; return d; };
  const fmtDur = m => { const h = Math.floor(m / 60), r = m % 60; return h ? (r ? `${h}س ${r}د` : `${h}س`) : `${r}د`; };
  const fmt12 = t => { if (!t) return '--'; const p = t.split(':'), h = +p[0]; return `${h % 12 || 12}:${p[1]} ${h >= 12 ? 'م' : 'ص'}`; };
  const minToTime = m => { m = Math.round(m) % 1440; return String(Math.floor(m / 60)).padStart(2, '0') + ':' + String(m % 60).padStart(2, '0'); };
  const inCls = 'text-xs bg-gray-900 border border-gray-700 rounded px-2 py-1 text-gray-200';

  function firstKey() {
    const ks = Object.keys(H().log).concat(Object.keys(state.history || {})).filter(k => /^\d{4}-\d{2}-\d{2}$/.test(k)).sort();
    return ks.length ? ks[0] : getTodayKey();
  }
  function streakOf(h) {
    const tk = getTodayKey();
    const d = keyToDate(firstKey()), end = keyToDate(tk);
    let run = 0, best = 0;
    for (; d <= end; d.setDate(d.getDate() + 1)) {
      const k = getFormattedDate(d);
      if (isFri(k)) continue;
      if (isDone(h, k)) { run++; if (run > best) best = run; }
      else if (k !== tk) run = 0;
    }
    return { cur: run, best };
  }
  let ST = {};

  function badgeList() {
    const out = [];
    H().list.forEach(h => {
      const st = ST[h.id] || streakOf(h);
      const nm = BADGE_NAMES[h.id] || [h.name, '🏅'];
      let shownLocked = false;
      TIERS.forEach((t, i) => {
        const un = st.best >= t;
        if (un || !shownLocked) {
          out.push({ key: `h${h.id}_${t}`, emoji: nm[1], title: nm[0] + ' ' + '⭐'.repeat(i + 1), desc: `${t} يوم متواصل — ${h.name}`, un, prog: `${Math.min(st.cur, t)}/${t}` });
          if (!un) shownLocked = true;
        }
      });
    });
    return out;
  }
  function checkBadges(list) {
    if (!H().badgesSeen) {
      H().badgesSeen = {};
      list.filter(b => b.un).forEach(b => { H().badgesSeen[b.key] = 1; });
      saveData();
      return;
    }
    const fresh = list.filter(b => b.un && !H().badgesSeen[b.key]);
    fresh.forEach((b, i) => {
      H().badgesSeen[b.key] = 1;
      setTimeout(() => showToast(`🏅 وسام جديد: ${b.emoji} ${b.title}`), i * 3300);
    });
    if (fresh.length) saveData();
  }
  function renderBadges() {
    const box = document.getElementById('habitsBadges');
    if (!box) return;
    const bl = badgeList();
    checkBadges(bl);
    box.innerHTML = `
      <div class="flex justify-between items-center">
        <h3 class="text-sm font-bold text-yellow-300">🏅 الإنجازات</h3>
        <span class="text-[10px] text-gray-400">${bl.filter(b => b.un).length} مفتوحة</span>
      </div>
      <div class="grid grid-cols-2 gap-2">${bl.map(b => `
        <div class="rounded-lg border p-2 text-center ${b.un ? 'border-yellow-500/60 bg-yellow-950/20' : 'border-gray-800 opacity-50'}">
          <div class="text-2xl">${b.un ? b.emoji : '🔒'}</div>
          <div class="text-[11px] font-bold ${b.un ? 'text-yellow-200' : 'text-gray-400'}">${esc(b.title)}</div>
          <div class="text-[9px] text-gray-400">${esc(b.desc)}</div>
          ${b.un ? '' : `<div class="text-[9px] text-amber-400">${b.prog}</div>`}
        </div>`).join('')}</div>`;
  }

  let selDay = getTodayKey();
  let hbTab = 'habits';
  let viewY = new Date().getFullYear(), viewM = new Date().getMonth();

  const section = document.createElement('section');
  section.id = 'view-habits';
  section.className = 'hidden space-y-3';
  const tabCls = 'py-2 rounded-lg border text-[10px] font-bold transition bg-gray-900 border-gray-800 text-gray-400';
  section.innerHTML = `
    <div class="card-bg p-3 rounded-xl border border-amber-500/40 flex justify-between items-center">
      <div><h2 class="text-sm font-bold text-amber-400">📊 التراكينج <span class="text-[9px] text-gray-500">v7</span></h2>
      <p id="habitsDayLabel" class="text-[11px] text-gray-400"></p></div>
    </div>
    <div class="grid grid-cols-4 gap-1">
      <button id="htab-habits" onclick="hbTabSet('habits')" class="${tabCls}">✅ العادات</button>
      <button id="htab-blocks" onclick="hbTabSet('blocks')" class="${tabCls}">⏱ بلوكينج</button>
      <button id="htab-day" onclick="hbTabSet('day')" class="${tabCls}">😴 النوم</button>
      <button id="htab-cals" onclick="hbTabSet('cals')" class="${tabCls}">🥗 السعرات</button>
    </div>
    <div id="habitsMonth" class="card-bg p-3 rounded-xl border border-gray-800"></div>
    <div id="paneHabits" class="space-y-3">
      <div id="habitsSummary" class="card-bg p-3 rounded-xl border border-gray-800 space-y-2"></div>
      <div id="habitsList" class="space-y-4"></div>
      <div id="habitsBadges" class="card-bg p-3 rounded-xl border border-yellow-500/40 space-y-2"></div>
    </div>
    <div id="paneBlocks" class="hidden space-y-3">
      <div id="habitsBlocks" class="card-bg p-3 rounded-xl border border-teal-500/40 space-y-2"></div>
    </div>
    <div id="paneDay" class="hidden space-y-3">
      <div id="habitsSleep" class="card-bg p-3 rounded-xl border border-sky-500/40 space-y-2"></div>
    </div>
    <div id="paneCals" class="hidden space-y-3">
      <div id="habitsCals" class="card-bg p-3 rounded-xl border border-orange-500/40 space-y-3"></div>
    </div>`;
  document.querySelector('main').appendChild(section);

  window.renderHabitsView = function () {
    selDay = getTodayKey(); hbTab = 'habits';
    viewY = new Date().getFullYear(); viewM = new Date().getMonth();
    render();
  };
  window.setMainTab = n => { hbTab = n; render(); };

  function setTabUI() {
    [['habits', 'paneHabits'], ['blocks', 'paneBlocks'], ['day', 'paneDay'], ['cals', 'paneCals']].forEach(x => {
      document.getElementById(x[1]).classList.toggle('hidden', x[0] !== hbTab);
      document.getElementById('htab-' + x[0]).className = 'py-2 rounded-lg border text-[10px] font-bold transition ' +
        (x[0] === hbTab ? 'bg-amber-950 border-amber-400 text-amber-300' : 'bg-gray-900 border-gray-800 text-gray-400');
    });
  }

  function renderMonth(today) {
    const list = H().list;
    const first = new Date(viewY, viewM, 1, 12);
    const dim = new Date(viewY, viewM + 1, 0).getDate();
    const offset = (first.getDay() - WEEK_START + 7) % 7;
    const title = first.toLocaleDateString('ar-EG', { month: 'long', year: 'numeric' });
    const atNow = viewY === new Date().getFullYear() && viewM === new Date().getMonth();
    let head = '';
    for (let i = 0; i < 7; i++) head += `<span>${SHORT[(WEEK_START + i) % 7]}</span>`;
    let cells = '';
    for (let i = 0; i < offset; i++) cells += '<div></div>';
    for (let day = 1; day <= dim; day++) {
      const k = getFormattedDate(new Date(viewY, viewM, day, 12));
      const fut = k > today, fri = isFri(k), sel = k === selDay;
      const n = list.filter(h => isDone(h, k)).length;
      const sub = fri ? '📝' : (fut ? '·' : n + '/' + list.length);
      const cls = sel ? 'bg-amber-500 text-black border-amber-400 font-bold'
        : (fri ? 'bg-indigo-950/50 border-indigo-500/50 text-indigo-300' : 'bg-gray-900 border-gray-800 text-gray-300');
      cells += `<button ${fut ? 'disabled' : ''} onclick="hbDay('${k}')" class="py-1 rounded-lg border text-center transition ${cls} ${fut ? 'opacity-30' : ''} ${k === today ? 'ring-1 ring-amber-300' : ''}">
        <div class="text-xs font-bold">${day}</div><div class="text-[9px] ${sel ? '' : 'text-amber-400'}">${sub}</div></button>`;
    }
    document.getElementById('habitsMonth').innerHTML = `
      <div class="flex justify-between items-center mb-2">
        <button onclick="hbMonth(-1)" class="text-[11px] px-2 py-1 bg-gray-900 border border-gray-700 rounded text-gray-300">▶ السابق</button>
        <span class="text-xs font-bold text-amber-300">${title}</span>
        <button onclick="hbMonth(1)" ${atNow ? 'disabled' : ''} class="text-[11px] px-2 py-1 bg-gray-900 border border-gray-700 rounded text-gray-300 ${atNow ? 'opacity-30' : ''}">التالي ◀</button>
      </div>
      <div class="grid grid-cols-7 gap-1 text-center text-[9px] text-gray-500 mb-1 font-semibold">${head}</div>
      <div class="grid grid-cols-7 gap-1">${cells}</div>`;
  }

  function reviewHTML(wk, past) {
    const list = H().list;
    const rv = Object.assign({ won: '', change: '' }, H().reviews[wk[0]]);
    const a = keyToDate(wk[0]), b = keyToDate(wk[6]);
    const rows = list.map(h => {
      const c = past.filter(k => isDone(h, k)).length;
      const p = past.length ? Math.round(c / past.length * 100) : 0;
      let extra = '';
      if (h.type === 'time') {
        let st = 0, me = 0;
        past.forEach(k => { const x = entry(h, k); if (x && x.min > 0) { if (x.mode === 'memo') me += x.min; else st += x.min; } });
        extra = `<div class="text-[10px] text-gray-400 mt-0.5">📚 مذاكرة ${fmt(st)} • 📖 حفظ ${fmt(me)}</div>`;
      }
      return `<div>
        <div class="flex justify-between text-xs"><span class="text-gray-200">${esc(h.name)}</span><span class="text-amber-400 font-bold">${c}/${past.length} (${p}%)</span></div>
        <div class="w-full bg-gray-800 h-1.5 rounded-full overflow-hidden mt-1"><div class="bg-amber-400 h-1.5" style="width:${p}%"></div></div>${extra}</div>`;
    }).join('');
    const qs = [].concat((state.routines && state.routines.day1) || [], (state.routines && state.routines.day2) || []);
    const wrows = qs.map(q => {
      let t = 0, n = 0;
      wk.forEach(k => { const r = state.questHistory && state.questHistory[k] ? state.questHistory[k][q.id] : 0; if (r > 0) { t += r; n++; } });
      return n ? `<div class="flex justify-between text-xs"><span class="text-gray-300">${esc(q.name)}</span><span class="text-cyan-300">${(t / n).toFixed(1)} (في ${n} أيام)</span></div>` : '';
    }).join('');
    let wsec = 0;
    wk.forEach(k => { wsec += (state.workoutTimes && state.workoutTimes[k]) || 0; });
    return `<div class="card-bg p-3 rounded-xl border border-indigo-500/40 space-y-3">
      <h3 class="text-sm font-bold text-indigo-300">📝 مراجعة الأسبوع (${a.getDate()}/${a.getMonth() + 1} – ${b.getDate()}/${b.getMonth() + 1})</h3>
      <div class="space-y-2">${rows || '<p class="text-xs text-gray-500">مفيش عادات</p>'}</div>
      ${wrows ? `<div class="pt-2 border-t border-gray-800 space-y-1"><p class="text-[11px] text-gray-400">📈 متوسط التمارين${wsec ? ` • إجمالي وقت التمرين: ${fmtDur(Math.round(wsec / 60))}` : ''}</p>${wrows}</div>` : ''}
      <div class="pt-2 border-t border-gray-800 space-y-2">
        <label class="text-[11px] text-gray-300">✅ إيه اللي نجح الأسبوع ده؟</label>
        <textarea rows="3" onchange="hbReview('${wk[0]}','won',this.value)" class="w-full text-xs bg-gray-900 border border-gray-700 rounded p-2 text-gray-200">${esc(rv.won)}</textarea>
        <label class="text-[11px] text-gray-300">🔧 إيه اللي هغيّره الأسبوع الجاي؟</label>
        <textarea rows="3" onchange="hbReview('${wk[0]}','change',this.value)" class="w-full text-xs bg-gray-900 border border-gray-700 rounded p-2 text-gray-200">${esc(rv.change)}</textarea>
      </div></div>`;
  }

  function render() {
    const today = getTodayKey();
    ST = {};
    H().list.forEach(h => { ST[h.id] = streakOf(h); });
    setTabUI();
    renderMonth(today);
    const sd = keyToDate(selDay), fri = isFri(selDay);
    document.getElementById('habitsDayLabel').innerText = (hbTab === 'habits' && fri)
      ? 'الجمعة: مراجعة الأسبوع (معفية من العادات)'
      : (selDay === today ? 'اليوم' : 'يوم') + ': ' + DAYS[sd.getDay()] + ' ' + sd.getDate();
    if (hbTab === 'habits') renderHabitsPane(today);
    else if (hbTab === 'blocks') renderBlocks();
    else if (hbTab === 'day') renderSleep();
    else if (hbTab === 'cals') renderCalories();
    if (typeof renderToday === 'function') renderToday();
  }

  function habitCard(h, today, trk, past) {
    const d = isDone(h, selDay);
    const st = ST[h.id] || { cur: 0, best: 0 };
    const wCount = past.filter(k => isDone(h, k)).length;
    const dots = trk.map(k => `<span class="w-3 h-3 rounded-sm ${isDone(h, k) ? 'bg-amber-400' : 'bg-gray-800'} ${k === selDay ? 'ring-1 ring-amber-300' : ''} ${k > today ? 'opacity-30' : ''}"></span>`).join('');
    let middle = '', extra = '';
    if (h.type === 'time') {
      const e = entry(h, selDay) || { min: 0, mode: 'study' };
      middle = `<div class="flex items-center gap-2 mt-2">
        <button onclick="hbMode(${h.id})" class="px-2.5 py-1 rounded text-xs font-bold bg-gray-900 border border-amber-500/50 text-amber-300">${e.mode === 'memo' ? '📖 الحفظ' : '📚 المذاكرة'} ⇄</button>
        <button onclick="hbMin(${h.id})" class="px-2.5 py-1 rounded text-xs font-bold ${e.min > 0 ? 'bg-amber-500 text-black' : 'bg-gray-800 text-amber-300 border border-amber-500/40'}">⏱ ${e.min > 0 ? fmt(e.min) : 'سجّل الوقت'}</button></div>`;
      let ss = 0, me = 0;
      past.forEach(k => { const x = entry(h, k); if (x && x.min > 0) { if (x.mode === 'memo') me += x.min; else ss += x.min; } });
      extra = ` • مذاكرة ${fmt(ss)} • حفظ ${fmt(me)}`;
    }
    const mark = h.type === 'time'
      ? `<span class="w-7 h-7 rounded-full flex items-center justify-center text-sm ${d ? 'bg-amber-500 text-black' : 'bg-gray-800 text-gray-600'}">✔</span>`
      : `<button onclick="hbToggle(${h.id}, event)" class="w-7 h-7 rounded-full flex items-center justify-center text-sm font-bold transition ${d ? 'bg-amber-500 text-black' : 'bg-gray-800 text-gray-500 border border-gray-700'}">✔</button>`;
    const card = document.createElement('div');
    card.className = `card-bg p-3 rounded-xl border transition ${d ? 'border-amber-500/70 bg-amber-950/10' : 'border-gray-800'}`;
    card.innerHTML = `
      <div class="flex justify-between items-center">
        <div class="flex items-center gap-2.5">${mark}
          <div>
            <div class="text-xs font-bold text-gray-200">${esc(h.name)}</div>
            <div class="text-[10px] text-orange-400">🔥 ${st.cur} يوم <span class="text-gray-500">• 🏆 أفضل ${st.best}</span></div>
          </div>
        </div>
        <div class="flex items-center gap-1">
          <button onclick="hbMove(${h.id},-1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
          <button onclick="hbMove(${h.id},1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
          <button onclick="hbEdit(${h.id})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
          <button onclick="hbDel(${h.id})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
        </div>
      </div>${middle}
      <div class="flex justify-between items-center mt-2 pt-2 border-t border-gray-800/80">
        <div class="flex gap-1">${dots}</div>
        <span class="text-[10px] text-gray-400">الأسبوع: <strong class="text-amber-400">${wCount}/${trk.length}</strong>${extra}</span>
      </div>`;
    return card;
  }

  function renderHabitsPane(today) {
    const box = document.getElementById('habitsList');
    const list = H().list;
    const wk = weekKeysOf(selDay);
    const trk = wk.filter(k => !isFri(k));
    const past = trk.filter(k => k <= today);
    const fri = isFri(selDay);

    const wDone = list.reduce((s, h) => s + past.filter(k => isDone(h, k)).length, 0);
    const wMax = Math.max(1, list.length * past.length);
    const wPct = Math.round(wDone / wMax * 100);
    let sum = '';
    if (!fri) {
      const dDone = list.filter(h => isDone(h, selDay)).length;
      const dPct = list.length ? Math.round(dDone / list.length * 100) : 0;
      sum += `<div class="flex justify-between text-xs"><span class="text-gray-300">اليوم المختار</span><span class="text-amber-400 font-bold">${dDone} / ${list.length} (${dPct}%)</span></div>
        <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden"><div class="bg-amber-400 h-2 transition-all" style="width:${dPct}%"></div></div>`;
    }
    sum += `<div class="flex justify-between text-xs pt-1"><span class="text-gray-300">إجمالي الأسبوع</span><span class="text-cyan-400 font-bold">${wDone} / ${wMax} (${wPct}%)</span></div>
      <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden"><div class="bg-cyan-400 h-2 transition-all" style="width:${wPct}%"></div></div>`;
    document.getElementById('habitsSummary').innerHTML = sum;

    if (fri) { box.innerHTML = reviewHTML(wk, past); renderBadges(); return; }

    box.innerHTML = '';
    HB.forEach(b => {
      const items = list.filter(h => blockOf(h) === b.id);
      const done = items.filter(h => isDone(h, selDay)).length;
      const wrap = document.createElement('div');
      wrap.className = 'space-y-2';
      wrap.innerHTML = `
        <div class="flex justify-between items-center px-1 pt-1">
          <div class="flex items-center gap-2">
            <h3 class="text-xs font-bold text-amber-300">${esc(b.name)}</h3>
            <span class="text-[10px] text-gray-400">${done}/${items.length}</span>
          </div>
          <button onclick="hbAdd('${b.id}')" class="text-[10px] bg-amber-950 border border-amber-500 px-2 py-1 rounded text-amber-300 font-bold">+ عادة</button>
        </div>
        ${items.length ? '' : '<p class="text-[11px] text-gray-500 px-1">مفيش عادات في البلوك ده. اضغط + عادة.</p>'}`;
      items.forEach(h => wrap.appendChild(habitCard(h, today, trk, past)));
      box.appendChild(wrap);
    });
    renderBadges();
  }

  function renderBlocks() {
    const box = document.getElementById('habitsBlocks');
    const tpl = H().blockTpl, txt = H().blockText[selDay] || {};
    const rows = tpl.map((b, i) => `
      <div class="bg-gray-900/60 border border-gray-800 rounded-lg p-2 space-y-1.5">
        <div class="flex items-center justify-between">
          <span class="text-xs font-bold text-teal-200">${esc(b.label)}</span>
          <div class="flex items-center gap-1">
            <button onclick="tbMove(${i},-1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
            <button onclick="tbMove(${i},1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
            <button onclick="tbRename(${b.id})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
            <button onclick="tbDel(${b.id})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
          </div>
        </div>
        <input type="text" value="${esc(txt[b.id] || '')}" placeholder="هتعمل إيه في البلوك ده؟" onchange="tbText(${b.id}, this.value)" class="w-full ${inCls}">
      </div>`).join('');
    box.innerHTML = `
      <div class="flex justify-between items-center">
        <h3 class="text-sm font-bold text-teal-300">⏱ تايم بلوكينج</h3>
        <button onclick="tbAdd()" class="text-[10px] bg-teal-950 border border-teal-500 px-2 py-1 rounded text-teal-300 font-bold">+ بلوك جديد</button>
      </div>
      <p class="text-[10px] text-gray-400">البلوكات ثابتة لكل الأيام، واللي بتكتبه قدام كل بلوك بيتحفظ لليوم المختار بس.</p>
      ${tpl.length ? `<div class="space-y-2">${rows}</div>` : '<p class="text-[11px] text-gray-500">مفيش بلوكات. ضيف أول بلوك.</p>'}`;
  }

  function renderSleep() {
    const box = document.getElementById('habitsSleep');
    const today = getTodayKey();
    const sl = Object.assign({ bed: '', wake: '' }, H().sleep[selDay]);
    const dur = sl.bed && sl.wake ? durMin(sl.bed, sl.wake) : 0;
    let n = 0, sumD = 0, sumBed = 0, sumWake = 0;
    weekKeysOf(selDay).filter(k => k <= today).forEach(k => {
      const x = H().sleep[k];
      if (x && x.bed && x.wake) {
        n++; sumD += durMin(x.bed, x.wake);
        let b = toMin(x.bed); if (b < 720) b += 1440;
        sumBed += b; sumWake += toMin(x.wake);
      }
    });
    box.innerHTML = `
      <h3 class="text-sm font-bold text-sky-300">😴 النوم والاستيقاظ</h3>
      <p class="text-[10px] text-gray-400">سجّل نمت إمتى امبارح وصحيت إمتى في اليوم المختار</p>
      <div class="grid grid-cols-2 gap-2">
        <div><label class="text-[11px] text-gray-300 block mb-1">🌙 وقت النوم</label><input type="time" value="${sl.bed}" onchange="slSet('bed',this.value)" class="w-full ${inCls}"></div>
        <div><label class="text-[11px] text-gray-300 block mb-1">☀️ وقت الاستيقاظ</label><input type="time" value="${sl.wake}" onchange="slSet('wake',this.value)" class="w-full ${inCls}"></div>
      </div>
      ${dur ? `<p class="text-xs text-sky-200">مدة النوم: <strong>${fmtDur(dur)}</strong></p>` : ''}
      <div class="pt-2 border-t border-gray-800 text-[11px] text-gray-300 space-y-0.5">
        ${n ? `<div>📊 متوسط الأسبوع (${n} أيام): نوم <strong class="text-sky-300">${fmtDur(Math.round(sumD / n))}</strong></div>
        <div>🌙 متوسط وقت النوم: <strong class="text-sky-300">${fmt12(minToTime(sumBed / n))}</strong> • ☀️ متوسط الاستيقاظ: <strong class="text-sky-300">${fmt12(minToTime(sumWake / n))}</strong></div>` : '<div class="text-gray-500">لسه مفيش أيام مسجلة الأسبوع ده</div>'}
      </div>`;
  }

  function renderCalories() {
    const box = document.getElementById('habitsCals');
    const meals = H().calories[selDay] || [];
    const goal = H().calGoal || 0;
    let totCal = 0, totPro = 0, totFat = 0, totCarb = 0;
    meals.forEach(m => {
      totCal += Number(m.cal) || 0;
      totPro += Number(m.pro) || 0;
      totFat += Number(m.fat) || 0;
      totCarb += Number(m.carb) || 0;
    });

    const rows = meals.map((m, idx) => `
      <div class="flex justify-between items-center bg-gray-900/70 border border-gray-800 rounded-lg p-2.5 text-xs">
        <div>
          <strong class="text-orange-300 block text-sm">${esc(m.name)}</strong>
          <span class="text-[10px] text-gray-400">🔥 ${m.cal || 0} كالوري • بروتين: ${m.pro || 0}جم • دهون: ${m.fat || 0}جم • كارب: ${m.carb || 0}جم</span>
        </div>
        <button onclick="calDel(${idx})" class="text-red-400 hover:text-red-300 px-2 py-1 text-xs">✕</button>
      </div>`).join('');

    box.innerHTML = `
      <div class="flex justify-between items-center">
        <h3 class="text-sm font-bold text-orange-400">🥗 تراكينج السعرات والماكروز</h3>
        <span class="text-[10px] text-gray-400">المجموع: <strong class="text-orange-300">${totCal}</strong> / <strong onclick="calGoal()" class="text-cyan-400 underline cursor-pointer">${goal || 'حدد الهدف'}</strong> kcal</span>
      </div>
      ${goal ? `<div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden"><div class="${totCal > goal ? 'bg-red-500' : 'bg-orange-400'} h-2 transition-all" style="width:${Math.min(100, Math.round(totCal / goal * 100))}%"></div></div>
      <p class="text-[10px] ${totCal > goal ? 'text-red-400' : 'text-gray-400'}">${totCal > goal ? 'زيادة ' + (totCal - goal) : 'متبقي ' + (goal - totCal)} كالوري</p>` : ''}
      <div class="grid grid-cols-4 gap-1 text-center bg-black/40 p-2 rounded-xl border border-gray-800 text-[10px]">
        <div><span class="text-gray-400 block">السعرات</span><strong class="text-orange-400 text-xs">${totCal}</strong></div>
        <div><span class="text-gray-400 block">بروتين</span><strong class="text-cyan-400 text-xs">${totPro}ج</strong></div>
        <div><span class="text-gray-400 block">دهون</span><strong class="text-yellow-400 text-xs">${totFat}ج</strong></div>
        <div><span class="text-gray-400 block">كارب</span><strong class="text-emerald-400 text-xs">${totCarb}ج</strong></div>
      </div>
      <div class="space-y-2">${rows || '<p class="text-[11px] text-gray-500 text-center py-2">مفيش وجبات مسجلة اليوم.</p>'}</div>
      <div class="pt-2 border-t border-gray-800 space-y-2">
        <input type="text" id="mName" placeholder="اسم الوجبة (مثلاً: صدور فراخ ورز)..." class="w-full ${inCls}">
        <div class="grid grid-cols-4 gap-1.5">
          <input type="number" id="mCal" placeholder="كالوري" class="w-full text-center ${inCls}">
          <input type="number" id="mPro" placeholder="بروتين" class="w-full text-center ${inCls}">
          <input type="number" id="mFat" placeholder="دهون" class="w-full text-center ${inCls}">
          <input type="number" id="mCarb" placeholder="كارب" class="w-full text-center ${inCls}">
        </div>
        <button onclick="calAdd()" class="w-full py-2 bg-orange-600 hover:bg-orange-500 text-white rounded-xl font-bold text-xs transition">+ إضافة الوجبة</button>
      </div>`;
  }

  window.calGoal = () => {
    const v = prompt("هدف السعرات اليومي (كالوري):", H().calGoal || "");
    if (v === null) return;
    H().calGoal = Math.max(0, parseInt(v, 10) || 0);
    saveData(); renderCalories();
    if (typeof renderToday === 'function') renderToday();
  };

  window.calAdd = () => {
    const name = document.getElementById('mName').value.trim();
    const cal = parseInt(document.getElementById('mCal').value, 10) || 0;
    const pro = parseInt(document.getElementById('mPro').value, 10) || 0;
    const fat = parseInt(document.getElementById('mFat').value, 10) || 0;
    const carb = parseInt(document.getElementById('mCarb').value, 10) || 0;
    if (!name) { alert('اكتب اسم الوجبة!'); return; }
    H().calories[selDay] = H().calories[selDay] || [];
    H().calories[selDay].push({ name, cal, pro, fat, carb });
    saveData(); renderCalories();
    if (typeof renderToday === 'function') renderToday();
  };

  window.calDel = idx => {
    if (confirm('حذف هذه الوجبة؟')) {
      H().calories[selDay].splice(idx, 1);
      saveData(); renderCalories();
      if (typeof renderToday === 'function') renderToday();
    }
  };

  window.hbTabSet = n => { hbTab = n; render(); };
  window.hbDay = k => { selDay = k; render(); };
  window.hbMonth = dir => {
    let y = viewY, m = viewM + dir;
    if (m < 0) { m = 11; y--; } else if (m > 11) { m = 0; y++; }
    const now = new Date();
    if (y > now.getFullYear() || (y === now.getFullYear() && m > now.getMonth())) return;
    viewY = y; viewM = m; render();
  };
  window.hbReview = (wk, field, v) => {
    H().reviews[wk] = Object.assign({ won: '', change: '' }, H().reviews[wk], { [field]: v });
    saveData();
  };
  window.hbToggle = (id, e) => {
    if (!isDone(find(id), selDay)) fx(e, '✅ تمام');
    setE(id, selDay, !isDone(find(id), selDay));
  };
  window.hbMode = id => {
    const e = entry(find(id), selDay) || { min: 0, mode: 'study' };
    setE(id, selDay, { min: e.min, mode: e.mode === 'memo' ? 'study' : 'memo' });
  };
  window.hbMin = id => {
    const e = entry(find(id), selDay) || { min: 0, mode: 'study' };
    const v = prompt("عملت كام دقيقة؟", e.min || "");
    if (v === null) return;
    setE(id, selDay, { min: Math.max(0, parseInt(v, 10) || 0), mode: e.mode });
  };
  window.hbAdd = blockId => {
    const bid = HB.some(b => b.id === blockId) ? blockId : 'career';
    const n = prompt("اسم العادة:");
    if (!n || !n.trim()) return;
    const timed = confirm("العادة دي بالوقت؟\nموافق = بالوقت (دقايق)\nإلغاء = علامة صح");
    H().list.push({ id: Date.now(), name: n.trim(), type: timed ? 'time' : 'check', block: bid });
    saveData(); render();
  };
  window.hbEdit = id => { const h = find(id), n = prompt("تعديل اسم العادة:", h.name); if (n && n.trim()) { h.name = n.trim(); saveData(); render(); } };
  window.hbDel = id => { if (confirm("تحذف العادة دي؟")) { H().list = H().list.filter(h => h.id !== id); saveData(); render(); } };
  window.hbMove = (id, dir) => {
    const l = H().list;
    const i = l.findIndex(h => h.id === id);
    if (i < 0) return;
    const blk = blockOf(l[i]);
    let j = i + dir;
    while (j >= 0 && j < l.length && blockOf(l[j]) !== blk) j += dir;
    if (j < 0 || j >= l.length) return;
    [l[i], l[j]] = [l[j], l[i]];
    saveData(); render();
  };

  window.tbText = (id, v) => {
    H().blockText[selDay] = H().blockText[selDay] || {};
    H().blockText[selDay][id] = v;
    saveData();
  };
  window.tbAdd = () => {
    const l = prompt("وقت البلوك (مثلاً: 3 – 6 م أو المغرب – العشاء):");
    if (l && l.trim()) { H().blockTpl.push({ id: Date.now(), label: l.trim() }); saveData(); renderBlocks(); }
  };
  window.tbRename = id => {
    const b = H().blockTpl.find(x => x.id === id);
    const l = prompt("تعديل وقت البلوك:", b.label);
    if (l && l.trim()) { b.label = l.trim(); saveData(); renderBlocks(); }
  };
  window.tbDel = id => {
    if (confirm("تحذف البلوك ده؟")) { H().blockTpl = H().blockTpl.filter(b => b.id !== id); saveData(); renderBlocks(); }
  };
  window.tbMove = (i, dir) => {
    const l = H().blockTpl, t = i + dir;
    if (t < 0 || t >= l.length) return;
    [l[i], l[t]] = [l[t], l[i]];
    saveData(); renderBlocks();
  };

  window.slSet = (field, v) => {
    H().sleep[selDay] = Object.assign({ bed: '', wake: '' }, H().sleep[selDay], { [field]: v });
    saveData(); renderSleep();
    if (typeof renderToday === 'function') renderToday();
  };
})();

// ================= كارت النهارده في الرئيسية =================
window.renderToday = function () {
  const box = document.getElementById('today-card');
  if (!box) return;
  const DAYS_T = ['الأحد', 'الإثنين', 'الثلاثاء', 'الأربعاء', 'الخميس', 'الجمعة', 'السبت'];
  const k = getTodayKey(), now = new Date();
  const bar = (p, c) => `<div class="w-full bg-gray-800 h-1.5 rounded-full overflow-hidden mt-2"><div class="${c} h-1.5" style="width:${Math.max(0, Math.min(100, p))}%"></div></div>`;
  const tile = (label, value, pct, done, go, color) => `
    <button onclick="${go}" class="rounded-xl border p-2.5 text-right transition ${done ? 'border-emerald-500/60 bg-emerald-950/20' : 'border-gray-800 bg-gray-900/40'}">
      <div class="text-[10px] text-gray-400">${label}</div>
      <div class="text-sm font-bold ${done ? 'text-emerald-300' : 'text-gray-100'} mt-0.5">${value}</div>
      ${bar(pct, done ? 'bg-emerald-400' : color)}
    </button>`;

  const list = (state.habits && state.habits.list) ? state.habits.list : [];
  let habitsTile;
  if (now.getDay() === 5) habitsTile = tile('✅ العادات', '📝 مراجعة الجمعة', 0, false, "showView('habits')", 'bg-amber-400');
  else {
    const n = list.filter(h => {
      const e = ((state.habits.log || {})[k] || {})[h.id];
      if (h.type === 'time') return !!(e && e.min > 0);
      if (e === true) return true;
      if (e === false) return false;
      return h.auto === 'workout' && (state.history[k] === 'completed' || state.history[k] === true);
    }).length;
    habitsTile = tile('✅ العادات', `${n} / ${list.length}`, list.length ? n / list.length * 100 : 0, list.length > 0 && n === list.length, "showView('habits')", 'bg-amber-400');
  }

  const completed = state.history[k] === 'completed' || state.history[k] === true;
  const rest = state.history[k] === 'rest';
  const qs = (state.routines && state.routines[state.activeRoutine]) || [];
  const qd = qs.filter(q => q.current >= q.target).length;
  let wv, wp = 0, wdone = false;
  if (completed) { wv = '✅ خلصت'; wp = 100; wdone = true; }
  else if (rest) { wv = '🌿 يوم راحة'; wp = 100; wdone = true; }
  else if (state.penaltyActive) wv = '⚠️ عقوبة';
  else { wv = `${qd} / ${qs.length} تمرين`; wp = qs.length ? qd / qs.length * 100 : 0; }
  const wt = (state.workoutTimes && state.workoutTimes[k]) || 0;
  if (wt) wv += ` • ⏱ ${Math.round(wt / 60)}د`;
  const workoutTile = tile('🏋️ التمرين', wv, wp, wdone, "showView('workouts')", 'bg-cyan-400');

  const az = state.azkar || [], rem = az.filter(z => z.current > 0).length;
  const azTile = tile('📿 الأذكار', rem ? `باقي ${rem} من ${az.length}` : '✅ خلصتهم', az.length ? (az.length - rem) / az.length * 100 : 0, az.length > 0 && rem === 0, "showView('recovery');recTab('adhkar')", 'bg-emerald-400');

  const du = state.duas || [], dn = du.filter(d => d.done).length;
  const duTile = tile('🤲 الدعاء', `${dn} / ${du.length}`, du.length ? dn / du.length * 100 : 0, du.length > 0 && dn === du.length, "showView('recovery');recTab('duaa')", 'bg-blue-400');

  const sl = state.habits && state.habits.sleep && state.habits.sleep[k];
  const sleepOk = sl && sl.bed && sl.wake;
  const durMinCalc = (a, b) => {
    const toMin = t => { if (!t) return null; const p = t.split(':'); return (+p[0]) * 60 + (+p[1]); };
    const x = toMin(a), y = toMin(b); if (x == null || y == null) return 0; let d = y - x; if (d < 0) d += 1440; return d;
  };
  const fmtDurCalc = m => { const h = Math.floor(m / 60), r = m % 60; return h ? (r ? `${h}س ${r}د` : `${h}س`) : `${r}د`; };
  const sleepTile = tile('😴 النوم', sleepOk ? fmtDurCalc(durMinCalc(sl.bed, sl.wake)) : 'سجّل نومك', sleepOk ? 100 : 0, !!sleepOk, 'openDayTrackerFromHome()', 'bg-sky-400');

  const meals = (state.habits && state.habits.calories && state.habits.calories[k]) || [];
  const totCals = meals.reduce((s, m) => s + (Number(m.cal) || 0), 0);
  const goal = (state.habits && state.habits.calGoal) || 0;
  const calsTile = tile('🥗 السعرات', goal ? `${totCals} / ${goal}` : `${totCals} kcal`, goal ? totCals / goal * 100 : (totCals ? 50 : 0), goal ? (totCals >= goal * 0.9 && totCals <= goal * 1.1) : totCals > 0, "openDayTrackerFromHome()", 'bg-orange-400');

  box.innerHTML = `
    <div class="flex justify-between items-center">
      <h3 class="text-sm font-bold text-cyan-300">📍 النهارده</h3>
      <span class="text-[10px] text-gray-400">${DAYS_T[now.getDay()]} ${now.getDate()}</span>
    </div>
    <div class="grid grid-cols-2 gap-2">${habitsTile}${workoutTile}${azTile}${duTile}${sleepTile}${calsTile}</div>
    <div class="text-[10px] text-gray-400 pt-1">🔥 ستريك التمرين: <strong class="text-orange-400">${state.streak || 0}</strong> يوم</div>`;
};
window.renderToday();

// ================= النسخ الاحتياطي على تليجرام =================
let backupBusy = false;
function renderBackupStatus() {
  const el = document.getElementById('backup-status');
  if (!el) return;
  const b = state.lastBackup;
  el.innerText = b ? `آخر نسخة: ${b.date}${b.auto ? ' (تلقائية)' : ''}` : 'لسه مفيش نسخة احتياطية';
}

async function backupToTelegram(manual, e) {
  if (backupBusy) return false;
  if (!(CONFIG.TELEGRAM_BOT_TOKEN && CONFIG.TELEGRAM_CHAT_ID)) {
    if (manual) alert('اضغط ⚙️ إعداد تليجرام في ركن اليوميات الأول.');
    return false;
  }
  backupBusy = true;
  const el = document.getElementById('backup-status');
  if (manual && el) el.innerText = '⏳ جاري الإرسال...';
  try {
    const today = getTodayKey();
    const blob = new Blob([JSON.stringify(state, null, 2)], { type: 'application/json' });
    const fd = new FormData();
    fd.append('chat_id', CONFIG.TELEGRAM_CHAT_ID);
    fd.append('document', blob, `hunter_backup_${today}.json`);
    fd.append('caption', `☁️ نسخة احتياطية Hunter • ${today}`);
    const res = await fetch(`${TG_API()}/sendDocument`, { method: 'POST', body: fd });
    const data = await res.json();
    if (!data.ok) throw new Error(data.description);
    state.lastBackup = { date: today, ts: Date.now(), auto: !manual };
    saveData();
    if (manual) fx(e, '☁️ اتبعتت');
    return true;
  } catch (err) {
    if (manual) alert('تعذر إرسال النسخة: ' + (err.message || 'تأكد من الإنترنت'));
    return false;
  } finally {
    backupBusy = false;
    renderBackupStatus();
  }
}

function autoBackupCheck() {
  const today = getTodayKey();
  const last = state.lastBackup ? state.lastBackup.date : null;
  if (last === today) return;
  const isFriday = new Date().getDay() === 5;
  const daysSince = last ? Math.floor((new Date(today + 'T12:00:00') - new Date(last + 'T12:00:00')) / 86400000) : 999;
  if (isFriday || daysSince >= 7) backupToTelegram(false);
}

renderBackupStatus();
autoBackupCheck();
document.addEventListener('visibilitychange', () => { if (!document.hidden) autoBackupCheck(); });
</script>
</body>
</html>
