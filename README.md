<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hunter Life System</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { background-color: #08090d; color: #e2e8f0; font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace; }
    .neon-cyan { border: 1px solid #00e5ff; box-shadow: 0 0 10px rgba(0, 229, 255, 0.25); }
    .neon-red { border: 1px solid #ff3333; box-shadow: 0 0 12px rgba(255, 51, 51, 0.35); }
    .card-bg { background-color: #12151f; }
    .glow-cyan { text-shadow: 0 0 8px rgba(0, 229, 255, 0.7); }
    .glow-red { text-shadow: 0 0 8px rgba(255, 51, 51, 0.7); }
    .wheel-container { position: relative; width: 260px; height: 260px; margin: 0 auto; }
    .wheel-pointer { position: absolute; top: -10px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 12px solid transparent; border-right: 12px solid transparent; border-top: 20px solid #ef4444; z-index: 10; }
  </style>
</head>
<body class="p-3 pb-20 min-h-screen flex flex-col items-center select-none text-right">

  <header class="w-full max-w-md flex justify-between items-center p-3 mb-3 card-bg rounded-xl neon-cyan">
    <div class="flex items-center gap-2 cursor-pointer" onclick="showView('home')">
      <span class="text-xl">⚡</span>
      <div>
        <h1 class="text-sm font-bold text-cyan-400 glow-cyan font-mono">HUNTER LIFE SYSTEM</h1>
        <p class="text-[10px] text-gray-400" id="top-user-name">Mostafa Abdelrahman</p>
      </div>
    </div>
    <button onclick="showView('home')" class="px-3 py-1 text-xs bg-gray-900 border border-cyan-500/50 hover:bg-cyan-950 rounded text-cyan-400 font-bold transition">🏠 الرئيسية</button>
  </header>

  <main class="w-full max-w-md">

    <section id="view-home" class="space-y-3">
      <div class="card-bg p-4 rounded-xl border border-gray-800 text-center">
        <h2 class="text-base font-bold text-gray-100 mb-1">لوحة قيادة البطل ⚔️</h2>
        <p class="text-xs text-gray-400">اختر البوابة المطلوبة لمواصلة التطوير والتعافي:</p>
      </div>
      <div class="grid grid-cols-1 gap-2.5">
        <button onclick="showView('workouts')" class="p-4 rounded-xl card-bg border border-cyan-500/40 hover:border-cyan-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-cyan-950/60 border border-cyan-500/50">⚔️</span>
            <div>
              <h3 class="text-sm font-bold text-cyan-400">نظام تمارين Hunter</h3>
              <p class="text-xs text-gray-400">Day 1 / Day 2، الرتب، السجل الشهري والمتوسط الأسبوعي</p>
            </div>
          </div>
          <span class="text-cyan-400 text-sm">◀</span>
        </button>

        <div class="p-4 rounded-xl card-bg border border-emerald-500/40 flex justify-between items-center">
          <div>
            <h3 class="text-sm font-bold text-emerald-400">🛡️ عداد التعافي والصمود</h3>
            <div class="flex items-center gap-2 mt-1">
              <label class="text-[11px] text-gray-400">البداية:</label>
              <input type="date" id="recovery-start-input" onchange="updateRecoveryStart()" class="text-xs bg-gray-900 border border-gray-700 rounded px-1.5 py-0.5 text-gray-200">
            </div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-emerald-400 font-mono" id="recovery-days-count">0</div>
            <button onclick="reportRecoverySlip()" class="text-[10px] text-red-400 border border-red-500/40 px-1.5 py-0.5 rounded mt-0.5 hover:bg-red-950">سجلت زلة (-1)</button>
          </div>
        </div>

        <button onclick="showView('adhkar')" class="p-4 rounded-xl card-bg border border-emerald-500/40 hover:border-emerald-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-emerald-950/60 border border-emerald-500/50">📿</span>
            <div>
              <h3 class="text-sm font-bold text-emerald-400">أذكار المساء والتحصين</h3>
              <p class="text-xs text-gray-400">تعديل، إضافة، ترتيب، وتتبع بعدّاد تفاعلي</p>
            </div>
          </div>
          <span class="text-emerald-400 text-sm">◀</span>
        </button>

        <button onclick="showView('duaa')" class="p-4 rounded-xl card-bg border border-blue-500/40 hover:border-blue-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-blue-950/60 border border-blue-500/50">🤲</span>
            <div>
              <h3 class="text-sm font-bold text-blue-400">أدعية الثبات والاستعاذة</h3>
              <p class="text-xs text-gray-400">تحصين النفس مع تفعيل علامة الصح والإدارة الكاملة</p>
            </div>
          </div>
          <span class="text-blue-400 text-sm">◀</span>
        </button>

        <button onclick="showView('journal')" class="p-4 rounded-xl card-bg border border-purple-500/40 hover:border-purple-400 text-right flex items-center justify-between transition hover:scale-[1.01]">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-purple-950/60 border border-purple-500/50">🎙️</span>
            <div>
              <h3 class="text-sm font-bold text-purple-400">اليوميات المربوطة بتليجرام</h3>
              <p class="text-xs text-gray-400">تسجيلات صوتية + توثيق بالصور مباشرة لمحادثتك</p>
            </div>
          </div>
          <span class="text-purple-400 text-sm">◀</span>
        </button>

        <button onclick="showView('wheel')" class="p-4 rounded-xl card-bg border border-red-500/50 hover:border-red-400 text-right flex items-center justify-between transition hover:scale-[1.01] bg-red-950/20">
          <div class="flex items-center gap-3">
            <span class="text-2xl p-2 rounded-lg bg-red-950/80 border border-red-500/70">🎡</span>
            <div>
              <h3 class="text-sm font-bold text-red-400 glow-red">عجلة الطوارئ (وقت الخطر)</h3>
              <p class="text-xs text-gray-400">تعديل المهام، إضافة خطط هروب، وكسر الرغبة فوراً</p>
            </div>
          </div>
          <span class="text-red-400 text-sm">◀</span>
        </button>
      </div>
    </section>

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

      <div class="flex justify-between items-center text-xs px-1">
        <div class="flex gap-1.5">
          <button onclick="exportData()" class="px-2 py-1 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded">💾 Export</button>
          <button onclick="document.getElementById('import-file').click()" class="px-2 py-1 bg-gray-900 border border-gray-700 hover:border-cyan-500 rounded">📂 Import</button>
          <input type="file" id="import-file" accept=".json" class="hidden" onchange="importData(event)">
        </div>
        <button id="rest-toggle-btn" onclick="toggleTodayRest()" class="px-2.5 py-1 bg-gray-900 border border-green-700 text-green-400 rounded font-semibold">🌿 Rest Day</button>
      </div>

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

      <div id="rest-day-banner" class="p-3 rounded-xl bg-emerald-950/40 border border-emerald-500/50 hidden">
        <p class="text-xs text-emerald-300 font-bold">🌿 يوم استشفاء مفعل: أنت معفي اليوم من التمارين والعقوبات.</p>
      </div>

      <div id="penalty-card" class="p-3 rounded-xl bg-red-950/30 border border-red-500 hidden space-y-2">
        <div class="flex justify-between items-center">
          <h4 class="text-xs font-bold text-red-400">⚠️ PENALTY QUEST ACTIVE</h4>
          <button onclick="editPenaltyText()" class="text-[10px] text-red-400 border border-red-500 px-1.5 py-0.5 rounded">تعديل</button>
        </div>
        <p id="penalty-task-text" class="text-xs text-gray-200">1000 استغفار</p>
        <button onclick="confirmPenaltyDone()" class="w-full py-1.5 rounded bg-red-600 font-bold text-xs">إتمام العقوبة وفتح النظام</button>
      </div>

      <div class="flex justify-between items-center">
        <div class="flex gap-2">
          <button id="tab-day1" onclick="switchRoutine('day1')" class="px-3 py-1.5 rounded-lg text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400">⚡ DAY 1</button>
          <button id="tab-day2" onclick="switchRoutine('day2')" class="px-3 py-1.5 rounded-lg text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400">🔥 DAY 2</button>
        </div>
        <button onclick="openAddQuestModal()" class="text-xs border border-cyan-500 text-cyan-400 px-2.5 py-1.5 rounded hover:bg-cyan-950">+ إضافة تمرين</button>
      </div>

      <div id="quest-list" class="space-y-2.5"></div>

      <button id="complete-day-btn" onclick="completeDay()" class="w-full py-3 rounded-lg font-bold text-xs uppercase border border-cyan-500 text-cyan-400 hover:bg-cyan-950 transition">COMPLETE DAY</button>
    </section>

    <section id="view-adhkar" class="hidden space-y-3">
      <div class="card-bg p-3 rounded-xl border border-emerald-500/40 flex justify-between items-center">
        <div>
          <h2 class="text-sm font-bold text-emerald-400">📿 أذكار المساء والتحصين</h2>
          <p class="text-[11px] text-gray-400">تعديل، ترتيب، وحفظ أذكارك الخاصة</p>
        </div>
        <div class="flex gap-1.5">
          <button onclick="resetAzkarCounters()" class="text-[10px] bg-gray-900 border border-emerald-500/50 px-2 py-1 rounded text-emerald-400">🔄 تصفير</button>
          <button onclick="openAddZekrPrompt()" class="text-[10px] bg-emerald-950 border border-emerald-500 px-2 py-1 rounded text-emerald-300 font-bold">+ ذكر جديد</button>
        </div>
      </div>
      <div id="azkarList" class="space-y-2.5"></div>
    </section>

    <section id="view-duaa" class="hidden space-y-3">
      <div class="card-bg p-3 rounded-xl border border-blue-500/40 flex justify-between items-center">
        <div>
          <h2 class="text-sm font-bold text-blue-400">🤲 أدعية الثبات والاستعاذة</h2>
          <p class="text-[11px] text-gray-400">اضغط ✔ لتسجيل قراءة الدعاء، أو رتب وعدل</p>
        </div>
        <div class="flex gap-1.5">
          <button onclick="resetDuaaChecks()" class="text-[10px] bg-gray-900 border border-blue-500/50 px-2 py-1 rounded text-blue-400">🔄 تصفير الصح</button>
          <button onclick="openAddDuaaPrompt()" class="text-[10px] bg-blue-950 border border-blue-500 px-2 py-1 rounded text-blue-300 font-bold">+ دعاء جديد</button>
        </div>
      </div>
      <div id="duaaList" class="space-y-2.5"></div>
    </section>

    <section id="view-journal" class="hidden space-y-3">
      <div class="card-bg p-4 rounded-xl border border-purple-500/40 space-y-3">
        <div class="flex justify-between items-start">
          <div>
            <h2 class="text-sm font-bold text-purple-400">🎙️ ركن اليوميات الصوتية والتوثيق</h2>
            <p class="text-[11px] text-gray-400">يتم إرسال الفويس والصور فوراً لمحادثتك على تليجرام</p>
          </div>
          <button onclick="setupTelegram()" class="text-[10px] border border-purple-500/50 text-purple-300 px-2 py-1 rounded whitespace-nowrap">⚙️ إعداد تليجرام</button>
        </div>
        <div class="p-3 bg-black/40 rounded-xl border border-gray-800 flex items-center justify-between">
          <div class="flex items-center gap-2.5">
            <button id="recBtn" onclick="toggleRecord()" class="px-3.5 py-1.5 rounded-lg bg-blue-600 hover:bg-blue-500 text-white font-bold text-xs transition">بدء التسجيل ⏺</button>
            <span id="rec-status" class="text-xs text-gray-400">جاهز للتسجيل</span>
          </div>
        </div>
        <div id="audioList" class="space-y-1.5"></div>
        <div class="pt-2 border-t border-gray-800">
          <p class="text-xs text-gray-300 mb-2">📸 توثيق بالصور (إرسال لتليجرام):</p>
          <label class="w-full block text-center py-2.5 px-3 rounded-lg bg-gray-900 border border-purple-500/60 text-purple-300 hover:bg-purple-950/40 text-xs font-bold cursor-pointer transition">
            📷 اختيار أو التقاط صورة
            <input type="file" id="photoInput" accept="image/*" class="hidden" onchange="sendPhotoToTelegram(this)">
          </label>
          <div id="photoStatus" class="text-[11px] text-cyan-400 text-center mt-2"></div>
        </div>
      </div>
    </section>

    <section id="view-wheel" class="hidden space-y-4 text-center">
      <div class="card-bg p-3.5 rounded-xl neon-red">
        <h2 class="text-sm font-bold text-red-400 glow-red mb-0.5">🚨 عجلة الطوارئ وكسر الرغبة</h2>
        <p class="text-xs text-gray-300">لف العجلة واهرب فوراً لتنفيذ المهمة!</p>
      </div>
      <div class="wheel-container">
        <div class="wheel-pointer"></div>
        <canvas id="wheelCanvas" width="500" height="500" class="w-full h-full rounded-full shadow-[0_0_15px_rgba(255,51,51,0.4)]"></canvas>
      </div>
      <div id="spinResult" class="text-xs font-bold text-yellow-300 min-h-[24px]">اضغط على الزر واهرب فوراً</div>
      <button id="spinBtn" onclick="spinWheel()" class="w-full py-3 rounded-xl bg-red-600 hover:bg-red-500 text-white font-bold text-xs uppercase shadow-[0_0_12px_rgba(255,51,51,0.5)] transition">🎯 لف العجلة الآن</button>
      <div class="text-right">
        <button onclick="toggleTaskManager()" class="text-xs text-gray-400 hover:text-cyan-400 flex items-center gap-1 border border-gray-800 px-2.5 py-1 rounded bg-gray-900">⚙️ تعديل وإضافة مهام العجلة</button>
        <div id="taskManager" class="mt-2 card-bg p-3 rounded-xl border border-gray-800 hidden space-y-2">
          <div id="taskList" class="space-y-1.5 max-h-48 overflow-y-auto pr-1"></div>
          <div class="flex gap-1.5 pt-2 border-t border-gray-800">
            <input type="text" id="newTaskInput" placeholder="مهمة هروب جديدة..." class="flex-1 text-xs bg-gray-900 border border-gray-700 rounded px-2 py-1 text-gray-200">
            <button onclick="addTask()" class="text-xs px-3 py-1 bg-cyan-600 text-white rounded font-bold">إضافة</button>
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
  STORAGE_KEY: "hunter_ultimate_v4",
  OLD_STORAGE_KEY: "hunter_system_data_v2",
  RANKS: ["E-Rank", "D-Rank", "C-Rank", "B-Rank", "A-Rank", "S-Rank"],
  OFF_DAYS: [4, 5]
};

// ================= STATE =================
function getFormattedDate(d) {
  return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}-${String(d.getDate()).padStart(2, '0')}`;
}
function getTodayKey() { return getFormattedDate(new Date()); }

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
  recoveryStart: getTodayKey(),
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
  wheelPlans: defaultWheelPlans
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
  calculateRecoveryDays();
  renderAll();
}

function saveData() { localStorage.setItem(CONFIG.STORAGE_KEY, JSON.stringify(state)); }

function renderAll() {
  renderWorkouts(); renderAzkar(); renderDuas(); renderTasks(); drawWheel(); calculateRecoveryDays();
}

function showView(view) {
  ['home', 'workouts', 'adhkar', 'duaa', 'journal', 'wheel'].forEach(v => {
    const el = document.getElementById(`view-${v}`);
    if (el) el.classList.add('hidden');
  });
  const target = document.getElementById(`view-${view}`);
  if (target) target.classList.remove('hidden');
  if (view === 'wheel') drawWheel();
  if (view === 'adhkar') renderAzkar();
  if (view === 'duaa') renderDuas();
  if (view === 'workouts') renderWorkouts();
}

// ================= RECOVERY =================
function calculateRecoveryDays() {
  if (!state.recoveryStart) state.recoveryStart = getTodayKey();
  document.getElementById("recovery-start-input").value = state.recoveryStart;
  const diff = new Date() - new Date(state.recoveryStart);
  const days = Math.floor(diff / 86400000) - (state.recoveryPenaltyDays || 0);
  document.getElementById("recovery-days-count").innerText = days < 0 ? 0 : days;
}
function updateRecoveryStart() {
  state.recoveryStart = document.getElementById("recovery-start-input").value;
  state.recoveryPenaltyDays = 0;
  saveData();
  calculateRecoveryDays();
}
function reportRecoverySlip() {
  if (confirm("الزلة مش نهاية المطاف، كمل بكل قوتك! نخصم يوم؟")) {
    state.recoveryPenaltyDays = (state.recoveryPenaltyDays || 0) + 1;
    saveData();
    calculateRecoveryDays();
  }
}

// ================= WORKOUTS =================
function calculateWeeklyAverage(questId) {
  let totalReps = 0, trainingDays = 0;
  const today = new Date();
  for (let i = 0; i < 7; i++) {
    const d = new Date();
    d.setDate(today.getDate() - i);
    if (!CONFIG.OFF_DAYS.includes(d.getDay())) {
      const key = getFormattedDate(d);
      trainingDays++;
      if (state.questHistory && state.questHistory[key] && state.questHistory[key][questId]) {
        totalReps += state.questHistory[key][questId];
      }
    }
  }
  return (totalReps / Math.max(1, trainingDays)).toFixed(1);
}

function checkDayTransition() {
  const today = getTodayKey();
  if (!state.lastActiveDate) { state.lastActiveDate = today; saveData(); return; }
  if (state.lastActiveDate !== today) {
    const status = state.history[state.lastActiveDate];
    const wasDone = status === 'completed' || status === 'rest' || status === true;
    if (!wasDone && !state.penaltyActive) { state.penaltyActive = true; state.streak = 0; }
    if (state.routines) {
      Object.keys(state.routines).forEach(r => state.routines[r].forEach(q => q.current = 0));
    }
    state.lastActiveDate = today;
    saveData();
  }
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
  if (state.history[k] === 'rest') delete state.history[k];
  else { state.history[k] = 'rest'; state.penaltyActive = false; }
  recalculateStreakAndLevel();
  saveData();
  renderWorkouts();
}

function switchRoutine(r) { state.activeRoutine = r; saveData(); renderWorkouts(); }

function renderWorkouts() {
  document.getElementById("hunter-name").innerText = state.name + " ✏️️";
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
    restBtn.className = "px-2.5 py-1 bg-green-950 border border-green-400 text-green-300 rounded font-semibold text-xs";
    restBtn.innerText = "🌿 Rest Active";
  } else {
    restBanner.classList.add("hidden");
    restBtn.className = "px-2.5 py-1 bg-gray-900 border border-green-700 hover:border-green-400 text-green-400 rounded transition font-semibold text-xs";
    restBtn.innerText = "🌿 Rest Day";
  }

  const on = "px-3 py-1.5 rounded-lg text-xs font-bold border border-cyan-400 bg-cyan-950 text-cyan-400";
  const off = "px-3 py-1.5 rounded-lg text-xs font-bold border border-gray-800 bg-gray-900 text-gray-400";
  document.getElementById("tab-day1").className = state.activeRoutine === 'day1' ? on : off;
  document.getElementById("tab-day2").className = state.activeRoutine === 'day1' ? off : on;

  document.getElementById("penalty-task-text").innerText = state.penaltyText;
  const penaltyEl = document.getElementById("penalty-card");
  if (state.penaltyActive && !restActive) penaltyEl.classList.remove("hidden");
  else penaltyEl.classList.add("hidden");

  renderCalendar();

  const listEl = document.getElementById("quest-list");
  listEl.innerHTML = "";
  const todayKey = getTodayKey();
  const doneToday = state.history[todayKey] === 'completed' || state.history[todayKey] === true;
  const quests = state.routines[state.activeRoutine] || [];
  const dis = state.penaltyActive || doneToday || restActive ? 'disabled' : '';

  quests.forEach((q, index) => {
    const pct = Math.min(100, Math.floor((q.current / q.target) * 100));
    const avg = calculateWeeklyAverage(q.id);
    const card = document.createElement("div");
    card.className = `card-bg p-3 rounded-lg border transition ${pct >= 100 ? "border-cyan-500/70" : "border-gray-800"}`;
    card.innerHTML = `
      <div class="flex justify-between items-center mb-1">
        <div class="flex items-center gap-1.5">
          <span class="font-bold text-xs text-gray-200">${q.name}</span>
          <button onclick="editQuestName(${q.id})" class="text-[10px] text-gray-400 hover:text-cyan-400">✏️</button>
        </div>
        <div class="flex items-center gap-1">
          <button onclick="moveQuest(${index}, -1)" class="text-xs px-1 bg-gray-800 text-gray-400 rounded">▲</button>
          <button onclick="moveQuest(${index}, 1)" class="text-xs px-1 bg-gray-800 text-gray-400 rounded">▼</button>
          <button onclick="deleteQuest(${q.id})" class="text-xs text-gray-500 hover:text-red-400 px-1">✕</button>
        </div>
      </div>
      <div class="flex justify-between items-center text-xs text-gray-400 mb-1">
        <span>Progress: ${q.current} / <strong onclick="editTarget(${q.id})" class="text-cyan-400 underline cursor-pointer">${q.target}</strong></span>
        <span class="text-cyan-400 font-semibold">${pct}%</span>
      </div>
      <div class="text-[10px] text-gray-400 mb-1.5 flex justify-between">
        <span class="text-cyan-300 font-mono">📈 متوسط أسبوعي: <strong>${avg}</strong> عَدّة/يوم</span>
      </div>
      <div class="w-full bg-gray-800 h-1.5 rounded-full overflow-hidden mb-2">
        <div class="bg-cyan-400 h-1.5 transition-all duration-200" style="width: ${pct}%"></div>
      </div>
      <div class="flex justify-end gap-1.5 text-xs">
        <button onclick="updateQuest(${q.id}, -1)" ${dis} class="px-2 py-0.5 bg-gray-800 rounded hover:bg-gray-700 text-gray-300 disabled:opacity-30">-1</button>
        <button onclick="updateQuest(${q.id}, 1)" ${dis} class="px-2.5 py-0.5 bg-gray-800 rounded hover:bg-cyan-900 text-cyan-400 disabled:opacity-30">+1</button>
        <button onclick="completeSingleQuest(${q.id})" ${dis} class="px-2.5 py-0.5 bg-cyan-950 border border-cyan-500 text-cyan-400 hover:bg-cyan-900 rounded font-semibold disabled:opacity-30">✔ Done</button>
      </div>
    `;
    listEl.appendChild(card);
  });

  const btn = document.getElementById("complete-day-btn");
  if (restActive) {
    btn.className = "w-full py-3.5 rounded-lg font-bold text-xs uppercase border border-green-500 bg-green-950/40 text-green-400 cursor-not-allowed";
    btn.innerText = "🌿 REST DAY ACTIVE (PROTECTED)";
  } else if (doneToday) {
    btn.className = "w-full py-3.5 rounded-lg font-bold text-xs uppercase border border-cyan-700 bg-cyan-950/40 text-cyan-400 cursor-not-allowed opacity-80";
    btn.innerText = "✅ TODAY ALREADY COMPLETED";
  } else if (state.penaltyActive) {
    btn.className = "w-full py-3.5 rounded-lg font-bold text-xs uppercase border border-red-900 bg-red-950/30 text-red-400 cursor-not-allowed";
    btn.innerText = "LOCKED (PENALTY ACTIVE)";
  } else {
    btn.className = "w-full py-3.5 rounded-lg font-bold text-xs uppercase border border-cyan-400 bg-cyan-500/20 text-cyan-400 hover:bg-cyan-500/30 transition shadow-[0_0_12px_rgba(0,229,255,0.3)] cursor-pointer";
    btn.innerText = "COMPLETE DAY";
  }
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
    box.className = `p-1.5 rounded cursor-pointer border transition flex flex-col items-center justify-center ${borderClass}`;
    box.innerHTML = `<span class="text-[10px] font-bold">${day}</span><span class="text-[9px]">${icon}</span>`;
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

function findQuest(id) { return state.routines[state.activeRoutine].find(x => x.id === id); }

function updateQuest(id, amt) {
  if (state.penaltyActive || isTodayRest()) return;
  const q = findQuest(id);
  if (!q) return;
  q.current = Math.max(0, q.current + amt);
  saveData(); renderWorkouts();
}

function completeSingleQuest(id) {
  if (state.penaltyActive || isTodayRest()) return;
  const q = findQuest(id);
  if (!q) return;
  q.current = q.target;
  saveData(); renderWorkouts();
}

function editTarget(id) {
  const q = findQuest(id);
  if (!q) return;
  const t = prompt("Target:", q.target);
  if (t && parseInt(t) > 0) { q.target = parseInt(t); saveData(); renderWorkouts(); }
}

function editQuestName(id) {
  const q = findQuest(id);
  if (!q) return;
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
  state.routines[state.activeRoutine].push({ id: Date.now(), name: n.trim(), current: 0, target: t });
  saveData(); renderWorkouts();
}

function deleteQuest(id) {
  if (confirm("Delete this quest?")) {
    state.routines[state.activeRoutine] = state.routines[state.activeRoutine].filter(x => x.id !== id);
    saveData(); renderWorkouts();
  }
}

function completeDay() {
  const todayKey = getTodayKey();
  if (state.history[todayKey] === 'completed') { alert("You already completed your quests for today!"); return; }
  if (isTodayRest()) { alert("Today is a Rest Day!"); return; }
  if (state.routines[state.activeRoutine].some(q => q.current < q.target)) { alert("⚠️ لم تنهِ كل التمارين المطلوبة بعد!"); return; }

  if (!state.questHistory) state.questHistory = {};
  state.questHistory[todayKey] = {};
  state.routines[state.activeRoutine].forEach(q => { state.questHistory[todayKey][q.id] = q.current; });

  state.history[todayKey] = 'completed';
  const prevLevel = state.level;
  recalculateStreakAndLevel();
  saveData(); renderWorkouts();

  if (state.level > prevLevel) alert(`🔥 [LEVEL UP] وصلت إلى LEVEL ${state.level}!`);
  else alert(`✅ تم تسجيل اليوم بنجاح! الستريك: ${state.streak} يوم.`);
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
    div.className = `card-bg p-3 rounded-xl border transition ${isDone ? 'border-emerald-500/70 bg-emerald-950/20' : 'border-gray-800'}`;
    div.innerHTML = `
      <div class="text-xs text-gray-200 leading-relaxed mb-2">${item.text}</div>
      <div class="flex justify-between items-center pt-2 border-t border-gray-800/80">
        <button onclick="decrementZekr(${index})" class="px-3 py-1 rounded text-xs font-bold transition ${isDone ? 'bg-emerald-500 text-black' : 'bg-emerald-950 border border-emerald-500/60 text-emerald-400'}">
          ${isDone ? 'تم الاكتفاء ✔️' : `متبقي: ${item.current} /${item.total}`}
        </button>
        <div class="flex items-center gap-1">
          <button onclick="moveZekr(${index}, -1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
          <button onclick="moveZekr(${index}, 1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
          <button onclick="editZekr(${index})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
          <button onclick="deleteZekr(${index})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
        </div>
      </div>
    `;
    container.appendChild(div);
  });
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
    div.className = `card-bg p-3 rounded-xl border transition ${d.done ? 'border-blue-500/80 bg-blue-950/20' : 'border-gray-800'}`;
    div.innerHTML = `
      <div class="text-xs text-blue-100 leading-relaxed mb-2">${d.text}</div>
      <div class="flex justify-between items-center pt-2 border-t border-gray-800/80">
        <button onclick="toggleDuaCheck(${index})" class="px-3 py-1 rounded text-xs font-bold transition ${d.done ? 'bg-blue-500 text-black' : 'bg-gray-800 text-blue-300 border border-blue-500/40'}">
          ${d.done ? '✔ تم الدعاء' : 'وضع علامة صح ✔'}
        </button>
        <div class="flex items-center gap-1">
          <button onclick="moveDua(${index}, -1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
          <button onclick="moveDua(${index}, 1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
          <button onclick="editDua(${index})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
          <button onclick="deleteDua(${index})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
        </div>
      </div>
    `;
    container.appendChild(div);
  });
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

  for (let i = 0; i < n; i++) {
    const start = i * seg + currentWheelAngle;
    ctx.beginPath();
    ctx.moveTo(250, 250);
    ctx.arc(250, 250, 240, start, start + seg);
    ctx.fillStyle = wheelColors[i % wheelColors.length];
    ctx.fill();
    ctx.stroke();

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
  ctx.fill();
  ctx.strokeStyle = "#fff";
  ctx.lineWidth = 3;
  ctx.stroke();
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
    div.className = "flex justify-between items-center bg-gray-900 border border-gray-800 p-2 rounded text-xs";
    div.innerHTML = `
      <span class="text-gray-200">${task}</span>
      <div class="flex gap-1">
        <button onclick="editTask(${idx})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded">✏️</button>
        <button onclick="removeTask(${idx})" class="px-1.5 py-0.5 bg-red-950 text-red-400 rounded">✕</button>
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
  state.wheelPlans.splice(idx, 1);
  saveData(); renderTasks(); drawWheel();
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
        btn.className = "px-3.5 py-1.5 rounded-lg bg-blue-600 hover:bg-blue-500 text-white font-bold text-xs transition";
      };

      mediaRecorder.start();
      isRecording = true;
      btn.innerText = "⏹ إيقاف وإرسال";
      btn.className = "px-3.5 py-1.5 rounded-lg bg-red-600 hover:bg-red-500 text-white font-bold text-xs transition animate-pulse";
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
      saveData(); recalculateStreakAndLevel(); renderAll();
      alert("✅ تم استيراد كل بياناتك بنجاح!");
    } catch (err) { alert("خطأ في قراءة ملف النسخة الاحتياطية."); }
  };
  reader.readAsText(file);
  e.target.value = "";
}

// ================= TIMER + START =================
function updateTimer() {
  const now = new Date();
  const midnight = new Date(now);
  midnight.setHours(24, 0, 0, 0);
  const diff = midnight - now;
  checkDayTransition();
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
</script>
</body>
</html>
