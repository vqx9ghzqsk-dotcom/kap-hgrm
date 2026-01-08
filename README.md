<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Enquête KAP – Cancer du sein (HGRM)</title>

<style>
*{box-sizing:border-box}
body{font-family:system-ui;background:#f1f5f9;padding:15px}
h1,h2{color:#1e40af}
.section{background:#fff;padding:18px;border-radius:14px;margin-bottom:20px;box-shadow:0 4px 12px rgba(0,0,0,.08)}
label{display:block;margin:6px 0}
input,select,textarea{width:100%;padding:10px;margin:5px 0;border-radius:8px;border:2px solid #e5e7eb}
.scale{display:flex;justify-content:space-between}
.scale label{text-align:center;flex:1}
button{width:100%;padding:16px;background:#1e40af;color:#fff;border:none;border-radius:14px;font-size:18px;font-weight:600;margin-top:15px}
.entry{background:#eff6ff;padding:12px;border-left:4px solid #1e40af;border-radius:8px;margin-top:10px}
</style>
</head>

<body>

<h1>📋 Enquête KAP – Cancer du sein</h1>
<p><strong>Hôpital Général de Référence de Makala (HGRM)</strong></p>

<form id="kapForm">

<!-- I IDENTIFICATION -->
<div class="section">
<h2>I. Identification</h2>
<input name="code" placeholder="Code de l’enquêtée" required>
<input type="date" name="date" required>
<input name="service" placeholder="Service">
<input name="enqueteur" placeholder="Enquêteur(trice)">
</div>

<!-- II CONSENTEMENT -->
<div class="section">
<h2>II. Consentement éclairé</h2>
<label><input type="radio" name="consentement" value="Oui" required> J’accepte</label>
<label><input type="radio" name="consentement" value="Non"> Je refuse</label>
</div>

<!-- III SOCIODEMOGRAPHIE -->
<div class="section">
<h2>III. Données sociodémographiques</h2>

<label>Sexe</label>
<label><input type="radio" name="sexe" value="Femme"> Femme</label>
<label><input type="radio" name="sexe" value="Homme"> Homme</label>

<input type="number" name="age" placeholder="Âge (ans)">

<label>État civil</label>
<select name="etat_civil">
<option>Célibataire</option>
<option>Mariée</option>
<option>Autre</option>
</select>

<label>Niveau d’études</label>
<select name="niveau">
<option>Infirmière diplômée</option>
<option>Licence</option>
<option>Master</option>
<option>Autre</option>
</select>

<input type="number" name="experience" placeholder="Années d’expérience">

<label>Statut professionnel</label>
<select name="statut">
<option>Titulaire</option>
<option>Contractuelle</option>
<option>Stagiaire</option>
<option>Autre</option>
</select>

<input name="service_affectation" placeholder="Service d’affectation">

<label>Antécédents cancer du sein</label>
<label><input type="radio" name="antecedents" value="Oui"> Oui</label>
<label><input type="radio" name="antecedents" value="Non"> Non</label>
<input name="antecedents_details" placeholder="Préciser si oui">
</div>

<!-- IV CONNAISSANCES -->
<div class="section">
<h2>IV. Connaissances</h2>

<label>Le risque augmente avec l’âge</label>
<label><input type="radio" name="k1" value="1"> Vrai</label>
<label><input type="radio" name="k1" value="0"> Faux</label>

<label>L’obésité est un facteur de risque</label>
<label><input type="radio" name="k2" value="1"> Vrai</label>
<label><input type="radio" name="k2" value="0"> Faux</label>

<label>Antécédents familiaux augmentent le risque</label>
<label><input type="radio" name="k3" value="1"> Vrai</label>
<label><input type="radio" name="k3" value="0"> Faux</label>

<label>L’autopalpation détecte les anomalies</label>
<label><input type="radio" name="k4" value="1"> Vrai</label>
<label><input type="radio" name="k4" value="0"> Faux</label>

<label>Âge conseillé pour mammographie</label>
<input type="number" name="k_age">
</div>

<!-- VI ATTITUDES -->
<div class="section">
<h2>VI. Attitudes (1 à 5)</h2>

<label>La prévention est une priorité</label>
<div class="scale">
<label>1<input type="radio" name="a1" value="1"></label>
<label>2<input type="radio" name="a1" value="2"></label>
<label>3<input type="radio" name="a1" value="3"></label>
<label>4<input type="radio" name="a1" value="4"></label>
<label>5<input type="radio" name="a1" value="5"></label>
</div>

<label>À l’aise pour expliquer l’autopalpation</label>
<div class="scale">
<label>1<input type="radio" name="a2" value="1"></label>
<label>2<input type="radio" name="a2" value="2"></label>
<label>3<input type="radio" name="a2" value="3"></label>
<label>4<input type="radio" name="a2" value="4"></label>
<label>5<input type="radio" name="a2" value="5"></label>
</div>
</div>

<!-- VII PRATIQUES -->
<div class="section">
<h2>VII. Pratiques</h2>
<label>Autopalpation personnelle</label>
<label><input type="radio" name="p1" value="1"> Oui</label>
<label><input type="radio" name="p1" value="0"> Non</label>

<label>Réalisez-vous l’examen clinique ?</label>
<select name="p2">
<option>Toujours</option>
<option>Parfois</option>
<option>Jamais</option>
</select>

<label>Enseignez-vous l’autopalpation ?</label>
<label><input type="radio" name="p3" value="1"> Oui</label>
<label><input type="radio" name="p3" value="0"> Non</label>
</div>

<!-- VIII OBSTACLES -->
<div class="section">
<h2>VIII. Obstacles</h2>
<label><input type="checkbox" name="obs" value="Matériel"> Manque de matériel</label>
<label><input type="checkbox" name="obs" value="Formation"> Manque de formation</label>
<label><input type="checkbox" name="obs" value="Temps"> Manque de temps</label>
<label><input type="checkbox" name="obs" value="Coût"> Coût élevé</label>
<label><input type="checkbox" name="obs" value="Tabous"> Tabous culturels</label>
</div>

<!-- IX RECOMMANDATIONS -->
<div class="section">
<h2>IX. Recommandations</h2>
<label>Besoin de formation supplémentaire ?</label>
<label><input type="radio" name="rec" value="Oui"> Oui</label>
<label><input type="radio" name="rec" value="Non"> Non</label>
<textarea name="suggestions" placeholder="Suggestions pour améliorer la prévention"></textarea>
</div>

<button type="submit">💾 Enregistrer l’enquête</button>

</form>

<div class="section">
<h2>📊 Enquêtes enregistrées</h2>
<div id="liste"></div>
<button onclick="exportCSV()">📁 Exporter vers Excel</button>
</div>

<script>
const KEY="KAP_HGRM_FINAL";
let db=JSON.parse(localStorage.getItem(KEY))||[];

document.getElementById("kapForm").addEventListener("submit",e=>{
e.preventDefault();
const f=new FormData(e.target);
const o=Object.fromEntries(f.entries());
o.obstacles=[...document.querySelectorAll("input[name='obs']:checked")].map(x=>x.value).join("|");
o.scoreK=(+o.k1||0)+(+o.k2||0)+(+o.k3||0)+(+o.k4||0);
o.scoreA=((+o.a1||0)+(+o.a2||0))/2;
o.scoreP=(+o.p1||0)+(+o.p3||0);
o.dateSave=new Date().toLocaleString("fr-FR");
db.unshift(o);
localStorage.setItem(KEY,JSON.stringify(db));
e.target.reset();
afficher();
});

function afficher(){
document.getElementById("liste").innerHTML=db.map(e=>
`<div class="entry">
<strong>${e.code}</strong><br>
Scores → K:${e.scoreK} A:${e.scoreA.toFixed(1)} P:${e.scoreP}<br>
<small>${e.dateSave}</small>
</div>`).join("");
}

function exportCSV(){
let csv="Code,ScoreK,ScoreA,ScoreP,Obstacles\n";
db.forEach(e=>csv+=`${e.code},${e.scoreK},${e.scoreA},${e.scoreP},"${e.obstacles}"\n`);
const a=document.createElement("a");
a.href=URL.createObjectURL(new Blob([csv],{type:"text/csv"}));
a.download="KAP_HGRM_FINAL.csv";
a.click();
}

afficher();
</script>

</body>
</html>
