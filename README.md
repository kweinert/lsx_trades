# lsx_trades

Tägliche Handelsdaten der LSX.

## Interpretation der Spalten

Ich habe von der Seite ls-x.de Nachhandelsdaten heruntergeladen. Es handelt sich um eine CSV-Datei. Die Struktur sieht so aus (Ich verwende die Programmiersprache R):

```
> str(dat)
'data.frame':	329723 obs. of  10 variables:
 $ isin         : chr  "DE000A1K0235" "IE00B4L5Y983" "IE00B3RBWM25" "IE000RHYOR04" ...
 $ tradeTime    : chr  "2025-03-26T06:30:00.305000Z" "2025-03-26T06:30:00.291000Z" "2025-03-26T06:30:00.277000Z" "2025-03-26T06:30:00.287000Z" ...
 $ quotation    : chr  "MONE" "MONE" "MONE" "MONE" ...
 $ price        : num  41.7 101.11 129.26 5.43 345.24 ...
 $ currency     : chr  "EUR" "EUR" "EUR" "EUR" ...
 $ size         : int  10 10 7 1842 29 8 22 9 5 5 ...
 $ TVTIC        : chr  "HAMLDE000A1K0235202503260630003619258A0000001" "HAMLIE00B4L5Y983202503260630003908008A0000005" "HAMLIE00B3RBWM25202503260630003907098A0000004" "HAMLIE000RHYOR04202503260630003722518A0000002" ...
 $ mic          : chr  "HAML;HAMN" "HAML;HAMN" "HAML;HAMN" "HAML;HAMN" ...
 $ flags        : chr  "ALGO;" "ALGO;" "ALGO;" "ALGO;" ...
 $ publishedTime: chr  "2025-03-26T06:30:00.457000Z" "2025-03-26T06:30:00.468000Z" "2025-03-26T06:30:00.474000Z" "2025-03-26T06:30:00.475000Z" ...
```

Was bedeuten die einzelnen Spalten? Formuliere deine Antwort so, dass ich es für ein README verwenden kann.

Antwort: https://grok.com/share/bGVnYWN5_28b83a21-73d2-4004-a28b-e528b3281f2d

1. **`isin` (Character)**  
   - **Bedeutung**: Die International Securities Identification Number (ISIN) des gehandelten Wertpapiers.  
   - **Beispiel**: `"DE000A1K0235"`  
   - **Zweck**: Eindeutige Identifikation eines Wertpapiers (z. B. Aktien, ETFs).

2. **`tradeTime` (Character)**  
   - **Bedeutung**: Zeitpunkt des Handels im ISO-8601-Format (UTC) mit Millisekunden Genauigkeit.  
   - **Beispiel**: `"2025-03-26T06:30:00.305000Z"`  
   - **Zweck**: Angabe, wann der Handel ausgeführt wurde.

3. **`quotation` (Character)**  
   - **Bedeutung**: Art der Quotierung oder des Handelssystems.  
   - **Beispiel**: `"MONE"`  
   - **Zweck**: Identifiziert das Handelssystem oder die Quotierungsart (Details können spezifisch für ls-x.de sein).

4. **`price` (Numeric)**  
   - **Bedeutung**: Preis des Wertpapiers pro Einheit zum Zeitpunkt des Handels.  
   - **Beispiel**: `41.7`  
   - **Zweck**: Gibt den gehandelten Preis in der angegebenen Währung an.

5. **`currency` (Character)**  
   - **Bedeutung**: Währung, in der der Preis angegeben ist.  
   - **Beispiel**: `"EUR"`  
   - **Zweck**: Definiert die Währungseinheit des Preises (hier Euro).

6. **`size` (Integer)**  
   - **Bedeutung**: Anzahl der gehandelten Einheiten (z. B. Aktien oder Anteile).  
   - **Beispiel**: `10`  
   - **Zweck**: Zeigt das Volumen des Handels an.

7. **`TVTIC` (Character)**  
   - **Bedeutung**: Transaction Venue Trade Identification Code (TVTIC), eine eindeutige Kennung für den Handel.  
   - **Beispiel**: `"HAMLDE000A1K0235202503260630003619258A0000001"`  
   - **Zweck**: Ermöglicht die Nachverfolgung und Identifikation eines spezifischen Handels.

8. **`mic` (Character)**  
   - **Bedeutung**: Market Identifier Code (MIC), der den Handelsplatz angibt.  
   - **Beispiel**: `"HAML;HAMN"`  
   - **Zweck**: Identifiziert die Börse oder den Handelsplatz (hier vermutlich Hamburg mit mehreren MICs).

9. **`flags` (Character)**  
   - **Bedeutung**: Zusätzliche Kennzeichen oder Attribute des Handels.  
   - **Beispiel**: `"ALGO;"`  
   - **Zweck**: Gibt spezielle Eigenschaften an, z. B. ob der Handel algorithmisch (`ALGO`) durchgeführt wurde.

10. **`publishedTime` (Character)**  
    - **Bedeutung**: Zeitpunkt der Veröffentlichung des Handels im ISO-8601-Format (UTC) mit Millisekunden Genauigkeit.  
    - **Beispiel**: `"2025-03-26T06:30:00.457000Z"`  
    - **Zweck**: Zeigt an, wann die Handelsdaten veröffentlicht wurden (kann sich vom `tradeTime` unterscheiden).


## Github Workflow

Ich möchte gern einen neuen github workflow anlegen. 
Er soll jeden Tag um 1:00 morgens laufen und zusätzlich manuell gestartet werden können.
Zunächst soll ein neuer Branch angelegt werden.
Dann soll die URL https://www.ls-x.de/_rpc/json/.lstc/instrument/list/lsxtradesyesterday abgerufen werden, und unter dem Namen lsx_trades_XXXX.csv.gz in diesem Branch abgelegt und gepusht werden, wobei XXXX das Datum des Vortags im Format %Y-%m-%d ist.
Kannst du dann einen Prüfschritt einbauen, ob die heruntergeladene und gezippte Datei größer als 1 MB ist? Falls nicht, ist etwas schiefgelaufen.
Dieser Branch soll dann zu einem Release verpackt und veröffentlicht werden. Dafür braucht der Workflow Schreibrechte, stelle das sicher. Benutze gh statt actions/create-release@v1 bzw. actions/upload-release-asset@v1.
Danach kann der Branch gelöscht werden. Nutze dazu gh und referenziere den Branch explizit.

Antwort: [https://grok.com/share/bGVnYWN5_7c9cc8e6-365d-492a-a356-9aa529318e30](https://grok.com/share/bGVnYWN5_a22c02f4-c3a2-46ad-a521-ca886b796ccf)

## Lokal synchronisieren

Schreibe ein bash-Skript, welches bei Aufruf folgendes tut. Fehlermeldungen, Kommentare usw. auf Englisch bitte.
Rufe "https://api.github.com/repos/kweinert/lsx_trades/releases" ab. Es handelt sich um Releases von Github im JSON-Format. Speichere die Datei als releases.json ab.
Finde heraus, welche csv.gz veröffentlicht wurden und unter welcher URL sie abrufbar sind. Speichere diese  als Umgebungsvariablen ab.
Prüfe, für welche .csv.gz es ein Release gibt, das nicht im Unterordner $LSX vorliegt.
Lade diese herunter und speichere sie in dem Unterordner $LSX.

Antwort: https://grok.com/share/bGVnYWN5_12b31830-5bc1-41ed-b090-2dd4356ca8cc
