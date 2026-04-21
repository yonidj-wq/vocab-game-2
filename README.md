<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>משימות ותקציב — עורף 9220</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<style>
:root {
  --bg:#111318; --s1:#1a1d24; --s2:#22262f;
  --border:#2e3340; --border2:#3a4050;
  --gold:#c9a84c; --gold-l:#e2c97e;
  --lime:#8db63c; --lime-l:#aed45a;
  --text:#e8e4d8; --muted:#8a8880; --dim:#44444a;
  --red:#ef4444; --orange:#f97316; --purple:#a855f7; --blue:#60a5fa;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:'Segoe UI',Arial,sans-serif;background:var(--bg);color:var(--text);direction:rtl;min-height:100vh;}

header{background:linear-gradient(135deg,#1e2130,#111318);padding:14px 28px;border-bottom:2px solid var(--gold);display:flex;align-items:center;gap:16px;}
header img{height:58px;width:58px;object-fit:contain;filter:drop-shadow(0 2px 6px rgba(0,0,0,.6));}
.htext h1{font-size:1.5rem;color:var(--gold-l);font-weight:800;}
.htext .sub{font-size:.82rem;color:var(--muted);margin-top:2px;}
.nav-links{margin-right:auto;display:flex;gap:10px;}
.nav-btn{background:var(--s1);border:1px solid var(--border2);color:var(--muted);padding:6px 16px;border-radius:8px;cursor:pointer;font-size:.84rem;text-decoration:none;transition:border-color .15s,color .15s;}
.nav-btn:hover,.nav-btn.active{border-color:var(--gold);color:var(--gold-l);}

.main{padding:22px 28px;}
.sec-title{font-size:1rem;font-weight:700;color:var(--gold);border-bottom:1px solid var(--border);padding-bottom:8px;margin-bottom:16px;display:flex;align-items:center;justify-content:space-between;}
.row{display:grid;gap:16px;margin-bottom:24px;}
.row-4{grid-template-columns:repeat(auto-fit,minmax(180px,1fr));}
.row-2{grid-template-columns:1fr 1fr;}
.row-3{grid-template-columns:1fr 1fr 1fr;}
@media(max-width:760px){.row-2,.row-3{grid-template-columns:1fr;}}
.card{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:18px;}
.card h3{font-size:.9rem;color:var(--muted);font-weight:600;margin-bottom:12px;}

/* KPIs */
.kpi-mini{text-align:center;padding:16px 12px;position:relative;overflow:hidden;}
.kpi-mini::before{content:'';position:absolute;top:0;right:0;left:0;height:3px;}
.kpi-mini.gold::before{background:var(--gold);}
.kpi-mini.lime::before{background:var(--lime);}
.kpi-mini.red::before{background:var(--red);}
.kpi-mini.blue::before{background:var(--blue);}
.kpi-mini.orange::before{background:var(--orange);}
.kpi-mini .kv{font-size:1.9rem;font-weight:800;line-height:1.1;}
.kpi-mini.gold .kv{color:var(--gold-l);}
.kpi-mini.lime .kv{color:var(--lime-l);}
.kpi-mini.red .kv{color:#fca5a5;}
.kpi-mini.blue .kv{color:var(--blue);}
.kpi-mini.orange .kv{color:#fdba74;}
.kpi-mini .kl{font-size:.78rem;color:var(--muted);margin-top:4px;}
.kpi-mini .ks{font-size:.7rem;color:var(--dim);margin-top:2px;}

/* Budget pool */
.pool-card{background:var(--s1);border:2px solid var(--gold);border-radius:14px;padding:22px;margin-bottom:24px;}
.pool-top{display:flex;justify-content:space-between;align-items:flex-start;gap:20px;flex-wrap:wrap;margin-bottom:18px;}
.pool-balance{text-align:center;}
.pool-balance .pb-val{font-size:2.6rem;font-weight:900;color:var(--gold-l);line-height:1;}
.pool-balance .pb-lbl{font-size:.8rem;color:var(--muted);margin-top:4px;}
.pool-nums{display:flex;gap:24px;flex-wrap:wrap;align-items:center;}
.pool-num{text-align:center;}
.pool-num .pn-val{font-size:1.4rem;font-weight:800;}
.pool-num.income .pn-val{color:var(--lime-l);}
.pool-num.spent .pn-val{color:#fca5a5;}
.pool-num.planned .pn-val{color:var(--gold-l);}
.pool-num .pn-lbl{font-size:.72rem;color:var(--muted);margin-top:2px;}
.pool-bar-wrap{background:var(--bg);border-radius:8px;height:10px;overflow:hidden;margin-bottom:6px;}
.pool-bar-inner{height:100%;border-radius:8px;display:flex;gap:2px;}
.pool-seg{height:100%;border-radius:6px;transition:width .4s;}
.pool-legend{display:flex;gap:16px;font-size:.75rem;color:var(--muted);flex-wrap:wrap;}
.pool-legend span{display:flex;align-items:center;gap:5px;}
.pool-legend .dot{width:8px;height:8px;border-radius:50%;}

/* Income list */
.income-list{display:flex;flex-direction:column;gap:6px;}
.income-row{display:flex;align-items:center;gap:10px;padding:8px 12px;background:var(--bg);border-radius:8px;font-size:.84rem;}
.income-row .ir-type{padding:2px 8px;border-radius:10px;font-size:.72rem;font-weight:700;white-space:nowrap;}
.ir-donation{background:#1e2812;color:var(--lime-l);}
.ir-campaign{background:#252018;color:var(--gold-l);}
.ir-other{background:#1a1e30;color:var(--blue);}
.income-row .ir-desc{flex:1;color:var(--text);}
.income-row .ir-date{color:var(--dim);font-size:.75rem;width:76px;flex-shrink:0;}
.income-row .ir-amount{color:var(--lime-l);font-weight:700;white-space:nowrap;}

/* Persons */
.persons-row{display:grid;grid-template-columns:repeat(auto-fit,minmax(190px,1fr));gap:14px;margin-bottom:24px;}
.person-card{background:var(--s1);border:1px solid var(--border);border-radius:12px;padding:16px;cursor:pointer;transition:border-color .15s,transform .15s;}
.person-card:hover{border-color:var(--gold);transform:translateY(-2px);}
.person-card.active-person{border-color:var(--gold);box-shadow:0 0 0 2px rgba(201,168,76,.25);}
.person-avatar{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.2rem;font-weight:800;}
.person-name{font-weight:700;font-size:.95rem;color:var(--text);}
.person-role{font-size:.73rem;color:var(--muted);margin-top:2px;line-height:1.4;}
.person-stats{display:flex;gap:6px;margin-top:10px;flex-wrap:wrap;}
.pstat{font-size:.7rem;padding:2px 7px;border-radius:10px;font-weight:600;}
.pstat-open{background:#25200f;color:var(--gold-l);}
.pstat-done{background:#1a2812;color:var(--lime-l);}
.pstat-urgent{background:#2a1010;color:#fca5a5;}
.pstat-budget{background:#1a1e30;color:var(--blue);}

/* Domain tabs */
.domain-tabs{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:20px;}
.dtab{padding:7px 18px;border-radius:20px;border:1px solid var(--border2);background:var(--s1);color:var(--muted);cursor:pointer;font-size:.84rem;transition:all .15s;}
.dtab:hover{border-color:var(--gold);color:var(--gold-l);}
.dtab.active{background:#252018;border-color:var(--gold);color:var(--gold-l);font-weight:700;}

/* Filters */
.task-filters{display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-bottom:14px;}
.task-filters input[type=search]{background:var(--bg);border:1px solid var(--border2);color:var(--text);padding:7px 14px;border-radius:8px;font-size:.85rem;outline:none;width:220px;direction:rtl;}
.task-filters input:focus{border-color:var(--gold);}
.task-filters select{background:var(--bg);border:1px solid var(--border2);color:var(--text);padding:7px 12px;border-radius:8px;font-size:.84rem;outline:none;direction:rtl;}
.task-filters select:focus{border-color:var(--gold);}

/* Task table */
.task-table{width:100%;border-collapse:collapse;font-size:.84rem;}
.task-table thead th{background:var(--bg);color:var(--gold);padding:9px 12px;text-align:right;font-weight:700;border-bottom:2px solid var(--border);white-space:nowrap;}
.task-table tbody tr{border-bottom:1px solid var(--s1);transition:background .12s;}
.task-table tbody tr:hover{background:var(--s2);}
.task-table tbody td{padding:8px 12px;vertical-align:middle;}
.task-expand-row td{background:var(--bg);padding:0;}
.task-detail{padding:14px 20px;display:grid;grid-template-columns:1fr 1fr;gap:12px;font-size:.82rem;}
.td-section{display:flex;flex-direction:column;gap:6px;}
.td-label{font-size:.72rem;color:var(--muted);font-weight:600;margin-bottom:2px;}

/* Badges */
.status-badge{display:inline-block;padding:2px 10px;border-radius:12px;font-size:.72rem;font-weight:700;white-space:nowrap;}
.s-open{background:#252018;color:var(--gold-l);}
.s-progress{background:#1a1e30;color:#93c5fd;}
.s-done{background:#1a2812;color:var(--lime-l);}
.s-blocked{background:#2a1010;color:#fca5a5;}
.priority-dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-left:5px;}
.p-high{background:var(--red);}
.p-mid{background:var(--orange);}
.p-low{background:var(--lime);}
.domain-chip{display:inline-block;padding:2px 8px;border-radius:10px;font-size:.72rem;font-weight:600;white-space:nowrap;}
.d-0{background:#252018;color:var(--gold-l);}
.d-1{background:#1a1e30;color:#93c5fd;}
.d-2{background:#251a30;color:#d8b4fe;}
.d-3{background:#1a2814;color:var(--lime-l);}
.assignee-chip{display:inline-flex;align-items:center;gap:5px;padding:2px 8px;border-radius:10px;font-size:.72rem;font-weight:600;white-space:nowrap;}
.assignee-dot{width:7px;height:7px;border-radius:50%;}

/* Task budget mini bar */
.task-budget-bar{display:flex;align-items:center;gap:8px;font-size:.75rem;}
.tbbar-wrap{flex:1;background:var(--bg);border-radius:4px;height:5px;overflow:hidden;min-width:40px;}
.tbbar-fill{height:100%;border-radius:4px;transition:width .3s;}

/* Expense rows inside task */
.exp-mini-row{display:flex;align-items:center;gap:8px;padding:4px 0;border-bottom:1px solid var(--border);font-size:.78rem;}
.exp-mini-row:last-child{border-bottom:none;}
.exp-mini-date{color:var(--dim);width:70px;flex-shrink:0;}
.exp-mini-desc{flex:1;color:var(--text);}
.exp-mini-amount{color:var(--gold-l);font-weight:700;}

/* Buttons */
.btn{padding:7px 16px;border-radius:8px;cursor:pointer;font-size:.84rem;border:none;transition:background .15s;font-family:inherit;}
.btn-gold{background:var(--gold);color:#0e1010;font-weight:700;}
.btn-gold:hover{background:var(--gold-l);}
.btn-outline{background:var(--s1);border:1px solid var(--border2);color:var(--muted);}
.btn-outline:hover{border-color:var(--gold);color:var(--gold-l);}
.btn-lime{background:#1e2812;border:1px solid var(--lime);color:var(--lime-l);}
.btn-lime:hover{background:#2a3a18;}
.btn-sm{padding:3px 10px;font-size:.75rem;}
.icon-btn{background:none;border:none;cursor:pointer;padding:3px 6px;border-radius:6px;font-size:.85rem;font-family:inherit;}
.icon-btn:hover{background:var(--s2);}

/* Month timeline */
.month-chart-wrap{position:relative;height:220px;}

/* Modal */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.72);z-index:100;display:flex;align-items:center;justify-content:center;padding:20px;}
.modal-overlay.hidden{display:none;}
.modal{background:var(--s1);border:1px solid var(--border2);border-radius:16px;padding:26px;width:100%;max-width:560px;max-height:90vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,.6);}
.modal h2{font-size:1.1rem;color:var(--gold-l);margin-bottom:18px;}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.fg{display:flex;flex-direction:column;gap:5px;}
.fg.span2{grid-column:span 2;}
.fg label{font-size:.78rem;color:var(--muted);}
.fg input,.fg select,.fg textarea{background:var(--bg);border:1px solid var(--border2);color:var(--text);padding:8px 12px;border-radius:8px;font-size:.88rem;outline:none;direction:rtl;font-family:inherit;}
.fg input:focus,.fg select:focus,.fg textarea:focus{border-color:var(--gold);}
.fg textarea{resize:vertical;min-height:65px;}
.modal-footer{display:flex;gap:10px;justify-content:flex-end;margin-top:18px;}
.empty-state{text-align:center;padding:36px;color:var(--dim);font-size:.9rem;}
.divider{border:none;border-top:1px solid var(--border);margin:14px 0;}
</style>
</head>
<body>

<header>
  <img src="לוגו עורף.jpg" alt="לוגו">
  <div class="htext">
    <h1>תא עורף 9220 — בית-חורון</h1>
    <div class="sub">ניהול משימות ותקציב</div>
  </div>
  <div class="nav-links">
    <a href="dashboard.html" class="nav-btn">אלפון כוח אדם</a>
    <a href="tasks.html"     class="nav-btn active">משימות ותקציב</a>
  </div>
</header>

<div class="main">

  <!-- ── KPIs ── -->
  <div class="row row-4" id="kpiRow" style="margin-bottom:20px"></div>

  <!-- ── Budget Pool ── -->
  <div class="sec-title">
    מאגר תקציב כולל
    <button class="btn btn-lime btn-sm" onclick="openIncomeModal()">+ הכנסה / תרומה</button>
  </div>

  <div class="pool-card" id="poolCard"></div>

  <div class="row row-2" style="margin-bottom:24px">
    <div class="card">
      <h3>הכנסות vs הוצאות לפי חודש</h3>
      <div class="month-chart-wrap"><canvas id="monthChart"></canvas></div>
    </div>
    <div class="card">
      <h3>הוצאות לפי תחום</h3>
      <div class="month-chart-wrap"><canvas id="domainChart"></canvas></div>
    </div>
  </div>

  <!-- ── Persons ── -->
  <div class="sec-title">בעלי תפקידים</div>
  <div class="persons-row" id="personsRow"></div>

  <!-- ── Tasks ── -->
  <div class="sec-title">
    משימות
    <button class="btn btn-gold btn-sm" onclick="openTaskModal()">+ משימה חדשה</button>
  </div>
  <div class="domain-tabs" id="domainTabs"></div>

  <div class="card" style="margin-bottom:28px">
    <div class="task-filters">
      <input type="search" id="taskSearch" placeholder="🔍 חיפוש משימה...">
      <select id="filterPerson"><option value="">כל האנשים</option></select>
      <select id="filterStatus">
        <option value="">כל הסטטוסים</option>
        <option value="open">פתוח</option>
        <option value="progress">בביצוע</option>
        <option value="done">הושלם</option>
        <option value="blocked">חסום</option>
      </select>
      <select id="filterPriority">
        <option value="">כל העדיפויות</option>
        <option value="high">דחוף</option>
        <option value="mid">בינוני</option>
        <option value="low">נמוך</option>
      </select>
    </div>
    <div style="overflow-x:auto">
      <table class="task-table" id="taskTable">
        <thead><tr>
          <th style="width:28px"></th>
          <th style="width:28px"></th>
          <th>משימה</th>
          <th>תחום</th>
          <th>אחראי</th>
          <th>עדיפות</th>
          <th>סטטוס</th>
          <th>יעד</th>
          <th>תקציב</th>
          <th>בפועל</th>
          <th style="width:68px"></th>
        </tr></thead>
        <tbody id="taskTbody"></tbody>
      </table>
    </div>
    <div id="taskEmpty" class="empty-state" style="display:none">אין משימות התואמות את הסינון</div>
  </div>

</div>

<!-- ── Task Modal ── -->
<div class="modal-overlay hidden" id="taskModal">
  <div class="modal">
    <h2 id="modalTitle">משימה חדשה</h2>
    <div class="form-grid">
      <div class="fg span2"><label>כותרת</label><input type="text" id="fTitle" placeholder="תיאור קצר"></div>
      <div class="fg"><label>תחום</label><select id="fDomain"></select></div>
      <div class="fg"><label>אחראי</label><select id="fPerson"><option value="">— בחר —</option></select></div>
      <div class="fg"><label>עדיפות</label>
        <select id="fPriority"><option value="high">דחוף</option><option value="mid" selected>בינוני</option><option value="low">נמוך</option></select>
      </div>
      <div class="fg"><label>סטטוס</label>
        <select id="fStatus"><option value="open">פתוח</option><option value="progress">בביצוע</option><option value="done">הושלם</option><option value="blocked">חסום</option></select>
      </div>
      <div class="fg"><label>תאריך יעד</label><input type="date" id="fDue"></div>
      <div class="fg"><label>תקציב מתוכנן (₪)</label><input type="number" id="fBudget" placeholder="0" min="0"></div>
      <div class="fg span2"><label>הערות</label><textarea id="fNotes" placeholder="פרטים נוספים..."></textarea></div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeTaskModal()">ביטול</button>
      <button class="btn btn-gold" onclick="saveTask()">שמור</button>
    </div>
  </div>
</div>

<!-- ── Expense Modal ── -->
<div class="modal-overlay hidden" id="expenseModal">
  <div class="modal" style="max-width:420px">
    <h2>הוסף הוצאה — <span id="expTaskName" style="color:var(--muted)"></span></h2>
    <div class="form-grid">
      <div class="fg span2"><label>תיאור</label><input type="text" id="eDesc" placeholder="למה שולם?"></div>
      <div class="fg"><label>סכום (₪)</label><input type="number" id="eAmount" placeholder="0" min="0"></div>
      <div class="fg"><label>תאריך</label><input type="date" id="eDate"></div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeExpModal()">ביטול</button>
      <button class="btn btn-gold" onclick="saveExp()">הוסף</button>
    </div>
  </div>
</div>

<!-- ── Income Modal ── -->
<div class="modal-overlay hidden" id="incomeModal">
  <div class="modal" style="max-width:440px">
    <h2>הוסף הכנסה למאגר</h2>
    <div class="form-grid">
      <div class="fg span2"><label>תיאור</label><input type="text" id="iDesc" placeholder='למשל: "תרומת משפחת כהן"'></div>
      <div class="fg"><label>סוג</label>
        <select id="iType">
          <option value="donation">תרומה</option>
          <option value="campaign">קמפיין</option>
          <option value="other">אחר</option>
        </select>
      </div>
      <div class="fg"><label>סכום (₪)</label><input type="number" id="iAmount" placeholder="0" min="0"></div>
      <div class="fg"><label>תאריך</label><input type="date" id="iDate"></div>
      <div class="fg"><label>תורם / מקור (אופציונלי)</label><input type="text" id="iSource" placeholder="שם / ארגון"></div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="closeIncomeModal()">ביטול</button>
      <button class="btn btn-gold" onclick="saveIncome()">הוסף</button>
    </div>
  </div>
</div>

<script>
// ── Constants ────────────────────────────────────────────────────
const PERSONS = [
  {id:'yoni',   name:'יוני',    role:'מוביל צוות העורף',                       color:'#c9a84c',bg:'#252018'},
  {id:'tzahala',name:'צהלה',    role:'קצינת העורף\nקשר עם מובילות פלוגתיות', color:'#a78bfa',bg:'#1e1830'},
  {id:'ortom',  name:'אור תום', role:'מנהל קהילה',                             color:'#34d399',bg:'#0d2420'},
  {id:'ido',    name:'עידו',    role:'מוביל עורף',                             color:'#60a5fa',bg:'#101c30'},
  {id:'dekel',  name:'דקל',     role:'מוביל עורף',                             color:'#f97316',bg:'#201408'},
];
const DOMAINS = [
  {id:'donations',name:'גיוס תרומות',   icon:'💰',cls:'d-0'},
  {id:'families', name:'קשר עם המשפחות',icon:'👨‍👩‍👧',cls:'d-1'},
  {id:'events',   name:'אירועים',        icon:'🎉',cls:'d-2'},
  {id:'personal', name:'עזרה פרטנית',   icon:'🤝',cls:'d-3'},
];
const DOMAIN_COLORS = ['#c9a84c','#60a5fa','#a78bfa','#34d399'];

// ── Storage ──────────────────────────────────────────────────────
const K = k => 'oref9220_' + k;
function load(k,def){ try{return JSON.parse(localStorage.getItem(K(k)))??def;}catch{return def;} }
function save(k,v){ localStorage.setItem(K(k),JSON.stringify(v)); }

let tasks    = load('tasks2', []);
let incomes  = load('incomes', []);
// expenses are stored per-task: task.expenses = [{id,desc,amount,date}]

// ── State ────────────────────────────────────────────────────────
let activeDomain = 'all';
let activePersonFilter = '';
let editingTaskId = null;
let expenseTaskId = null;
let expandedTaskId = null;
let monthChartInst = null;
let domainChartInst = null;

// ── Helpers ──────────────────────────────────────────────────────
const genId = () => Date.now().toString(36) + Math.random().toString(36).slice(2,6);
const person = id => PERSONS.find(p=>p.id===id);
const domain = id => DOMAINS.find(d=>d.id===id);
const fmtMoney = n => '₪' + Number(n||0).toLocaleString('he-IL');
const fmtDate  = d => { if(!d) return '—'; const[y,m,dy]=d.split('-'); return dy+'/'+m+'/'+y; };
const today    = () => new Date().toISOString().slice(0,10);
const isOverdue= d => d && d < today();
const taskSpent= t => (t.expenses||[]).reduce((s,e)=>s+e.amount,0);
const totalIncome = () => incomes.reduce((s,i)=>s+i.amount,0);
const totalSpent  = () => tasks.reduce((s,t)=>s+taskSpent(t),0);
const totalPlanned= () => tasks.filter(t=>t.status!=='done').reduce((s,t)=>s+(t.budget||0),0);
const balance     = () => totalIncome() - totalSpent();

const statusLabel = s=>({open:'פתוח',progress:'בביצוע',done:'הושלם',blocked:'חסום'}[s]||s);
const statusClass = s=>({open:'s-open',progress:'s-progress',done:'s-done',blocked:'s-blocked'}[s]||'s-open');
const prioLabel   = p=>({high:'דחוף',mid:'בינוני',low:'נמוך'}[p]||p);
const prioClass   = p=>({high:'p-high',mid:'p-mid',low:'p-low'}[p]||'p-low');

function monthKey(dateStr) {
  if(!dateStr) return null;
  return dateStr.slice(0,7); // YYYY-MM
}
function monthLabel(k) {
  const[y,m]=k.split('-');
  const names=['','ינו','פבר','מרץ','אפר','מאי','יוני','יולי','אוג','ספט','אוק','נוב','דצ'];
  return names[parseInt(m)]+"'"+y.slice(2);
}

// ── Render KPIs ──────────────────────────────────────────────────
function renderKPIs() {
  const open    = tasks.filter(t=>t.status!=='done').length;
  const done    = tasks.filter(t=>t.status==='done').length;
  const urgent  = tasks.filter(t=>t.priority==='high'&&t.status!=='done').length;
  const overdue = tasks.filter(t=>t.status!=='done'&&isOverdue(t.due)).length;
  const bal     = balance();
  const balColor= bal>=0?'lime':'red';
  document.getElementById('kpiRow').innerHTML = `
    <div class="card kpi-mini gold"><div class="kv">${open}</div><div class="kl">משימות פתוחות</div><div class="ks">${overdue} מאחרות</div></div>
    <div class="card kpi-mini lime"><div class="kv">${done}</div><div class="kl">הושלמו</div></div>
    <div class="card kpi-mini red"><div class="kv">${urgent}</div><div class="kl">דחוף לטיפול</div></div>
    <div class="card kpi-mini blue"><div class="kv">${fmtMoney(totalIncome())}</div><div class="kl">סה"כ הכנסות</div></div>
    <div class="card kpi-mini ${balColor}"><div class="kv">${fmtMoney(Math.abs(bal))}</div><div class="kl">${bal>=0?'יתרה':'גרעון'}</div><div class="ks">הוצאות: ${fmtMoney(totalSpent())}</div></div>
  `;
}

// ── Render Pool ──────────────────────────────────────────────────
function renderPool() {
  const inc     = totalIncome();
  const spent   = totalSpent();
  const planned = totalPlanned();
  const bal     = inc - spent;
  const maxBar  = Math.max(inc, spent + planned, 1);
  const spentPct   = Math.min(100, spent/maxBar*100);
  const plannedPct = Math.min(100-spentPct, planned/maxBar*100);

  const incomeRows = [...incomes].reverse().map(i => `
    <div class="income-row">
      <span class="ir-date">${fmtDate(i.date)}</span>
      <span class="ir-type ${i.type==='donation'?'ir-donation':i.type==='campaign'?'ir-campaign':'ir-other'}">
        ${i.type==='donation'?'תרומה':i.type==='campaign'?'קמפיין':'אחר'}
      </span>
      <span class="ir-desc">${i.desc}${i.source?' · <span style="color:var(--dim)">'+i.source+'</span>':''}</span>
      <span class="ir-amount">${fmtMoney(i.amount)}</span>
      <button class="icon-btn btn-sm" onclick="deleteIncome('${i.id}')">×</button>
    </div>`).join('');

  document.getElementById('poolCard').innerHTML = `
    <div class="pool-top">
      <div class="pool-balance">
        <div class="pb-val" style="color:${bal>=0?'var(--lime-l)':'#fca5a5'}">${fmtMoney(Math.abs(bal))}</div>
        <div class="pb-lbl">${bal>=0?'יתרה פנויה':'גרעון'}</div>
      </div>
      <div class="pool-nums">
        <div class="pool-num income"><div class="pn-val">${fmtMoney(inc)}</div><div class="pn-lbl">סה"כ הכנסות</div></div>
        <div class="pool-num spent"><div class="pn-val">${fmtMoney(spent)}</div><div class="pn-lbl">הוצא בפועל</div></div>
        <div class="pool-num planned"><div class="pn-val">${fmtMoney(planned)}</div><div class="pn-lbl">מתוכנן (פתוח)</div></div>
        <div class="pool-num" style="text-align:center">
          <div class="pn-val" style="color:${(spent+planned)<=inc?'var(--lime-l)':'#fca5a5'}">${fmtMoney(Math.max(0,inc-spent-planned))}</div>
          <div class="pn-lbl">זמין לתכנון</div>
        </div>
      </div>
    </div>
    <div class="pool-bar-wrap">
      <div class="pool-bar-inner">
        <div class="pool-seg" style="width:${spentPct}%;background:#ef4444"></div>
        <div class="pool-seg" style="width:${plannedPct}%;background:var(--gold)"></div>
      </div>
    </div>
    <div class="pool-legend" style="margin-bottom:${incomes.length?'16px':'0'}">
      <span><span class="dot" style="background:#ef4444"></span>הוצא (${Math.round(spentPct)}%)</span>
      <span><span class="dot" style="background:var(--gold)"></span>מתוכנן (${Math.round(plannedPct)}%)</span>
      <span><span class="dot" style="background:var(--border)"></span>פנוי</span>
    </div>
    ${incomes.length ? `<div class="income-list">${incomeRows}</div>` : '<div style="color:var(--dim);font-size:.82rem;text-align:center;padding:8px">לא הוזנו הכנסות עדיין — לחץ "+ הכנסה / תרומה"</div>'}
  `;
}

// ── Render Charts ────────────────────────────────────────────────
function renderCharts() {
  // collect all months
  const allMonths = new Set();
  incomes.forEach(i=>{ if(i.date) allMonths.add(monthKey(i.date)); });
  tasks.forEach(t=>(t.expenses||[]).forEach(e=>{ if(e.date) allMonths.add(monthKey(e.date)); }));
  const months = [...allMonths].sort();

  const incByMonth  = {};
  const spentByMonth = {};
  months.forEach(m=>{ incByMonth[m]=0; spentByMonth[m]=0; });
  incomes.forEach(i=>{ if(monthKey(i.date)) incByMonth[monthKey(i.date)] += i.amount; });
  tasks.forEach(t=>(t.expenses||[]).forEach(e=>{ if(monthKey(e.date)) spentByMonth[monthKey(e.date)] += e.amount; }));

  if(monthChartInst) monthChartInst.destroy();
  monthChartInst = new Chart(document.getElementById('monthChart'),{
    type:'bar',
    data:{ labels: months.map(monthLabel),
      datasets:[
        {label:'הכנסות', data:months.map(m=>incByMonth[m]),  backgroundColor:'#2d5a1f', borderRadius:4},
        {label:'הוצאות', data:months.map(m=>spentByMonth[m]),backgroundColor:'#c9a84c', borderRadius:4},
      ]},
    options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{labels:{color:'#8a8880',font:{size:11}}}},
      scales:{x:{ticks:{color:'#8a8880'},grid:{color:'#1a1d24'}},y:{ticks:{color:'#8a8880'},grid:{color:'#2e3340'}}}}
  });

  // domain bar chart
  const domainSpent = DOMAINS.map(d=>
    tasks.filter(t=>t.domain===d.id).reduce((s,t)=>s+taskSpent(t),0)
  );
  const domainPlanned = DOMAINS.map(d=>
    tasks.filter(t=>t.domain===d.id&&t.status!=='done').reduce((s,t)=>s+(t.budget||0),0)
  );
  if(domainChartInst) domainChartInst.destroy();
  domainChartInst = new Chart(document.getElementById('domainChart'),{
    type:'bar',
    data:{ labels:DOMAINS.map(d=>d.name),
      datasets:[
        {label:'מתוכנן', data:domainPlanned, backgroundColor:'#2e3340', borderRadius:4},
        {label:'בפועל',  data:domainSpent,   backgroundColor:DOMAIN_COLORS, borderRadius:4},
      ]},
    options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{labels:{color:'#8a8880',font:{size:11}}}},
      scales:{x:{ticks:{color:'#8a8880'},grid:{color:'#1a1d24'}},y:{ticks:{color:'#8a8880'},grid:{color:'#2e3340'}}}}
  });
}

// ── Render Persons ───────────────────────────────────────────────
function renderPersons() {
  document.getElementById('personsRow').innerHTML = PERSONS.map(p => {
    const mine   = tasks.filter(t=>t.person===p.id);
    const open   = mine.filter(t=>t.status!=='done').length;
    const done   = mine.filter(t=>t.status==='done').length;
    const urgent = mine.filter(t=>t.priority==='high'&&t.status!=='done').length;
    const budget = mine.reduce((s,t)=>s+(t.budget||0),0);
    const isAct  = activePersonFilter===p.id;
    return `<div class="person-card ${isAct?'active-person':''}" onclick="togglePerson('${p.id}')">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:8px">
        <div class="person-avatar" style="background:${p.bg};color:${p.color}">${p.name[0]}</div>
        <div><div class="person-name">${p.name}</div><div class="person-role">${p.role.replace('\n','<br>')}</div></div>
      </div>
      <div class="person-stats">
        ${open   ?`<span class="pstat pstat-open">${open} פתוחות</span>`:''}
        ${done   ?`<span class="pstat pstat-done">${done} הושלמו</span>`:''}
        ${urgent ?`<span class="pstat pstat-urgent">${urgent} דחוף</span>`:''}
        ${budget ?`<span class="pstat pstat-budget">${fmtMoney(budget)}</span>`:''}
        ${!open&&!done?'<span class="pstat pstat-done">ללא משימות</span>':''}
      </div>
    </div>`;
  }).join('');
}

// ── Render Tabs ──────────────────────────────────────────────────
function renderTabs() {
  document.getElementById('domainTabs').innerHTML =
    `<div class="dtab ${activeDomain==='all'?'active':''}" onclick="setDomain('all')">הכל (${tasks.length})</div>` +
    DOMAINS.map(d=>{
      const n=tasks.filter(t=>t.domain===d.id).length;
      return `<div class="dtab ${activeDomain===d.id?'active':''}" onclick="setDomain('${d.id}')">${d.icon} ${d.name} (${n})</div>`;
    }).join('');
}

// ── Render Tasks ─────────────────────────────────────────────────
function renderTasks() {
  const q   = document.getElementById('taskSearch').value.trim().toLowerCase();
  const pF  = document.getElementById('filterPerson').value;
  const sF  = document.getElementById('filterStatus').value;
  const prF = document.getElementById('filterPriority').value;

  let list = [...tasks];
  if(activeDomain!=='all') list=list.filter(t=>t.domain===activeDomain);
  if(pF)  list=list.filter(t=>t.person===pF);
  if(sF)  list=list.filter(t=>t.status===sF);
  if(prF) list=list.filter(t=>t.priority===prF);
  if(q)   list=list.filter(t=>(t.title+' '+(t.notes||'')).toLowerCase().includes(q));

  const po={high:0,mid:1,low:2};
  list.sort((a,b)=>{
    if(a.status==='done'&&b.status!=='done') return 1;
    if(b.status==='done'&&a.status!=='done') return -1;
    if(po[a.priority]!==po[b.priority]) return po[a.priority]-po[b.priority];
    return (a.due||'9999')<(b.due||'9999')?-1:1;
  });

  const tbody=document.getElementById('taskTbody');
  if(!list.length){ tbody.innerHTML=''; document.getElementById('taskEmpty').style.display='block'; return; }
  document.getElementById('taskEmpty').style.display='none';

  const rows=[];
  list.forEach(t=>{
    const p   = person(t.person);
    const d   = domain(t.domain);
    const ov  = isOverdue(t.due)&&t.status!=='done';
    const sp  = taskSpent(t);
    const bg  = t.budget||0;
    const pct = bg ? Math.min(100,Math.round(sp/bg*100)) : 0;
    const bc  = pct>=90?'#ef4444':pct>=70?'#f97316':bg?'#8db63c':'#3a4050';
    const isExp = expandedTaskId===t.id;

    rows.push(`<tr style="${t.status==='done'?'opacity:.5':''}">
      <td>
        <input type="checkbox" ${t.status==='done'?'checked':''} onchange="toggleDone('${t.id}')"
          style="accent-color:var(--lime);width:15px;height:15px;cursor:pointer">
      </td>
      <td>
        <button class="icon-btn" onclick="toggleExpand('${t.id}')" title="פרטים">${isExp?'▲':'▼'}</button>
      </td>
      <td>
        <span style="font-weight:600;${t.status==='done'?'text-decoration:line-through;color:var(--dim)':''}">${t.title}</span>
      </td>
      <td><span class="domain-chip ${d?.cls||''}">${d?.icon||''} ${d?.name||'—'}</span></td>
      <td>${p?`<span class="assignee-chip" style="background:${p.bg};border:1px solid ${p.color}55">
        <span class="assignee-dot" style="background:${p.color}"></span>
        <span style="color:${p.color}">${p.name}</span></span>`:'—'}</td>
      <td><span class="priority-dot ${prioClass(t.priority)}"></span>${prioLabel(t.priority)}</td>
      <td><span class="status-badge ${statusClass(t.status)}">${statusLabel(t.status)}</span></td>
      <td style="color:${ov?'#fca5a5':'var(--muted)'}${ov?';font-weight:700':''}">${fmtDate(t.due)}${ov?' ⚠':''}</td>
      <td style="color:var(--gold-l)">${bg?fmtMoney(bg):'—'}</td>
      <td>
        ${bg||sp ? `<div class="task-budget-bar">
          <span style="color:${bc};font-weight:700;min-width:34px">${fmtMoney(sp)}</span>
          <div class="tbbar-wrap"><div class="tbbar-fill" style="width:${pct}%;background:${bc}"></div></div>
          <span style="color:var(--dim);font-size:.7rem">${pct}%</span>
        </div>` : '<span style="color:var(--dim)">—</span>'}
      </td>
      <td>
        <button class="icon-btn" onclick="openExpModal('${t.id}')" title="הוסף הוצאה">💸</button>
        <button class="icon-btn" onclick="openTaskModal('${t.id}')" title="ערוך">✏️</button>
        <button class="icon-btn" onclick="deleteTask('${t.id}')" title="מחק">🗑️</button>
      </td>
    </tr>`);

    if(isExp) {
      const exps = (t.expenses||[]).slice().reverse();
      rows.push(`<tr class="task-expand-row"><td colspan="11">
        <div class="task-detail">
          <div class="td-section">
            <div class="td-label">הוצאות (${exps.length})</div>
            ${exps.length ? exps.map(e=>`
              <div class="exp-mini-row">
                <span class="exp-mini-date">${fmtDate(e.date)}</span>
                <span class="exp-mini-desc">${e.desc}</span>
                <span class="exp-mini-amount">${fmtMoney(e.amount)}</span>
                <button class="icon-btn btn-sm" onclick="deleteExp('${t.id}','${e.id}')">×</button>
              </div>`).join('') : '<span style="color:var(--dim)">אין הוצאות</span>'}
            <div style="margin-top:8px">
              <button class="btn btn-outline btn-sm" onclick="openExpModal('${t.id}')">+ הוסף הוצאה</button>
            </div>
          </div>
          <div class="td-section">
            ${t.notes?`<div class="td-label">הערות</div><div style="color:var(--muted);font-size:.82rem;line-height:1.5">${t.notes}</div>`:''}
            ${bg?`<div class="td-label" style="margin-top:${t.notes?'12px':'0'}">תקציב</div>
              <div style="display:flex;gap:16px;font-size:.8rem;flex-wrap:wrap">
                <span>מתוכנן: <b style="color:var(--gold-l)">${fmtMoney(bg)}</b></span>
                <span>בפועל: <b style="color:${bc}">${fmtMoney(sp)}</b></span>
                <span>נותר: <b style="color:${sp<=bg?'var(--lime-l)':'#fca5a5'}">${fmtMoney(bg-sp)}</b></span>
              </div>`:''}
          </div>
        </div>
      </td></tr>`);
    }
  });

  tbody.innerHTML=rows.join('');
}

// ── Toggle expand ────────────────────────────────────────────────
function toggleExpand(id) {
  expandedTaskId = expandedTaskId===id ? null : id;
  renderTasks();
}

// ── Toggle done ──────────────────────────────────────────────────
function toggleDone(id) {
  const t=tasks.find(x=>x.id===id);
  if(!t) return;
  t.status = t.status==='done'?'open':'done';
  persist(); renderAll();
}

function deleteTask(id) {
  if(!confirm('למחוק משימה זו?')) return;
  tasks=tasks.filter(t=>t.id!==id);
  persist(); renderAll();
}

// ── Task Modal ───────────────────────────────────────────────────
function populateSelects() {
  document.getElementById('fDomain').innerHTML =
    DOMAINS.map(d=>`<option value="${d.id}">${d.icon} ${d.name}</option>`).join('');
  const pOpts = PERSONS.map(p=>`<option value="${p.id}">${p.name}</option>`).join('');
  document.getElementById('fPerson').innerHTML = '<option value="">— בחר —</option>' + pOpts;
  document.getElementById('filterPerson').innerHTML = '<option value="">כל האנשים</option>' + pOpts;
}

function openTaskModal(id) {
  editingTaskId = id||null;
  document.getElementById('modalTitle').textContent = id?'עריכת משימה':'משימה חדשה';
  const t = id ? tasks.find(x=>x.id===id) : null;
  document.getElementById('fTitle').value    = t?.title    || '';
  document.getElementById('fDomain').value   = t?.domain   || (activeDomain!=='all'?activeDomain:DOMAINS[0].id);
  document.getElementById('fPerson').value   = t?.person   || activePersonFilter || '';
  document.getElementById('fPriority').value = t?.priority || 'mid';
  document.getElementById('fStatus').value   = t?.status   || 'open';
  document.getElementById('fDue').value      = t?.due      || '';
  document.getElementById('fBudget').value   = t?.budget   || '';
  document.getElementById('fNotes').value    = t?.notes    || '';
  document.getElementById('taskModal').classList.remove('hidden');
}
function closeTaskModal(){ document.getElementById('taskModal').classList.add('hidden'); }

function saveTask() {
  const title=document.getElementById('fTitle').value.trim();
  if(!title){ alert('נא להזין כותרת'); return; }
  const existing = editingTaskId ? tasks.find(x=>x.id===editingTaskId) : null;
  const t = {
    id:       editingTaskId || genId(),
    title,
    domain:   document.getElementById('fDomain').value,
    person:   document.getElementById('fPerson').value,
    priority: document.getElementById('fPriority').value,
    status:   document.getElementById('fStatus').value,
    due:      document.getElementById('fDue').value,
    budget:   parseInt(document.getElementById('fBudget').value)||0,
    notes:    document.getElementById('fNotes').value.trim(),
    expenses: existing?.expenses || [],
    created:  existing?.created  || new Date().toISOString(),
  };
  tasks = editingTaskId ? tasks.map(x=>x.id===editingTaskId?t:x) : [...tasks,t];
  persist(); closeTaskModal(); renderAll();
}

// ── Expense Modal ────────────────────────────────────────────────
function openExpModal(tid) {
  expenseTaskId = tid;
  const t = tasks.find(x=>x.id===tid);
  document.getElementById('expTaskName').textContent = t?.title || '';
  document.getElementById('eDesc').value   = '';
  document.getElementById('eAmount').value = '';
  document.getElementById('eDate').value   = today();
  document.getElementById('expenseModal').classList.remove('hidden');
}
function closeExpModal(){ document.getElementById('expenseModal').classList.add('hidden'); }

function saveExp() {
  const desc   = document.getElementById('eDesc').value.trim();
  const amount = parseFloat(document.getElementById('eAmount').value);
  if(!desc||isNaN(amount)||amount<=0){ alert('נא למלא תיאור וסכום'); return; }
  const t = tasks.find(x=>x.id===expenseTaskId);
  if(!t) return;
  t.expenses = t.expenses || [];
  t.expenses.push({id:genId(),desc,amount,date:document.getElementById('eDate').value});
  persist(); closeExpModal(); renderAll();
}

function deleteExp(tid,eid) {
  const t=tasks.find(x=>x.id===tid);
  if(!t) return;
  t.expenses=(t.expenses||[]).filter(e=>e.id!==eid);
  persist(); renderAll();
}

// ── Income Modal ─────────────────────────────────────────────────
function openIncomeModal() {
  document.getElementById('iDesc').value   = '';
  document.getElementById('iType').value   = 'donation';
  document.getElementById('iAmount').value = '';
  document.getElementById('iSource').value = '';
  document.getElementById('iDate').value   = today();
  document.getElementById('incomeModal').classList.remove('hidden');
}
function closeIncomeModal(){ document.getElementById('incomeModal').classList.add('hidden'); }

function saveIncome() {
  const desc   = document.getElementById('iDesc').value.trim();
  const amount = parseFloat(document.getElementById('iAmount').value);
  if(!desc||isNaN(amount)||amount<=0){ alert('נא למלא תיאור וסכום'); return; }
  incomes.push({
    id:genId(), desc, amount,
    type:   document.getElementById('iType').value,
    source: document.getElementById('iSource').value.trim(),
    date:   document.getElementById('iDate').value,
  });
  persist(); closeIncomeModal(); renderAll();
}

function deleteIncome(id) {
  incomes = incomes.filter(i=>i.id!==id);
  persist(); renderAll();
}

// ── Filters ──────────────────────────────────────────────────────
function togglePerson(pid) {
  activePersonFilter = activePersonFilter===pid?'':pid;
  document.getElementById('filterPerson').value = activePersonFilter;
  renderPersons(); renderTasks();
}
function setDomain(id) { activeDomain=id; renderTabs(); renderTasks(); }

// ── Persist ──────────────────────────────────────────────────────
function persist() {
  save('tasks2', tasks);
  save('incomes', incomes);
}

function renderAll() {
  renderKPIs();
  renderPool();
  renderCharts();
  renderPersons();
  renderTabs();
  renderTasks();
}

// ── Init ─────────────────────────────────────────────────────────
['taskModal','expenseModal','incomeModal'].forEach(id=>{
  document.getElementById(id).addEventListener('click',e=>{ if(e.target.id===id) document.getElementById(id).classList.add('hidden'); });
});
document.getElementById('taskSearch').addEventListener('input',renderTasks);
document.getElementById('filterPerson').addEventListener('change',e=>{ activePersonFilter=e.target.value; renderPersons(); renderTasks(); });
document.getElementById('filterStatus').addEventListener('change',renderTasks);
document.getElementById('filterPriority').addEventListener('change',renderTasks);

populateSelects();
renderAll();
</script>
</body>
</html>
