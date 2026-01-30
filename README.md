<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Espace Administrateur Sécurisé</title>
    <style>
        /* --- STYLE GLOBAL (Design inchangé) --- */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: #333;
        }

        /* --- CONTENEUR PRINCIPAL --- */
        .container {
            background-color: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            text-align: center;
            width: 100%;
            max-width: 400px;
            transition: all 0.3s ease;
        }

        h2 {
            margin-bottom: 1.5rem;
            color: #2c3e50;
        }

        /* --- FORMULAIRE DE LOGIN --- */
        #login-section {
            display: block;
        }

        input[type="password"] {
            width: 80%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s;
        }

        input[type="password"]:focus {
            border-color: #3498db;
        }

        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            border-radius: 6px;
            cursor: pointer;
            transition: background-color 0.3s;
            width: 100%;
        }

        button:hover {
            background-color: #2980b9;
        }

        .error-msg {
            color: #e74c3c;
            margin-top: 10px;
            font-size: 14px;
            display: none;
        }

        /* --- TABLEAU DE BORD (Caché par défaut) --- */
        #dashboard-section {
            display: none;
            text-align: left;
        }

        .success-icon {
            color: #27ae60;
            font-size: 40px;
            margin-bottom: 10px;
            display: block;
            text-align: center;
        }

        .logout-btn {
            background-color: #e74c3c;
            margin-top: 20px;
        }
        .logout-btn:hover {
            background-color: #c0392b;
        }
    </style>
</head>
<body>

    <div class="container">
        
        <div id="login-section">
            <h2>Accès Restreint</h2>
            <p style="color:#666; font-size: 0.9em; margin-bottom: 20px;">Veuillez entrer le code administrateur.</p>
            
            <input type="password" id="code-input" placeholder="Entrez le code..." onkeypress="handleEnter(event)">
            <button onclick="verifierCode()">Connexion</button>
            <p id="error-message" class="error-msg">Code incorrect. Veuillez réessayer.</p>
        </div>

        <div id="dashboard-section">
            <span class="success-icon">✔</span>
            <h2 style="text-align: center;">Bienvenue Admin</h2>
            <hr style="border: 0; border-top: 1px solid #eee; margin: 20px 0;">
            <p>Accès autorisé au système.</p>
            <ul>
                <li><strong>Statut :</strong> Connecté</li>
                <li><strong>Niveau :</strong> Super Administrateur</li>
                <li><strong>Session :</strong> Active</li>
            </ul>
            <button class="logout-btn" onclick="deconnexion()">Déconnexion</button>
        </div>

    </div>

    <script>
        // --- CONFIGURATION ---
        // C'est ici que le code a été modifié selon ta demande
        const CODE_ADMIN = "1398"; 

        function verifierCode() {
            const inputUser = document.getElementById("code-input").value;
            const errorMsg = document.getElementById("error-message");
            const loginSection = document.getElementById("login-section");
            const dashboardSection = document.getElementById("dashboard-section");

            if (inputUser === CODE_ADMIN) {
                // Code Correct
                errorMsg.style.display = "none";
                loginSection.style.display = "none";
                dashboardSection.style.display = "block";
            } else {
                // Code Incorrect
                errorMsg.style.display = "block";
                
                // Petit effet de vibration pour l'erreur
                const container = document.querySelector('.container');
                container.style.transform = "translateX(5px)";
                setTimeout(() => { container.style.transform = "translateX(-5px)"; }, 100);
                setTimeout(() => { container.style.transform = "translateX(0)"; }, 200);
            }
        }

        function deconnexion() {
            document.getElementById("code-input").value = "";
            document.getElementById("dashboard-section").style.display = "none";
            document.getElementById("login-section").style.display = "block";
            document.getElementById("error-message").style.display = "none";
        }

        // Permet de valider avec la touche Entrée
        function handleEnter(e) {
            if(e.key === "Enter"){
                verifierCode();
            }
        }
    </script>

</body>
</html>
