<form id="kapForm">
    <div class="section-title">I. IDENTIFICATION & PROFIL (Sociodémographique)</div>
    <div class="row">
        <div class="field">
            <label>1. Code Enquêté(e)</label>
            <select id="code-enquete"></select>
        </div>
        <div class="field">
            <label style="color:#b03060;">2. Consentement Éclairé</label>
            <select id="consentement">
                <option value="oui">Oui, accepte de participer</option>
                <option value="non">Non (Refus)</option>
            </select>
        </div>
        <div class="field">
            <label>3. Province d'exercice (Q7)</label>
            <select id="province">
                <option value="Kinshasa" selected>Kinshasa</option>
                <option value="Kongo Central">Kongo Central</option>
                <option value="Haut Katanga">Haut Katanga</option>
                <option value="Nord Kivu">Nord Kivu</option>
                <option value="Autre">Autre</option>
            </select>
        </div>
    </div>
    <div class="row">
        <div class="field">
            <label>4. Type d'établissement (Q6)</label>
            <select id="etablissement">
                <option value="Hôpital Universitaire">Hôpital Universitaire</option>
                <option value="HGR Public">Hôpital Général Réf. (Public)</option>
                <option value="Privé">Clinique/Hôpital Privé</option>
                <option value="Centre Santé">Centre de Santé</option>
            </select>
        </div>
        <div class="field">
            <label>5. Profession / Service</label>
            <select id="service">
                <option value="" disabled selected>Choisir...</option>
                <option>Médecin Généraliste</option>
                <option>Médecin Spécialiste (Gynéco/Onco)</option>
                <option>Interne/Résident</option>
                <option>Infirmier(e) / Sage-femme</option>
            </select>
        </div>
        <div class="field">
            <label>6. Années de pratique (Q5)</label>
            <input type="number" id="anciennete" min="0" placeholder="Ex: 5">
        </div>
    </div>

    <div class="section-title">II. CONNAISSANCES THÉORIQUES</div>
    
    <div class="sub-title">A. Connaissances Générales & Moléculaires (Q9-Q14)</div>
    <div class="row">
        <div class="field">
            <label>Avez-vous entendu parler des sous-types moléculaires ?</label>
            <select id="q-moleculaire">
                <option value="non">Non</option>
                <option value="oui">Oui</option>
            </select>
        </div>
        <div class="field">
            <label>Connaissance du concept "HER2 Low" ?</label>
            <select id="q-her2">
                <option value="non">Non</option>
                <option value="oui">Oui</option>
            </select>
        </div>
        <div class="field">
            <label>Avez-vous une idée sur les thérapies ciblées ?</label>
            <select id="q-therapie">
                <option value="non">Non</option>
                <option value="oui">Oui</option>
            </select>
        </div>
    </div>

    <div class="sub-title">B. Facteurs de risque (Q17 - Liste Complète PDF)</div>
    <div class="check-group" id="group-risques">
        <label class="check-item"><input type="checkbox" value="age40"> Âge > 40 ans</label>
        <label class="check-item"><input type="checkbox" value="famille"> Antécédents familiaux</label>
        <label class="check-item"><input type="checkbox" value="graisse"> Régime riche en graisses</label>
        <label class="check-item"><input type="checkbox" value="contraceptif"> Prise de contraceptifs oraux</label>
        <label class="check-item"><input type="checkbox" value="alcool_tabac"> Alcool / Tabac</label>
        <label class="check-item"><input type="checkbox" value="regles_precoces"> Ménarche précoce (< 12 ans)</label>
        <label class="check-item"><input type="checkbox" value="menopause_tardive"> Ménopause tardive (> 55 ans)</label>
        <label class="check-item"><input type="checkbox" value="obesite"> Obésité post-ménopause</label>
    </div>

    <div class="sub-title">C. Signes Cliniques (Q19)</div>
    <div class="check-group" id="group-signes">
        <label class="check-item"><input type="checkbox" value="masse_indolore"> Masse mammaire indolore</label>
        <label class="check-item"><input type="checkbox" value="ecoulement"> Écoulement mamelonnaire</label>
        <label class="check-item"><input type="checkbox" value="asymetrie"> Asymétrie / Modif. forme</label>
        <label class="check-item"><input type="checkbox" value="retraction"> Rétraction du mamelon</label>
        <label class="check-item"><input type="checkbox" value="ulceration"> Ulcération cutanée</label>
        <label class="check-item"><input type="checkbox" value="peau_orange"> Peau d'orange / Inflammation</label>
        <label class="check-item"><input type="checkbox" value="ganglion"> Masse aisselle (axillaire)</label>
    </div>

    <div class="sub-title">D. Dépistage (Mammographie & APS)</div>
    <div class="row">
        <div class="field">
            <label>La mammographie détecte-t-elle précocement ? (Q36)</label>
            <select id="q-mammo-eff">
                <option value="oui">Oui</option>
                <option value="non">Non</option>
            </select>
        </div>
        <div class="field">
            <label>À quel âge débuter la mammographie ? (Q39)</label>
            <select id="q-age-mammo">
                <option value="20">20 ans</option>
                <option value="40">40 ans</option>
                <option value="50">50 ans</option>
            </select>
        </div>
        <div class="field">
            <label>Meilleur moment pour l'Auto-Palpation (APS) ? (Q25)</label>
            <select id="q-moment-aes">
                <option value="apres_regles">Une semaine après les règles</option>
                <option value="pendant_regles">Pendant les règles</option>
                <option value="nimporte">N'importe quand</option>
            </select>
        </div>
    </div>

    <div class="section-title">III. PRATIQUES CLINIQUES</div>
    <div class="row">
        <div class="field">
            <label>Fréquence examen clinique des patientes (Q34)</label>
            <select id="prac-pro-freq">
                <option value="syst">Systématiquement / Annuel</option>
                <option value="plainte">Uniquement si plainte</option>
                <option value="jamais">Jamais</option>
            </select>
        </div>
        <div class="field">
            <label>Zone clé souvent oubliée ?</label>
            <select id="prac-zone">
                <option value="axillaire">Creux axillaire (Aisselle)</option>
                <option value="mamelon">Mamelon</option>
                <option value="autre">Autre</option>
            </select>
        </div>
        <div class="field">
            <label>Technique utilisée (Q33/27)</label>
            <select id="prac-main">
                <option value="pulpe">Pulpe des 3 doigts</option>
                <option value="pince">Pince (Pouce-Index)</option>
                <option value="main">Pleine main</option>
            </select>
        </div>
    </div>
    
    <label style="margin:10px 0; display:block; font-weight:bold; color:#b03060;">Mouvements de palpation connus :</label>
    <div class="check-group" id="group-mouv">
        <label class="check-item"><input type="checkbox" value="circulaire"> Circulaire (Spirale)</label>
        <label class="check-item"><input type="checkbox" value="vertical"> Vertical (Bandelettes)</label>
        <label class="check-item"><input type="checkbox" value="radial"> Radial (Étoile)</label>
    </div>

    <div class="section-title">IV. BESOINS & PERSPECTIVES</div>
    <div class="row">
        <div class="field">
            <label>Souhaitez-vous une formation suppl. ? (Q41)</label>
            <select id="besoin-formation">
                <option value="oui">Oui</option>
                <option value="non">Non</option>
            </select>
        </div>
        <div class="field">
            <label>Connaissez-vous le CNLC ? (Q42)</label>
            <select id="connaissance-cnlc">
                <option value="non">Non</option>
                <option value="oui">Oui</option>
            </select>
        </div>
        <div class="field">
            <label>Prêt à participer à un registre national ? (Q45)</label>
            <select id="registre-national">
                <option value="oui">Oui</option>
                <option value="non">Non</option>
            </select>
        </div>
    </div>

    <div class="field">
        <label>Suggestions pour améliorer la prise en charge (Q43/44) :</label>
        <textarea id="reco-verbatim" rows="3" placeholder="Ex: Campagnes de sensibilisation, Gratuité des soins, Formation..."></textarea>
    </div>

    <button type="button" id="save-btn" class="btn-save" onclick="window.saveRecord()">☁️ ENREGISTRER DANS LE CLOUD</button>
</form>
