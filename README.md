<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Юный химик | лаборатория элементов</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #f5f7e9 0%, #eef2e0 100%);
            font-family: 'Times New Roman', Times, serif;
            color: #1e2f1c;
            padding: 20px;
            min-height: 100vh;
        }

        .app {
            max-width: 1300px;
            margin: 0 auto;
            background: rgba(255, 252, 235, 0.9);
            border-radius: 48px;
            box-shadow: 0 20px 35px rgba(0, 20, 0, 0.2);
            overflow: hidden;
            backdrop-filter: blur(2px);
            border: 1px solid #cdd8b0;
        }

        .hero {
            background: #2c4b2b;
            padding: 24px 30px 18px 30px;
            text-align: center;
            border-bottom: 5px solid #ffcd7e;
        }

        .hero h1 {
            font-size: 3.2rem;
            letter-spacing: 2px;
            color: #fff3da;
            text-shadow: 4px 4px 0 #1a3a18;
            font-weight: bold;
            font-family: 'Times New Roman', Times, serif;
        }

        .hero p {
            color: #f9e0a0;
            font-size: 1.2rem;
            margin-top: 8px;
            font-style: italic;
        }

        .nav-tabs {
            display: flex;
            background: #e7eace;
            gap: 4px;
            padding: 12px 24px 0 24px;
            border-bottom: 1px solid #bec8a2;
            justify-content: center;
            flex-wrap: wrap;
        }

        .tab-btn {
            background: #dadfbe;
            border: none;
            font-family: 'Times New Roman', Times, serif;
            font-size: 1.4rem;
            font-weight: bold;
            padding: 10px 28px;
            border-radius: 30px 30px 0 0;
            cursor: pointer;
            transition: 0.2s;
            color: #2a4728;
            box-shadow: inset 0 -1px 0 #b3b98d;
        }

        .tab-btn.active {
            background: #fff9e8;
            color: #1e441b;
            box-shadow: none;
            border-bottom: 3px solid #ffb347;
        }

        .tab-btn:hover:not(.active) {
            background: #f2f3df;
            transform: translateY(-2px);
        }

        .page {
            display: none;
            padding: 32px 28px 40px 28px;
            animation: fadeSlide 0.25s ease;
        }

        .page.active-page {
            display: block;
        }

        @keyframes fadeSlide {
            from { opacity: 0; transform: translateY(8px);}
            to { opacity: 1; transform: translateY(0);}
        }

        /* ГЛАВНЫЕ ЭЛЕМЕНТЫ ПО ЦЕНТРУ */
        .table-title {
            font-size: 2rem;
            font-weight: bold;
            text-align: center;
            margin-bottom: 25px;
            color: #2f532c;
            background: #fff2cf;
            display: inline-block;
            width: auto;
            padding: 8px 32px;
            border-radius: 60px;
            letter-spacing: 1px;
            box-shadow: inset 0 0 0 1px #ffe0a3, 0 2px 8px rgba(0,0,0,0.05);
            margin-left: auto;
            margin-right: auto;
        }

        .periodic-grid {
            display: grid;
            grid-template-columns: repeat(8, minmax(80px, 1fr));
            gap: 12px;
            background: #fef7e0;
            padding: 20px;
            border-radius: 56px;
            box-shadow: inset 0 0 0 2px #fffff0, 0 8px 20px rgba(0,0,0,0.05);
        }

        .element-card {
            background: #ffffffdb;
            backdrop-filter: blur(4px);
            border-radius: 28px;
            text-align: center;
            padding: 12px 6px;
            transition: 0.1s linear;
            border: 1px solid #cdddb0;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
            cursor: pointer;
        }

        .element-card:hover {
            transform: scale(1.02);
            background: #fff6e8;
            border-color: #f5b042;
        }

        .element-symbol {
            font-size: 1.9rem;
            font-weight: 800;
            font-family: 'Times New Roman', Times, serif;
            line-height: 1;
        }

        .element-number {
            font-size: 0.75rem;
            color: #6f6f4b;
            font-weight: bold;
        }

        .element-name {
            font-size: 0.7rem;
            text-transform: uppercase;
            font-weight: 600;
            color: #3d613a;
        }

        /* симулятор стили */
        .lab-box {
            background: #fcf9ed;
            border-radius: 56px;
            padding: 20px 28px;
            margin-bottom: 35px;
            box-shadow: 0 8px 18px rgba(70, 50, 10, 0.1);
        }

        .reactor-title {
            font-size: 1.8rem;
            font-weight: bold;
            text-align: center;
            background: #fff0cf;
            padding: 12px;
            border-radius: 80px;
            margin-bottom: 25px;
            color: #3a5a32;
        }

        .reagent-selectors {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            margin-bottom: 25px;
            justify-content: center;
        }

        .selector-group {
            flex: 1;
            min-width: 200px;
        }

        .selector-group label {
            display: block;
            font-weight: bold;
            margin-bottom: 8px;
            font-size: 1.1rem;
            color: #3b6137;
            text-align: center;
        }

        select {
            width: 100%;
            padding: 12px 14px;
            font-family: 'Times New Roman', Times, serif;
            font-size: 1rem;
            background: white;
            border: 2px solid #d3dfb0;
            border-radius: 60px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
        }

        select:focus {
            border-color: #ff9f4a;
            outline: none;
        }

        .button-group {
            display: flex;
            gap: 20px;
            justify-content: center;
            flex-wrap: wrap;
            margin-bottom: 25px;
        }

        .mix-btn, .reset-btn {
            font-family: 'Times New Roman', Times, serif;
            font-weight: bold;
            font-size: 1.3rem;
            padding: 10px 28px;
            border-radius: 60px;
            cursor: pointer;
            transition: 0.1s;
            border: none;
        }

        .mix-btn {
            background: #ffaa55;
            color: #2a3b22;
            box-shadow: 0 3px 0 #aa6f2c;
        }

        .reset-btn {
            background: #c9d4ae;
            color: #2d4a28;
            box-shadow: 0 3px 0 #8f9e72;
        }

        .mix-btn:active, .reset-btn:active {
            transform: translateY(2px);
            box-shadow: none;
        }

        .reaction-result {
            background: #e6f0da;
            border-radius: 48px;
            padding: 20px 25px;
            text-align: center;
        }

        .result-equation {
            font-size: 1.6rem;
            font-weight: bold;
            background: #fffaf0;
            display: inline-block;
            padding: 12px 24px;
            border-radius: 80px;
            margin: 15px 0;
            font-family: monospace;
            letter-spacing: 1px;
        }

        .result-desc {
            font-size: 1.2rem;
            font-style: italic;
            color: #2c5823;
        }

        .journal-entry {
            background: #fff7e5;
            border-radius: 48px;
            padding: 18px 24px;
            margin-bottom: 20px;
            border-left: 12px solid #ffaa55;
        }

        .journal-date {
            font-weight: bold;
            color: #8b6b2c;
            font-size: 0.9rem;
        }

        .journal-text {
            font-size: 1.1rem;
            margin-top: 8px;
        }

        .clear-journal {
            background: #cdb88a;
            border: none;
            padding: 8px 20px;
            border-radius: 60px;
            font-weight: bold;
            cursor: pointer;
            font-family: 'Times New Roman', Times, serif;
            margin-top: 10px;
        }

        .note {
            background: #fff2cf;
            margin-top: 25px;
            padding: 12px;
            border-radius: 60px;
            text-align: center;
            font-size: 0.9rem;
            border-left: 6px solid #ffac57;
        }

        hr {
            margin: 20px 0;
            border: 1px solid #e2e0b8;
        }

        footer {
            text-align: center;
            padding: 18px;
            background: #e2e8ce;
            font-size: 0.8rem;
            color: #516d46;
            border-top: 1px solid #ccdaae;
        }
        @media (max-width: 700px) {
            .periodic-grid { grid-template-columns: repeat(4, 1fr); gap: 8px; }
            .result-equation { font-size: 1rem; word-break: break-word; white-space: normal;}
            .tab-btn { padding: 6px 16px; font-size: 1.1rem;}
            .hero h1 { font-size: 2.2rem; }
        }
        sub { font-size: 0.75rem; vertical-align: sub; }
    </style>
