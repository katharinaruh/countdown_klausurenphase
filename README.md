<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Täglicher Spruch & Countdown</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            text-align: center;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 800px;
        }

        .spruch {
            font-size: 1.2em;
            margin-bottom: 20px;
            color: #4CAF50;
        }

        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .countdown {
            font-size: 1.2em;
            margin-top: 20px;
            color: #f44336;
        }

    </style>
</head>
<body>
    <div class="container">
        <h1>Dein täglicher Spruch</h1>
        <div id="spruch" class="spruch"></div>
        <button onclick="neuerSpruch()">Neuen Spruch Ziehen</button>

        <h2>Countdown zur Klausur</h2>
        <div id="countdown" class="countdown"></div>
    </div>

    <script>
        // Liste der 50 Sprüche
        const sprueche = [
            "Erfolg kommt nicht von heute auf morgen, sondern von kontinuierlicher Arbeit und Hingabe. Jedes Mal, wenn du dich hinsetzt, um zu lernen, schaffst du eine Grundlage für deinen zukünftigen Erfolg. Denke daran, dass jeder Schritt, so klein er auch sein mag, dich deinem Ziel näher bringt.",
            "Lernen ist der Schlüssel, der Türen zu unendlichen Möglichkeiten öffnet. Es ist nicht nur eine Pflicht, sondern ein Privileg, Wissen zu erwerben. Gib nie auf, auch wenn der Weg steinig erscheint, denn am Ende wirst du mit einer Weisheit und Klarheit belohnt, die niemand dir wegnehmen kann.",
            "Der wahre Wert des Lernens liegt nicht nur in den Fakten, die wir uns aneignen, sondern in der Art und Weise, wie es uns verändert. Jede neue Fähigkeit, jede neue Erkenntnis hilft uns, eine bessere Version von uns selbst zu werden. Bleibe also dran, auch wenn es schwer wird.",
            "Der Weg zum Erfolg ist selten geradlinig. Es gibt Hürden, die uns herausfordern, Momente der Verzweiflung, in denen wir glauben, nicht weiterzukommen. Doch genau in diesen Momenten des Zweifels müssen wir unsere größte Stärke finden: die Fähigkeit, weiterzumachen, weiterzulernen und niemals aufzugeben.",
            "Jeder, der je etwas Großes erreicht hat, hat es nicht durch Zufall getan. Es war die konsequente Entscheidung, jeden Tag ein Stück mehr zu lernen, zu wachsen und sich zu verbessern. Deine Reise mag lang und herausfordernd sein, aber denke daran, dass das Lernen selbst der größte Erfolg ist.",
            "Es gibt keine Abkürzungen, wenn es um das Lernen geht. Der einzige Weg, wirklich erfolgreich zu sein, ist, den Prozess zu respektieren, auch wenn er anstrengend oder frustrierend ist. Jeder Augenblick des Lernens bringt dich näher an dein Ziel.",
            "Lernen ist nicht nur der Erwerb von Wissen, sondern auch die Entwicklung von Fähigkeiten, die uns helfen, unsere Träume zu verwirklichen. Es ist ein kontinuierlicher Prozess, der nie endet, solange wir offen für neue Erfahrungen und Herausforderungen bleiben.",
            "Die größten Veränderungen in unserem Leben beginnen oft mit einem einzigen, kleinen Schritt. Und dieser Schritt ist oft das Lernen – das Streben nach neuen Erkenntnissen und Erfahrungen. Es mag nicht immer einfach sein, aber es ist der Weg zu einer besseren Zukunft.",
            "Erinnere dich immer daran: Du bist nicht allein auf deiner Reise. Jeder, der es geschafft hat, hat genau wie du angefangen – mit Zweifeln, Herausforderungen und einem Willen, durchzuhalten. Dein Lernen ist ein Zeichen deiner Entschlossenheit, deine Träume zu verwirklichen.",
            "Das Lernen ist wie das Bauen eines Hauses. Es braucht Zeit, Geduld und Sorgfalt, um eine solide Grundlage zu schaffen. Aber mit jeder neuen Lektion baust du ein stärkeres Fundament für deine Zukunft. Halte durch, auch wenn es mühsam ist – das Resultat wird es wert sein.",
            "Dein Lernprozess ist wie ein langer, stiller Fluss. Er mag nicht immer schnell sein, aber er bahnt sich mit stetiger Kraft seinen Weg und formt die Landschaft um ihn herum. Jeder Moment, in dem du dich dem Lernen widmest, bringt dich näher zu dem, was du erreichen möchtest.",
            "Lernen ist nicht nur eine Sache des Verstehens, sondern auch des Fühlens und Erlebens. Es geht darum, sich zu engagieren, zu forschen und Fragen zu stellen. Der wahre Fortschritt kommt nicht nur durch das Auswendiglernen, sondern durch das tiefere Verständnis und die Anwendung von Wissen.",
            "Manchmal fühlt es sich an, als ob der Lernprozess niemals endet, aber genau diese ständige Weiterentwicklung ist der Schlüssel zum Erfolg. Die Fähigkeit, niemals aufzugeben und immer weiter zu lernen, macht uns stärker und bringt uns den gewünschten Erfolg näher.",
            "Es gibt keinen schnellen Weg zum Erfolg, aber es gibt eine Reise, die du mit Leidenschaft und Hingabe bestreiten kannst. Wenn du dich darauf konzentrierst, stetig zu lernen, wirst du eines Tages zurückblicken und erkennen, wie weit du gekommen bist.",
            "Jeder Schritt, den du auf dem Weg des Lernens machst, bringt dich näher an deine Ziele. Manchmal fühlt es sich an, als würde der Fortschritt langsam voranschreiten, aber erinnere dich daran: Jeder Moment zählt und bringt dich der Erfüllung deiner Träume näher.",
            "Lernen erfordert Ausdauer. Es ist wie das Pflügen eines Feldes: Anfangs sieht es vielleicht chaotisch aus, aber mit der Zeit werden die Samen des Wissens erblühen und dir Erfolge bringen, die du dir nie erträumt hättest.",
            "Es ist nicht die Frage, wie schnell du lernst, sondern wie konsequent du dranbleibst. Der wahre Erfolg liegt nicht im schnellen Erreichen eines Ziels, sondern in der Disziplin, immer weiter zu machen, selbst wenn es schwerfällt.",
            "Lernen ist ein Weg, der nie endet, und genau das ist es, was das Leben so spannend macht. Wenn du offen für Wissen bleibst, wirst du entdecken, dass jeder Tag neue Möglichkeiten bringt, zu wachsen und dich weiterzuentwickeln.",
            "Es ist leicht, den Glauben an sich selbst zu verlieren, wenn die Dinge schwierig werden. Aber genau in diesen Momenten der Herausforderung wächst dein Potenzial. Dein Lernen ist das Werkzeug, das dir hilft, Hindernisse zu überwinden und stärker daraus hervorzugehen.",
            "Lernen ist wie ein Feuer, das in dir brennt. Wenn du ihm Nahrung gibst, wird es stärker. Wenn du es ignorierst, wird es langsam erlöschen. Achte darauf, es immer wieder zu füttern, und du wirst erkennen, dass du nicht nur Wissen erwirbst, sondern auch deine Leidenschaft entfacht.",
            "Du wirst niemals wissen, wie stark du wirklich bist, bis du vor Herausforderungen stehst und dich dem Lernen widmest. Genau in diesen Momenten wächst deine Stärke und deine Entschlossenheit. Lass niemals zu, dass die Schwierigkeiten dich davon abhalten, weiterzulernen.",
            "Lernen bedeutet, sich selbst zu hinterfragen, neue Perspektiven zu entwickeln und nie in den alten Mustern zu verharren. Wenn du lernst, dich immer wieder neu zu erfinden, wirst du feststellen, dass es keine Grenzen für deinen Erfolg gibt.",
            "Die größten Erfolge entstehen aus den kleinsten Anfängen. Jeder Tag, an dem du etwas Neues lernst, fügt ein weiteres Puzzleteil zu deinem Erfolg hinzu. Auch wenn der Fortschritt langsam erscheint, jedes Stück Wissen bringt dich ein Stück näher an dein Ziel.",
            "Lernen ist wie das Navigieren auf einem weiten Ozean: Du kannst nicht immer das Ziel sehen, aber mit jedem gesegelten Tag kommst du ihm näher. Dein Engagement und deine Ausdauer werden dich sicher an dein Ziel bringen, auch wenn der Weg ungewiss erscheint.",
            "Die größte Belohnung im Leben ist nicht der Ruhm, sondern das Wissen, dass du deine Ängste überwunden und neue Fähigkeiten erlernt hast. Jeder Tag des Lernens, jedes Hindernis, das du überwindest, ist ein Schritt in Richtung deiner besten Version.",
            "Lernen ist ein Prozess der ständigen Verbesserung. Es geht nicht darum, perfekt zu sein, sondern darum,."
        ];

        // Funktion, um einen zufälligen Spruch anzuzeigen
        function neuerSpruch() {
            const randomIndex = Math.floor(Math.random() * sprueche.length);
            document.getElementById('spruch').innerText = sprueche[randomIndex];
        }

        // Funktion für den Countdown
        function countdown() {
            const klausurDatum = new Date('2025-02-14T00:00:00'); // Datum der Klausur
            const heute = new Date();
            const diff = klausurDatum - heute;

            if (diff <= 0) {
                document.getElementById('countdown').innerText = 'Die Klausur beginnt jetzt!';
            } else {
                const tage = Math.floor(diff / (1000 * 60 * 60 * 24));
                document.getElementById('countdown').innerText = `Noch ${tage} Tage bis zur Klausur.`;
            }
        }

        // Initiale Anzeige eines Spruchs und des Countdowns
        neuerSpruch();
        countdown();

        // Countdown alle 24 Stunden aktualisieren
        setInterval(countdown, 86400000);
    </script>
</body>
</html>

