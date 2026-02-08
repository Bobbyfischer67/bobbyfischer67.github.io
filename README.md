<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Simulateur DPE Gratuit – Estimation Immédiate</title>
</head>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
:root {
  --primary:#2563eb;
  --primary-dark:#1e40af;
  --border:#e2e8f0;
  --text:#334155;
  --text-light:#64748b;
  --radius:16px;
  --shadow:0 10px 25px rgba(0,0,0,.08);
}

*{box-sizing:border-box;margin:0;padding:0}

body{
  font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,sans-serif;
  background:#f1f5f9;
  color:var(--text);
  padding:20px;
}

.container{
  max-width:900px;
  margin:auto;
  background:white;
  border-radius:var(--radius);
  box-shadow:var(--shadow);
  overflow:hidden;
}

.header{
  background:linear-gradient(135deg,var(--primary),#3b82f6);
  color:white;
  padding:30px;
  text-align:center;
}

.header h1{font-size:28px;margin-bottom:6px}
.header p{opacity:.9}

.content{padding:30px}

.progress-bar{
  display:flex;
  justify-content:center;
  gap:8px;
  margin-bottom:30px;
}
.progress-step{
  width:12px;height:12px;border-radius:50%;
  background:var(--border);
}
.progress-step.active{
  background:var(--primary);
  transform:scale(1.3);
}

.step{display:none;animation:fade .4s ease}
.step.active{display:block}

@keyframes fade{
  from{opacity:0;transform:translateY(10px)}
  to{opacity:1;transform:none}
}

h2{
  color:var(--primary);
  margin-bottom:20px;
  border-bottom:2px solid var(--border);
  padding-bottom:10px;
}

.form-columns{
  display:grid;
  grid-template-columns:1fr;
  gap:20px;
}

@media(min-width:768px){
  .form-columns{grid-template-columns:1fr 1fr}
  .full-width{grid-column:1/-1}
}

label{
  font-size:14px;
  font-weight:600;
  margin-bottom:6px;
  display:block;
}

input,select{
  width:100%;
  padding:14px;
  border:2px solid var(--border);
  border-radius:12px;
  font-size:16px;
}

input:focus,select:focus{
  outline:none;
  border-color:var(--primary);
  box-shadow:0 0 0 3px rgba(37,99,235,.15);
}

.button-group{
  display:flex;
  gap:12px;
  margin-top:30px;
}

button{
  flex:1;
  padding:16px;
  border:none;
  border-radius:12px;
  font-size:16px;
  font-weight:600;
  cursor:pointer;
}

.btn-primary{
  background:var(--primary);
  color:white;
}
.btn-primary:hover{
  background:var(--primary-dark);
}

.btn-secondary{
  background:#f1f5f9;
}

.result-container{text-align:center}

.score-display{
  font-size:42px;
  font-weight:800;
  margin:20px 0;
}

/* === JAUGE ADEME === */

.dpe-scale{
  margin:30px auto;
  max-width:420px;
  display:flex;
  flex-direction:column;
  gap:6px;
}

.dpe-item{
  padding:12px 16px;
  font-weight:800;
  font-size:18px;
  color:white;
  border-radius:8px;
  opacity:.35;
  position:relative;
}

.dpe-item.A{background:#16a34a;width:55%}
.dpe-item.B{background:#22c55e;width:65%}
.dpe-item.C{background:#a3e635;color:#1f2937;width:75%}
.dpe-item.D{background:#fde047;color:#1f2937;width:85%}
.dpe-item.E{background:#fb923c;width:92%}
.dpe-item.F{background:#f97316;width:97%}
.dpe-item.G{background:#dc2626;width:100%}

.dpe-item.active{
  opacity:1;
  transform:scale(1.03);
}

.dpe-item.active::after{
  content:"◀";
  position:absolute;
  right:-18px;
  top:50%;
  transform:translateY(-50%);
  color:#111827;
}

.recommandations{
  background:#f8fafc;
  padding:20px;
  border-radius:var(--radius);
  margin-top:25px;
  text-align:left;
}

.recommandations h3{
  color:var(--primary);
  margin-bottom:10px;
}

.recommandations li{
  margin-bottom:8px;
}

.disclaimer{
  font-size:12px;
  color:var(--text-light);
  margin-top:25px;
  border-top:1px solid var(--border);
  padding-top:15px;
}
</style>
</head>

<body>
<div class="container">

<div class="header">
  <h1>Simulateur DPE Gratuit</h1>
  <p>Estimation immédiate – résultat indicatif</p>
</div>

<div class="content">

<div class="progress-bar">
  <div class="progress-step active"></div>
  <div class="progress-step"></div>
  <div class="progress-step"></div>
</div>

<!-- STEP 1 -->
<div class="step active" id="step1">
<h2>Caractéristiques du logement</h2>

<div class="form-columns">
  <div>
    <label>Type de logement</label>
    <select id="type">
      <option value="1">Appartement</option>
      <option value="2">Maison</option>
    </select>
  </div>

  <div>
    <label>Surface (m²)</label>
    <input type="number" id="surface" value="80">
  </div>

  <div class="full-width">
    <label>Année de construction</label>
    <select id="annee">
      <option value="3">Avant 1948</option>
      <option value="2">1949 – 1974</option>
      <option value="1" selected>1975 – 2005</option>
      <option value="0">Après 2006</option>
    </select>
  </div>
</div>

<div class="button-group">
  <button class="btn-primary" onclick="nextStep(2)">Continuer →</button>
</div>
</div>

<!-- STEP 2 -->
<div class="step" id="step2">
<h2>Isolation & équipements</h2>

<div class="form-columns">
  <div><label>Murs</label><select id="murs"><option value="2">Aucune</option><option value="1" selected>Partielle</option><option value="0">Bonne</option></select></div>
  <div><label>Toiture</label><select id="toiture"><option value="2">Aucune</option><option value="1" selected>Moyenne</option><option value="0">Bonne</option></select></div>
  <div><label>Fenêtres</label><select id="fenetres"><option value="3">Simple</option><option value="2" selected>Double ancien</option><option value="1">Double récent</option><option value="0">Triple</option></select></div>
  <div><label>Chauffage</label><select id="chauffage"><option value="4">Fioul</option><option value="3">Électrique</option><option value="2" selected>Gaz / Bois</option><option value="1">PAC</option></select></div>
  <div><label>Ventilation</label><select id="ventilation"><option value="2" selected>Naturelle</option><option value="1">VMC simple</option><option value="0">VMC double</option></select></div>
</div>

<div class="button-group">
  <button class="btn-secondary" onclick="nextStep(1)">← Retour</button>
  <button class="btn-primary" onclick="calculer()">Calculer</button>
</div>
</div>

<!-- STEP 3 -->
<div class="step" id="step3">
<h2>Résultat</h2>

<div class="result-container">
<div id="scoreText" class="score-display"></div>

<div class="dpe-scale">
  <div class="dpe-item A" data-c="A">A</div>
  <div class="dpe-item B" data-c="B">B</div>
  <div class="dpe-item C" data-c="C">C</div>
  <div class="dpe-item D" data-c="D">D</div>
  <div class="dpe-item E" data-c="E">E</div>
  <div class="dpe-item F" data-c="F">F</div>
  <div class="dpe-item G" data-c="G">G</div>
</div>

<div id="reco" class="recommandations"></div>

<div class="button-group">
  <button class="btn-secondary" onclick="nextStep(2)">Modifier</button>
  <button class="btn-primary" onclick="nextStep(1)">Nouvelle estimation</button>
</div>
</div>

<div class="disclaimer">
Estimation indicative basée sur les seuils DPE réglementaires (ADEME).  
Ne remplace pas un DPE officiel.
</div>
</div>

</div>
</div>

<script>
function nextStep(n){
  document.querySelectorAll('.step').forEach(s=>s.classList.remove('active'));
  document.getElementById('step'+n).classList.add('active');
  document.querySelectorAll('.progress-step').forEach((p,i)=>p.classList.toggle('active',i<n));
}

function calculer(){
  const s=+surface.value||80;
  let score=annee.value*20+murs.value*30+toiture.value*20+fenetres.value*15+chauffage.value*30+ventilation.value*15;
  if(type.value==2)score+=35;
  if(s<50)score-=20;
  if(s>120)score+=30;
  score=Math.max(20,Math.min(score,350));

  let c="G";
  if(score<=70)c="A";else if(score<=110)c="B";else if(score<=180)c="C";
  else if(score<=250)c="D";else if(score<=330)c="E";else if(score<=420)c="F";

  scoreText.innerHTML=`${c}<br><span style="font-size:18px">${score} kWh/m²/an</span>`;

  document.querySelectorAll('.dpe-item').forEach(e=>e.classList.toggle('active',e.dataset.c===c));

  reco.innerHTML=`<h3>Recommandations</h3><ul><li>Classe ${c} – actions adaptées recommandées.</li></ul>`;
  nextStep(3);
}

</script>
</body>
</html>

