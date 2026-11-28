# BTC-Live-Dashboard

Live-Dashboard für Bitcoin (und ETH, ZEC, Gold, Silber) mit Chart, Analyse, Zonen, Papier-Depot und einem Auto-Trader zum **Testen** von Handelsstrategien. Alles läuft als eine einzige HTML-Datei direkt im Browser.

**Live:** https://alf2255.github.io/Dashboard/

> ⚠️ Nur Papier-Handel. Kein echtes Geld, keine Anlageberatung. Ergebnisse aus Backtests sind keine Garantie für die Zukunft.

## Was drin ist

- Live-Kurse von Coinbase (Krypto) bzw. Binance Futures (Gold/Silber)
- Chart mit Zonen, Fibonacci, Elliott-Wellen, Trendwende-Anzeige
- Papier-Depot mit Trade-Protokoll (SHA-256-verkettet), Steuer-Hilfs-PDF, Backup als JSON
- **Auto-Trader** mit 10 Strategien auf 4 Zeitrahmen (1m, 1h, 4h, 1d)
  - Backtest mit Gebühren (0,05 %) und Slippage (0,03 %) je Seite
  - Walk-Forward-Test außerhalb der Stichprobe
  - **Handelssperre:** Der Bot handelt nur bei belegtem Vorteil (t ≥ 2,5 und mindestens 30 Trades außerhalb der Stichprobe)
  - Marktphasen-Filter (bullisch / bärisch / seitwärts)
- Derivate-Stimmung: Funding Rate und Open Interest (Binance Futures)
- **Ampel-Backtest** (ab v3.5): prüft die Ampel der Langfrist-Prognose rückwirkend an der ganzen Historie und vergleicht sie mit einem Zufallssignal; prüft außerdem, ob die Szenario-Prozente (bullisch/seitwärts/bärisch) und das 80 %-Band in der Vergangenheit gestimmt haben
- **Szenarien aus echten Kursbewegungen** (ab v3.7): bis 4 Wochen werden Bullisch/Seitwärts/Bärisch aus der Verteilung der vergangenen, standardisierten Kursbewegungen berechnet statt aus einer Glockenkurve (Bitcoin bewegt sich meist wenig und manchmal extrem); 6 und 12 Monate weiter mit Glockenkurve
- **Szenarien im Chart** (ab v3.8): Schalter „Szenarien“ zeichnet Bullisch/Seitwärts/Bärisch mit Wahrscheinlichkeit und Bestätigungsmarken in den Chart; Horizont wählbar (passend zur Zeiteinheit, 4 Std, 7 Tage, 4 Wochen)
- **Robuste Strategiewahl** (ab v3.11): im Walk-Forward-Test zählen nur Strategien mit mind. 15 Trades im Lernzeitraum, gewählt nach t-Wert statt Durchschnitt – Strategien mit wenigen Zufallstreffern werden nicht mehr gewählt; abschaltbar zum Vergleich
- **Nur Long** (ab v3.9): Schalter beim Auto-Trader – der Bot eröffnet keine Shorts; gilt gleich im Backtest, Walk-Forward und live, aus = Verhalten wie bisher
- **Marktwetten** (ab v3.10): Karte mit dem, was Händler auf der US-Prognosebörse Kalshi für Bitcoin, Ethereum und Gold zu festen Terminen einpreisen (nächste Stunde, Tag, Woche, Monat, länger): Mitte, 80 %-Bereich und Chance „höher als jetzt“; dazu ein Vergleich mit den Prozenten der Karte „Szenarien“. Ab v3.10.1 mit Trefferprotokoll: stündliche Schnappschüsse, geprüft mit dem offiziellen Kalshi-Abrechnungskurs. Nur Anzeige, der Bot nutzt es nicht. Falls der Browser den Abruf blockiert, lässt sich eine Umweg-Adresse eintragen
- **Prognose-Labor** (ab v3.6): testet 26 Signal-Ideen auf Stunden-, Tages- und Monatsebene (Übertreibung, RSI, Trend, Funding, 200-Tage-Linie, Mayer-Multiple, Regenbogen) ohne Blick in die Zukunft; „bestanden“ nur bei t ≥ 2,5, mind. 30 unabhängigen Fällen und Vorteil in beiden Hälften des Testzeitraums
- Bitcoin-Regenbogen als Langfrist-Bewertung (nur Anzeige)
- **Papier-Test MACD-Trendfolge Krypto** (ab v3.13): beobachtet ab einem Startdatum den Kandidaten aus der Chartwerk-Strategie-Suche (Tageskerzen, MACD 12/26/9, Einstieg bei Kreuzung der Nulllinie, Ausstieg bei Gegenkreuzung oder Notbremse 2× ATR) auf BTC, ETH, SOL und ZEC – nur Signale nach dem Start zählen. Urteil wie beim Bot (t ≥ 2,5, mind. 30 Trades). Nur Anzeige, der Bot handelt damit nicht

## Mehrere Geräte (ab v3.4)

