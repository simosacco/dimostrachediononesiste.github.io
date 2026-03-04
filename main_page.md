<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anatomia Interattiva Pro - 45 Etichette con Opzioni Post-Verifica</title>
    <style>
        :root {
            --primary: #2563eb;
            --success: #16a34a;
            --error: #dc2626;
            --bg: #0f172a;
            --panel: #ffffff;
            --accent: #f59e0b;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background-color: var(--bg);
            color: #1e293b;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 20px;
        }

        .setup-container {
            background: var(--panel);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            margin-bottom: 20px;
            width: 100%;
            max-width: 600px;
            text-align: center;
        }

        .image-wrapper {
            position: relative;
            display: none;
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }

        #main-img {
            display: block;
            width: 1000px;
            height: auto;
        }

        .labels-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .input-group {
            position: absolute;
            pointer-events: auto;
            transform: translate(-50%, -50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            z-index: 10;
        }

        input {
            width: 95px;
            padding: 4px 8px;
            border: 1.5px solid #94a3b8;
            border-radius: 4px;
            font-size: 10px;
            text-align: center;
            background: rgba(255, 255, 255, 0.95);
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        input:focus {
            width: 130px;
            border-color: var(--primary);
            outline: none;
            z-index: 30;
            background: white;
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
        }

        input.is-correct { 
            border-color: var(--success); 
            background-color: #f0fdf4; 
            color: var(--success); 
            font-weight: bold;
            pointer-events: none; /* Impedisce modifiche se già corretta */
        }

        input.is-wrong { 
            border-color: var(--error); 
            background-color: #fef2f2; 
            animation: shake 0.4s;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-4px); }
            75% { transform: translateX(4px); }
        }

        .solution-text {
            display: none;
            background: var(--error);
            color: white;
            font-size: 9px;
            font-weight: bold;
            padding: 2px 6px;
            border-radius: 3px;
            margin-top: 3px;
            white-space: nowrap;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }

        /* Toolbar e Modale Scelte */
        .toolbar {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: white;
            padding: 15px 35px;
            border-radius: 50px;
            display: none;
            gap: 15px;
            box-shadow: 0 15px 40px rgba(0,0,0,0.4);
            z-index: 100;
            border: 1px solid #e2e8f0;
        }

        .post-verify-options {
            display: none; /* Nascosto inizialmente, appare dopo la verifica */
            gap: 10px;
        }

        button {
            padding: 12px 28px;
            border: none;
            border-radius: 25px;
            font-weight: 700;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            transition: all 0.2s;
        }

        .btn-check { background: var(--primary); color: white; }
        .btn-continue { background: var(--accent); color: white; }
        .btn-reset { background: #64748b; color: white; }

        button:hover { filter: brightness(1.1); transform: translateY(-3px); }
        button:active { transform: translateY(0); }

        #result-status {
            margin-top: 15px;
            font-weight: bold;
            color: #f8fafc;
            font-size: 1.3rem;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }
    </style>
</head>
<body>

<header>
    <h1>Anatomia Umana Professionale</h1>
    <p>Completa tutte le 45 etichette dello schema anatomico</p>
</header>

<div class="setup-container" id="uploader-box">
    <p>Carica l'immagine originale per iniziare l'esercitazione</p>
    <input type="file" id="file-upload" accept="image/*" style="cursor: pointer;">
</div>