</head>
<body>
<div class="app">
    <div class="hero">
        <h1>🧪 Юный химик 🧪</h1>
        <p>лаборатория элементов и реакций по таблице Менделеева</p>
    </div>

    <div class="nav-tabs">
        <button class="tab-btn active" data-page="table">📖 Таблица Менделеева</button>
        <button class="tab-btn" data-page="lab">⚗️ Симулятор реакций</button>
        <button class="tab-btn" data-page="journal">📓 Лабораторный журнал</button>
    </div>

    <!-- СТРАНИЦА 1: ПЕРИОДИЧЕСКАЯ ТАБЛИЦА -->
    <div id="tablePage" class="page active-page">
        <div class="table-title">⭐ главные элементы ⭐</div>
        <div class="periodic-grid" id="periodicGrid"></div>
        <div class="note">
            🔬 нажми на элемент чтобы узнать его символ
        </div>
    </div>

    <!-- СТРАНИЦА 2: СИМУЛЯТОР РЕАКЦИЙ -->
    <div id="labPage" class="page">
        <div class="lab-box">
            <div class="reactor-title">
                🧴 смешивай реагенты → наблюдай реакцию 🧴
            </div>
            <div class="reagent-selectors">
                <div class="selector-group">
                    <label>🧪 Вещество №1</label>
                    <select id="reagentA"></select>
                </div>
                <div class="selector-group">
                    <label>🧫 Вещество №2</label>
                    <select id="reagentB"></select>
                </div>
            </div>
            <div class="button-group">
                <button class="mix-btn" id="mixButton">⚡ смешать ⚡</button>
                <button class="reset-btn" id="resetReactionBtn">🔄 сброс реакции</button>
            </div>
            <div class="reaction-result" id="reactionDisplay">
                <div style="font-weight:bold; font-size:1.3rem;">🌀 результат опыта</div>
                <div id="reactionEquation" class="result-equation">—</div>
                <div id="reactionDescription" class="result-desc">выбери вещества и нажми смешать</div>
            </div>
            <div class="note">
                ⚡ реакции только из таблицы Менделеева — никакой выдуманной химии
            </div>
        </div>
    </div>

    <!-- СТРАНИЦА 3: ЛАБОРАТОРНЫЙ ЖУРНАЛ (третья вкладка) -->
    <div id="journalPage" class="page">
        <div class="reactor-title" style="background:#efe3c9;">
            📖 история твоих экспериментов
        </div>
        <div id="journalEntriesContainer">
            <div class="journal-entry" style="background:#fff9ef;">
                <div class="journal-text">✨ пока тут пусто. смешай реакцию во вкладке "симулятор" и она появится здесь ✨</div>
            </div>
        </div>
        <div style="display: flex; justify-content: flex-end; margin-top: 15px;">
            <button id="clearJournalBtn" class="clear-journal">🗑️ очистить журнал</button>
        </div>
        <div class="note">
            💡 каждая успешная реакция сохраняется в твой личный лабораторный дневник
        </div>
    </div>
    <footer>
        ⚗️ симулятор «Юный химик» | реакции настоящие, журнал опытов ведётся автоматически
    </footer>
