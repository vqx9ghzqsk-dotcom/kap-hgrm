<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAP-HGRM - Expert Breast Cancer RDC</title>
    <style>
        body { font-family: 'Segoe UI', Arial, sans-serif; background-color: #f0f2f5; margin: 0; padding: 15px; }
        .container { max-width: 1100px; margin: auto; background: white; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.2); }
        
        /* Header & Tabs */
        .header-tabs { display: flex; background: #fff; border-bottom: 3px solid #b03060; padding: 12px; align-items: center; gap: 8px; position: sticky; top:0; z-index:100; }
        .tab { padding: 10px 15px; font-weight: bold; font-size: 12px; text-decoration: none; border-radius: 4px; border: 1px solid #ddd; color: #555; background: #f8f9fa; cursor: pointer; }
        .tab.active { background: #b03060; color: white; border-color: #b03060; }
        
        /* MASQUER LES ONGLETS D'ANALYSE POUR LES UTILISATEURS */
        .tab:nth-child(2), .tab:nth-child(3), .tab:nth-child(4), .btn-excel { 
            display: none !important; 
        }

        .form-content { padding: 30px; }
        .content-section { display: none; }
        .content-section.active { display: block; }

        .section-title { background: #fce4ec; color: #b03060; padding: 15px; font-weight: bold; border-left: 8px solid #b03060; margin: 30px 0 15px 0; text-transform: uppercase; font-size: 15px; display: flex; align-items: center; justify-content: space-between; }
        
        .row { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 15px; }
        .field { display: flex; flex-direction: column; }
        label { font-size: 13px; font-weight: 700; margin-bottom: 6px; color: #222; line-height: 1.2; }
        select, input { padding: 12px; border: 1px solid #bbb; border-radius: 6px; font-size: 14px; background: #fff; }

        /* Tables Likert */
        table { width: 100%; border-collapse: collapse; margin: 20px 0; font-size: 13px; }
        th { background: #f8f9fa; padding: 12px; border: 1px solid #ddd; }
        td { border: 1px solid #eee; padding: 12px; text-align: center; }
        .text-left { text-align: left; width: 60%; font-weight: 500; padding-left: 15px; }

        /* Grid Checkboxes */
        .check-group { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 12px; background: #fdfdfd; padding: 20px; border-radius: 8px; border: 1px solid #eee; }
        .check-item { display: flex; align-items: center; font-size: 13px; cursor: pointer; padding: 5px; }
        .check-item input { margin-right: 15px; transform: scale(1.4); }

        .btn-save { width: 100%; background: #b03060; color: white; padding: 25px; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 40px; text-transform: uppercase; transition: 0.3s; }
        .btn-save:hover { background: #8e244d; transform: translateY(-2px); }
    </style>
</head>
<body>

<div class="container">
    <div class="header-tabs">
        <div class="tab active">1. COLLECTE DES DONNÉES</div>
        <div class="tab">2. DÉPOUILLEMENT</div>
        <div class="tab">3. ANALYSE</div>
        <div class="tab">4. CONCLUSION</div>
        <button type="button" class="btn-excel">📊 EXPORT</button>
    </div>

    <div id="section1" class="content-section active">
        <form class="form-content" id="mainForm">
            <div class="section-title">I. IDENTIFICATION & PROFIL (RDC)</div>
            <div class="row">
                <div class="field">
                    <label>Code Enquêté(e)</label>
                    <select id="code-enquete" name="code"></select>
                </div>
                <div class="field">
                    <label>Service / Département</label>
                    <select name="service">
                        <option selected>Gynécologie-Obstétrique</option>
                        <option>Maternité / Salle d'accouchement</option>
                        <option>Chirurgie Générale</option>
                        <option>Oncologie (si existant)</option>
                    </select>
                </div>
                <div class="field">
                    <label>Statut Professionnel</label>
                    <select name="statut">
                        <option selected>Titulaire du service</option>
                        <option>Infirmier(e) de garde</option>
                        <option>Stagiaire (Fin de cycle)</option>
                        <option>Sous-statutaire (Bénévole)</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="field"><label>Âge de l'infirmier(e)</label><select id="age-select" name="age"></select></div>
                <div class="field"><label>Années d'expérience professionnelle</label><select id="exp-select" name="experience"></select></div>
                <div class="field">
                    <label>Niveau d'étude le plus élevé</label>
                    <select name="etude" id="etude_input">
                        <option value="A2">A2 (Diplômée d'État)</option>
                        <option value="A1" selected>A1 (Graduée en Sciences Infirmières)</option>
                        <option value="L">L0/L1 (Licenciée nouveau système)</option>
                        <option value="M">Master / Doctorat</option>
                    </select>
                </div>
            </div>

            <div class="section-title">II. CONNAISSANCES SUR LE CANCER DU SEIN (SAVOIRS)</div>
            <div class="row">
                <div class="field">
                    <label>Le cancer du sein est-il la première cause de décès par cancer chez la femme en RDC ?</label>
                    <select name="k1"><option value="1" selected>Vrai (Oui)</option><option value="0">Faux (Non)</option></select>
                </div>
                <div class="field">
                    <label>À quel âge une femme devrait-elle commencer l'autopalpation (AES) ?</label>
                    <select name="k2"><option value="0">Dès 12 ans</option><option value="1" selected>Dès 20 ans</option><option value="0">Après 40 ans</option></select>
                </div>
                <div class="field">
                    <label>Quel est le meilleur moment pour l'AES ?</label>
                    <select name="k3"><option value="1" selected>7 jours après les règles</option><option value="0">Pendant les règles</option></select>
                </div>
            </div>

            <div class="section-title">III. ATTITUDES ET PERCEPTIONS (LIKERT)</div>
            <table>
                <thead>
                    <tr>
                        <th class="text-left">Énoncés</th>
                        <th>1</th><th>2</th><th>3</th><th>4</th><th>5</th>
                    </tr>
                </thead>
                <tbody>
                    <tr><td class="text-left">Je me sens capable de détecter un nodule suspect.</td><td><input type="radio" name="p1" value="1"></td><td><input type="radio" name="p1" value="2"></td><td><input type="radio" name="p1" value="3"></td><td><input type="radio" name="p1" value="4" checked></td><td><input type="radio" name="p1" value="5"></td></tr>
                    <tr><td class="text-left">L'influence culturelle empêche mes patientes de se déshabiller.</td><td><input type="radio" name="p2" value="1"></td><td><input type="radio" name="p2" value="2"></td><td><input type="radio" name="p2" value="3"></td><td><input type="radio" name="p2" value="4"></td><td><input type="radio" name="p2" value="5" checked></td></tr>
                </tbody>
            </table>

            <div class="section-title">IV. PRATIQUES PROFESSIONNELLES</div>
            <div class="row">
                <div class="field">
                    <label>Palpation clinique des seins (ECS) :</label>
                    <select name="pra1">
                        <option value="1" selected>Systématique</option>
                        <option value="0">Rarement</option>
                    </select>
                </div>
                <div class="field">
                    <label>Enseignement de l'AES :</label>
                    <select name="pra2">
                        <option value="1" selected>Démonstration physique</option>
                        <option value="0">Verbalement / Jamais</option>
                    </select>
                </div>
            </div>

            <button type="button" class="btn-save" onclick="saveData()">VALIDER ET ENREGISTRER LA FICHE</button>
        </form>
    </div>
</div>

<script>
    // FONCTION D'ENVOI VERS GOOGLE SHEETS
    async function saveData() {
        const form = document.getElementById('mainForm');
        const fd = new FormData(form);
        
        // Calcul du score Savoir
        let sk = parseInt(fd.get('k1')) + parseInt(fd.get('k2')) + parseInt(fd.get('k3'));
        // Calcul du score Pratique
        let sp = parseInt(fd.get('pra1')) + parseInt(fd.get('pra2'));

        const row = {
            code: fd.get('code'),
            service: fd.get('service'),
            age: fd.get('age'),
            etude: fd.get('etude'),
            experience: fd.get('experience'),
            savoir: sk >= 2 ? 'Bon' : 'Faible',
            pratique: sp >= 1 ? 'Correcte' : 'Incorrecte'
        };

        // TON URL GOOGLE SCRIPT
        const url = "https://script.google.com/macros/s/AKfycbzWHoyx-UHrmMmeKUrDv7MXMs0osx1tA95EMR3FEQJD5J_zcuccVEiIg2qBr_KP2CCT/exec";

        try {
            await fetch(url, {
                method: 'POST',
                mode: 'no-cors',
                body: JSON.stringify(row)
            });
            
            alert('Merci ! Fiche ID: ' + row.code + ' enregistrée avec succès.');
            form.reset();
        } catch (error) {
            alert("Erreur de connexion. Les données n'ont pas pu être envoyées.");
        }
    }

    // INITIALISATION DES LISTES DÉROULANTES
    window.onload = () => {
        const codeSelect = document.getElementById('code-enquete');
        for (let i = 1; i <= 200; i++) { codeSelect.options.add(new Option("ID: " + i, i)); }
        
        const ageSelect = document.getElementById('age-select');
        for (let i = 18; i <= 65; i++) { ageSelect.options.add(new Option(i + " ans", i)); }

        const expSelect = document.getElementById('exp-select');
        for (let i = 0; i <= 40; i++) { expSelect.options.add(new Option(i + " ans", i)); }
    };
</script>

</body>
</html>