<div class="image-wrapper" id="quiz-container">
    <img id="main-img" src="" alt="Schema Anatomico">
    <div class="labels-overlay">
        
        <div class="input-group" style="top: 5.5%; left: 13.5%;"><input type="text" data-ans="osso frontale"><span class="solution-text">osso frontale</span></div>
        <div class="input-group" style="top: 13.5%; left: 14%;"><input type="text" data-ans="clavicola"><span class="solution-text">clavicola</span></div>
        <div class="input-group" style="top: 16.5%; left: 10%;"><input type="text" data-ans="testa dell'omero"><span class="solution-text">testa dell'omero</span></div>
        <div class="input-group" style="top: 22.5%; left: 11%;"><input type="text" data-ans="sterno"><span class="solution-text">sterno</span></div>
        <div class="input-group" style="top: 28.5%; left: 9%;"><input type="text" data-ans="coste"><span class="solution-text">coste</span></div>
        <div class="input-group" style="top: 34.5%; left: 14%;"><input type="text" data-ans="vertebra"><span class="solution-text">vertebra</span></div>
        <div class="input-group" style="top: 42%; left: 9.5%;"><input type="text" data-ans="ileo"><span class="solution-text">ileo</span></div>
        <div class="input-group" style="top: 50.5%; left: 9%;"><input type="text" data-ans="pube"><span class="solution-text">pube</span></div>
        <div class="input-group" style="top: 56%; left: 13.5%;"><input type="text" data-ans="ischio"><span class="solution-text">ischio</span></div>
        <div class="input-group" style="top: 80%; left: 14%;"><input type="text" data-ans="malleolo interno"><span class="solution-text">malleolo interno</span></div>
        <div class="input-group" style="top: 94%; left: 12%;"><input type="text" data-ans="calcagno"><span class="solution-text">calcagno</span></div>

        <div class="input-group" style="top: 7%; left: 40.5%;"><input type="text" data-ans="osso temporale"><span class="solution-text">osso temporale</span></div>
        <div class="input-group" style="top: 15%; left: 41%;"><input type="text" data-ans="mandibola"><span class="solution-text">mandibola</span></div>
        <div class="input-group" style="top: 27%; left: 43.5%;"><input type="text" data-ans="omero"><span class="solution-text">omero</span></div>
        <div class="input-group" style="top: 35.5%; left: 44.5%;"><input type="text" data-ans="radio"><span class="solution-text">radio</span></div>
        <div class="input-group" style="top: 38%; left: 44.5%;"><input type="text" data-ans="ulna"><span class="solution-text">ulna</span></div>
        <div class="input-group" style="top: 44.5%; left: 43.5%;"><input type="text" data-ans="testa del femore"><span class="solution-text">testa del femore</span></div>
        <div class="input-group" style="top: 62%; left: 43.5%;"><input type="text" data-ans="femore"><span class="solution-text">femore</span></div>
        <div class="input-group" style="top: 65.5%; left: 43.5%;"><input type="text" data-ans="rotula"><span class="solution-text">rotula</span></div>
        <div class="input-group" style="top: 78.5%; left: 43.5%;"><input type="text" data-ans="tibia"><span class="solution-text">tibia</span></div>
        <div class="input-group" style="top: 82.5%; left: 43.5%;"><input type="text" data-ans="perone"><span class="solution-text">perone</span></div>
        <div class="input-group" style="top: 85.5%; left: 43.5%;"><input type="text" data-ans="astragalo"><span class="solution-text">astragalo</span></div>

        <div class="input-group" style="top: 6%; left: 63.5%;"><input type="text" data-ans="atlante"><span class="solution-text">atlante</span></div>
        <div class="input-group" style="top: 11.5%; left: 63.5%;"><input type="text" data-ans="epistrofeo"><span class="solution-text">epistrofeo</span></div>
        <div class="input-group" style="top: 28%; left: 64%;"><input type="text" data-ans="regione dorsale"><span class="solution-text">regione dorsale</span></div>
        <div class="input-group" style="top: 41.5%; left: 64.5%;"><input type="text" data-ans="regione sacrale"><span class="solution-text">regione sacrale</span></div>
        <div class="input-group" style="top: 46%; left: 58%;"><input type="text" data-ans="carpo"><span class="solution-text">carpo</span></div>
        <div class="input-group" style="top: 49%; left: 58.5%;"><input type="text" data-ans="metacarpo"><span class="solution-text">metacarpo</span></div>
        <div class="input-group" style="top: 53.5%; left: 56%;"><input type="text" data-ans="falangi"><span class="solution-text">falangi</span></div>
        <div class="input-group" style="top: 84.5%; left: 64%;"><input type="text" data-ans="malleolo esterno"><span class="solution-text">malleolo esterno</span></div>

        <div class="input-group" style="top: 5.5%; left: 91%;"><input type="text" data-ans="osso parietale"><span class="solution-text">osso parietale</span></div>
        <div class="input-group" style="top: 9%; left: 91%;"><input type="text" data-ans="osso occipitale"><span class="solution-text">osso occipitale</span></div>
        <div class="input-group" style="top: 15%; left: 93%;"><input type="text" data-ans="regione cervicale"><span class="solution-text">regione cervicale</span></div>
        <div class="input-group" style="top: 20%; left: 95%;"><input type="text" data-ans="acromion"><span class="solution-text">acromion</span></div>
        <div class="input-group" style="top: 23%; left: 95%;"><input type="text" data-ans="scapola"><span class="solution-text">scapola</span></div>
        <div class="input-group" style="top: 31%; left: 95%;"><input type="text" data-ans="olecrano"><span class="solution-text">olecrano</span></div>
        <div class="input-group" style="top: 38%; left: 88%;"><input type="text" data-ans="regione lombare"><span class="solution-text">regione lombare</span></div>
        <div class="input-group" style="top: 58%; left: 90%;"><input type="text" data-ans="regione coccigea"><span class="solution-text">regione coccigea</span></div>
        <div class="input-group" style="top: 61.5%; left: 63%;"><input type="text" data-ans="femore"><span class="solution-text">femore</span></div>
        <div class="input-group" style="top: 63%; left: 92.5%;"><input type="text" data-ans="condili"><span class="solution-text">condili</span></div>
        <div class="input-group" style="top: 78%; left: 90%;"><input type="text" data-ans="tibia"><span class="solution-text">tibia</span></div>
        <div class="input-group" style="top: 81.5%; left: 91%;"><input type="text" data-ans="perone"><span class="solution-text">perone</span></div>
        <div class="input-group" style="top: 86.5%; left: 90%;"><input type="text" data-ans="tarso"><span class="solution-text">tarso</span></div>
        <div class="input-group" style="top: 89.5%; left: 91%;"><input type="text" data-ans="metatarso"><span class="solution-text">metatarso</span></div>
        <div class="input-group" style="top: 95%; left: 93.5%;"><input type="text" data-ans="falangi"><span class="solution-text">falangi</span></div>
    </div>
