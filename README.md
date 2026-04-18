<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GM KPI Dashboard 2026 - Editable Fixed</title>
<style>
  :root{
    --bg:#0b1020;
    --panel:#121933;
    --line:#2b3967;
    --text:#eef3ff;
    --muted:#aeb9d8;
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:Inter,Arial,sans-serif;
    background:linear-gradient(180deg,#09101f,#101935);
    color:var(--text);
  }
  .container{max-width:1800px;margin:0 auto;padding:22px}
  .hero,.card,.section{
    background:var(--panel);
    border:1px solid var(--line);
    border-radius:18px;
  }
  .hero{padding:24px}
  .hero h1{margin:0 0 8px;font-size:30px}
  .hero p{margin:0;color:var(--muted);line-height:1.55}
  .toolbar{display:flex;gap:10px;flex-wrap:wrap;margin:18px 0}
  button{
    background:linear-gradient(180deg,#284486,#1c2f62);
    color:#fff;
    border:1px solid #4465b4;
    border-radius:12px;
    padding:10px 14px;
    font-weight:800;
    cursor:pointer
  }
  button.secondary{background:#182247;border-color:var(--line)}
  .topgrid{display:grid;grid-template-columns:1.2fr .9fr .9fr .9fr;gap:16px;margin:18px 0}
  .card{padding:18px}
  .label{font-size:12px;color:#d9e4ff;text-transform:uppercase;letter-spacing:.9px}
  .big{font-size:34px;font-weight:900;line-height:1.05;margin-top:8px}
  .sub{margin-top:8px;color:var(--muted);font-size:13px;line-height:1.45}
  .scorebar{height:12px;background:#0f1530;border:1px solid #334271;border-radius:999px;overflow:hidden;margin-top:12px}
  .fill{height:100%;background:linear-gradient(90deg,#f75d59 0%,#f5b342 45%,#19c37d 100%)}
  .pill{
    display:inline-block;padding:6px 10px;border-radius:999px;
    font-size:12px;font-weight:900;letter-spacing:.2px;white-space:nowrap
  }
  .ex{background:rgba(25,195,125,.15);border:1px solid rgba(25,195,125,.3);color:#82efc9}
  .vg{background:rgba(125,178,255,.15);border:1px solid rgba(125,178,255,.3);color:#bfd7ff}
  .gd{background:rgba(245,179,66,.15);border:1px solid rgba(245,179,66,.3);color:#ffd793}
  .wk{background:rgba(247,93,89,.15);border:1px solid rgba(247,93,89,.3);color:#ffaca8}
  .ni{background:rgba(247,93,89,.23);border:1px solid rgba(247,93,89,.4);color:#ffd8d6}
  .legend{display:flex;gap:8px;flex-wrap:wrap}
  .section{margin-top:18px;overflow:hidden}
  .section-head{
    display:grid;grid-template-columns:1.3fr .8fr .8fr .8fr;gap:14px;
    padding:18px;background:linear-gradient(180deg,#162149,#101834);
    border-bottom:1px solid var(--line)
  }
  .section h2{margin:0;font-size:24px}
  .section-meta{color:var(--muted);margin-top:6px;line-height:1.5;font-size:13px}
  .table-wrap{overflow:auto;padding:0}
  table{width:100%;border-collapse:collapse;min-width:1500px}
  th,td{padding:10px 8px;border-bottom:1px solid var(--line);vertical-align:top}
  th{
    background:#141d3d;
    text-align:left;
    font-size:12px;
    color:#dbe4ff;
    position:sticky;
    top:0;
    z-index:1;
  }
  td{font-size:13px}
  td input{
    display:block;
    width:78px;
    min-width:78px;
    padding:8px 8px;
    background:#0f1530;
    color:#fff;
    border:1px solid #31406e;
    border-radius:8px;
    outline:none;
    pointer-events:auto;
  }
  td input:focus{
    border-color:#7db2ff;
    box-shadow:0 0 0 2px rgba(125,178,255,.15)
  }
  .num{text-align:right;white-space:nowrap}
  .mini{font-size:12px;color:var(--muted);margin-top:3px}
  .note{padding:14px 18px;color:var(--muted);font-size:13px;line-height:1.6;border-top:1px solid var(--line);background:#0f1631}
  .footer{margin:18px 0 8px;color:var(--muted);font-size:12px}
  @media (max-width:1200px){.topgrid,.section-head{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="container">
  <div class="hero">
    <h1>GM KPI Dashboard 2026 - Editable Fixed</h1>
    <p>This version removes the interaction problem. Monthly cells are simple editable inputs. Quarterly, YTD, section scores, and overall score update as you type.</p>
  </div>

  <div class="toolbar">
    <button onclick="loadExample()">Reload Example</button>
    <button class="secondary" onclick="clearAll()">Clear All</button>
  </div>

  <div class="topgrid">
    <div class="card">
      <div class="label">Overall Weighted Score</div>
      <div class="big" id="overallScore">0.0%</div>
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
  <div class="footer">Section weights follow the playbook exactly: Financial 25%, Manufacturing 25%, Sales & Pipeline 25%, People & Organization 15%, Digitalization 5%, PR & Industry 5%. fileciteturn1file0</div>
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

function render(){
  const host = document.getElementById("sections");
  host.innerHTML = sections.map(section => `
    <div class="section">
      <div class="section-head">
        <div>
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
          <div class="big" id="${section.id}_score">0.0%</div>
          <div class="sub" id="${section.id}_rating">Awaiting input</div>
        </div>
        <div>
          <div class="label">Contribution</div>
          <div class="big" id="${section.id}_contribution">0.0</div>
          <div class="sub">Weighted points into overall score</div>
        </div>
      </div>
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
                <td><strong>${k.name}</strong><div class="mini">${k.unit}</div></td>
                <td>${k.note}</td>
                <td><strong>${k.annualTarget}</strong><div class="mini">${k.better === "lower" ? "Lower is better" : k.better === "zero" ? "Zero is target" : k.better === "range" ? "Target range" : "Higher is better"}</div></td>
                ${months.map((m,i)=>`<td><input type="number" step="0.01" data-kpi="${k.id}" data-month="${i}"></td>`).join("")}
                <td class="num" id="${k.id}_q1">-</td>
                <td class="num" id="${k.id}_q2">-</td>
                <td class="num" id="${k.id}_q3">-</td>
                <td class="num" id="${k.id}_q4">-</td>
                <td class="num" id="${k.id}_ytd">-</td>
                <td class="num" id="${k.id}_score">-</td>
                <td id="${k.id}_ratingcell">-</td>
              </tr>
            `).join("")}
          </tbody>
        </table>
      </div>
      <div class="note">Simple input table. No sticky overlays on cells. Edit any monthly number and the outputs recalculate.</div>
    </div>
  `).join("");

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

render();
loadExample();
</script>
</body>
</html>
