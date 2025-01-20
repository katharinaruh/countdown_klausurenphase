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
          
