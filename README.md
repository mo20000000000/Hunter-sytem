<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hunter Life System</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background-color: #08090d;
      color: #e2e8f0;
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
    }
    .neon-cyan {
      border: 1px solid #00e5ff;
      box-shadow: 0 0 12px rgba(0, 229, 255, 0.25);
    }
    .neon-green {
      border: 1px solid #10b981;
      box-shadow: 0 0 12px rgba(16, 185, 129, 0.25);
    }
    .neon-red {
      border: 1px solid #ff3333;
      box-shadow: 0 0 14px rgba(255, 51, 51, 0.35);
    }
    .card-bg {
      background-color: #12151f;
    }
    .glow-cyan {
      text-shadow: 0 0 8px rgba(0, 229, 255, 0.7);
    }
    .glow-red {
      text-shadow: 0 0 8px rgba(255, 51, 51, 0.7);
    }
    .wheel {
      transition: transform 3.5s cubic-bezier(0.15, 0.9, 0.25, 1);
    }
  </style>
</head>
<body class="p-3 pb-20 min-h-screen flex flex-col items-center select-none">

  <!-- Header & Navigation Bar -->
  <header class="w-full max-w-md flex justify-between items-center p-3 mb-3 card-bg rounded-xl neon-cyan">
    <div class="flex items-center gap-2 cursor-pointer" onclick="showView('home')">
      <span class="text-xl">⚡</span>
      <div>
        <h1 class="text-sm font-bold text-cyan-400 glow-cyan">HUNTER LIFE SYSTEM</h1>
        <p class="text-[10px] text-gray-400">Mostafa Abdelrahman</p>
      </div>
    </div>
    <button onclick="showView('home')" class="px-2.5 py-1 text-xs bg-gray-900 border border-cyan-500/50 hover:bg-cyan-950 rounded text-cyan-400">
      🏠 الرئيسية
    </button>
  </header>

  <main class="w-full max-w-md">

    <!-- ================= VIEW 1: HOME DASHBOARD (الواجهة الرئيسية) ================= -->
    <section id="view-home" class="space-y-3">
      <div class="card-bg p-4 rounded-xl border border-gray-800 text-center">
        <h2 class="text-base font-bold text-gray-100 mb-1">لوحة تحكم البطل ⚔️</h2>
        <p class="text-xs text-gray-400">اختر البوابة التي تريد الدخول إليها الآن:</p>
      </div>

      <div class="grid grid-cols-1 gap-2.5">
        <!-- Gate 1: Workouts -->
        <button onclick="showView('workouts')" class="p-4 rounded-xl card-bg border border-cyan-500/40 hover:border-cyan-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-cyan-950/60 border border-cyan-500/50">⚔️️</span>
            <div>
              <h3 class="text-sm font-bold text-cyan-400">نظام تمارين Hunter</h3>
              <p class="text-xs text-gray-400">Day 1 / Day 2، الرتب، السجل الشهري والستريك</p>
            </div>
          </div>
          <span class="text-cyan-400 text-sm">◀</span>
        </button>

        <!-- Gate 2: Evening Adhkar -->
        <button onclick="showView('adhkar')" class="p-4 rounded-xl card-bg border border-emerald-500/40 hover:border-emerald-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-emerald-950/60 border border-emerald-500/50">📿</span>
            <div>
              <h3 class="text-sm font-bold text-emerald-400">أذكار المساء</h3>
              <p class="text-xs text-gray-400">حصنك اليومي مع عدّاد تسبيح تفاعلي</p>
            </div>
          </div>
          <span class="text-emerald-400 text-sm">◀</span>
        </button>

        <!-- Gate 3: Duaa -->
        <button onclick="showView('duaa')" class="p-4 rounded-xl card-bg border border-blue-500/40 hover:border-blue-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-blue-950/60 border border-blue-500/50">🤲</span>
            <div>
              <h3 class="text-sm font-bold text-blue-400">أدعية الثبات والتحصين</h3>
              <p class="text-xs text-gray-400">أدعية الشفاء، الهداية، ومقاومة الزلات</p>
            </div>
          </div>
          <span class="text-blue-400 text-sm">◀</span>
        </button>

        <!-- Gate 4: Journal & Audio -->
        <button onclick="showView('journal')" class="p-4 rounded-xl card-bg border border-purple-500/40 hover:border-purple-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-purple-950/60 border border-purple-500/50">🎙️</span>
            <div>
              <h3 class="text-sm font-bold text-purple-400">يوميات الصياد</h3>
              <p class="text-xs text-gray-400">تسجيلات صوتية، صور، وتفريغ ذهني يومي</p>
            </div>
          </div>
          <span class="text-purple-400 text-sm">◀</span>
        </button>

        <!-- Gate 5: Emergency Wheel -->
        <button onclick="showView('wheel')" class="p-4 rounded-xl card-bg border border-red-500/50 hover:border-red-400 text-right flex items-center justify-between transition hover:scale-[1.01] bg-red-950/20">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-red-950/80 border border-red-500/70">🎡</span>
            <div>
              <h3 class="text-sm font-bold text-red-400 glow-red">عجلة الطوارئ (SOS)</h3>
              <p class="text-xs text-gray-400">مهام كسر الرغبة الفورية وتشتيت المحفزات</p>
            </div>
          </div>
          <span class="text-red-400 text-sm">◀</span>
        </button>
      </div>
    </section>

    <!-- ================= VIEW 2: HUNTER WORKOUTS ================= -->
    <section id="view-workouts" class="hidden space-y-4">
      <div class="card-bg p-4 rounded-xl neon-cyan">
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
        <div class="mt-3 pt-3 border-t border-gray-800">
          <div class="flex justify-between text-xs mb-1">
            <span class="text-gray-300">Streak: <strong id="streak-count" class="text-cyan-400">0</strong> Days</span>
            <span id="weekly-status-text" class="text-gray-400">Level Progress</span>
          </div>
          <div class="w-full bg-gray-800 rounded-full h-2 overflow-hidden">
            <div id="streak-bar" class="bg-cyan-400 h-2 transition-all duration-300" style="width: 0%"></div>
          </div>
        </div>
      </div>

      <!-- Workout Actions -->
      <div class="flex justify-between items-center text-xs px-1">
        <div class="flex gap-1.5">
          <button onclick="exportData()" class="px-2 py-1 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded">💾 Export</button>
          <button onclick="document.getElementById('import-file').click()" class="px-2 py-1 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded">📂 Import</button>
          <input type="file" id="import-file" accept=".json" class="hidden" onchange="importData(event)">
        </div>
        <button id="rest-toggle-btn" onclick="toggleTodayRest()" class="px-2.5 py-1 bg-gray-900 border border-green-700 text-green-400 rounded font-semibold">
          🌿 Rest Day
        </button>
      </div>

      <!-- Month Log Calendar -->
      <div class="card-bg p-3 rounded-xl border border-gray-800">
        <div class="flex justify-between items-center mb-2 px-1">
          <span id="calendar-month-title" class="text-xs font-bold text-cyan-400">📅 MONTH LOG</span>
          <span class="text-[10px] text-gray-400">اضغط لتبديل حالة اليوم</span>
        </div>
        <div class="grid grid-cols-7 gap-1 text-center text-[10px] text-gray-500 mb-1 font-semibold">
          <span>S</span><span>M</span><span>T</span><span>W</span><span>T</span><span>F</span><span>S</span>
        </div>
        <div id="calendar-days" class="grid grid-cols-7 gap-1 text-center"></div>
      </div>

      <!-- Rest Day Banner -->
      <div id="rest-day-banner" class="p-3 rounded-xl bg-emerald-950/40 border border-emerald-500/50 hidden">
        <p class="text-xs text-emerald-300 font-bold">🌿 يوم استشفاء مفعل: أنت معفي اليوم من التمارين والعقوبات.</p>
      </div>

      <!-- Penalty Card -->
      <div id="penalty-card" class="p-3 rounded-xl bg-red-950/30 border border-red-500 hidden space-y-2">
        <div class="flex justify-between items-center">
          <h4 class="text-xs font-bold text-red-400">⚠️ PENALTY QUEST ACTIVE</h4>
          <button onclick="editPenaltyText()" class="text-[10px] text-red-400 border border-red-500 px-1.5 py-0.5 rounded">تعديل</button>
        </div>
        <p id="penalty-task-text" class="text-xs text-gray-200">1000 استغفار</p>
        <button onclick="confirmPenaltyDone()" class="w-full py-1.5 rounded bg-red-600 font-bold text-xs">إتمام العقوبة وفتح النظام</button>
      </div>

      <!-- Routine Tabs -->
      <div class="flex justify-between items-center">
        <div class="flex gap-2">
          <button id="tab-day1" onclick="switchRoutine('day1')" class="px-3 py-1.5 rounded-lg text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400">⚡ DAY 1</button>
          <button id="tab-day2" onclick="switchRoutine('day2')" class="px-3 py-1.5 rounded-lg text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400">🔥 DAY 2</button>
        </div>
        <button onclick="openAddQuestModal()" class="text-xs border border-cyan-500 text-cyan-400 px-2 py-1.5 rounded hover:bg-cyan-950">+ إضافة تمرين</button>
      </div>

      <!-- Quests Container -->
      <div id="quest-list" class="space-y-2.5"></div>

      <!-- Complete Button -->
      <button id="complete-day-btn" onclick="completeDay()" class="w-full py-3 rounded-lg font-bold text-xs uppercase border border-cyan-500 text-cyan-400 hover:bg-cyan-950 transition">
        COMPLETE DAY
      </button>
    </section>

    <!-- ================= VIEW 3: ADHKAR (أذكار المساء) ================= -->
    <section id="view-adhkar" class="hidden space-y-3">
      <div class="card-bg p-3 rounded-xl border border-emerald-500/40 flex justify-between items-center">
        <div>
          <h2 class="text-sm font-bold text-emerald-400">📿 أذكار المساء والتحصين</h2>
          <p class="text-[11px] text-gray-400">اضغط على بطاقة الذكر لتسجيل التكرار</p>
        </div>
        <button onclick="resetAdhkar()" class="text-[10px] border border-emerald-500/50 px-2 py-1 rounded text-emerald-400">إعادة التصفير</button>
      </div>

      <div id="adhkar-container" class="space-y-2.5"></div>
    </section>

    <!-- ================= VIEW 4: DUAA (أدعية الثبات) ================= -->
    <section id="view-duaa" class="hidden space-y-3">
      <div class="card-bg p-3 rounded-xl border border-blue-500/40 flex justify-between items-center">
        <div>
          <h2 class="text-sm font-bold text-blue-400">🤲 أدعية الثبات والانكسار لله</h2>
          <p class="text-[11px] text-gray-400">حصنك عند الخلوة والضعف</p>
        </div>
        <button onclick="addNewDuaa()" class="text-xs border border-blue-500/50 px-2 py-1 rounded text-blue-400">+ إضافة دعاء</button>
      </div>

      <div id="duaa-container" class="space-y-2.5"></div>
    </section>

    <!-- ================= VIEW 5: JOURNAL & AUDIO (اليوميات) ================= -->
    <section id="view-journal" class="hidden space-y-3">
      <div class="card-bg p-3 rounded-xl border border-purple-500/40">
        <h2 class="text-sm font-bold text-purple-400 mb-1">🎙️ تفريغ المشاعر واليوميات</h2>
        <p class="text-[11px] text-gray-400 mb-2">سجل أفكارك صوتياً، اكتب ما يقلقك، أو أرفق صورة لتوثيق يومك</p>

        <!-- Audio Recorder -->
        <div class="p-2.5 bg-black/40 rounded-lg border border-gray-800 flex items-center justify-between mb-3">
          <div class="flex items-center gap-2">
            <button id="record-btn" onclick="toggleAudioRecord()" class="w-8 h-8 rounded-full bg-red-600 hover:bg-red-500 text-white flex items-center justify-center font-bold text-xs">
              ⏺
            </button>
            <span id="record-status" class="text-xs text-gray-300">تسجيل صوتي جديد</span>
          </div>
          <span id="record-timer" class="text-xs font-mono text-purple-400">00:00</span>
        </div>

        <textarea id="journal-input" rows="3" placeholder="اكتب ما يدور في بالك الآن بصراحة..." class="w-full p-2.5 text-xs bg-gray-900 border border-gray-800 rounded-lg text-gray-200 focus:outline-none focus:border-purple-500"></textarea>

        <div class="flex justify-between items-center mt-2">
          <label class="text-xs border border-gray-700 px-2.5 py-1.5 rounded cursor-pointer hover:border-purple-400 text-gray-300">
            📷 إرفاق صورة
            <input type="file" id="journal-img-input" accept="image/*" class="hidden" onchange="previewJournalImg(event)">
          </label>
          <button onclick="saveJournalEntry()" class="px-4 py-1.5 bg-purple-600 hover:bg-purple-500 text-white rounded text-xs font-bold">
            حفظ التدوينة
          </button>
        </div>
        <div id="journal-img-preview" class="mt-2 hidden">
          <img id="preview-img" src="" class="h-20 rounded border border-purple-500/50 object-cover">
        </div>
      </div>

      <div id="journal-entries" class="space-y-2"></div>
    </section>

    <!-- ================= VIEW 6: EMERGENCY WHEEL (عجلة الطوارئ) ================= -->
    <section id="view-wheel" class="hidden space-y-4 text-center">
      <div class="card-bg p-4 rounded-xl neon-red">
        <h2 class="text-base font-bold text-red-400 glow-red mb-1">🚨 بروتوكول الطوارئ (SOS)</h2>
        <p class="text-xs text-gray-300">عند الشعور برغبة ملحة أو ضغط، دور العجلة ونفذ الأمر فوراً دون تفكير!</p>
      </div>

      <div class="relative w-64 h-64 mx-auto flex items-center justify-center">
        <!-- Pointer -->
        <div class="absolute -top-3 z-10 text-2xl text-red-500">▼</div>
        <!-- Wheel Canvas -->
        <canvas id="wheel-canvas" width="250" height="250" class="wheel rounded-full border-2 border-red-500 shadow-[0_0_15px_rgba(255,51,51,0.4)]"></canvas>
      </div>

      <button id="spin-btn" onclick="spinWheel()" class="w-full py-3.5 rounded-xl bg-red-600 hover:bg-red-500 text-white font-bold text-sm tracking-wider uppercase shadow-[0_0_15px_rgba(255,51,51,0.5)] transition">
        🎯 تدوير العجلة الآن
      </button>

      <div id="wheel-result" class="p-3 rounded-xl card-bg border border-red-500/60 hidden">
        <p class="text-xs text-gray-400 mb-1">المهمة المطلوبة فوراً:</p>
        <h3 id="wheel-task-title" class="text-sm font-bold text-cyan-400"></h3>
      </div>
    </section>

  </main>

  <script>
    // ================= GLOBAL STATE & STORAGE =================
    const RANKS = ["E-Rank", "D-Rank", "C-Rank", "B-Rank", "A-Rank", "S-Rank"];

    function getFormattedDate(d) {
      const year = d.getFullYear();
      const month = String(d.getMonth() + 1).padStart(2, '0');
      const day = String(d.getDate()).padStart(2, '0');
      return `${year}-${month}-${day}`;
    }

    function getTodayKey() {
      return getFormattedDate(new Date());
    }

    async function requestPersistentStorage() {
      if (navigator.storage && navigator.storage.persist) {
        await navigator.storage.persist();
      }
    }
    requestPersistentStorage();

    let state = {
      name: "Mostafa Abdelrahman",
      level: 1,
      streak: 0,
      penaltyText: "1000 استغفار",
      penaltyActive: false,
      lastActiveDate: getTodayKey(),
      activeRoutine: "day1",
      history: {},
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
      adhkar: [
        { id: 1, text: "أمسينا وأمسى الملك لله، والحمد لله، لا إله إلا الله وحده لا شريك له", count: 0, target: 1 },
        { id: 2, text: "اللهم بك أمسينا، وبك أصبحنا، وبك نحيا، وبك نموت، وإليك المصير", count: 0, target: 1 },
        { id: 3, text: "سيد الاستغفار: اللهم أنت ربي لا إله إلا أنت، خلقتني وأنا عبدك...", count: 0, target: 1 },
        { id: 4, text: "اللهم إني أسألك العافية في الدنيا والآخرة...", count: 0, target: 1 },
        { id: 5, text: "بسم الله الذي لا يضر مع اسمه شيء في الأرض ولا في السماء", count: 0, target: 3 },
        { id: 6, text: "أعوذ بكلمات الله التامات من شر ما خلق", count: 0, target: 3 },
        { id: 7, text: "سبحان الله وبحمده", count: 0, target: 100 }
      ],
      duaaList: [
        "اللهم يا مقلب القلوب ثبت قلبي على دينك وطاعتك.",
        "اللهم إني أعوذ بك من شر سمعي، ومن شر بصري، ومن شر لساني، ومن شر قلبي، ومن شر منيِي.",
        "اللهم حصّن فرجي، وطهّر قلبي، واغفر ذنبي، ووفقني لمرضاتك.",
        "اللهم باعد بيني وبين خطاياي كما باعدت بين المشرق والمغرب."
      ],
      journals: []
    };

    function loadData() {
      const saved = localStorage.getItem("hunter_hub_data_v3");
      if (saved) {
        try {
          const parsed = JSON.parse(saved);
          state = Object.assign(state, parsed);
        } catch (e) {}
      } else {
        const v2 = localStorage.getItem("hunter_system_data_v2");
        if (v2) {
          try {
            const old = JSON.parse(v2);
            state = Object.assign(state, old);
          } catch(e) {}
        }
      }
      checkDayTransition();
      recalculateStreakAndLevel();
      renderAll();
    }

    function saveData() {
      localStorage.setItem("hunter_hub_data_v3", JSON.stringify(state));
    }

    // ================= NAVIGATION =================
    function showView(viewName) {
      const views = ['home', 'workouts', 'adhkar', 'duaa', 'journal', 'wheel'];
      views.forEach(v => {
        const el = document.getElementById(`view-${v}`);
        if (el) el.classList.add('hidden');
      });
      const activeEl = document.getElementById(`view-${viewName}`);
      if (activeEl) activeEl.classList.remove('hidden');

      if (viewName === 'wheel') drawWheel();
      if (viewName === 'adhkar') renderAdhkar();
      if (viewName === 'duaa') renderDuaa();
      if (viewName === 'journal') renderJournals();
      if (viewName === 'workouts') renderWorkouts();
    }

    // ================= WORKOUT LOGIC =================
    function checkDayTransition() {
      const today = getTodayKey();
      if (!state.lastActiveDate) {
        state.lastActiveDate = today;
        saveData();
        return;
      }
      if (state.lastActiveDate !== today) {
        const status = state.history[state.lastActiveDate];
        const wasDone = status === 'completed' || status === 'rest' || status === true;
        if (!wasDone && !state.penaltyActive) {
          state.penaltyActive = true;
          state.streak = 0;
        }
        if (state.routines) {
          Object.keys(state.routines).forEach(r => {
            state.routines[r].forEach(q => q.current = 0);
          });
        }
        state.lastActiveDate = today;
        saveData();
      }
    }

    function recalculateStreakAndLevel() {
      let currentStreak = 0;
      let checkDate = new Date();
      const todayKey = getFormattedDate(checkDate);
      if (state.history[todayKey]) currentStreak++;
      checkDate.setDate(checkDate.getDate() - 1);
      while (true) {
        const key = getFormattedDate(checkDate);
        if (state.history[key]) {
          currentStreak++;
          checkDate.setDate(checkDate.getDate() - 1);
        } else break;
      }
      state.streak = currentStreak;
      state.level = 1 + Math.floor(state.streak / 7);
    }

    function isTodayRest() {
      return state.history[getTodayKey()] === 'rest';
    }

    function toggleTodayRest() {
      const todayKey = getTodayKey();
      if (state.history[todayKey] === 'rest') {
        delete state.history[todayKey];
      } else {
        state.history[todayKey] = 'rest';
        state.penaltyActive = false;
      }
      recalculateStreakAndLevel();
      saveData();
      renderWorkouts();
    }

    function switchRoutine(r) {
      state.activeRoutine = r;
      saveData();
      renderWorkouts();
    }

    function renderWorkouts() {
      document.getElementById("hunter-name").innerText = state.name + " ✏️";
      const rankIndex = Math.min(Math.floor((state.level - 1) / 2), RANKS.length - 1);
      document.getElementById("hunter-rank-level").innerText = `${RANKS[rankIndex].toUpperCase()} HUNTER | LEVEL ${state.level}`;
      document.getElementById("streak-count").innerText = state.streak;

      const dayInWeek = (state.streak % 7) + 1;
      const progressPercent = Math.min(100, Math.floor(((state.streak % 7) / 7) * 100));
      document.getElementById("streak-bar").style.width = `${progressPercent}%`;

      const restActive = isTodayRest();
      const statusText = document.getElementById("weekly-status-text");
      if (restActive) statusText.innerHTML = `<span class="text-green-400 font-bold">RECOVERY DAY 🌿</span>`;
      else statusText.innerText = `Day ${dayInWeek} of 7`;

      const restBanner = document.getElementById("rest-day-banner");
      const restBtn = document.getElementById("rest-toggle-btn");
      if (restActive) {
        restBanner.classList.remove("hidden");
        restBtn.innerText = "🌿 Rest Active";
      } else {
        restBanner.classList.add("hidden");
        restBtn.innerText = "🌿 Rest Day";
      }

      const tab1 = document.getElementById("tab-day1");
      const tab2 = document.getElementById("tab-day2");
      if (state.activeRoutine === 'day1') {
        tab1.className = "px-3 py-1.5 rounded-lg text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400";
        tab2.className = "px-3 py-1.5 rounded-lg text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400";
      } else {
        tab2.className = "px-3 py-1.5 rounded-lg text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400";
        tab1.className = "px-3 py-1.5 rounded-lg text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400";
      }

      document.getElementById("penalty-task-text").innerText = state.penaltyText;
      const penaltyEl = document.getElementById("penalty-card");
      if (state.penaltyActive && !restActive) penaltyEl.classList.remove("hidden");
      else penaltyEl.classList.add("hidden");

      renderCalendar();

      const listEl = document.getElementById("quest-list");
      listEl.innerHTML = "";
      const todayKey = getTodayKey();
      const isDayCompletedToday = state.history[todayKey] === 'completed' || state.history[todayKey] === true;
      const quests = state.routines[state.activeRoutine] || [];

      quests.forEach((q, index) => {
        const pct = Math.min(100, Math.floor((q.current / q.target) * 100));
        const card = document.createElement("div");
        card.className = `card-bg p-3 rounded-lg border transition ${pct >= 100 ? "border-cyan-500/70" : "border-gray-800"}`;
        card.innerHTML = `
          <div class="flex justify-between items-center mb-1">
            <span class="font-bold text-xs text-gray-200">${q.name}</span>
            <div class="flex items-center gap-1">
              <button onclick="editTarget(${q.id})" class="text-[10px] text-cyan-400 border border-cyan-500/40 px-1 rounded">🎯 ${q.target}</button>
              <button onclick="deleteQuest(${q.id})" class="text-xs text-gray-500 hover:text-red-400 px-1">✕</button>
            </div>
          </div>
          <div class="w-full bg-gray-800 h-1.5 rounded-full overflow-hidden mb-2">
            <div class="bg-cyan-400 h-1.5 transition-all duration-200" style="width: ${pct}%"></div>
          </div>
          <div class="flex justify-between items-center text-xs">
            <span class="text-gray-400">${q.current} / ${q.target} (${pct}%)</span>
            <div class="flex gap-1">
              <button onclick="updateQuest(${q.id}, -1)" ${state.penaltyActive || isDayCompletedToday || restActive ? 'disabled' : ''} class="px-2 py-0.5 bg-gray-800 rounded">-1</button>
              <button onclick="updateQuest(${q.id}, 1)" ${state.penaltyActive || isDayCompletedToday || restActive ? 'disabled' : ''} class="px-2 py-0.5 bg-gray-800 text-cyan-400 rounded">+1</button>
              <button onclick="completeSingleQuest(${q.id})" ${state.penaltyActive || isDayCompletedToday || restActive ? 'disabled' : ''} class="px-2 py-0.5 bg-cyan-950 border border-cyan-500 text-cyan-400 rounded font-semibold">✔</button>
            </div>
          </div>
        `;
        listEl.appendChild(card);
      });

      const completeBtn = document.getElementById("complete-day-btn");
      if (restActive) {
        completeBtn.innerText = "🌿 REST DAY (PROTECTED)";
        completeBtn.disabled = true;
      } else if (isDayCompletedToday) {
        completeBtn.innerText = "✅ TODAY ALREADY COMPLETED";
        completeBtn.disabled = true;
      } else {
        completeBtn.innerText = "COMPLETE DAY";
        completeBtn.disabled = false;
      }
    }

    function renderCalendar() {
      const calEl = document.getElementById("calendar-days");
      calEl.innerHTML = "";
      const now = new Date();
      const year = now.getFullYear();
      const month = now.getMonth();
      document.getElementById("calendar-month-title").innerText = `📅 ${now.toLocaleString('en-US', { month: 'short', year: 'numeric' }).toUpperCase()}`;
      const firstDay = new Date(year, month, 1).getDay();
      const days = new Date(year, month + 1, 0).getDate();

      for (let i = 0; i < firstDay; i++) {
        calEl.appendChild(document.createElement("div"));
      }
      for (let day = 1; day <= days; day++) {
        const d = new Date(year, month, day);
        const key = getFormattedDate(d);
        const status = state.history[key];
        const box = document.createElement("div");
        box.onclick = () => toggleDayStatus(key);
        let cls = "p-1 rounded cursor-pointer border text-center text-[10px] ";
        if (status === 'rest') cls += "border-green-600 bg-green-950/40 text-green-400";
        else if (status === 'completed' || status === true) cls += "border-cyan-500 bg-cyan-950 text-cyan-400";
        else cls += "border-gray-800 bg-gray-900/40 text-gray-500";
        box.className = cls;
        box.innerText = day;
        calEl.appendChild(box);
      }
    }

    function toggleDayStatus(k) {
      if (!state.history[k]) state.history[k] = 'completed';
      else if (state.history[k] === 'completed' || state.history[k] === true) state.history[k] = 'rest';
      else delete state.history[k];
      recalculateStreakAndLevel();
      saveData();
      renderWorkouts();
    }

    function updateQuest(id, amt) {
      const q = state.routines[state.activeRoutine].find(x => x.id === id);
      if (!q) return;
      q.current = Math.max(0, q.current + amt);
      saveData();
      renderWorkouts();
    }

    function completeSingleQuest(id) {
      const q = state.routines[state.activeRoutine].find(x => x.id === id);
      if (!q) return;
      q.current = q.target;
      saveData();
      renderWorkouts();
    }

    function editTarget(id) {
      const q = state.routines[state.activeRoutine].find(x => x.id === id);
      if (!q) return;
      const t = prompt("Target:", q.target);
      if (t && parseInt(t) > 0) {
        q.target = parseInt(t);
        saveData();
        renderWorkouts();
      }
    }

    function openAddQuestModal() {
      const n = prompt("Quest Name:");
      if (!n) return;
      const t = parseInt(prompt("Target:", "100"), 10) || 100;
      state.routines[state.activeRoutine].push({ id: Date.now(), name: n, current: 0, target: t });
      saveData();
      renderWorkouts();
    }

    function deleteQuest(id) {
      state.routines[state.activeRoutine] = state.routines[state.activeRoutine].filter(x => x.id !== id);
      saveData();
      renderWorkouts();
    }

    function completeDay() {
      const todayKey = getTodayKey();
      const unfinished = state.routines[state.activeRoutine].filter(q => q.current < q.target);
      if (unfinished.length > 0) {
        alert("⚠️ لم تنهِ كل تمارين اليوم بعد!");
        return;
      }
      state.history[todayKey] = 'completed';
      recalculateStreakAndLevel();
      saveData();
      renderWorkouts();
      alert("✅ عاش يا بطل! تم تسجيل يوم التمرين بنجاح.");
    }

    // ================= ADHKAR LOGIC =================
    function renderAdhkar() {
      const container = document.getElementById("adhkar-container");
      container.innerHTML = "";
      state.adhkar.forEach(a => {
        const isDone = a.count >= a.target;
        const card = document.createElement("div");
        card.onclick = () => incrementZekr(a.id);
        card.className = `p-3 rounded-xl card-bg border cursor-pointer transition ${isDone ? 'border-emerald-500 bg-emerald-950/20' : 'border-gray-800 hover:border-gray-600'}`;
        card.innerHTML = `
          <p class="text-xs text-gray-200 leading-relaxed mb-2">${a.text}</p>
          <div class="flex justify-between items-center text-xs">
            <span class="text-gray-400 font-mono">الهدف: ${a.target}</span>
            <span class="px-3 py-1 rounded-full font-bold ${isDone ? 'bg-emerald-500 text-black' : 'bg-gray-800 text-emerald-400'}">
              ${a.count} / ${a.target} ${isDone ? '✔' : ''}
            </span>
          </div>
        `;
        container.appendChild(card);
      });
    }

    function incrementZekr(id) {
      const item = state.adhkar.find(x => x.id === id);
      if (!item) return;
      if (item.count < item.target) {
        item.count++;
        if (navigator.vibrate) navigator.vibrate(30);
        saveData();
        renderAdhkar();
      }
    }

    function resetAdhkar() {
      state.adhkar.forEach(a => a.count = 0);
      saveData();
      renderAdhkar();
    }

    // ================= DUAA LOGIC =================
    function renderDuaa() {
      const container = document.getElementById("duaa-container");
      container.innerHTML = "";
      state.duaaList.forEach((d, i) => {
        const card = document.createElement("div");
        card.className = "p-3 rounded-xl card-bg border border-blue-900/40 relative";
        card.innerHTML = `
          <p class="text-xs text-blue-100 leading-relaxed">${d}</p>
          <button onclick="deleteDuaa(${i})" class="absolute top-2 left-2 text-gray-500 hover:text-red-400 text-xs">✕</button>
        `;
        container.appendChild(card);
      });
    }

    function addNewDuaa() {
      const text = prompt("أدخل نص الدعاء:");
      if (text && text.trim()) {
        state.duaaList.push(text.trim());
        saveData();
        renderDuaa();
      }
    }

    function deleteDuaa(index) {
      state.duaaList.splice(index, 1);
      saveData();
      renderDuaa();
    }

    // ================= JOURNAL & AUDIO =================
    let mediaRecorder = null;
    let audioChunks = [];
    let recordInterval = null;
    let secondsRecorded = 0;
    let currentImageBase64 = null;

    async function toggleAudioRecord() {
      const btn = document.getElementById("record-btn");
      const status = document.getElementById("record-status");

      if (mediaRecorder && mediaRecorder.state === "recording") {
        mediaRecorder.stop();
        clearInterval(recordInterval);
        btn.innerText = "⏺";
        btn.classList.remove("animate-pulse");
        status.innerText = "تم حفظ المقطع الصوتي";
      } else {
        try {
          const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
          mediaRecorder = new MediaRecorder(stream);
          audioChunks = [];
          mediaRecorder.ondataavailable = e => audioChunks.push(e.data);
          mediaRecorder.onstop = () => {
            const audioBlob = new Blob(audioChunks, { type: 'audio/webm' });
            const reader = new FileReader();
            reader.readAsDataURL(audioBlob);
            reader.onloadend = () => {
              window.lastAudioBase64 = reader.result;
            };
          };
          mediaRecorder.start();
          secondsRecorded = 0;
          recordInterval = setInterval(() => {
            secondsRecorded++;
            const m = String(Math.floor(secondsRecorded / 60)).padStart(2, '0');
            const s = String(secondsRecorded % 60).padStart(2, '0');
            document.getElementById("record-timer").innerText = `${m}:${s}`;
          }, 1000);
          btn.innerText = "⏹";
          btn.classList.add("animate-pulse");
          status.innerText = "جارِ التسجيل الآن...";
        } catch (e) {
          alert("يرجى منح إذن الميكروفون للتسجيل.");
        }
      }
    }

    function previewJournalImg(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = ev => {
        currentImageBase64 = ev.target.result;
        document.getElementById("preview-img").src = currentImageBase64;
        document.getElementById("journal-img-preview").classList.remove("hidden");
      };
      reader.readAsDataURL(file);
    }

    function saveJournalEntry() {
      const text = document.getElementById("journal-input").value.trim();
      const audio = window.lastAudioBase64 || null;
      const img = currentImageBase64 || null;

      if (!text && !audio && !img) {
        alert("يرجى كتابة نص أو تسجيل صوت أو إرفاق صورة أولاً.");
        return;
      }

      state.journals.unshift({
        id: Date.now(),
        date: new Date().toLocaleString('ar-EG'),
        text: text,
        audio: audio,
        img: img
      });

      document.getElementById("journal-input").value = "";
      document.getElementById("journal-img-preview").classList.add("hidden");
      currentImageBase64 = null;
      window.lastAudioBase64 = null;
      saveData();
      renderJournals();
    }

    function renderJournals() {
      const container = document.getElementById("journal-entries");
      container.innerHTML = "";
      state.journals.forEach((j, index) => {
        const item = document.createElement("div");
        item.className = "p-3 rounded-xl card-bg border border-gray-800 space-y-2";
        item.innerHTML = `
          <div class="flex justify-between items-center text-[10px] text-gray-500">
            <span>${j.date}</span>
            <button onclick="deleteJournal(${index})" class="text-red-400">حذف</button>
          </div>
          ${j.text ? `<p class="text-xs text-gray-200 leading-relaxed">${j.text}</p>` : ''}
          ${j.audio ? `<audio controls src="${j.audio}" class="w-full h-8 mt-1"></audio>` : ''}
          ${j.img ? `<img src="${j.img}" class="rounded-lg max-h-48 object-cover mt-1 border border-gray-700">` : ''}
        `;
        container.appendChild(item);
      });
    }

    function deleteJournal(i) {
      state.journals.splice(i, 1);
      saveData();
      renderJournals();
    }

    // ================= EMERGENCY WHEEL =================
    const wheelTasks = [
      "قم فوراً وتوضأ وصلِّ ركعتين خاشعتين",
      "العب 30 عدة ضغط بأقصى سرعة وقوة",
      "اخرج من الغرفة فوراً واغسل وجهك بماء مثلج",
      "اتصل بصديق أو شخص مقرب وتحدث معه",
      "اقرأ صفحة واحدة من القرآن بصوت مسموع",
      "انزل للشارع للمشي 10 دقائق دون هاتف",
      "استغفر 100 مرة متتالية بتركيز تام",
      "اكتب ما تشعر به الآن على ورقة ثم مزقها"
    ];

    function drawWheel() {
      const canvas = document.getElementById("wheel-canvas");
      if (!canvas) return;
      const ctx = canvas.getContext("2d");
      const numSegments = wheelTasks.length;
      const arcSize = (2 * Math.PI) / numSegments;
      const colors = ["#ef4444", "#06b6d4", "#10b981", "#8b5cf6", "#f59e0b", "#3b82f6", "#ec4899", "#14b8a6"];

      ctx.clearRect(0, 0, 250, 250);
      for (let i = 0; i < numSegments; i++) {
        const angle = i * arcSize;
        ctx.beginPath();
        ctx.fillStyle = colors[i % colors.length];
        ctx.moveTo(125, 125);
        ctx.arc(125, 125, 120, angle, angle + arcSize);
        ctx.lineTo(125, 125);
        ctx.fill();

        ctx.save();
        ctx.translate(125, 125);
        ctx.rotate(angle + arcSize / 2);
        ctx.textAlign = "right";
        ctx.fillStyle = "#ffffff";
        ctx.font = "bold 10px monospace";
        ctx.fillText(`مهمة ${i+1}`, 110, 4);
        ctx.restore();
      }
    }

    let isSpinning = false;
    let currentWheelAngle = 0;

    function spinWheel() {
      if (isSpinning) return;
      isSpinning = true;
      const canvas = document.getElementById("wheel-canvas");
      const btn = document.getElementById("spin-btn");
      btn.disabled = true;

      const randomRounds = 5 + Math.floor(Math.random() * 5);
      const randomTaskIndex = Math.floor(Math.random() * wheelTasks.length);
      const arcDeg = 360 / wheelTasks.length;
      const targetDeg = (360 - (randomTaskIndex * arcDeg)) - (arcDeg / 2);
      currentWheelAngle += (randomRounds * 360) + targetDeg;

      canvas.style.transform = `rotate(${currentWheelAngle}deg)`;

      setTimeout(() => {
        isSpinning = false;
        btn.disabled = false;
        const resultCard = document.getElementById("wheel-result");
        document.getElementById("wheel-task-title").innerText = wheelTasks[randomTaskIndex];
        resultCard.classList.remove("hidden");
        if (navigator.vibrate) navigator.vibrate([100, 50, 100]);
      }, 3500);
    }

    // ================= EXPORT / IMPORT =================
    function exportData() {
      const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(state, null, 2));
      const a = document.createElement('a');
      a.href = dataStr;
      a.download = `hunter_life_backup_${getTodayKey()}.json`;
      a.click();
    }

    function importData(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = ev => {
        try {
          const parsed = JSON.parse(ev.target.result);
          state = Object.assign(state, parsed);
          saveData();
          recalculateStreakAndLevel();
          renderAll();
          alert("✅ تم استرجاع النسخة الاحتياطية بنجاح!");
        } catch(err) {
          alert("خطأ في قراءة الملف.");
        }
      };
      reader.readAsText(file);
      e.target.value = "";
    }

    function editName() {
      const n = prompt("Enter Hunter Name:", state.name);
      if (n && n.trim()) {
        state.name = n.trim();
        saveData();
        renderWorkouts();
      }
    }

    function editPenaltyText() {
      const t = prompt("مهمة العقوبة:", state.penaltyText);
      if (t) {
        state.penaltyText = t;
        saveData();
        renderWorkouts();
      }
    }

    function confirmPenaltyDone() {
      if (confirm("هل أتممت مهمة العقوبة بالكامل؟")) {
        state.penaltyActive = false;
        saveData();
        renderWorkouts();
      }
    }

    function updateTimer() {
      const now = new Date();
      const midnight = new Date(now);
      midnight.setHours(24, 0, 0, 0);
      const diff = midnight - now;
      checkDayTransition();
      const h = String(Math.floor((diff / (1000 * 60 * 60)) % 24)).padStart(2, '0');
      const m = String(Math.floor((diff / (1000 * 60)) % 60)).padStart(2, '0');
      const s = String(Math.floor((diff / 1000) % 60)).padStart(2, '0');
      const timerEl = document.getElementById("countdown");
      if (timerEl) timerEl.innerText = `${h}:${m}:${s}`;
    }

    function renderAll() {
      renderWorkouts();
      renderAdhkar();
      renderDuaa();
      renderJournals();
    }

    setInterval(updateTimer, 1000);
    updateTimer();
    loadData();
  </script>
</body>
</html>
