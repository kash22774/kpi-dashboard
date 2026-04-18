<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GM KPI Dashboard 2026</title>
<style>
  :root{
    --bg:#0b1020; --panel:#121933; --panel2:#162149; --line:#2b3967; --text:#eef3ff; --muted:#aeb9d8;
  }
  *{box-sizing:border-box}
  body{
    margin:0; font-family:Inter,Arial,sans-serif;
    background:linear-gradient(180deg,#09101f,#101935); color:var(--text);
  }
  .container{max-width:1820px; margin:0 auto; padding:22px}
  .hero,.card,.section,.summary-card{
    background:var(--panel); border:1px solid var(--line); border-radius:18px;
  }
  .hero{padding:24px}
  .hero h1{margin:0 0 8px; font-size:30px}
  .hero p{margin:0; color:var(--muted); line-height:1.55}
  .toolbar{display:flex; gap:10px; flex-wrap:wrap; margin:18px 0}
  button{
    background:linear-gradient(180deg,#284486,#1c2f62);
    color:#fff; border:1px solid #4465b4; border-radius:12px;
    padding:10px 14px; font-weight:800; cursor:pointer;
  }
  button.secondary{background:#182247; border-color:var(--line)}
  .topgrid{display:grid; grid-template-columns:1.2fr .9fr .9fr .9fr; gap:16px; margin:18px 0}
  .card{padding:18px}
  .label{font-size:12px; color:#d9e4ff; text-transform:uppercase; letter-spacing:.9px}
  .big{font-size:34px; font-weight:900; line-height:1.05; margin-top:8px}
  .sub{margin-top:8px; color:var(--muted); font-size:13px; line-height:1.45}
  .scorebar{height:12px; background:#0f1530; border:1px solid #334271; border-radius:999px; overflow:hidden; margin-top:12px}
  .fill{height:100%; background:linear-gradient(90deg,#f75d59 0%,#f5b342 45%,#19c37d 100%)}
  .pill{
    display:inline-block; padding:6px 10px; border-radius:999px; font-size:12px;
    font-weight:900; letter-spacing:.2px; white-space:nowrap
  }
  .ex{background:rgba(25,195,125,.15); border:1px solid rgba(25,195,125,.3); color:#82efc9}
  .vg{background:rgba(125,178,255,.15); border:1px solid rgba(125,178,255,.3); color:#bfd7ff}
  .gd{background:rgba(245,179,66,.15); border:1px solid rgba(245,179,66,.3); color:#ffd793}
  .wk{background:rgba(247,93,89,.15); border:1px solid rgba(247,93,89,.3); color:#ffaca8}
  .ni{background:rgba(247,93,89,.23); border:1px solid rgba(247,93,89,.4); color:#ffd8d6}
  .legend{display:flex; gap:8px; flex-wrap:wrap}
  .section{margin-top:18px; overflow:hidden}
  .section-head{
    display:grid; grid-template-columns:1.3fr .8fr .8fr .8fr; gap:14px;
    padding:18px; background:linear-gradient(180deg,#162149,#101834);
    border-bottom:1px solid var(--line)
  }
  .section h2{margin:0; font-size:24px}
  .section-meta{color:var(--muted); margin-top:6px; line-height:1.5; font-size:13px}
  .table-wrap{overflow:auto}
  table{width:100%; border-collapse:collapse; min-width:1560px}
  th,td{padding:10px 8px; border-bottom:1px solid var(--line); vertical-align:top}
  th{
    background:#141d3d; text-align:left; font-size:12px; color:#dbe4ff;
    position:sticky; top:0; z-index:1;
  }
  td{font-size:13px}
  td input{
    display:block; width:78px; min-width:78px; padding:8px 8px;
    background:#0f1530; color:#fff; border:1px solid #31406e; border-radius:8px; outline:none;
  }
  td input:focus{border-color:#7db2ff; box-shadow:0 0 0 2px rgba(125,178,255,.15)}
  .num{text-align:right; white-space:nowrap}
  .mini{font-size:12px; color:var(--muted); margin-top:3px}
  .note{padding:14px 18px; color:var(--muted); font-size:13px; line-height:1.6; border-top:1px solid var(--line); background:#0f1631}
  .footer{margin:18px 0 8px; color:var(--muted); font-size:12px}
  .cell-wrap{display:flex; align-items:center; gap:6px}
  td input.kpi-input{width:78px; min-width:78px}
  .comment-btn{
    width:26px; height:26px; border-radius:8px; border:1px solid #3b4c7e;
    background:#162149; color:#dbe4ff; font-size:14px; line-height:1; cursor:pointer;
    display:inline-flex; align-items:center; justify-content:center; padding:0;
  }
  .comment-btn:hover{filter:brightness(1.08)}
  .comment-btn.has-comment{
    border-color:#7db2ff; box-shadow:0 0 0 1px rgba(125,178,255,.25) inset; background:#1c2a58;
  }
  .comment-btn.output-btn{width:24px; height:24px; font-size:13px}
  .out-wrap{display:flex; align-items:center; justify-content:flex-end; gap:6px}
  .head-wrap{display:flex; align-items:center; gap:8px; flex-wrap:wrap}
  .summary-card{margin-top:18px; padding:18px}
  .summary-card h3{margin:0 0 12px; font-size:18px}
  .summary-empty{color:var(--muted); font-size:13px}
  .comment-list{display:grid; gap:10px}
  .comment-item{
    border:1px solid var(--line); border-radius:14px; padding:12px 14px; background:#0f1631;
  }
  .comment-item-head{display:flex; justify-content:space-between; gap:12px; align-items:center; margin-bottom:6px}
  .comment-key{font-weight:800}
  .comment-body{white-space:pre-wrap; color:#dfe8ff; line-height:1.5; font-size:13px}
  .modal-backdrop{
    position:fixed; inset:0; background:rgba(0,0,0,.55); display:none; align-items:center; justify-content:center;
    z-index:9999; padding:20px
  }
  .modal{
    width:min(760px, 96vw); background:#101834; border:1px solid #31406e; border-radius:18px;
    box-shadow:0 24px 60px rgba(0,0,0,.45); overflow:hidden
  }
  .modal-head{
    padding:16px 18px; border-bottom:1px solid #2b3967; background:linear-gradient(180deg,#162149,#101834)
  }
  .modal-title{font-size:18px; font-weight:800}
  .modal-sub{font-size:12px; color:#aeb9d8; margin-top:4px}
  .modal-body{padding:16px 18px}
  .comment-text{
    width:100%; min-height:180px; resize:vertical; padding:12px 14px; border-radius:12px;
    border:1px solid #31406e; background:#0f1530; color:#eef3ff; outline:none; font:inherit
  }
  .modal-actions{display:flex; justify-content:space-between; gap:10px; padding:0 18px 18px}
  .btn-row{display:flex; gap:10px}
  @media (max-width:1200px){.topgrid,.section-head{grid-template-columns:1fr}}

  body.app-shell{min-height:100vh}
  .container{padding:18px 18px 110px}
  .hero{position:sticky; top:0; z-index:20; backdrop-filter:blur(14px); background:rgba(18,25,51,.88); box-shadow:0 10px 30px rgba(0,0,0,.18)}
  .hero h1{font-size:26px; letter-spacing:-.02em}
  .toolbar{position:sticky; top:96px; z-index:19; padding:10px; margin:14px 0 18px; background:rgba(11,16,32,.72); backdrop-filter:blur(12px); border:1px solid rgba(67,87,141,.35); border-radius:18px}
  button{min-height:42px; box-shadow:0 8px 24px rgba(0,0,0,.18)}
  .card,.section,.summary-card,.hero{box-shadow:0 10px 28px rgba(0,0,0,.16)}
  .table-wrap{padding:10px}
  .summary-card{position:relative}
  .app-bottom-bar{display:none}
  @media (max-width:900px){
    body{background:linear-gradient(180deg,#060b18,#0d1430 45%,#0f1837)}
    .container{padding:12px 12px 104px; max-width:100%}
    .hero{padding:16px 16px 14px; border-radius:20px}
    .hero h1{font-size:22px; margin:0}
    .toolbar{top:78px; gap:8px; padding:8px; margin:12px 0 14px; overflow:auto; flex-wrap:nowrap}
    .toolbar button{white-space:nowrap; flex:0 0 auto; padding:10px 12px; border-radius:14px}
    .topgrid{grid-template-columns:1fr 1fr; gap:10px; margin:14px 0}
    .card{padding:14px; border-radius:20px}
    .big{font-size:26px}
    .sub{font-size:12px}
    .section{border-radius:22px; margin-top:14px}
    .section-head{padding:14px; gap:10px}
    .section h2{font-size:20px}
    .table-wrap{overflow:visible; padding:12px}
    table, thead, tbody, th, td, tr{display:block; width:100%}
    thead{display:none}
    table{min-width:0}
    tbody{display:grid; gap:12px}
    tr{background:#0f1631; border:1px solid #2b3967; border-radius:18px; padding:12px; box-shadow:0 8px 20px rgba(0,0,0,.12)}
    td{display:flex; justify-content:space-between; gap:12px; align-items:flex-start; border-bottom:1px dashed rgba(67,87,141,.35); padding:8px 0; font-size:12px}
    td:last-child{border-bottom:0}
    td::before{content:attr(data-label); min-width:96px; max-width:96px; color:#aeb9d8; font-size:11px; text-transform:uppercase; letter-spacing:.06em; line-height:1.4}
    td > *{flex:1}
    td input, td input.kpi-input{width:100%; min-width:0; max-width:none}
    .cell-wrap,.out-wrap{width:100%; justify-content:flex-end}
    .cell-wrap{align-items:center}
    .out-wrap span{text-align:right; display:block; width:100%}
    .head-wrap{justify-content:space-between}
    .comment-btn{flex:0 0 auto}
    .modal{width:min(96vw,560px); border-radius:20px}
    .comment-text{min-height:150px}
    .summary-card{padding:14px; border-radius:20px}
    .footer{padding:0 4px 8px; text-align:center}
    .app-bottom-bar{display:flex; position:fixed; left:12px; right:12px; bottom:12px; z-index:30; gap:10px; padding:10px; background:rgba(16,24,52,.9); border:1px solid rgba(67,87,141,.4); border-radius:20px; backdrop-filter:blur(16px); box-shadow:0 18px 36px rgba(0,0,0,.28)}
    .app-bottom-bar button{flex:1; margin:0; font-size:12px; padding:10px 8px}
  }
  @media (max-width:560px){
    .topgrid{grid-template-columns:1fr}
    td{flex-direction:column; align-items:stretch; gap:6px}
    td::before{min-width:0; max-width:none}
    .cell-wrap,.out-wrap{justify-content:flex-start}
    .out-wrap span{text-align:left}
  }


  .section-jump{display:flex; gap:8px; flex-wrap:wrap; margin:14px 0 4px}
  .jump-chip{padding:8px 12px; border:1px solid #3b4c7e; border-radius:999px; background:#101834; color:#dfe8ff; font-size:12px; font-weight:700; text-decoration:none}
  .jump-chip:hover{filter:brightness(1.08)}
  .section-toggle{display:none}
  .section-body{display:block}
  @media (max-width:900px){
    .section-toggle{display:flex; width:100%; align-items:center; justify-content:space-between; gap:12px; background:transparent; border:0; padding:0; box-shadow:none; min-height:auto}
    .section-toggle .toggle-title{font-size:20px; font-weight:800; text-align:left}
    .section-toggle .toggle-icon{width:34px; height:34px; border-radius:12px; border:1px solid #3b4c7e; display:flex; align-items:center; justify-content:center; background:#162149; font-size:18px}
    .section-head > div:first-child h2,.section-head > div:first-child > .section-meta{display:none}
    .section-body.collapsed{display:none}
  }

</style>
</head>
<body class="app-shell">
<div class="container">
  <div class="hero">
    <h1>GM KPI Dashboard 2026</h1>
    
  </div>

  <div class="toolbar">
    <button onclick="loadExample()">Reload Example</button>
    <button class="secondary" onclick="clearAll()">Clear All</button>
    <button class="secondary" onclick="exportComments()">Export Comments JSON</button>
  </div>

  <div class="section-jump" id="sectionJump"></div>

  <div class="topgrid">
    <div class="card">
      <div class="label">Overall Weighted Score</div>
      <div class="head-wrap">
        <div class="big" id="overallScore">0.0%</div>
        <button type="button" class="comment-btn" data-comment-key="overall_score" onclick="openCommentModal('overall_score','Overall Weighted Score','Overall')">+</button>
      </div>
      <div class="sub" id="overallRating">Awaiting input</div>
      <div class="scorebar"><div class="fill" id="overallFill" style="width:0%"></div></div>
    </div>
    <div class="card">
      <div class="label">Mandate Revenue</div>
      <div class="big">75.18M</div>
      <div class="sub">Annual revenue under GM accountability</div>
    </div>
    <div class="card">
      <div class="label">Q1 + Q2 Red Line</div>
      <div class="big">35.57M</div>
      <div class="sub">Miss by more than 10% triggers review</div>
    </div>
    <div class="card">
      <div class="label">Rating Bands</div>
      <div class="legend" style="margin-top:10px">
        <span class="pill ex">Exceptional 110%+</span>
        <span class="pill vg">Very Good 100-109.9%</span>
        <span class="pill gd">Good 90-99.9%</span>
        <span class="pill wk">Weak 75-89.9%</span>
        <span class="pill ni">Needs Improvement &lt;75%</span>
      </div>
    </div>
  </div>

  <div id="sections"></div>

  <div class="summary-card">
    <h3>Commentary Summary</h3>
    <div id="commentsSummary" class="summary-empty">No comments saved yet.</div>
  </div>

  <div class="footer">Section weights follow the playbook exactly: Financial 25%, Manufacturing 25%, Sales & Pipeline 25%, People & Organization 15%, Digitalization 5%, PR & Industry 5%.</div>
</div>

<div class="app-bottom-bar">
  <button onclick="window.scrollTo({top:0,behavior:'smooth'})">Top</button>
  <button class="secondary" onclick="document.getElementById('commentsSummary').scrollIntoView({behavior:'smooth', block:'start'})">Comments</button>
  <button onclick="exportComments()">Export</button>
</div>

<div class="modal-backdrop" id="commentModal">
  <div class="modal">
    <div class="modal-head">
      <div class="modal-title" id="commentModalTitle">Comment</div>
      <div class="modal-sub" id="commentModalSub">Add explanation for this KPI period</div>
    </div>
    <div class="modal-body">
      <textarea id="commentText" class="comment-text" placeholder="Add commentary, reason for variance, action taken, risk, or context..."></textarea>
    </div>
    <div class="modal-actions">
      <div class="btn-row">
        <button type="button" onclick="saveComment()">Save Comment</button>
        <button type="button" class="secondary" onclick="clearComment()">Clear Comment</button>
      </div>
      <div class="btn-row">
        <button type="button" class="secondary" onclick="closeCommentModal()">Close</button>
      </div>
    </div>
  </div>
</div>

<script>
const months = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];
const quarterIdx = [[0,1,2],[3,4,5],[6,7,8],[9,10,11]];
const sections = [
  {id:"financial", title:"Financial", weight:25, focus:"The Scoreboard", redline:"Revenue, margin uplift, EBITDA, overhead discipline, and VO recovery.",
   kpis:[
    {id:"revenue", name:"Revenue vs Target", type:"sum", unit:"M", better:"higher", annualTarget:75.18, note:"Monthly revenue in millions", example:[4.5,4.7,5.1,6.1,6.6,6.9,5.9,6.1,6.5,7.0,7.4,7.8]},
    {id:"gm", name:"Gross Profit Margin Uplift", type:"avg", unit:"index", better:"higher", annualTarget:105, note:"2025 GM indexed as 100, target 105", example:[100,101,103,104,105,106,106,107,107,108,108,109]},
    {id:"ebitda", name:"EBITDA %", type:"avg", unit:"%", better:"higher", annualTarget:15, note:"Target 15%", example:[12,12.5,13,13.5,14,14.5,15,15,15.5,15.2,15.4,15.6]},
    {id:"overhead", name:"Overhead %", type:"avg", unit:"%", better:"lower", annualTarget:23, note:"Reduce from 27% to 23%", example:[27,26.5,26,25.5,24.5,24,23.8,23.5,23.3,23.2,23,22.8]},
    {id:"vo", name:"VO Recovery %", type:"avg", unit:"%", better:"higher", annualTarget:15, note:"VO recovery as % of contract value", example:[8,9,10,10.5,11,12,13,13,14,14.5,15,15]}
   ]},
  {id:"manufacturing", title:"Manufacturing", weight:25, focus:"The Engine", redline:"Production output, delivery discipline, rework, wastage, and OT control.",
   kpis:[
    {id:"eff", name:"Production Efficiency", type:"avg", unit:"index", better:"higher", annualTarget:125, note:"2025 indexed at 100, target 125", example:[100,102,104,108,111,114,116,119,121,123,124,126]},
    {id:"otd", name:"On-Time Delivery %", type:"avg", unit:"%", better:"higher", annualTarget:95, note:"Target 95%", example:[82,84,86,88,90,92,93,94,95,95,96,96]},
    {id:"rework", name:"Quality Defect / Rework %", type:"avg", unit:"%", better:"lower", annualTarget:2, note:"Below 2%", example:[3.2,3.1,2.8,2.7,2.5,2.4,2.3,2.2,2.1,2.0,1.9,1.8]},
    {id:"wastage", name:"Material Wastage %", type:"avg", unit:"%", better:"lower", annualTarget:5, note:"Below 5%", example:[6.8,6.5,6.3,6.1,5.9,5.7,5.4,5.2,5.0,4.9,4.8,4.7]},
    {id:"otc", name:"OT as % of Labor Cost", type:"avg", unit:"%", better:"lower", annualTarget:8, note:"Below 8%", example:[10,9.8,9.4,9.2,8.9,8.6,8.2,8.1,8.0,7.9,7.8,7.8]}
   ]},
  {id:"sales", title:"Sales & Pipeline", weight:25, focus:"The Weapon", redline:"Pipeline health, conversion, KSA share, repeat business, and Q3 push.",
   kpis:[
    {id:"pipeline", name:"Live Pipeline Value", type:"avg", unit:"M", better:"higher", annualTarget:100, note:"Month-end live pipeline in millions", example:[68,72,76,81,87,92,98,102,104,105,103,101]},
    {id:"conversion", name:"Conversion Rate %", type:"avg", unit:"%", better:"higher", annualTarget:32.5, note:"Target midpoint 32.5%", example:[21,23,25,26,28,29,30,31,33,34,35,35]},
    {id:"ksa", name:"KSA Revenue Share %", type:"avg", unit:"%", better:"higher", annualTarget:48, note:"Above 48%", example:[40,41,42,43,45,46,47,48,49,49,50,51]},
    {id:"repeat", name:"Repeat Business %", type:"avg", unit:"%", better:"higher", annualTarget:40, note:"Target 40%", example:[28,29,30,31,33,34,35,36,38,39,40,41]},
    {id:"q3", name:"Q3 Acquisition Protocol", type:"avg", unit:"index", better:"higher", annualTarget:100, note:"0-100 progress index for Q3 funnel", example:[0,0,0,0,0,0,20,45,75,0,0,0]}
   ]},
  {id:"people", title:"People & Organization", weight:15, focus:"The Team", redline:"Revenue productivity, KSA shift, zero cross-border blue-collar rotation, and training.",
   kpis:[
    {id:"rpe", name:"Revenue per Employee", type:"avg", unit:"AEDk", better:"range", annualTarget:210, note:"Target band 200K-220K AED", example:[160,165,170,178,184,190,198,204,210,214,218,222]},
    {id:"shift", name:"KSA Resource Shift %", type:"avg", unit:"%", better:"higher", annualTarget:20, note:"Target 20% by May 20", example:[0,0,0,8,18,20,20,20,20,20,20,20]},
    {id:"blue", name:"Blue-Collar Cross-Border Travel", type:"avg", unit:"count", better:"zero", annualTarget:0, note:"Target zero", example:[9,8,6,4,1,0,0,0,0,0,0,0]},
    {id:"training", name:"Training Hours per Employee", type:"sum", unit:"hours", better:"higher", annualTarget:40, note:"Total annual hours per employee", example:[1.5,2.0,2.5,2.8,3.2,3.4,3.6,3.8,4.0,4.0,4.2,4.5]}
   ]},
  {id:"digital", title:"Digitalization", weight:5, focus:"The Multiplier", redline:"ERP usage and no-Excel dashboard discipline.",
   kpis:[
    {id:"erp", name:"ERP Adoption %", type:"avg", unit:"%", better:"higher", annualTarget:100, note:"% of active projects fully tracked in ERP", example:[20,30,40,55,72,88,95,97,100,100,100,100]},
    {id:"dash", name:"Daily Dashboard Refresh %", type:"avg", unit:"%", better:"higher", annualTarget:100, note:"Adherence to daily refresh, no Excel workaround", example:[40,55,65,75,82,88,92,95,97,98,99,100]}
   ]},
  {id:"pr", title:"PR & Industry", weight:5, focus:"The Brand", redline:"Marketing hire and content output only.",
   kpis:[
    {id:"hire", name:"Marketing Hire Completion %", type:"avg", unit:"%", better:"higher", annualTarget:100, note:"Progress to permanent hire", example:[0,0,25,50,75,100,100,100,100,100,100,100]},
    {id:"content", name:"Content & Case Study Output", type:"avg", unit:"index", better:"higher", annualTarget:100, note:"100 means 3 posts/week and 1 case study/month", example:[20,30,40,50,60,70,75,80,90,95,100,100]}
   ]}
];

let commentStore = {};
let activeCommentKey = null;

function sum(arr){ return arr.reduce((a,b)=>a+b,0); }
function avg(arr){ return arr.length ? sum(arr)/arr.length : 0; }
function num(v){ const n=parseFloat(v); return isNaN(n)?0:n; }
function getMetric(type, arr){ return type === "sum" ? sum(arr) : avg(arr); }
function score(actual,target,better){
  if (better === "higher") return target ? Math.min((actual/target)*100,120) : 0;
  if (better === "lower") return actual>0 ? Math.min((target/actual)*100,120) : 120;
  if (better === "zero"){
    if (actual === 0) return 120;
    if (actual <= 1) return 100;
    if (actual <= 3) return 85;
    if (actual <= 5) return 75;
    return 55;
  }
  if (better === "range"){
    if (actual >= 220) return 120;
    if (actual >= 210) return 100 + ((actual-210)/10)*20;
    return Math.min((actual/210)*100,100);
  }
  return 0;
}
function ratingClass(p){
  if (p >= 110) return ["Exceptional","ex"];
  if (p >= 100) return ["Very Good","vg"];
  if (p >= 90) return ["Good","gd"];
  if (p >= 75) return ["Weak","wk"];
  return ["Needs Improvement","ni"];
}
function pill(p){ const r=ratingClass(p); return `<span class="pill ${r[1]}">${r[0]}</span>`; }
function fmt(v){ return Number(v).toLocaleString(undefined,{minimumFractionDigits:1,maximumFractionDigits:1}); }

function loadComments(){
  try {
    commentStore = JSON.parse(localStorage.getItem("gmKpiCommentsComplete") || "{}");
  } catch(e){
    commentStore = {};
  }
}
function persistComments(){
  try {
    localStorage.setItem("gmKpiCommentsComplete", JSON.stringify(commentStore));
  } catch(e){}
}
function refreshCommentButtons(){
  document.querySelectorAll("[data-comment-key]").forEach(btn => {
    const key = btn.getAttribute("data-comment-key");
    const val = (commentStore[key] || "").trim();
    btn.classList.toggle("has-comment", !!val);
    btn.textContent = val ? "•" : "+";
    btn.title = val ? "View / edit comment" : "Add comment";
  });
  renderCommentSummary();
}
function openCommentModal(key, label, periodLabel){
  activeCommentKey = key;
  document.getElementById("commentModalTitle").textContent = label + " | " + periodLabel;
  document.getElementById("commentModalSub").textContent = "Add explanation, reason for variance, action, dependency, or context.";
  document.getElementById("commentText").value = commentStore[key] || "";
  document.getElementById("commentModal").style.display = "flex";
  setTimeout(() => document.getElementById("commentText").focus(), 50);
}
function closeCommentModal(){
  document.getElementById("commentModal").style.display = "none";
}
function saveComment(){
  if(!activeCommentKey) return;
  const val = document.getElementById("commentText").value || "";
  if(val.trim()){
    commentStore[activeCommentKey] = val;
  } else {
    delete commentStore[activeCommentKey];
  }
  persistComments();
  refreshCommentButtons();
  closeCommentModal();
}
function clearComment(){
  if(!activeCommentKey) return;
  delete commentStore[activeCommentKey];
  persistComments();
  refreshCommentButtons();
  document.getElementById("commentText").value = "";
  closeCommentModal();
}
function renderCommentSummary(){
  const host = document.getElementById("commentsSummary");
  const entries = Object.entries(commentStore).filter(([,v]) => (v||"").trim());
  if(!entries.length){
    host.className = "summary-empty";
    host.textContent = "No comments saved yet.";
    return;
  }
  host.className = "comment-list";
  host.innerHTML = entries.map(([k,v]) => `
    <div class="comment-item">
      <div class="comment-item-head">
        <div class="comment-key">${k}</div>
      </div>
      <div class="comment-body">${escapeHtml(v)}</div>
    </div>
  `).join("");
}
function exportComments(){
  const blob = new Blob([JSON.stringify(commentStore, null, 2)], {type:"application/json"});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = "gm_kpi_comments.json";
  a.click();
  URL.revokeObjectURL(a.href);
}
function escapeHtml(s){
  return String(s)
    .replaceAll("&","&amp;")
    .replaceAll("<","&lt;")
    .replaceAll(">","&gt;");
}
function renderSectionJump(){
  const host = document.getElementById("sectionJump");
  if(!host) return;
  host.innerHTML = sections.map(s => `<a class="jump-chip" href="#section_${s.id}">${s.title}</a>`).join("");
}
function toggleSection(sectionId){
  const body = document.getElementById(`section_body_${sectionId}`);
  const icon = document.getElementById(`toggle_icon_${sectionId}`);
  if(!body || !icon) return;
  body.classList.toggle('collapsed');
  icon.textContent = body.classList.contains('collapsed') ? '+' : '−';
}
window.addEventListener("keydown", function(e){
  if(e.key === "Escape") closeCommentModal();
});

function render(){
  renderSectionJump();
  const host = document.getElementById("sections");
  host.innerHTML = sections.map(section => `
    <div class="section" id="section_${section.id}">
      <div class="section-head">
        <div>
          <button type="button" class="section-toggle" onclick="toggleSection('${section.id}')">
            <div>
              <div class="toggle-title">${section.title}</div>
              <div class="section-meta">${section.focus}. ${section.redline}</div>
            </div>
            <div class="toggle-icon" id="toggle_icon_${section.id}">−</div>
          </button>
          <h2>${section.title}</h2>
          <div class="section-meta">${section.focus}. ${section.redline}</div>
        </div>
        <div>
          <div class="label">Section Weight</div>
          <div class="big">${section.weight}%</div>
          <div class="sub">Strategic section weighting</div>
        </div>
        <div>
          <div class="label">Section Score</div>
          <div class="head-wrap">
            <div class="big" id="${section.id}_score">0.0%</div>
            <button type="button" class="comment-btn" data-comment-key="${section.id}_section_score" onclick="openCommentModal('${section.id}_section_score','${section.title} Section Score','Section')">+</button>
          </div>
          <div class="sub" id="${section.id}_rating">Awaiting input</div>
        </div>
        <div>
          <div class="label">Contribution</div>
          <div class="big" id="${section.id}_contribution">0.0</div>
          <div class="sub">Weighted points into overall score</div>
        </div>
      </div>
      <div class="section-body" id="section_body_${section.id}">
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>KPI</th>
              <th>Support Note</th>
              <th>Annual Target</th>
              ${months.map(m=>`<th>${m}</th>`).join("")}
              <th>Q1</th><th>Q2</th><th>Q3</th><th>Q4</th>
              <th>YTD</th><th>Score</th><th>Rating</th>
            </tr>
          </thead>
          <tbody>
            ${section.kpis.map(k => `
              <tr>
                <td data-label="KPI"><strong>${k.name}</strong><div class="mini">${k.unit}</div></td>
                <td data-label="Support Note">${k.note}</td>
                <td data-label="Annual Target"><strong>${k.annualTarget}</strong><div class="mini">${k.better === "lower" ? "Lower is better" : k.better === "zero" ? "Zero is target" : k.better === "range" ? "Target range" : "Higher is better"}</div></td>
                ${months.map((m,i)=>`<td data-label="${m}"><div class="cell-wrap"><input class="kpi-input" type="number" step="0.01" data-kpi="${k.id}" data-month="${i}"><button type="button" class="comment-btn" data-comment-key="${k.id}_m_${i}" onclick="openCommentModal('${k.id}_m_${i}','${k.name}','${m}')">+</button></div></td>`).join("")}
                <td data-label="Q1" class="num"><div class="out-wrap"><span id="${k.id}_q1">-</span><button type="button" class="comment-btn output-btn" data-comment-key="${k.id}_q_1" onclick="openCommentModal('${k.id}_q_1','${k.name}','Q1')">+</button></div></td>
                <td data-label="Q2" class="num"><div class="out-wrap"><span id="${k.id}_q2">-</span><button type="button" class="comment-btn output-btn" data-comment-key="${k.id}_q_2" onclick="openCommentModal('${k.id}_q_2','${k.name}','Q2')">+</button></div></td>
                <td data-label="Q3" class="num"><div class="out-wrap"><span id="${k.id}_q3">-</span><button type="button" class="comment-btn output-btn" data-comment-key="${k.id}_q_3" onclick="openCommentModal('${k.id}_q_3','${k.name}','Q3')">+</button></div></td>
                <td data-label="Q4" class="num"><div class="out-wrap"><span id="${k.id}_q4">-</span><button type="button" class="comment-btn output-btn" data-comment-key="${k.id}_q_4" onclick="openCommentModal('${k.id}_q_4','${k.name}','Q4')">+</button></div></td>
                <td data-label="YTD" class="num"><div class="out-wrap"><span id="${k.id}_ytd">-</span><button type="button" class="comment-btn output-btn" data-comment-key="${k.id}_y" onclick="openCommentModal('${k.id}_y','${k.name}','Year / YTD')">+</button></div></td>
                <td data-label="Score" class="num" id="${k.id}_score">-</td>
                <td data-label="Rating" id="${k.id}_ratingcell">-</td>
              </tr>
            `).join("")}
          </tbody>
        </table>
      </div>
      <div class="note">Use + to add commentary at monthly, quarterly, yearly, section, and overall level.</div>
      </div>
    </div>
  `).join("");

  refreshCommentButtons();
  document.querySelectorAll('input[data-kpi]').forEach(input => {
    input.addEventListener('input', calculate);
    input.addEventListener('change', calculate);
    input.addEventListener('keyup', calculate);
  });
}

function calculate(){
  let overall = 0;
  sections.forEach(section => {
    let sectionTotal = 0;
    let activeCount = 0;
    section.kpis.forEach(k => {
      const vals = months.map((_,i)=>num(document.querySelector(`input[data-kpi="${k.id}"][data-month="${i}"]`).value));
      const entered = vals.some(v => v !== 0);
      const q1 = getMetric(k.type, quarterIdx[0].map(i=>vals[i]));
      const q2 = getMetric(k.type, quarterIdx[1].map(i=>vals[i]));
      const q3 = getMetric(k.type, quarterIdx[2].map(i=>vals[i]));
      const q4 = getMetric(k.type, quarterIdx[3].map(i=>vals[i]));
      const ytd = getMetric(k.type, vals);
      const sc = score(ytd, k.annualTarget, k.better);

      document.getElementById(`${k.id}_q1`).textContent = entered ? fmt(q1) : "-";
      document.getElementById(`${k.id}_q2`).textContent = entered ? fmt(q2) : "-";
      document.getElementById(`${k.id}_q3`).textContent = entered ? fmt(q3) : "-";
      document.getElementById(`${k.id}_q4`).textContent = entered ? fmt(q4) : "-";
      document.getElementById(`${k.id}_ytd`).textContent = entered ? fmt(ytd) : "-";
      document.getElementById(`${k.id}_score`).textContent = entered ? fmt(sc) + "%" : "-";
      document.getElementById(`${k.id}_ratingcell`).innerHTML = entered ? pill(sc) : "-";

      if (entered){
        sectionTotal += sc;
        activeCount += 1;
      }
    });
    const sectionScore = activeCount ? sectionTotal / activeCount : 0;
    const contribution = (sectionScore / 100) * section.weight;
    overall += contribution;

    document.getElementById(`${section.id}_score`).textContent = fmt(sectionScore) + "%";
    document.getElementById(`${section.id}_rating`).innerHTML = activeCount ? pill(sectionScore) : "Awaiting input";
    document.getElementById(`${section.id}_contribution`).textContent = fmt(contribution);
  });
  document.getElementById("overallScore").textContent = fmt(overall) + "%";
  document.getElementById("overallRating").innerHTML = overall > 0 ? "Overall rating: " + pill(overall) : "Awaiting input";
  document.getElementById("overallFill").style.width = Math.min(overall,120) + "%";
}

function clearAll(){
  document.querySelectorAll('input[data-kpi]').forEach(input => input.value = "");
  calculate();
}
function loadExample(){
  sections.forEach(section => {
    section.kpis.forEach(k => {
      k.example.forEach((v,i) => {
        const el = document.querySelector(`input[data-kpi="${k.id}"][data-month="${i}"]`);
        if (el) el.value = v;
      });
    });
  });
  calculate();
}

loadComments();
render();
loadExample();
refreshCommentButtons();
</script>
</body>
</html>
