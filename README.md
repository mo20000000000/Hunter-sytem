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
  // المتوسط = إجمالي العدات ÷ عدد الأيام اللي عملت فيها التمرين فعلاً (آخر 7 أيام)
  let totalReps = 0, daysDone = 0;
  const today = new Date();
  for (let i = 0; i < 7; i++) {
    const d = new Date();
    d.setDate(today.getDate() - i);
    const key = getFormattedDate(d);
    const reps = state.questHistory && state.questHistory[key] ? state.questHistory[key][questId] : 0;
    if (reps > 0) { totalReps += reps; daysDone++; }
  }
  return { avg: daysDone ? (totalReps / daysDone).toFixed(1) : "0", days: daysDone };
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
    // تصفير الأذكار والأدعية كل يوم جديد
    if (state.azkar) state.azkar.forEach(z => z.current = z.total);
    if (state.duas) state.duas.forEach(d => d.done = false);
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
    const wa = calculateWeeklyAverage(q.id);
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
        <span class="text-cyan-300 font-mono">📈 متوسط أسبوعي: <strong>${wa.avg}</strong> عَدّة (في ${wa.days} أيام)</span>
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

// ===== متتبع العادات (سبت–خميس تسجيل، الجمعة مراجعة أسبوعية، عرض الشهر كامل) =====
(function () {
  const WEEK_START = 6;            // 6 = السبت
  const STREAK_MIN_PERCENT = 100;  // نسبة العادات المطلوبة عشان اليوم يتحسب في الستريك
  const DAYS = ['الأحد', 'الإثنين', 'الثلاثاء', 'الأربعاء', 'الخميس', 'الجمعة', 'السبت'];
  const SHORT = ['أحد', 'اثنين', 'ثلاثاء', 'أربعاء', 'خميس', 'جمعة', 'سبت'];

  let dirty = false;
  if (!state.habits) {
    state.habits = {
      list: [
        { id: 1, name: "الفجر", type: "check" },
        { id: 2, name: "المذاكرة / الحفظ", type: "time" },
        { id: 3, name: "ورد المراجعة", type: "check" },
        { id: 4, name: "التمرين", type: "check", auto: "workout" },
        { id: 5, name: "التعافي (اليوميات والأذكار)", type: "check" },
        { id: 6, name: "قيام الليل", type: "check" }
      ],
      log: {}
    };
    dirty = true;
  }
  if (!state.habits.reviews) { state.habits.reviews = {}; dirty = true; }
  if (dirty) saveData();

  // تنظيف أي نسخة قديمة من العادات لو اتلصقت مرتين
  const oldSec = document.getElementById('view-habits'); if (oldSec) oldSec.remove();
  document.querySelectorAll('#view-home .grid > button').forEach(b => { if (b.textContent.includes('متتبع العادات اليومية')) b.remove(); });

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
  const setE = (id, k, v) => { (H().log[k] = H().log[k] || {})[id] = v; saveData(); render(); };
  const find = id => H().list.find(h => h.id === id);

  // ستريك العادات: الجمعة معفية (مش بتزود ولا بتكسر)
  function habitsStreak() {
    const list = H().list;
    if (!list.length) return 0;
    const ok = k => (list.filter(h => isDone(h, k)).length / list.length) * 100 >= STREAK_MIN_PERCENT;
    const tk = getTodayKey();
    const d = new Date(); d.setHours(12);
    let s = 0;
    for (let i = 0; i < 400; i++) {
      const k = getFormattedDate(d);
      if (!isFri(k)) {
        if (ok(k)) s++;
        else if (k !== tk) break;
      }
      d.setDate(d.getDate() - 1);
    }
    return s;
  }

  let selDay = getTodayKey();
  let viewY = new Date().getFullYear(), viewM = new Date().getMonth();

  const section = document.createElement('section');
  section.id = 'view-habits';
  section.className = 'hidden space-y-3';
  section.innerHTML = `
    <div class="card-bg p-3 rounded-xl border border-amber-500/40 flex justify-between items-center">
      <div><h2 class="text-sm font-bold text-amber-400">✅ متتبع العادات <span class="text-[9px] text-gray-500">v4</span></h2>
      <p id="habitsDayLabel" class="text-[11px] text-gray-400"></p></div>
      <button onclick="hbAdd()" class="text-[10px] bg-amber-950 border border-amber-500 px-2 py-1 rounded text-amber-300 font-bold">+ عادة جديدة</button>
    </div>
    <div id="habitsMonth" class="card-bg p-3 rounded-xl border border-gray-800"></div>
    <div id="habitsSummary" class="card-bg p-3 rounded-xl border border-gray-800 space-y-2"></div>
    <div id="habitsList" class="space-y-2.5"></div>`;
  document.querySelector('main').appendChild(section);

  const homeBtn = document.createElement('button');
  homeBtn.dataset.key = 'habits';
  homeBtn.onclick = () => showView('habits');
  homeBtn.className = 'p-4 rounded-xl card-bg border border-amber-500/40 hover:border-amber-400 text-right flex items-center justify-between transition hover:scale-[1.01]';
  homeBtn.innerHTML = `<div class="flex items-center gap-3">
    <span class="text-2xl p-2 rounded-lg bg-amber-950/60 border border-amber-500/50">✅</span>
    <div><h3 class="text-sm font-bold text-amber-400">متتبع العادات اليومية</h3>
    <p class="text-xs text-gray-400">تسجيل من السبت للخميس، والجمعة مراجعة أسبوعية، وعرض الشهر كامل</p></div></div>
    <span class="text-amber-400 text-sm">◀</span>`;
  document.querySelector('#view-home .grid').prepend(homeBtn);

  const _showView = window.showView;
  window.showView = function (v) {
    document.getElementById('view-habits').classList.add('hidden');
    if (v === 'habits') {
      _showView('home');
      document.getElementById('view-home').classList.add('hidden');
      document.getElementById('view-habits').classList.remove('hidden');
      selDay = getTodayKey();
      viewY = new Date().getFullYear(); viewM = new Date().getMonth();
      render();
    } else _showView(v);
  };

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
    return `<div class="card-bg p-3 rounded-xl border border-indigo-500/40 space-y-3">
      <h3 class="text-sm font-bold text-indigo-300">📝 مراجعة الأسبوع (${a.getDate()}/${a.getMonth() + 1} – ${b.getDate()}/${b.getMonth() + 1})</h3>
      <div class="space-y-2">${rows || '<p class="text-xs text-gray-500">مفيش عادات</p>'}</div>
      ${wrows ? `<div class="pt-2 border-t border-gray-800 space-y-1"><p class="text-[11px] text-gray-400">📈 متوسط التمارين</p>${wrows}</div>` : ''}
      <div class="pt-2 border-t border-gray-800 space-y-2">
        <label class="text-[11px] text-gray-300">✅ إيه اللي نجح الأسبوع ده؟</label>
        <textarea rows="3" onchange="hbReview('${wk[0]}','won',this.value)" class="w-full text-xs bg-gray-900 border border-gray-700 rounded p-2 text-gray-200">${esc(rv.won)}</textarea>
        <label class="text-[11px] text-gray-300">🔧 إيه اللي هغيّره الأسبوع الجاي؟</label>
        <textarea rows="3" onchange="hbReview('${wk[0]}','change',this.value)" class="w-full text-xs bg-gray-900 border border-gray-700 rounded p-2 text-gray-200">${esc(rv.change)}</textarea>
      </div></div>`;
  }

  function render() {
    const box = document.getElementById('habitsList');
    if (!box) return;
    const today = getTodayKey(), list = H().list;
    const wk = weekKeysOf(selDay);
    const trk = wk.filter(k => !isFri(k));
    const past = trk.filter(k => k <= today);
    const fri = isFri(selDay);
    renderMonth(today);

    const sd = keyToDate(selDay);
    document.getElementById('habitsDayLabel').innerText = fri
      ? 'الجمعة: مراجعة الأسبوع (معفية من العادات)'
      : (selDay === today ? 'تسجيل اليوم' : 'تسجيل يوم') + ': ' + DAYS[sd.getDay()] + ' ' + sd.getDate();

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
      <div class="w-full bg-gray-800 h-2 rounded-full overflow-hidden"><div class="bg-cyan-400 h-2 transition-all" style="width:${wPct}%"></div></div>
      <div class="flex justify-between text-xs pt-1"><span class="text-gray-300">🔥 ستريك العادات (الجمعة معفية)</span><span class="text-orange-400 font-bold">${habitsStreak()} يوم</span></div>`;
    document.getElementById('habitsSummary').innerHTML = sum;

    if (fri) { box.innerHTML = reviewHTML(wk, past); return; }

    box.innerHTML = '';
    list.forEach((h, i) => {
      const d = isDone(h, selDay);
      const wCount = past.filter(k => isDone(h, k)).length;
      const dots = trk.map(k => `<span class="w-3 h-3 rounded-sm ${isDone(h, k) ? 'bg-amber-400' : 'bg-gray-800'} ${k === selDay ? 'ring-1 ring-amber-300' : ''} ${k > today ? 'opacity-30' : ''}"></span>`).join('');
      let middle = '', extra = '';
      if (h.type === 'time') {
        const e = entry(h, selDay) || { min: 0, mode: 'study' };
        middle = `<div class="flex items-center gap-2 mt-2">
          <button onclick="hbMode(${h.id})" class="px-2.5 py-1 rounded text-xs font-bold bg-gray-900 border border-amber-500/50 text-amber-300">${e.mode === 'memo' ? '📖 الحفظ' : '📚 المذاكرة'} ⇄</button>
          <button onclick="hbMin(${h.id})" class="px-2.5 py-1 rounded text-xs font-bold ${e.min > 0 ? 'bg-amber-500 text-black' : 'bg-gray-800 text-amber-300 border border-amber-500/40'}">⏱ ${e.min > 0 ? fmt(e.min) : 'سجّل الوقت'}</button></div>`;
        let st = 0, me = 0;
        past.forEach(k => { const x = entry(h, k); if (x && x.min > 0) { if (x.mode === 'memo') me += x.min; else st += x.min; } });
        extra = ` • مذاكرة ${fmt(st)} • حفظ ${fmt(me)}`;
      }
      const mark = h.type === 'time'
        ? `<span class="w-7 h-7 rounded-full flex items-center justify-center text-sm ${d ? 'bg-amber-500 text-black' : 'bg-gray-800 text-gray-600'}">✔</span>`
        : `<button onclick="hbToggle(${h.id})" class="w-7 h-7 rounded-full flex items-center justify-center text-sm font-bold transition ${d ? 'bg-amber-500 text-black' : 'bg-gray-800 text-gray-500 border border-gray-700'}">✔</button>`;
      const card = document.createElement('div');
      card.className = `card-bg p-3 rounded-xl border transition ${d ? 'border-amber-500/70 bg-amber-950/10' : 'border-gray-800'}`;
      card.innerHTML = `
        <div class="flex justify-between items-center">
          <div class="flex items-center gap-2.5">${mark}<span class="text-xs font-bold text-gray-200">${esc(h.name)}</span></div>
          <div class="flex items-center gap-1">
            <button onclick="hbMove(${i},-1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
            <button onclick="hbMove(${i},1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
            <button onclick="hbEdit(${h.id})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
            <button onclick="hbDel(${h.id})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
          </div>
        </div>${middle}
        <div class="flex justify-between items-center mt-2 pt-2 border-t border-gray-800/80">
          <div class="flex gap-1">${dots}</div>
          <span class="text-[10px] text-gray-400">الأسبوع: <strong class="text-amber-400">${wCount}/${trk.length}</strong>${extra}</span>
        </div>`;
      box.appendChild(card);
    });
  }

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
  window.hbToggle = id => setE(id, selDay, !isDone(find(id), selDay));
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
  window.hbAdd = () => {
    const n = prompt("اسم العادة:");
    if (!n || !n.trim()) return;
    const timed = confirm("العادة دي بالوقت؟\nموافق = بالوقت (دقايق)\nإلغاء = علامة صح");
    H().list.push({ id: Date.now(), name: n.trim(), type: timed ? 'time' : 'check' });
    saveData(); render();
  };
  window.hbEdit = id => { const h = find(id), n = prompt("تعديل اسم العادة:", h.name); if (n && n.trim()) { h.name = n.trim(); saveData(); render(); } };
  window.hbDel = id => { if (confirm("تحذف العادة دي؟")) { H().list = H().list.filter(h => h.id !== id); saveData(); render(); } };
  window.hbMove = (i, dir) => {
    const l = H().list, t = i + dir;
    if (t < 0 || t >= l.length) return;
    [l[i], l[t]] = [l[t], l[i]];
    saveData(); render();
  };
})();

// ================= HOME ORDER =================
(function () {
  const grid = document.querySelector('#view-home .grid');
  const base = ['workouts', 'recovery', 'adhkar', 'duaa', 'journal', 'wheel'];
  [...grid.children].filter(c => !c.dataset.key).forEach((c, i) => c.dataset.key = base[i]);
  let edit = false;

  function apply() {
    const order = state.homeOrder || [];
    const rank = c => { const i = order.indexOf(c.dataset.key); return i < 0 ? 999 : i; };
    const kids = [...grid.children];
    kids.forEach(c => { c.querySelectorAll('.ho-arrows').forEach(e => e.remove()); c.classList.remove('relative'); });
    kids.sort((a, b) => rank(a) - rank(b)).forEach(c => grid.appendChild(c));
    if (!edit) return;
    [...grid.children].forEach(c => {
      c.classList.add('relative');
      const w = document.createElement('div');
      w.className = 'ho-arrows absolute top-1 left-1 flex gap-1 z-10';
      const cls = 'px-2 py-0.5 bg-gray-800 border border-gray-600 text-gray-200 rounded text-xs cursor-pointer';
      w.innerHTML = `<span data-d="-1" class="${cls}">▲</span><span data-d="1" class="${cls}">▼</span>`;
      c.appendChild(w);
    });
  }

  grid.addEventListener('click', e => {
    if (!edit) return;
    e.stopPropagation(); e.preventDefault();
    const a = e.target.closest('.ho-arrows span');
    if (!a) return;
    const keys = [...grid.children].map(c => c.dataset.key);
    const k = a.closest('[data-key]').dataset.key, i = keys.indexOf(k), t = i + parseInt(a.dataset.d, 10);
    if (t < 0 || t >= keys.length) return;
    [keys[i], keys[t]] = [keys[t], keys[i]];
    state.homeOrder = keys;
    saveData(); apply();
  }, true);

  const head = document.querySelector('#view-home > div');
  const btn = document.createElement('button');
  btn.className = 'mt-2 text-[10px] border border-gray-600 text-gray-300 px-2 py-1 rounded';
  btn.innerText = '↕ ترتيب المهام';
  btn.onclick = () => { edit = !edit; btn.innerText = edit ? '✔ تم الترتيب' : '↕ ترتيب المهام'; apply(); };
  head.appendChild(btn);
  apply();
})();

// ===== المعتقدات (في ركن الدعاء) =====
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
  box.className = 'card-bg p-3 rounded-xl border border-indigo-500/40 space-y-2';
  box.innerHTML = `
    <div class="flex justify-between items-center">
      <h2 class="text-sm font-bold text-indigo-300">🧠 معتقداتي</h2>
      <button onclick="blAdd()" class="text-[10px] bg-indigo-950 border border-indigo-500 px-2 py-1 rounded text-indigo-300 font-bold">+ معتقد جديد</button>
    </div>
    <div id="beliefsList" class="space-y-1.5"></div>`;
  document.getElementById('duaaList').before(box);

  function render() {
    const list = document.getElementById('beliefsList');
    list.innerHTML = '';
    state.beliefs.forEach((b, i) => {
      const row = document.createElement('div');
      row.className = 'flex justify-between items-center gap-2 bg-gray-900/60 border border-gray-800 rounded-lg p-2';
      row.innerHTML = `
        <span class="text-xs text-indigo-100 leading-relaxed flex-1">${esc(b.text)}</span>
        <div class="flex items-center gap-1 shrink-0">
          <button onclick="blMove(${i},-1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▲</button>
          <button onclick="blMove(${i},1)" class="px-1.5 py-0.5 bg-gray-800 text-gray-300 rounded text-xs">▼</button>
          <button onclick="blEdit(${b.id})" class="px-1.5 py-0.5 bg-gray-800 text-cyan-400 rounded text-xs">✏️</button>
          <button onclick="blDel(${b.id})" class="px-1.5 py-0.5 bg-gray-800 text-red-400 rounded text-xs">✕</button>
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
</script>
</body>
</html>
