# lsx_trades

Tägliche Handelsdaten der LSX.

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
