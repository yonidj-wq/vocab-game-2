<!doctype html>
<html lang="he" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Unit 2 - משחק הכנה</title>
  <style>
    :root { font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial; }
    body { margin:0; background:#f6f7fb; color:#111; }
    header { background:#111827; color:#fff; padding:14px 16px; }
    header h1 { margin:0; font-size:18px; }
    header p { margin:6px 0 0; opacity:.9; font-size:13px; }

    main { padding:14px; max-width: 980px; margin: 0 auto; }

    .card {
      background:#fff; border:1px solid #e5e7eb; border-radius:16px; padding:14px; margin-bottom:12px;
      box-shadow: 0 1px 0 rgba(0,0,0,.02);
    }
    .row { display:flex; gap:10px; flex-wrap:wrap; align-items:center; }
    .row > * { flex: 1 1 auto; }
    .muted { color:#6b7280; font-size:13px; }
    .btn {
      border:1px solid #d1d5db; background:#fff; padding:10px 12px; border-radius:12px;
      cursor:pointer; font-weight:800;
    }
    .btn.primary { background:#2563eb; border-color:#2563eb; color:#fff; }
    .btn.good { background:#16a34a; border-color:#16a34a; color:#fff; }
    .btn.warn { background:#f59e0b; border-color:#f59e0b; color:#111; }
    .btn:disabled { opacity:.55; cursor:not-allowed; }

    select, input[type="number"] {
      width:100%; padding:10px 12px; border-radius:12px; border:1px solid #d1d5db; background:#fff;
      font-size:15px;
    }

    .pill { display:inline-flex; align-items:center; gap:8px; padding:8px 10px; border-radius:999px; background:#f3f4f6; border:1px solid #e5e7eb; }
    .listenBtn { padding:8px 10px; border-radius:999px; border:1px solid #d1d5db; background:#fff; cursor:pointer; font-weight:900; }
    .hr { height:1px; background:#e5e7eb; margin:12px 0; }

    .bigTitle { display:flex; align-items:center; justify-content:space-between; gap:10px; }
    .bigTitle h2 { margin:0; font-size:16px; }
    .bigTitle .muted { margin:0; }

    .task {
      border:1px solid #e5e7eb; border-radius:16px; padding:14px; background:#fff;
      display:flex; flex-direction:column; gap:10px;
    }
    .task .prompt { font-weight:900; font-size:16px; }
    .task .sub { color:#6b7280; font-size:13px; }
    .task .answers { display:flex; gap:10px; flex-wrap:wrap; }
    .task label {
      border:1px solid #e5e7eb; background:#fff; padding:10px 12px; border-radius:12px; cursor:pointer;
      display:flex; gap:8px; align-items:center;
    }
    .task input[type="radio"] { transform: scale(1.1); }

    .feedback { padding:10px 12px; border-radius:12px; border:1px solid #e5e7eb; background:#f9fafb; }
    .feedback.good { border-color:#16a34a55; background:#16a34a10; }
    .feedback.bad  { border-color:#ef444455; background:#ef444410; }

    .readingBox {
      background:#fff; border:1px solid #e5e7eb; border-radius:16px; padding:14px; line-height:1.55;
      direction:ltr; white-space:pre-wrap;
    }

    /* confetti */
    .confetti {
      position: fixed; inset: 0; pointer-events:none; overflow:hidden; z-index: 9999;
    }
    .confetti i {
      position:absolute; top:-20px; width:10px; height:14px; border-radius:3px;
      opacity:.9; animation: fall 900ms linear forwards;
    }
    @keyframes fall {
      to { transform: translateY(110vh) rotate(360deg); opacity: 0.9; }
    }

    @media (max-width: 720px) {
      .row { align-items:stretch; }
    }
  </style>
</head>

<body>
<header>
  <h1>Unit 2 - משחק הכנה</h1>
  <p>לחצו 🔊 כדי לשמוע. אפשר להחליף סט ולהגריל משחק חדש בכל פעם.</p>
</header>

<main>

  <div class="card">
    <div class="bigTitle">
      <h2>שליטה במשחק</h2>
      <p class="muted">הכל מתעדכן אוטומטית לפי הסט וההגרלה</p>
    </div>

    <div class="hr"></div>

    <div class="row">
      <div>
        <div class="muted">בחר סט (Deck)</div>
        <select id="deckSelect"></select>
      </div>

      <div>
        <div class="muted">כמה משימות במשחק</div>
        <input id="taskCount" type="number" min="5" max="30" step="1" value="12">
      </div>

      <div style="min-width: 190px;">
        <div class="muted">קול (English)</div>
        <select id="voiceSelect"></select>
      </div>
    </div>

    <div class="row" style="margin-top:10px;">
      <button class="btn warn" id="refreshBtn">רענן משחק (הגרלה חדשה)</button>
      <button class="btn primary" id="startBtn">התחל משחק</button>
      <button class="btn" id="resetBtn">איפוס ניקוד</button>
    </div>

    <div class="hr"></div>

    <div class="row">
      <span class="pill"><b>ניקוד</b> <span id="score">0</span></span>
      <span class="pill"><b>רצף נכון</b> <span id="streak">0</span></span>
      <span class="pill"><b>כוכבים</b> <span id="stars">0</span> ⭐</span>
      <span class="pill"><b>משימה</b> <span id="progress">0</span></span>
      <span class="muted">טיפ: באייפון, אם אין קול, לחץ פעם אחת על 🔊</span>
    </div>
  </div>

  <div id="gameArea" class="card">
    <div class="bigTitle">
      <h2>המשחק</h2>
      <p class="muted">לחצו "התחל משחק" כדי לקבל משימות</p>
    </div>
    <div class="hr"></div>
    <div id="taskHost"></div>
  </div>

  <div id="practiceArea" class="card">
    <div class="bigTitle">
      <h2>תרגול חופשי</h2>
      <p class="muted">מילים עם פירוש ושמיעה, בלי ניקוד</p>
    </div>
    <div class="hr"></div>
    <div id="wordList"></div>
  </div>

</main>

<div id="confetti" class="confetti" hidden></div>

<script>
/* =========================
   DATA: כאן הכי קל לעדכן
   =========================
   מוסיפים סט חדש תחת decks.
   כל סט יכול להכיל:
   vocab: [{en,he}]
   complete: [{template, choices, answer}]
   yesno: [{statement, answer:true/false}]
   listening: [{title, transcript, questions:[mcq]}]
   readings: [{title, text, questions:[mcq]}]
*/

const DATA = {
  settings: {
    defaultVoiceLang: "en-US",
    speechRate: 0.95,
    speechPitch: 1.0,
    speechVolume: 1.0,
  },

  decks: [
    {
      id: "unit2_main",
      name: "Unit 2 - כל החומר",
      vocab: [
        { en:"something", he:"משהו" },
        { en:"sick", he:"חולה" },
        { en:"plate", he:"צלחת" },
        { en:"road", he:"כביש / דרך" },
        { en:"again", he:"שוב" },
        { en:"think", he:"לחשוב" },
        { en:"club", he:"מועדון / חוג" },
        { en:"true", he:"נכון / אמת" },
        { en:"fix", he:"לתקן" },
        { en:"way", he:"דרך" },

        { en:"later", he:"אחר כך / מאוחר יותר" },
        { en:"clock", he:"שעון" },
        { en:"adult", he:"מבוגר" },
        { en:"winner", he:"מנצח" },
        { en:"artist", he:"אמן / צייר" },

        { en:"hurt", he:"כואב / לפצוע" },
        { en:"build", he:"לבנות" },
        { en:"wait", he:"לחכות" },
        { en:"more", he:"עוד / יותר" },
        { en:"a quarter to", he:"רבע ל-" },

        { en:"car", he:"מכונית" },
        { en:"bird", he:"ציפור" },
        { en:"children", he:"ילדים" },
        { en:"coffee", he:"קפה" },
        { en:"coat", he:"מעיל" },
        { en:"boots", he:"מגפיים" },
        { en:"ice", he:"קרח" },
        { en:"penguin", he:"פינגווין" },
        { en:"sign", he:"שלט" },
        { en:"cold", he:"קר" },
        { en:"tired", he:"עייף" },
        { en:"excited", he:"נרגש" },
        { en:"old", he:"זקן / ישן" },
        { en:"snow", he:"שלג" },
        { en:"black", he:"שחור" },
        { en:"white", he:"לבן" },
        { en:"big", he:"גדול" },
        { en:"happy", he:"שמח" },
        { en:"hat", he:"כובע" },
        { en:"snowman", he:"איש שלג" },
        { en:"weather", he:"מזג אוויר" },
      ],

      complete: [
        { template:"Some people like to drink cola with ___.", choices:["ice","boots","plate","club"], answer:"ice" },
        { template:"He was the first in the ___.", choices:["race","clock","sign","road"], answer:"race" },
        { template:"We want to go to our neighbors ___.", choices:["later","again","tired","winner"], answer:"later" },
        { template:"I always ___ at a quarter to seven.", choices:["get up","build","paint","wait"], answer:"get up" },
        { template:"I was in Canada two years ___.", choices:["ago","more","cold","true"], answer:"ago" },
        { template:"The ___ painted pictures on the walls.", choices:["artist","adult","penguin","winner"], answer:"artist" },
        { template:"There ___ five clocks in my house.", choices:["is","are"], answer:"are" },
        { template:"Rami ___ a green bag.", choices:["have","has"], answer:"has" },
      ],

      yesno: [
        { statement:"The girls learn about the new clubs from a sign.", answer:true },
        { statement:"The LEGO robotics club meets on Thursdays.", answer:false },
        { statement:"The judo club meets at a quarter to five.", answer:true },
        { statement:"Pam wants to do more sports.", answer:false },
        { statement:"The Blue Birds are a basketball team.", answer:true },
        { statement:"The Blue Birds play basketball for one hour every day.", answer:false },
        { statement:"The doctor says Zack can’t play basketball for a month.", answer:true },
        { statement:"Zack helped the Blue Birds win many games.", answer:true },
      ],

      listening: [
        {
          title: "Listening: Clubs",
          transcript:
            "Robin and Pam see a sign about new clubs. The art club is on Tuesdays. The judo club is at a quarter to five. Pam is scared of dogs, so she doesn’t want the Little Vets club. In the end, the girls choose the judo club.",
          questions: [
            {
              prompt: "On Tuesdays, Robin …",
              choices: [
                "has dance lessons",
                "paints pictures at the art club",
                "plays with a little boy",
                "goes to a club with her neighbor"
              ],
              answerIndex: 1
            },
            {
              prompt: "Pam doesn’t want to go to the Little Vets club because …",
              choices: [
                "she swims on the day the Little Vets meet",
                "the animals are dirty",
                "the art club meets at the same time",
                "she’s scared of dogs"
              ],
              answerIndex: 3
            },
            {
              prompt: "In the end, the girls …",
              choices: [
                "choose the judo club",
                "don’t go to a new club",
                "go to the art club",
                "want to swim together"
              ],
              answerIndex: 0
            }
          ]
        }
      ],

      readings: [
        {
          title: "Reading: Zack and the Blue Birds",
          text:
`Zack is a basketball player. He plays with a team called the Blue Birds. They practice for two hours every day at the park.

Zack’s team is very good. They win lots of games.

Zack’s team has an important game today. The players are excited. But Zack isn’t excited. He can’t play in the game. He has a problem with his arm. It hurts when he moves it. The doctor says he can’t play basketball for a month.

Zack goes to the game, but he doesn’t play. He has a big sign with his team’s name. He watches his friends in the game. They run and throw the ball. Zack is sad. It’s hard to watch the game. Zack wants to play too.

After two hours, the Blue Birds win the game. The players get medals. Zack gets a medal too because he helped them win lots of games. Now he’s happy. He can’t wait to play basketball again in a month.`,
          questions: [
            { prompt:"Zack isn’t playing in the game because …", choices:["he doesn’t practice","he is in a race","his arm hurts","he isn’t a good player"], answerIndex:2 },
            { prompt:"At the game, Zack …", choices:["throws the ball","feels excited","makes a sign","watches the players"], answerIndex:3 },
            { prompt:"Zack is happy after the game because …", choices:["he gets a medal","he can play basketball again","his arm doesn’t hurt","everyone likes his sign"], answerIndex:0 },
            { prompt:"A good name for this story is …", choices:["Zack Wins a Basketball Game","Zack’s Problem","A Sign for Zack","Zack’s Friends"], answerIndex:1 },
          ]
        }
      ]
    },

    // דוגמה לסט נוסף (רענון לפי נושא)
    {
      id: "unit2_quick",
      name: "Unit 2 - חזרה קצרה",
      vocab: [
        { en:"club", he:"מועדון / חוג" },
        { en:"sign", he:"שלט" },
        { en:"artist", he:"אמן / צייר" },
        { en:"winner", he:"מנצח" },
        { en:"a quarter to", he:"רבע ל-" },
        { en:"hurt", he:"כואב" },
        { en:"ice", he:"קרח" },
        { en:"boots", he:"מגפיים" },
        { en:"snowman", he:"איש שלג" },
        { en:"weather", he:"מזג אוויר" },
      ],
      complete: [
        { template:"The ___ painted pictures.", choices:["artist","penguin","plate"], answer:"artist" },
        { template:"Be careful on the ___.", choices:["ice","coffee","road"], answer:"ice" },
        { template:"It is a quarter to ___.", choices:["five","plate","club"], answer:"five" }, // אפשר להחליף למה שמתאים לכם
      ],
      yesno: [
        { statement:"A penguin can fly.", answer:false },
        { statement:"A snowman is made of snow.", answer:true },
      ],
      listening: [],
      readings: []
    }
  ]
};

/* =========================
   Audio (Speech)
   ========================= */
let voicesReady = false;
let chosenVoiceURI = "";

function getVoices() {
  return window.speechSynthesis?.getVoices?.() || [];
}

function populateVoices() {
  const sel = document.getElementById("voiceSelect");
  sel.innerHTML = "";
  const voices = getVoices();

  const english = voices.filter(v => (v.lang || "").toLowerCase().startsWith("en"));
  const list = english.length ? english : voices;

  list.forEach(v => {
    const opt = document.createElement("option");
    opt.value = v.voiceURI;
    opt.textContent = `${v.name} (${v.lang})`;
    sel.appendChild(opt);
  });

  const preferred = list.find(v => (v.lang || "").toLowerCase() === DATA.settings.defaultVoiceLang.toLowerCase());
  const fallback = preferred || list[0];
  if (fallback) {
    sel.value = fallback.voiceURI;
    chosenVoiceURI = fallback.voiceURI;
  }

  sel.addEventListener("change", () => {
    chosenVoiceURI = sel.value;
  });
}

function pickVoice() {
  const voices = getVoices();
  if (!voices.length) return null;
  if (chosenVoiceURI) return voices.find(v => v.voiceURI === chosenVoiceURI) || null;
  return voices[0] || null;
}

function speak(text) {
  if (!("speechSynthesis" in window)) {
    alert("אין תמיכה בהשמעה בדפדפן הזה.");
    return;
  }
  window.speechSynthesis.cancel();
  const u = new SpeechSynthesisUtterance(text);
  u.rate = DATA.settings.speechRate;
  u.pitch = DATA.settings.speechPitch;
  u.volume = DATA.settings.speechVolume;

  const v = pickVoice();
  if (v) {
    u.voice = v;
    u.lang = v.lang;
  }
  window.speechSynthesis.speak(u);
}

if ("speechSynthesis" in window) {
  window.speechSynthesis.onvoiceschanged = () => { voicesReady = true; populateVoices(); };
  setTimeout(() => { voicesReady = true; populateVoices(); }, 300);
}

/* =========================
   State
   ========================= */
const KEY = "unit2_fun_game_v1";
let state = {
  deckId: DATA.decks[0].id,
  seed: Date.now(),
  score: 0,
  streak: 0,
  stars: 0,
  currentTasks: [],
  taskIndex: 0,
};

function loadState() {
  try {
    const raw = localStorage.getItem(KEY);
    if (raw) state = Object.assign(state, JSON.parse(raw));
  } catch {}
}
function saveState() {
  localStorage.setItem(KEY, JSON.stringify(state));
  renderTop();
}
function resetScore() {
  state.score = 0;
  state.streak = 0;
  state.stars = 0;
  saveState();
  renderGame();
}
function getDeck() {
  return DATA.decks.find(d => d.id === state.deckId) || DATA.decks[0];
}

/* =========================
   Utils
   ========================= */
function el(tag, attrs={}, children=[]) {
  const node = document.createElement(tag);
  for (const [k,v] of Object.entries(attrs)) {
    if (k === "class") node.className = v;
    else if (k.startsWith("on") && typeof v === "function") node.addEventListener(k.slice(2), v);
    else if (k === "html") node.innerHTML = v;
    else node.setAttribute(k, v);
  }
  for (const c of children) node.appendChild(typeof c === "string" ? document.createTextNode(c) : c);
  return node;
}
function shuffle(arr, seed) {
  const a = arr.slice();
  let s = seed || Date.now();
  function rnd() { s = (s * 1664525 + 1013904223) % 4294967296; return s / 4294967296; }
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(rnd() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}
function listenBtn(text, label="🔊") {
  return el("button", { class:"listenBtn", type:"button", onclick: () => speak(text) }, [label]);
}
function feedback(msg, ok) {
  return el("div", { class: "feedback " + (ok ? "good":"bad") }, [msg]);
}

/* =========================
   Confetti
   ========================= */
function popConfetti() {
  const box = document.getElementById("confetti");
  box.innerHTML = "";
  box.hidden = false;

  const colors = ["#2563eb","#16a34a","#f59e0b","#ef4444","#8b5cf6"];
  for (let i = 0; i < 26; i++) {
    const piece = document.createElement("i");
    piece.style.left = Math.floor(Math.random()*100) + "vw";
    piece.style.background = colors[Math.floor(Math.random()*colors.length)];
    piece.style.transform = `translateY(0) rotate(${Math.random()*180}deg)`;
    piece.style.animationDuration = (650 + Math.random()*500) + "ms";
    box.appendChild(piece);
  }
  setTimeout(() => { box.hidden = true; box.innerHTML = ""; }, 950);
}

/* =========================
   Build tasks (ריענון)
   ========================= */
function buildTasks(taskCount) {
  const deck = getDeck();

  const tasks = [];

  // 1) Vocab meaning MCQ
  const vocab = deck.vocab || [];
  const vocabShuffled = shuffle(vocab, state.seed + 1);
  vocabShuffled.forEach((w) => {
    const wrongPool = shuffle(vocab.filter(x => x.en !== w.en), state.seed + w.en.length).slice(0, 3);
    const choices = shuffle([w.he, ...wrongPool.map(x => x.he)], state.seed + 7);
    tasks.push({
      type: "vocab_mcq",
      speakText: w.en,
      prompt: `מה הפירוש של "${w.en}"?`,
      sub: "בחר/י תשובה ואז בדיקה",
      choices,
      answer: w.he
    });
  });

  // 2) Complete sentences
  const comp = deck.complete || [];
  shuffle(comp, state.seed + 2).forEach((c) => {
    tasks.push({
      type: "complete",
      speakText: c.template.replace("___", c.answer),
      prompt: c.template.replace("___", "______"),
      sub: "בחר/י את המילה הנכונה",
      choices: c.choices,
      answer: c.answer
    });
  });

  // 3) Yes/No
  const yn = deck.yesno || [];
  shuffle(yn, state.seed + 3).forEach((q) => {
    tasks.push({
      type: "yesno",
      speakText: q.statement,
      prompt: q.statement,
      sub: "Yes או No",
      choices: ["Yes", "No"],
      answer: q.answer ? "Yes" : "No"
    });
  });

  // 4) Listening MCQ (use transcript + questions)
  const listening = deck.listening || [];
  shuffle(listening, state.seed + 4).forEach((set) => {
    if (!set.questions || !set.questions.length) return;
    const qs = shuffle(set.questions, state.seed + 40).slice(0, Math.min(2, set.questions.length));
    qs.forEach((q) => {
      tasks.push({
        type: "listening_mcq",
        speakText: set.transcript,
        prompt: `Listening: ${q.prompt}`,
        sub: "לחץ/י 🔊 כדי לשמוע את כל ההאזנה, ואז ענה/י",
        choices: q.choices,
        answer: q.choices[q.answerIndex]
      });
    });
  });

  // 5) Reading MCQ
  const readings = deck.readings || [];
  shuffle(readings, state.seed + 5).forEach((r) => {
    if (!r.questions || !r.questions.length) return;
    const q = shuffle(r.questions, state.seed + 50)[0];
    tasks.push({
      type: "reading_mcq",
      speakText: r.text,
      prompt: `Reading: ${q.prompt}`,
      sub: "לחץ/י 🔊 כדי לשמוע את הטקסט",
      choices: q.choices,
      answer: q.choices[q.answerIndex],
      extraText: r.text
    });
  });

  const final = shuffle(tasks, state.seed + 99).slice(0, taskCount);
  return final;
}

/* =========================
   Rendering
   ========================= */
function renderTop() {
  document.getElementById("score").textContent = String(state.score);
  document.getElementById("streak").textContent = String(state.streak);
  document.getElementById("stars").textContent = String(state.stars);
  document.getElementById("progress").textContent = state.currentTasks.length
    ? `${state.taskIndex + 1}/${state.currentTasks.length}`
    : "0";
}

function renderDeckSelect() {
  const sel = document.getElementById("deckSelect");
  sel.innerHTML = "";
  DATA.decks.forEach(d => {
    const opt = document.createElement("option");
    opt.value = d.id;
    opt.textContent = d.name;
    sel.appendChild(opt);
  });
  sel.value = state.deckId;
  sel.addEventListener("change", () => {
    state.deckId = sel.value;
    state.seed = Date.now();
    state.currentTasks = [];
    state.taskIndex = 0;
    saveState();
    renderPractice();
    renderGame();
  });
}

function renderPractice() {
  const deck = getDeck();
  const host = document.getElementById("wordList");
  host.innerHTML = "";

  const items = deck.vocab || [];
  const chunk = shuffle(items, state.seed + 123).slice(0, Math.min(24, items.length));

  chunk.forEach(w => {
    host.appendChild(
      el("div", { class:"row", style:"border:1px solid #e5e7eb; border-radius:14px; padding:10px 12px; margin-bottom:8px; background:#fff;" }, [
        el("div", {}, [ el("b", {}, [w.en]), el("div", { class:"muted" }, [w.he]) ]),
        el("div", { style:"display:flex; gap:10px; justify-content:flex-start;" }, [
          listenBtn(w.en),
          el("button", { class:"btn", type:"button", onclick: () => speak(w.en + ". " + w.he) }, ["🔊 מילה + פירוש"])
        ])
      ])
    );
  });

  host.appendChild(el("div", { class:"muted" }, ["רוצה עוד מילים אחרות? לחץ/י למעלה על רענן משחק."]));
}

function renderGame() {
  const host = document.getElementById("taskHost");
  host.innerHTML = "";

  if (!state.currentTasks.length) {
    host.appendChild(el("div", { class:"muted" }, ["עדיין לא התחלת משחק. לחץ/י על 'התחל משחק'."]));
    renderTop();
    return;
  }

  const task = state.currentTasks[state.taskIndex];
  const taskBox = el("div", { class:"task" });

  const header = el("div", { class:"row" }, [
    el("div", {}, [
      el("div", { class:"prompt" }, [task.prompt]),
      el("div", { class:"sub" }, [task.sub || ""])
    ]),
    el("div", { style:"display:flex; gap:10px; justify-content:flex-start; flex-wrap:wrap;" }, [
      listenBtn(task.speakText || task.prompt, "🔊"),
      el("button", { class:"btn", type:"button", onclick: () => speak(task.prompt) }, ["🔊 שאלה"]),
    ])
  ]);

  taskBox.appendChild(header);

  if (task.extraText) {
    taskBox.appendChild(el("div", { class:"readingBox" }, [task.extraText]));
  }

  const answers = el("div", { class:"answers" });
  const name = "q_" + state.taskIndex;

  task.choices.forEach(ch => {
    answers.appendChild(
      el("label", {}, [
        el("input", { type:"radio", name, value:ch }),
        ch
      ])
    );
  });

  taskBox.appendChild(answers);

  const btnRow = el("div", { class:"row" }, [
    el("button", { class:"btn primary", id:"checkBtn", type:"button" }, ["בדיקה"]),
    el("button", { class:"btn", id:"skipBtn", type:"button" }, ["דלג/י"])
  ]);

  taskBox.appendChild(btnRow);

  const checkBtn = btnRow.querySelector("#checkBtn");
  const skipBtn = btnRow.querySelector("#skipBtn");

  checkBtn.addEventListener("click", () => {
    const chosen = taskBox.querySelector(`input[name="${name}"]:checked`);
    const oldFb = taskBox.querySelector(".feedback");
    if (oldFb) oldFb.remove();

    if (!chosen) {
      taskBox.appendChild(feedback("בחר/י תשובה קודם.", false));
      return;
    }

    const ok = chosen.value === task.answer;

    if (ok) {
      state.score += 1;
      state.streak += 1;

      if (state.streak % 3 === 0) {
        state.stars += 1;
        popConfetti();
        taskBox.appendChild(feedback("רצף 3 נכון! קיבלת כוכב ⭐", true));
      } else {
        taskBox.appendChild(feedback("נכון! ✅", true));
      }
    } else {
      state.streak = 0;
      taskBox.appendChild(feedback(`לא בדיוק. התשובה: ${task.answer}`, false));
    }

    saveState();
    goNextAfter(650);
  });

  skipBtn.addEventListener("click", () => {
    const oldFb = taskBox.querySelector(".feedback");
    if (oldFb) oldFb.remove();
    state.streak = 0;
    saveState();
    goNextAfter(150);
  });

  host.appendChild(taskBox);
  renderTop();
}

function goNextAfter(ms) {
  setTimeout(() => {
    if (state.taskIndex < state.currentTasks.length - 1) {
      state.taskIndex += 1;
      saveState();
      renderGame();
      window.scrollTo({ top: 0, behavior: "smooth" });
    } else {
      endGame();
    }
  }, ms);
}

function endGame() {
  const host = document.getElementById("taskHost");
  host.innerHTML = "";

  const msg = el("div", { class:"card", style:"background:#111827; color:#fff; border-color:#111827;" }, [
    el("div", { class:"bigTitle" }, [
      el("h2", {}, ["סיימת משחק!"]),
      el("div", { class:"muted", style:"color:#cbd5e1;" }, ["בוא נרענן ונעשה עוד סיבוב"])
    ]),
    el("div", { class:"hr", style:"background:#334155;" }),
    el("div", { class:"row" }, [
      el("span", { class:"pill" }, [el("b", {}, ["ניקוד"]), " " + state.score]),
      el("span", { class:"pill" }, [el("b", {}, ["כוכבים"]), " " + state.stars + " ⭐"]),
      el("span", { class:"pill" }, [el("b", {}, ["רצף מקס"]), " " + state.streak]),
    ]),
    el("div", { style:"margin-top:10px; display:flex; gap:10px; flex-wrap:wrap;" }, [
      el("button", { class:"btn warn", type:"button", onclick: () => { state.seed = Date.now(); startGame(); } }, ["עוד משחק חדש"]),
      el("button", { class:"btn", type:"button", onclick: () => { renderPractice(); } }, ["תרגול מילים"]),
    ])
  ]);

  host.appendChild(msg);
  popConfetti();
  state.currentTasks = [];
  state.taskIndex = 0;
  saveState();
  renderTop();
}

/* =========================
   Controls
   ========================= */
function startGame() {
  const count = Math.max(5, Math.min(30, Number(document.getElementById("taskCount").value || 12)));
  state.currentTasks = buildTasks(count);
  state.taskIndex = 0;
  saveState();
  renderGame();
}

function refreshGame() {
  state.seed = Date.now();
  state.currentTasks = [];
  state.taskIndex = 0;
  saveState();
  renderPractice();
  renderGame();
}

/* =========================
   Init
   ========================= */
loadState();
renderDeckSelect();
renderPractice();
renderGame();
renderTop();

document.getElementById("startBtn").addEventListener("click", startGame);
document.getElementById("refreshBtn").addEventListener("click", refreshGame);
document.getElementById("resetBtn").addEventListener("click", () => {
  if (confirm("לאפס ניקוד, רצף וכוכבים?")) resetScore();
});
</script>

</body>
</html>