</div>

<div id="result-status"></div>

<div class="toolbar" id="main-toolbar">
    <button id="btn-main-check" class="btn-check" onclick="verifyQuiz()">Verifica</button>
    
    <div id="choice-container" class="post-verify-options">
        <button class="btn-continue" onclick="continuePractice()">Continua</button>
        <button class="btn-reset" onclick="hardReset()">Ricomincia da capo</button>
    </div>
</div>

<script>
    const fileIn = document.getElementById('file-upload');
    const previewImg = document.getElementById('main-img');
    const container = document.getElementById('quiz-container');
    const toolbar = document.getElementById('main-toolbar');
    const statusMsg = document.getElementById('result-status');
    const choiceBox = document.getElementById('choice-container');
    const checkBtn = document.getElementById('btn-main-check');

    fileIn.addEventListener('change', function(e) {
        const file = e.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = function(event) {
                previewImg.src = event.target.result;
                container.style.display = 'inline-block';
                toolbar.style.display = 'flex';
                document.getElementById('uploader-box').style.display = 'none';
            };
            reader.readAsDataURL(file);
        }
    });

    function verifyQuiz() {
        const inputs = document.querySelectorAll('input[type="text"]');
        let correct = 0;
        
        inputs.forEach(input => {
            const userAns = input.value.trim().toLowerCase();
            const realAns = input.getAttribute('data-ans').toLowerCase();
            const solution = input.nextElementSibling;

            if (userAns === realAns) {
                input.classList.remove('is-wrong');
                input.classList.add('is-correct');
                solution.style.display = 'none';
                correct++;
            } else {
                input.classList.remove('is-correct');
                input.classList.add('is-wrong');
                solution.style.display = 'block';
            }
        });

        statusMsg.innerHTML = `Analisi completata: ${correct} su ${inputs.length} esatte!`;
        
        // Mostra le opzioni post-verifica
        checkBtn.style.display = 'none';
        choiceBox.style.display = 'flex';
    }

    // Opzione CONTINUA: pulisce solo gli errori, mantiene le corrette
    function continuePractice() {
        const inputs = document.querySelectorAll('input[type="text"]');
        inputs.forEach(input => {
            if (input.classList.contains('is-wrong')) {
                input.value = '';
                input.classList.remove('is-wrong');
                input.nextElementSibling.style.display = 'none';
            }
        });
        
        // Torna allo stato di verifica
        statusMsg.innerHTML = "Prova a correggere gli errori!";
        choiceBox.style.display = 'none';
        checkBtn.style.display = 'block';
    }

    // Opzione RICOMINCIA: svuota tutto
    function hardReset() {
        const inputs = document.querySelectorAll('input[type="text"]');
        inputs.forEach(input => {
            input.value = '';
            input.classList.remove('is-correct', 'is-wrong');
            input.style.pointerEvents = 'auto';
            input.nextElementSibling.style.display = 'none';
        });
        
        statusMsg.innerHTML = "";
        choiceBox.style.display = 'none';
        checkBtn.style.display = 'block';
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }
</script>

</body>
</html>