</div>

<script>
    // ---------- 1. СПИСОК ВЕЩЕСТВ ДЛЯ РЕАКЦИЙ (только менделеевские) ----------
    const reagentsList = [
        { id: "h2", name: "Водород H₂", formula: "H₂" },
        { id: "o2", name: "Кислород O₂", formula: "O₂" },
        { id: "na", name: "Натрий Na", formula: "Na" },
        { id: "cl2", name: "Хлор Cl₂", formula: "Cl₂" },
        { id: "h2o", name: "Вода H₂O", formula: "H₂O" },
        { id: "hcl", name: "Соляная кислота HCl", formula: "HCl" },
        { id: "naoh", name: "Гидроксид натрия NaOH", formula: "NaOH" },
        { id: "cao", name: "Оксид кальция CaO", formula: "CaO" },
        { id: "co2", name: "Углекислый газ CO₂", formula: "CO₂" },
        { id: "fe", name: "Железо Fe", formula: "Fe" },
        { id: "s", name: "Сера S", formula: "S" },
        { id: "cu", name: "Медь Cu", formula: "Cu" },
        { id: "al", name: "Алюминий Al", formula: "Al" },
        { id: "zn", name: "Цинк Zn", formula: "Zn" },
        { id: "ch4", name: "Метан CH₄", formula: "CH₄" },
        { id: "n2", name: "Азот N₂", formula: "N₂" },
        { id: "nh3", name: "Аммиак NH₃", formula: "NH₃" },
        { id: "caco3", name: "Карбонат кальция CaCO₃", formula: "CaCO₃" },
        { id: "electro", name: "Электрический ток ⚡", formula: "эл.ток" },
        { id: "heat", name: "Нагревание 🔥", formula: "t°" },
        { id: "mg", name: "Магний Mg", formula: "Mg" }
    ];

    // ----- БАЗА РЕАКЦИЙ (ключ сортированный "id1|id2") -> { equationHtml, description }
    const reactionsDb = new Map();

    function addReaction(idA, idB, equation, desc) {
        let key1 = idA + "|" + idB;
        let key2 = idB + "|" + idA;
        reactionsDb.set(key1, { eq: equation, desc: desc });
        reactionsDb.set(key2, { eq: equation, desc: desc });
    }

    // наполнение реакциями (много)
    addReaction("h2", "o2", "2H₂ + O₂ → 2H₂O", "горение водорода, образуется вода");
    addReaction("na", "cl2", "2Na + Cl₂ → 2NaCl", "яркая реакция, поваренная соль");
    addReaction("h2", "cl2", "H₂ + Cl₂ → 2HCl", "на свету, получается хлороводород");
    addReaction("hcl", "naoh", "HCl + NaOH → NaCl + H₂O", "нейтрализация, выделяется тепло");
    addReaction("cao", "h2o", "CaO + H₂O → Ca(OH)₂", "гашеная известь, едкий раствор");
    addReaction("co2", "h2o", "CO₂ + H₂O ⇄ H₂CO₃", "образуется угольная кислота");
    addReaction("fe", "s", "Fe + S → FeS", "сульфид железа, чёрный порошок");
    addReaction("cu", "o2", "2Cu + O₂ → 2CuO", "медь окисляется, чёрный налёт");
    addReaction("al", "o2", "4Al + 3O₂ → 2Al₂O₃", "алюминий горит ярким светом");
    addReaction("zn", "hcl", "Zn + 2HCl → ZnCl₂ + H₂↑", "выделяется водород, шипение");
    addReaction("ch4", "o2", "CH₄ + 2O₂ → CO₂ + 2H₂O", "горение метана, выделяется тепло");
    addReaction("n2", "h2", "N₂ + 3H₂ ⇄ 2NH₃", "реакция Габера, синтез аммиака");
    addReaction("nh3", "hcl", "NH₃ + HCl → NH₄Cl", "белый дым хлорида аммония");
    addReaction("co2", "cao", "CO₂ + CaO → CaCO₃", "поглощение углекислого газа");
    addReaction("na", "h2o", "2Na + 2H₂O → 2NaOH + H₂↑", "бурная реакция с щелочью");
    addReaction("al", "hcl", "2Al + 6HCl → 2AlCl₃ + 3H₂↑", "алюминий растворяется с газом");
    addReaction("cu", "cl2", "Cu + Cl₂ → CuCl₂", "хлорид меди, жёлто-коричневый");
    addReaction("s", "o2", "S + O₂ → SO₂", "сернистый газ, резкий запах");
    addReaction("n2", "o2", "N₂ + O₂ → 2NO", "при высокой температуре, оксид азота");
    addReaction("ch4", "cl2", "CH₄ + Cl₂ → CH₃Cl + HCl", "реакция замещения на свету");
    addReaction("fe", "o2", "4Fe + 3O₂ → 2Fe₂O₃", "ржавление железа на воздухе");
    addReaction("h2o", "electro", "2H₂O → 2H₂↑ + O₂↑", "электролиз воды, пузырьки газа");
    addReaction("caco3", "heat", "CaCO₃ → CaO + CO₂↑", "обжиг известняка, углекислый газ");
    addReaction("caco3", "hcl", "CaCO₃ + 2HCl → CaCl₂ + H₂O + CO₂↑", "вскипание, выделение углекислого газа");
    addReaction("na", "o2", "4Na + O₂ → 2Na₂O", "оксид натрия, белый порошок");
    addReaction("mg", "o2", "2Mg + O₂ → 2MgO", "магний загорается ярким светом");
    addReaction("mg", "hcl", "Mg + 2HCl → MgCl₂ + H₂↑", "магний реагирует с кислотой");
    addReaction("co2", "mg", "2Mg + CO₂ → 2MgO + C", "магний горит в углекислом газе");
    addReaction("nh3", "h2o", "NH₃ + H₂O ⇄ NH₄OH", "аммиак растворяется, щелочная среда");
    addReaction("cao", "co2", "CaO + CO₂ → CaCO₃", "осаждение карбоната кальция");
    addReaction("al", "fe2o3", "2Al + Fe₂O₃ → Al₂O₃ + 2Fe", "алюминотермия, железо выделяется");
    addReaction("zn", "cuso4", "Zn + CuSO₄ → ZnSO₄ + Cu", "цинк вытесняет медь");
    // добавим ещё реакции с серой и железом
    addReaction("fe", "o2", "3Fe + 2O₂ → Fe₃O₄", "окалина железа на воздухе");
    addReaction("cu", "h2o", "2Cu + O₂ + CO₂ → Cu₂(OH)₂CO₃", "медь зеленеет во влажном воздухе");

    function getReaction(id1, id2) {
        let key = id1 + "|" + id2;
        if (reactionsDb.has(key)) return reactionsDb.get(key);
        let revKey = id2 + "|" + id1;
        return reactionsDb.has(revKey) ? reactionsDb.get(revKey) : null;
    }

    // заполнение выпадающих списков
    function populateSelects() {
        const selectA = document.getElementById('reagentA');
        const selectB = document.getElementById('reagentB');
        if (!selectA || !selectB) return;
        selectA.innerHTML = '';
        selectB.innerHTML = '';
        reagentsList.forEach( reagent => {
            let optionA = document.createElement('option');
            optionA.value = reagent.id;
            optionA.textContent = reagent.name;
            let optionB = document.createElement('option');
            optionB.value = reagent.id;
            optionB.textContent = reagent.name;
            selectA.appendChild(optionA);
            selectB.appendChild(optionB);
        });
        selectA.value = 'h2';
        selectB.value = 'o2';
    }

    // Журнал экспериментов (localStorage или массив)
    let journalEntries = [];

    function saveJournalToLocal() {
        localStorage.setItem('chemJournal', JSON.stringify(journalEntries));
    }

    function loadJournal() {
        const saved = localStorage.getItem('chemJournal');
        if (saved) {
            try {
                journalEntries = JSON.parse(saved);
            } catch(e) { journalEntries = []; }
        } else {
            journalEntries = [];
        }
        renderJournal();
    }

    function addToJournal(reagentAName, reagentBName, equation, description) {
        const now = new Date();
        const timeStr = `${now.toLocaleDateString()} ${now.toLocaleTimeString()}`;
        journalEntries.unshift({
            date: timeStr,
            text: `${reagentAName} + ${reagentBName} → ${equation}  (${description})`
        });
        if (journalEntries.length > 25) journalEntries.pop();
        saveJournalToLocal();
        renderJournal();
    }

    function renderJournal() {
        const container = document.getElementById('journalEntriesContainer');
        if (!container) return;
        if (journalEntries.length === 0) {
            container.innerHTML = `<div class="journal-entry" style="background:#fff9ef;"><div class="journal-text">✨ пока тут пусто. смешай реакцию во вкладке "симулятор" и она появится здесь ✨</div></div>`;
            return;
        }
        container.innerHTML = journalEntries.map(entry => `
            <div class="journal-entry">
                <div class="journal-date">📅 ${entry.date}</div>
                <div class="journal-text">${entry.text}</div>
            </div>
        `).join('');
    }

    function clearJournal() {
        if (confirm('очистить весь лабораторный журнал?')) {
            journalEntries = [];
            saveJournalToLocal();
            renderJournal();
        }
    }

    // сброс реакции (очистка полей вывода)
    function resetReactionDisplay() {
        const eqDiv = document.getElementById('reactionEquation');
        const descDiv = document.getElementById('reactionDescription');
        if (eqDiv) eqDiv.innerHTML = '—';
        if (descDiv) descDiv.innerHTML = 'выбери вещества и нажми смешать';
    }

    // основная функция смешивания с записью в журнал
    function updateReactionAndSave() {
        const selectA = document.getElementById('reagentA');
        const selectB = document.getElementById('reagentB');
        if (!selectA || !selectB) return;
        const idA = selectA.value;
        const idB = selectB.value;
        const reagentObjA = reagentsList.find(r => r.id === idA);
        const reagentObjB = reagentsList.find(r => r.id === idB);
        if (!reagentObjA || !reagentObjB) return;

        const reaction = getReaction(idA, idB);
        const eqDiv = document.getElementById('reactionEquation');
        const descDiv = document.getElementById('reactionDescription');
        
        if (reaction) {
            let cleanDesc = reaction.desc.replace(/\.$/, '').trim();
            eqDiv.innerHTML = reaction.eq;
            descDiv.innerHTML = `🧪 ${cleanDesc}`;
            // добавим в журнал, если реакция успешная (чтобы не дублировать слишком часто одинаковую? можно добавить всегда)
            addToJournal(reagentObjA.name, reagentObjB.name, reaction.eq, cleanDesc);
        } else {
            eqDiv.innerHTML = '✖️ нет реакции ✖️';
            descDiv.innerHTML = 'эти вещества не реагируют или реакция не изучается';
            // нет реакции — не записываем в журнал
        }
    }

    // ---------- ТАБЛИЦА МЕНДЕЛЕЕВА ----------
    const elementsData = [
        { num:1, sym:"H", name:"Водород" },{ num:2, sym:"He", name:"Гелий" },{ num:3, sym:"Li", name:"Литий" },{ num:4, sym:"Be", name:"Бериллий" },
        { num:5, sym:"B", name:"Бор" },{ num:6, sym:"C", name:"Углерод" },{ num:7, sym:"N", name:"Азот" },{ num:8, sym:"O", name:"Кислород" },
        { num:9, sym:"F", name:"Фтор" },{ num:10, sym:"Ne", name:"Неон" },{ num:11, sym:"Na", name:"Натрий" },{ num:12, sym:"Mg", name:"Магний" },
        { num:13, sym:"Al", name:"Алюминий" },{ num:14, sym:"Si", name:"Кремний" },{ num:15, sym:"P", name:"Фосфор" },{ num:16, sym:"S", name:"Сера" },
        { num:17, sym:"Cl", name:"Хлор" },{ num:18, sym:"Ar", name:"Аргон" },{ num:19, sym:"K", name:"Калий" },{ num:20, sym:"Ca", name:"Кальций" },
        { num:26, sym:"Fe", name:"Железо" },{ num:29, sym:"Cu", name:"Медь" },{ num:30, sym:"Zn", name:"Цинк" },{ num:47, sym:"Ag", name:"Серебро" },
        { num:79, sym:"Au", name:"Золото" },{ num:82, sym:"Pb", name:"Свинец" }
    ];
    const uniqueElements = [];
    const seen = new Set();
    for(let el of elementsData) {
        if(!seen.has(el.sym)) {
            seen.add(el.sym);
            uniqueElements.push(el);
        }
    }
    const finalElements = uniqueElements.slice(0,28);
    function buildPeriodicTable() {
        const grid = document.getElementById('periodicGrid');
        if (!grid) return;
        grid.innerHTML = '';
        finalElements.forEach(el => {
            const card = document.createElement('div');
            card.className = 'element-card';
            card.setAttribute('data-symbol', el.sym);
            card.innerHTML = `
                <div class="element-number">${el.num}</div>
                <div class="element-symbol">${el.sym}</div>
                <div class="element-name">${el.name}</div>
            `;
            card.addEventListener('click', () => {
                navigator.clipboard.writeText(el.sym).catch(()=>{});
                alert(`символ ${el.sym} скопирован`);
            });
            grid.appendChild(card);
        });
    }

    // переключение вкладок
    function initTabs() {
        const btns = document.querySelectorAll('.tab-btn');
        const pages = {
            table: document.getElementById('tablePage'),
            lab: document.getElementById('labPage'),
            journal: document.getElementById('journalPage')
        };
        btns.forEach(btn => {
            btn.addEventListener('click', () => {
                const pageId = btn.getAttribute('data-page');
                if (!pageId) return;
                btns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                Object.values(pages).forEach(p => p?.classList.remove('active-page'));
                if (pageId === 'table') pages.table.classList.add('active-page');
                if (pageId === 'lab') pages.lab.classList.add('active-page');
                if (pageId === 'journal') pages.journal.classList.add('active-page');
            });
        });
    }

    // запуск
    window.addEventListener('DOMContentLoaded', () => {
        populateSelects();
        buildPeriodicTable();
        initTabs();
        loadJournal();
        const mixBtn = document.getElementById('mixButton');
        if (mixBtn) mixBtn.addEventListener('click', updateReactionAndSave);
        const resetBtn = document.getElementById('resetReactionBtn');
        if (resetBtn) resetBtn.addEventListener('click', resetReactionDisplay);
        const clearJournalBtn = document.getElementById('clearJournalBtn');
        if (clearJournalBtn) clearJournalBtn.addEventListener('click', clearJournal);
        resetReactionDisplay();
    });
</script>
</body>
</html>
