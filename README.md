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
- **Prognose-Labor** (ab v3.6): testet 26 Signal-Ideen auf Stunden-, Tages- und Monatsebene (Übertreibung, RSI, Trend, Funding, 200-Tage-Linie, Mayer-Multiple, Regenbogen) ohne Blick in die Zukunft; „bestanden“ nur bei t ≥ 2,5, mind. 30 unabhängigen Fällen und Vorteil in beiden Hälften des Testzeitraums
- Bitcoin-Regenbogen als Langfrist-Bewertung (nur Anzeige)

## Mehrere Geräte (ab v3.4)

1. GitHub-Token anlegen: *Settings → Developer settings → Personal access tokens → Fine-grained* → Account permissions → **Gists: Read and write** (sonst nichts).
2. Am Gerät, auf dem der Bot laufen soll: Token und Gerätenamen eintragen → **„Dieses Gerät = Hauptgerät“**. Es legt ein geheimes Gist an und lädt den Stand jede Minute hoch (gepackt, ca. 0,25 MB).
3. An allen anderen Geräten: denselben Token eintragen → **„Dieses Gerät = nur ansehen“**. Sie übernehmen den Stand automatisch; Handeln und Bot sind dort gesperrt.
4. Hauptgerät wechseln: am neuen Gerät „Hauptgerät“ drücken – es übernimmt zuerst den neuesten Stand, das alte Gerät schaltet sich beim nächsten Abgleich selbst auf „ansehen“.

Der Token wird nur im jeweiligen Browser gespeichert – nicht in der Datei, nicht im Backup und nicht im Gist.

## Daten und Datenschutz

- Die Datei enthält **keine** API-Schlüssel oder Passwörter. Es werden nur öffentliche Kursdaten abgerufen.
- Konto, Trades und Einstellungen liegen ausschließlich **im eigenen Browser** (localStorage) und werden nirgends hochgeladen.
- Über GitHub Pages hat das Dashboard einen eigenen Browserspeicher. Daten aus einer lokal geöffneten Datei lassen sich über *Backup herunterladen* → *Backup laden* übernehmen.

## Versionen

`index.html` ist immer die aktuelle Version (derzeit **v3.7.0**). Ältere Stände stehen in der Git-Historie dieses Repositorys.

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

## Testergebnisse bisher (Papier, Nov. 2026)

Fünf Testläufe auf BTC und ZEC: Keine der kursbasierten Strategien zeigte nach Kosten einen belegbaren Vorteil. Die Handelssperre hat jedes Mal korrekt verhindert, dass der Bot ohne Vorteil handelt. v3.3 testet mit der Funding Rate erstmals eine neue Informationsquelle.
