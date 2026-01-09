<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Enquête CAP – Personnel infirmier</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
    font-family: Arial, sans-serif;
    background:#f1f5f9;
    margin:0;
    padding:15px;
}
h2{
    background:#8b1d1d;
    color:#fff;
    padding:10px;
}
section{
    background:#fff;
    padding:15px;
    margin-bottom:20px;
    border-radius:6px;
}
label{display:block;margin-top:10px;font-weight:bold;}
input, select{
    width:100%;
    padding:8px;
    margin-top:5px;
}
button{
    margin-top:15px;
    padding:10px;
    width:100%;
    background:#8b1d1d;
    color:white;
    border:none;
    font-size:16px;
}
.hidden{display:none}
table{
    width:100%;
    border-collapse:collapse;
}
th,td{
    border:1px solid #ccc;
    padding:5px;
    text-align:center;
}
</style>
</head>

<body>

<h1>ENQUÊTE CAP – PERSONNEL INFIRMIER</h1>

<!-- 1. COLLECTE -->
<section>
<h2>1. COLLECTE</h2>

<label>Âge</label>
<input type="number" id="age">

<label>Sexe</label>
<select id="sexe">
<option value="">-- Choisir --</option>
<option>Femme</option>
</select>

<label>Ancienneté (années)</label>
<input type="number" id="anciennete">

<label>Service</label>
<input type="text" id="service">
</section>

<!-- 2. BASE DE DONNÉES -->
<section>
<h2>2. BASE DE DONNÉES</h2>

<label>Connaît le cancer du sein ?</label>
<select id="connaissance">
<option value="">--</option>
<option value="1">Oui</option>
<option value="0">Non</option>
</select>

<label>Pratique l’auto-examen mammaire ?</label>
<select id="pratique">
<option value="">--</option>
<option value="1">Oui</option>
<option value="0">Non</option>
</select>

<label>A déjà conseillé le dépistage ?</label>
<select id="attitude">
<option value="">--</option>
<option value="1">Oui</option>
<option value="0">Non</option>
</select>

<button onclick="sauvegarder()">Sauvegarder les données</button>
</section>

<!-- 3. ANALYSE CAP -->
<section class="hidden" id="analyse">
<h2>3. ANALYSE CAP</h2>

<p><strong>Score Connaissance :</strong> <span id="scoreC"></span></p>
<p><strong>Score Attitude :</strong> <span id="scoreA"></span></p>
<p><strong>Score Pratique :</strong> <span id="scoreP"></span></p>

<h3>Base de données</h3>
<table id="table">
<tr>
<th>Âge</th><th>Sexe</th><th>Ancienneté</th><th>Service</th>
<th>C</th><th>A</th><th>P</th>
</tr>
</table>

<button onclick="exportCSV()">Exporter la base (CSV)</button>
</section>

<script>
let base = JSON.parse(localStorage.getItem("baseCAP")) || [];

function sauvegarder(){
    let data = {
        age: age.value,
        sexe: sexe.value,
        anciennete: anciennete.value,
        service: service.value,
        C: connaissance.value,
        A: attitude.value,
        P: pratique.value
    };
    base.push(data);
    localStorage.setItem("baseCAP", JSON.stringify(base));
    afficher();
}

function afficher(){
    document.getElementById("analyse").classList.remove("hidden");
    table.innerHTML = `<tr>
    <th>Âge</th><th>Sexe</th><th>Ancienneté</th><th>Service</th>
    <th>C</th><th>A</th><th>P</th></tr>`;

    let sc=0, sa=0, sp=0;

    base.forEach(d=>{
        sc+=Number(d.C);
        sa+=Number(d.A);
        sp+=Number(d.P);

        table.innerHTML += `<tr>
        <td>${d.age}</td><td>${d.sexe}</td><td>${d.anciennete}</td><td>${d.service}</td>
        <td>${d.C}</td><td>${d.A}</td><td>${d.P}</td>
        </tr>`;
    });

    scoreC.textContent = sc;
    scoreA.textContent = sa;
    scoreP.textContent = sp;
}

function exportCSV(){
    let csv="Age,Sexe,Anciennete,Service,Connaissance,Attitude,Pratique\n";
    base.forEach(d=>{
        csv+=`${d.age},${d.sexe},${d.anciennete},${d.service},${d.C},${d.A},${d.P}\n`;
    });
    let a=document.createElement("a");
    a.href="data:text/csv;charset=utf-8,"+encodeURI(csv);
    a.download="base_CAP.csv";
    a.click();
}

if(base.length>0) afficher();
</script>

</body>
</html>