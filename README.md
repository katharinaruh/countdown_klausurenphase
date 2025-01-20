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
        }

        .spruch {
            font-size: 1.5em;
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

        /* Liste der Sprüche */
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
        // Liste der Sprüche
        const sprueche = [
            "Glaub an dich selbst und du wirst erstaunt sein, was du erreichen kannst!",
            "Jeder Tag ist eine neue Chance, deine Träume zu verwirklichen.",
            "Erfolg ist das Ergebnis von harter Arbeit und Ausdauer.",
            "Du bist stärker, als du denkst.",
            "Nutze den heutigen Tag, um deinem Ziel näher zu kommen.",
            "Lernen ist der Schlüssel zum Erfolg.",
            "Bleib fokussiert und gib niemals auf.",
            "Jeder Schritt zählt – auch die kleinen.",
            "Glaube an deinen Fortschritt, nicht an Perfektion.",
            "Der Weg zum Erfolg beginnt mit dem ersten Schritt."
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