1. GitHub-Token anlegen: *Settings → Developer settings → Personal access tokens → Fine-grained* → Account permissions → **Gists: Read and write** (sonst nichts).
2. Am Gerät, auf dem der Bot laufen soll: Token und Gerätenamen eintragen → **„Dieses Gerät = Hauptgerät“**. Es legt ein geheimes Gist an und lädt den Stand jede Minute hoch (gepackt, ca. 0,25 MB).
3. An allen anderen Geräten: denselben Token eintragen → **„Dieses Gerät = nur ansehen“**. Sie übernehmen den Stand automatisch; Handeln und Bot sind dort gesperrt.
4. Hauptgerät wechseln: am neuen Gerät „Hauptgerät“ drücken – es übernimmt zuerst den neuesten Stand, das alte Gerät schaltet sich beim nächsten Abgleich selbst auf „ansehen“.

Der Token wird nur im jeweiligen Browser gespeichert – nicht in der Datei, nicht im Backup und nicht im Gist.

## Daten und Datenschutz

- Die Datei enthält **keine** API-Schlüssel oder Passwörter. Es werden nur öffentliche Kursdaten abgerufen (Coinbase, Binance, ab v3.10 auch öffentliche Marktdaten von Kalshi).
- Konto, Trades und Einstellungen liegen ausschließlich **im eigenen Browser** (localStorage) und werden nirgends hochgeladen.
- Über GitHub Pages hat das Dashboard einen eigenen Browserspeicher. Daten aus einer lokal geöffneten Datei lassen sich über *Backup herunterladen* → *Backup laden* übernehmen.

## Versionen

`index.html` ist immer die aktuelle Version (derzeit **v3.13.1**). Ältere Stände stehen in der Git-Historie dieses Repositorys.

| Version | Neu |
|---|---|
| v3 | Gebühren/Slippage im Backtest, strenge Edge-Prüfung, Handelssperre, Kostenfilter |
| v3.1 | Marktphasen-Filter, Versionsanzeige |
| v3.2 | Lange Historie (4h ≈ 2 Jahre, 1d ab 2015), Strategie Struktur-Bruch (BOS/CHoCH), Zonen-Invalidierung, Regenbogen, Rückfrage beim Instrumentwechsel |
| v3.3 | Funding Rate als getestete Strategie „Funding-Extrem“, Karte Derivate-Stimmung (Funding + Open Interest) |
| v3.4 | Synchronisierung zwischen Geräten über ein geheimes GitHub-Gist (ein Hauptgerät handelt, andere sehen zu) |
| v3.4.1 | Nur ein Tab je Browser handelt (weitere Tabs = Anzeige), Warnung wenn der Bot nirgends läuft, Rückfrage beim Umstellen des Hauptgeräts |
| v3.4.2 | Klarere Warnung, wenn ein zweiter Tab/ein zweites Fenster desselben Browsers noch Hauptgerät ist |
| v3.4.3 | Fehlerkorrektur: Hauptgerät stellte sich wegen zwischengespeicherter GitHub-Antworten fälschlich selbst auf „ansehen“ |
| v3.9.0 | Schalter „Nur Long“ für den Auto-Trader (Backtest, Walk-Forward und live identisch) |
| v3.10.0 | Karte „Marktwetten“: Kalshi-Einpreisung für BTC, ETH und Gold (Stunde bis Jahr) mit Vergleich zu „Szenarien“ – nur Anzeige |
| v3.10.1 | Marktwetten-Protokoll: stündlicher Schnappschuss (Hauptgerät), Prüfung mit dem Kalshi-Abrechnungskurs, Vergleich Szenarien gegen Markt (Brier) – synchronisiert über das Gist |
| v3.10.2 | Marktwetten-Protokoll schreibt Bitcoin und Gold immer beide mit, unabhängig vom gewählten Instrument |
| v3.10.3 | Eigene Karte „Hoch/Tief-Wetten“: Kalshi-Wetten auf Höchst- und Tiefststände bis Tag/Woche/Monat/Jahr (90 % · 50 % · 10 %) – nur Anzeige |
| v3.11.0 | Robuste Strategiewahl im Walk-Forward (mind. 15 Trades, Wahl nach t-Wert), abschaltbar |
| v3.12.0 | Marktwetten und Hoch/Tief-Wetten zusätzlich von **Polymarket** (Auswahl Kalshi / Polymarket / Beide); Protokoll schreibt beide Börsen mit (Polymarket geprüft mit dem Binance-Schlusskurs zum Termin) |
| v3.12.1 | Kursfenster per Knopf **„⛶ Groß“** bildschirmfüllend (Esc oder „✕ Klein“ schließt) |
| v3.13.0 | Karte „Papier-Test MACD-Trendfolge Krypto“: Kandidat aus Chartwerk ab Startdatum beobachten (nur Anzeige, Bot unverändert) |
| v3.13.1 | Papier-Test: „Gegenprobe“ – dieselben Regeln auf 16 Kryptos außerhalb der Suche (bis 8 Jahre), Urteil gesamt und je Hälfte |

## Testergebnisse bisher (Papier, Nov. 2026)

Fünf Testläufe auf BTC und ZEC: Keine der kursbasierten Strategien zeigte nach Kosten einen belegbaren Vorteil. Die Handelssperre hat jedes Mal korrekt verhindert, dass der Bot ohne Vorteil handelt. v3.3 testet mit der Funding Rate erstmals eine neue Informationsquelle.
