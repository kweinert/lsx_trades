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


