<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>KAP Cancer du Sein – RDC (Version Scientifique Complète)</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- LIBRAIRIES -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/docx/8.2.3/docx.umd.js"></script>

<style>
body{font-family:Arial;background:#f1f5f9;padding:15px}
.container{max-width:1200px;margin:auto;background:#fff;border-radius:10px;padding:25px}
h2{color:#b03060;border-left:6px solid #b03060;padding-left:10px}
.row{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:15px}
label{font-weight:bold;font-size:13px}
select,input{padding:10px;border:1px solid #bbb;border-radius:6px;width:100%}
.check-group{border:1px solid #ddd;padding:15px;border-radius:8px}
button{background:#b03060;color:white;padding:15px;border:none;border-radius:8px;font-size:16px;width:100%;margin:20px 0}
.stat{background:#fce4ec;padding:15px;border-radius:8px;margin:10px 0}
canvas{background:#fff;border:1px solid #ddd;border-radius:8px;margin-top:20px}
</style>
</head>

<body>
<div class="container">

<h2>I. IDENTIFICATION</h2>
<div class="row">
  <div><label>Code enquêté</label><input id="code"></div>
  <div>
    <label>Niveau d'étude</label>
    <select id="etude">
      <option value="">--</option>
      <option>A2</option>
      <option>A1</option>
      <option>L</option>
      <option>M</option>
    </select>
  </div>
</div>

<h2>II. CONNAISSANCES (K)</h2>
<div class="row">
  <div>
    <label>Cancer du sein fréquent chez la femme ?</label>
    <select id="k1"><option value="">--</option><option value="1">Oui</option><option value="0">Non</option></select>
  </div>
  <div>
    <label>Début AES recommandé</label>
    <select id="k2"><option value="">--</option><option value="1">≥ 20 ans</option><option value="0">Autre</option></select>
  </div>
  <div>
    <label>Moment optimal AES</label>
    <select id="k3"><option value="">--</option><option value="1">7j après règles</option><option value="0">Autre</option></select>
  </div>
</div>

<h2>III. ATTITUDES (A)</h2>
<div class="row">
  <div><label>Capacité de détection (1–5)</label><input type="number" id="p1" min="1" max="5"></div>
  <div><label>Barrière culturelle (1–5)</label><input type="number" id="p2" min="1" max="5"></div>
</div>

<h2>IV. PRATIQUES (P)</h2>
<div class="row">
  <div>
    <label>ECS systématique</label>
    <select id="pra1"><option value="">--</option><option value="1">Oui</option><option value="0">Non</option></select>
  </div>
  <div>
    <label>Enseignement AES</label>
    <select id="pra2"><option value="">--</option><option value="1">Démonstration</option><option value="0">Non</option></select>
  </div>
</div>

<h2>V. OBSTACLES</h2>
<div class="check-group">
  <label><input type="checkbox" value="Manque de formation"> Manque de formation</label><br>
  <label><input type="checkbox" value="Absence salle isolée"> Absence de salle isolée</label><br>
  <label><input type="checkbox" value="Coût mammographie"> Coût mammographie</label><br>
  <label><input type="checkbox" value="Croyances culturelles"> Croyances culturelles</label>
</div>

<button onclick="enregistrer()">ENREGISTRER LA FICHE</button>

<h2>VI. ANALYSES STATISTIQUES</h2>
<div id="resultats"></div>

<h2>VII. GRAPHIQUES</h2>
<canvas id="chartKP"></canvas>
<canvas id="chartObs"></canvas>

<button onclick="exportWord()">📄 EXPORTER LE RAPPORT WORD</button>

</div>

<script>
let DB=[];
let chart1=null, chart2=null;

function enregistrer(){
  const d={
    code:code.value,
    etude:etude.value,
    k:[+k1.value,+k2.value,+k3.value],
    a:[+p1.value,+p2.value],
    p:[+pra1.value,+pra2.value],
    obs:[...document.querySelectorAll('input[type=checkbox]:checked')].map(x=>x.value)
  };
  DB.push(d);
  analyser();
}

function analyser(){
  let N=DB.length;
  if(N===0) return;

  let K=DB.map(d=>(d.k.reduce((a,b)=>a+b)/3)*100);
  let A=DB.map(d=>d.a.reduce((a,b)=>a+b)/2);
  let P=DB.map(d=>(d.p.reduce((a,b)=>a+b)/2)*100);

  let Kbon=K.filter(x=>x>=75).length;
  let Pbon=P.filter(x=>x>=75).length;

  let a=0,b=0,c=0,d=0;
  DB.forEach((x,i)=>{
    if(K[i]>=75 && P[i]>=75) a++;
    else if(K[i]>=75) b++;
    else if(P[i]>=75) c++;
    else d++;
  });

  let chi=((a*d-b*c)**2*N)/((a+b)*(c+d)*(a+c)*(b+d)||1);
  let OR=(a*d)/(b*c||1);

  let obsCount={};
  DB.forEach(d=>d.obs.forEach(o=>obsCount[o]=(obsCount[o]||0)+1));
  let obsMaj=Object.entries(obsCount).sort((x,y)=>y[1]-x[1])[0];

  resultats.innerHTML=`
  <div class="stat"><b>Effectif (N)</b> : ${N}</div>
  <div class="stat"><b>Bon niveau de connaissances</b> : ${Math.round(Kbon/N*100)}%</div>
  <div class="stat"><b>Pratiques correctes</b> : ${Math.round(Pbon/N*100)}%</div>
  <div class="stat"><b>Chi²</b> : ${chi.toFixed(2)} (${chi>3.84?'Significatif':'Non significatif'})</div>
  <div class="stat"><b>Odds Ratio (K → P)</b> : ${OR.toFixed(2)}</div>
  <div class="stat"><b>Obstacle principal</b> : ${obsMaj?obsMaj[0]+' ('+Math.round(obsMaj[1]/N*100)+'%)':'--'}</div>
  <div class="stat"><b>Conclusion</b><br>
  ${Kbon/N>=0.75?'Bon niveau de connaissances observé.':'Connaissances insuffisantes.'}
  ${Pbon/N<0.5?' Faible traduction en pratique clinique.':' Bonne application clinique.'}
  </div>`;

  drawCharts(Kbon,Pbon,obsCount,N);
}

function drawCharts(Kbon,Pbon,obsCount,N){
  if(chart1) chart1.destroy();
  if(chart2) chart2.destroy();

  chart1=new Chart(chartKP,{
    type:'bar',
    data:{
      labels:['Connaissances bonnes','Pratiques correctes'],
      datasets:[{data:[Kbon/N*100,Pbon/N*100]}]
    },
    options:{plugins:{legend:{display:false}},scales:{y:{beginAtZero:true,max:100}}}
  });

  chart2=new Chart(chartObs,{
    type:'pie',
    data:{labels:Object.keys(obsCount),datasets:[{data:Object.values(obsCount)}]}
  });
}

function exportWord(){
  const {Document,Packer,Paragraph,TextRun}=docx;
  const doc=new Document({
    sections:[{children:[
      new Paragraph({children:[new TextRun({text:"ÉTUDE KAP – CANCER DU SEIN (RDC)",bold:true,size:28})]}),
      new Paragraph("MÉTHODES"),
      new Paragraph("Étude transversale de type KAP auprès du personnel infirmier. Les connaissances ont été évaluées par items binaires, les attitudes par échelle de Likert et les pratiques par questions dichotomiques."),
      new Paragraph("RÉSULTATS"),
      new Paragraph(`Effectif total : ${DB.length}. ${Math.round(DB.filter((d,i)=>(d.k.reduce((a,b)=>a+b)/3)*100>=75).length/DB.length*100)}% avaient un bon niveau de connaissances et ${Math.round(DB.filter((d,i)=>(d.p.reduce((a,b)=>a+b)/2)*100>=75).length/DB.length*100)}% adoptaient des pratiques correctes.`),
      new Paragraph("DISCUSSION"),
      new Paragraph("Un écart important est observé entre connaissances et pratiques, suggérant l’existence de barrières organisationnelles et comportementales."),
      new Paragraph("CONCLUSION"),
      new Paragraph("Le renforcement des formations pratiques et l’amélioration des conditions de travail sont recommandés.")
    ]}]
  });

  Packer.toBlob(doc).then(blob=>{
    const a=document.createElement("a");
    a.href=URL.createObjectURL(blob);
    a.download="Rapport_KAP_Cancer_Sein_RDC.docx";
    a.click();
  });
}
</script>
</body>
</html>