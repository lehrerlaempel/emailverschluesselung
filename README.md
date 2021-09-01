# Tutorial: Wie man eine sichere E-Mailverschlüsselung einfach einrichtet (Eine Anleitung)
v 1.1 | Stand: Juli 2021 | Lizenz: CC BY-NC-SA 4.0

# 1 Was hier beschrieben werden soll
Diese Anleitung erklärt, wie zwei Nutzer:innen mit Hilfe des Mailprogramms [Thunderbird](https://www.thunderbird.net/de/) und dem darin integrierten [OpenPGP](https://de.wikipedia.org/wiki/OpenPGP) eine Mailverschlüsselung einrichten können. Hierzu wird in der Anleitung Thunderbird in der Version 78 verwendet. Welches Betriebssystem die beiden Teilnehmer:innen nutzen, ist dabei egal.

# 2 Warum Mailverschlüsselung
Inzwischen werden Mails oft zwischen den Servern der Anbieter oder aber beim Abruf durch ein Mailprogramm automatisch verschlüsselt übertragen. Das wird dann gerne von den Anbietern mit tollen Grafiken z.B. unter dem Begriff ("E-Mail made in Germany")[https://www.e-mail-made-in-germany.de/] beworben. Das ist schön, schützt aber nicht davor, dass die Mails mindestens auf den Servern der Mailanbieter sowie auf den Computern von Sender und Empfänger offen und unverschlüsselt gespeichert sind. Auch kann nicht sicher nachvollzogen werden, ob tatsächlich alle Übertragungsstrecken verschlüsselt waren.

Es ist daher wichtig, schon im Mailprogramm der Nutzer:innen die Mails zu verschlüsseln und erst beim Emfpänger auf dem Computer wieder zu entschlüsseln. Nur so ist sicher gestellt, dass weder bei der Übertragung der Mails noch auf den Mailservern der verwendeten Mailanbieter unerwünschter Zugriff auf die Inhalte erfolgt.

Auch wenn sich Mailverschlüsselung im privaten Bereich nie nennenwert durchgesetzt hat, so bietet Sie doch sicherheitsbewussten Nutzer:innen eine kostenlose und zuverlässige Möglichkeit, Inhalte gut zu schützen bzw. sicher zu übertragen.

# 3 Die Grenzen von Mailverschlüsselung
## 3.1 Metadaten
E-Mailverschüsselung schützt zuverlässig die Inhalte einer Mail. Ausdrücklich nicht geschützt werden hingegen die Metadaten wie z.B. Adressen von Sender und Emfpänger oder zum Beispiel Datum und Sendezeit. Wer wann mit wem schreibt, ist also auch bei konsequenter Nutzung von Mailverschüsselung für alle Mailprovider sowie z.B. für Angreifer:innen auf den Übertragungswege jederzeit ersichtlich. Übrigens ist auch für alle mit Zugriff auf die Mails klar erkennbar, dass hier gerade verschlüsselt kommuniziert wird.

Das lässt sich entweder dadurch ein Stück weit entschärfen, indem für die sichere Kommunikation beide Gesprächspartner:innen eine Mailadresse nutzen, die nur für diesen Zweck und ohne die Preisgabe persönlicher Daten angelegt wurde. Dann sind auch die Metadaten erstmal wenig wert.

## 3.2 Abstreitbarkeit und Folgenlosigkeit
Das für Mailverschlüsselung meist verwendete OpenPGP funktioniert einmal eingerichtet zwar zuverlässig, führt in manchen Situationen jedoch zu Problemen, über die man sich vor der Verwendung kurz Gedanken machen sollte.

Einerseits führt die Verschlüsselung zu dem unerwünschten Nebeneffekt, dass die Kommunikation im Nachhinein theoretisch nicht abgestritten werden kann. Sollte z.B. eine staatliche Stelle einen Kommunikationspartner unterwandern, so erhält diese im Zweifelsfall viel Beweismaterial gegenüber dem anderen Gesprächsteilnehmer. Da nur dieser mit seinen Schlüsseln die Mails verfassen und signieren konnte, kann er später nicht abstreiten, einzelne Nachrichten geschickt zu haben. 

Ein weiteres Problem ist, dass dauerhaft mit den selben Schlüsseln gearbeitet wird. Gelingt einer Angreiferin also der Diebstahlt eines Schlüssels, kann diese im schlimmsten Fall die komplette Kommunikation rückwirkend entschlüsseln.

## 3.3 Und jetzt?
Wem das alles zu unsicher und problematisch klingt, der sollte sich für sensible Kommunikation von dem 50 Jahre alten Protokoll E-Mail verabschieden und auf moderen Messenger wie zum Beispiel [Signal](https://signal.org/de/) oder direkt [Briar](https://briarproject.org/) setzen, die viele der oben beschriebenen Probleme durch clevere Tricks versuchen zu umgehen. Oder man geht auf Nummer sicher, lässt alle elektronsichen Geräte zuhause und bespricht sich bei einem Spaziergang durch den Park.

Für alle anderen bietet Mailverschlüsselung aber einen soliden Schutz für die bequeme Übertragung sensibler Daten.

# 4 HowTo E-Mails verschlüsseln
Genug der Vorrede: Wir richten nun also für zwei Gesprächspartner:innen einen sicheren Kommunikationskanal via verschlüsselter E-Mail ein.

## 4.1 Anlegen der Mailadressen
Legen Sie bei zwei Mailprovidern ihrer Wahl je ein Postfächer an. Suchen Sie sich Provider, die IMAP/SMTP unterstützen und die für das Anlegen eines Kontos möglichst wenig persönliche Daten erheben. Vermeiden Sie es unbedingt, bei der Anmledung tatsächliche Mailadresse, Handynummern, Postanschriften, Namen o.ä. von Ihnen anzugeben!

Wollen Sie die Postfächer später nur über Tor nutzen, sollten Sie diese bereits aus dem TorNetz einrichten, damit durch die Mailprovider von Anfang an keine echte IP von Ihnen gespeichert werden kann.

## 4.2 Installation von Thunderbird
Sofern noch nicht vorhanden, installieren Sie nun bei beiden Kommunikationspartnern die für das jeweilige Betriebssystem aktuellste Version von [Thunderbird](https://www.thunderbird.net/de/).

## 4.3 Prüfen der Programmversion
Öffnen Sie Thunderbird. Wählen Sie nun zunächst über die drei Striche oben rechts die Option Hilfe, klicken Sie dann auf "Über Thunderbird". Hier wird Ihnen nun die auf Ihrem Computer installierte Thunderbird Version angezeigt. Ist die erste Zahl der Versionsnummer größer als 70, können Sie dieses Unterkapitel überspringen.

Alle anderen kümmern sich bitte erstmal um ein Update auf Version 78 oder neuer, bevor Sie weitermachen.

Warum wir nicht mit der alten Version arbeiten? Da ab der Version 78 die Verschlüsselung in Thunderbird grundlegend anders funktioniert, macht es keinen Sinn mehr, sich mit der Verschlüsselung in den alten Versionen zu befassen, auch wenn in manchen konservativen Linux-Systemen noch das alte Thunderbird mitgeliefert wird, solange dieses noch mit Sicherheitsupdates versorgt wird. Seien Sie froh, der Umweg lohnt sich: In den alten Versionen war das Einrichten einer Mailverschlüsselung deutlich umständlicher.

## 4.4 Postfach einrichten
Starten Sie nun auf beiden Rechnern Thunderbird und richten Sie für beide Kommunikationspartner:innen das eben angelegte Mail-Postfach in Thunderbird ein.

Falls Sie bei der Einrichtung Probleme haben: Bei manchen Postfächern (z.B. web.de) muss der Zugriff von externen Programmen via "POP3&IMAP" auf das Postfach über die Einstellungen in der Weboberfläche des Postfachs erst freigegeben werden, bevor Thunderbird sich mit dem Postfach verbinden kann.

## 4.5 Verschlüsselung aktivieren
Öffnen Sie die Konten-Einstellungen (Rechtsklick auf die Mailadresse, dann "Einstellungen"). In diesen öffnen Sie nun für Ihr Postfach den Reiter "Ende-zu-Ende-Verschlüsselung" und klicken dann auf "Schlüssel hinzufügen". Erzeugen Sie einen neuen OpenPGP Schüssel. Bei den Einstellungen zur Erzeugung geben Sie bitte an, dass der Schlüssel nie abbläuft. Sie wollen sich ja schließlich auf den Kommunikationskanal verlassen können. Wählen Sie dann als Schlüsseltyp RSA und die maximal mögliche Schlüsselgröße (4096?).

Stellen Sie zum Abschluss sicher, dass im Einstellungsmenü unter "Ende-zu-Ende-Verschlüsselung" der eben erstelle Schlüssel ausgewählt ist.

## 4.6 Schlüsseltausch
Beide Kommunikationspartner:innen verfassen nun eine neue E-Mail an den jeweils anderen. Geben Sie einen nichtssagenden Betreff und Inhalt ein. Hinweis: Für kapitel 4.9 ist es wichtig, dass Sie hier Betreff und Inhalt nicht leer lassen! Vor dem Senden klicken Sie im oberen Rahmen auf den Pfeil rechts neben "Sicherheit" und wählen "Meinen öffentlichen Schlüssel anhängen". Schicken Sie dann die Mail ab.

Beide erhalten nun eine Mail mit den öffentlichen Schlüssel des anderen im Anhang. Klicken Sie mit der rechten Maustaste auf den Anhang und wählen Sie die Option "OpenPGP-Schlüssel importieren". Wählen Sie anschließend "Aktzeptieren" und bestätigen Sie.

## 4.7 Prüfen der Schlüssel
Um sicherzustelle, dass Sie auch wirklich miteinander und nicht mit einem Angreifer in der Mitte verschlüsseln, sollten Sie nun noch die Fingerabdrücke der Schlüssel abgleichen - am besten persönlich oder telefonisch. Gehen Sie dazu wieder in die "Ende-zu-Ende-Verschlüsselung"-Einstellung und klicken Sie dann auf "OpenPGP-Schüssel verwalten". Dort können Sie nun via Rechtsklick und "Schlüsseleigenschaften" die Fingerabdrücke der beiden Schlüssel abgleichen. Stellen Sie unbedingt sicher, dass bei Ihnen und dem Gesprächspartner bei beiden Schlüssel die selben Fingerabdrücke angezeigt werden. Nur so ist sichergestellt, dass wirklich niemand unterwegs an Ihre Inhalte kommt.

## 4.8 Machen
Ab jetzt könnnen Sie sich jederzeit verschlüsselte Nachrichten schicken. Einfach eine "normale" Mail an den Empfänger schreiben, gerne auch mit Anhängen. Vor dem Absenden dann einfach neben Sicherheit auf den Pfeil klicken und "nur mit Verschlüsselung senden" auswählen. Fertig.

## 4.9 Ob das wohl funktioniert hat?
Es ist zum Glück für das gute Bauchgefühl relativ einfach zu testen, ob Sie nun tatsächlich verschlüsselte Mails schreiben. Wechseln Sie dazu nach dem Versand einer verschlüsselten Mail in Thunderbird in den Ordner gesendet. Dort finden Sie mindestens zwei Mails: Eine unverschlüsselte, mit der Sie Ihren öffentlichen Schlüssel verschickt haben, sowie eine verschlüsselte Nachricht. 

Aber wie können Sie eigentlich testen, ob die Nachricht tatsächlich verschlüsselt war? Ganz einfach: Öffnen Sie beide Mails und klicken dann jeweils Strg + U. Dadurch öffenen Sie den Quelltext der Mail. Falls Sie das noch nicht kannten: So sieht eine Mail tatsächlich aus.

Verschaffen Sie sich zunächst eine Übersicht über den Quelltext der unverschlüsselten Mail. Finden Sie den Absender, den Empfänger, den Betreff und die eigentiche Nachricht? Schauen Sie sich dann den Quelltext der verschlüsselten Mail an. Sind Absender, Empfänger, Betreff und der Inhalt noch zu finden?

# 5 Schlüssel-Server
Soll eine Mailadresse für ein größeres Publikum verschlüsselt erreichbar sein, so kann erwägt werden, diese inkl. zugehörigem public key auf einem Schlüsselserver zu veröffentlichen. So können Personen, zu denen bisher kein Kontakt bestand, direkt den public key des Empfängers herunterladen und schon die erste Mail verschlüsselt schicken. Hierzu können z.B. die folgenden Server verwendet werden:

- [MIT](http://pgp.mit.edu/)
- [Ubuntu](https://keyserver.ubuntu.com/)
- [Mailvelope](https://keys.mailvelope.com/manage.html)

Für vertrauliche Adressen hingegen, die nur im kleinen Kreis verwendet werden, wird von der Nutzung von Keyservern abgeraten.

# 6 Sonstiges
- Mailverschlüsselung ist immer eine gute Idee. Diese ist jedoch gleich doppelt wichtig, wenn sogenannte [Freemailer](https://de.wikipedia.org/wiki/Freemail) oder z.B. [GMail](https://mail.google.com/) verwendet werden, deren Geschäftsmodell ja im Wesentlichen darauf beruht, möglichst viel Geld aus den Daten der Kund:innen zu machen. Viele von diesen Anbietern machen übrigens [keinen Hehl daraus](https://www.heise.de/tp/features/Bei-jeder-Mail-wird-mitgelesen-3434025.html), dass Sie die E-Mails Ihrer Kund:innen systematisch ananlysieren.
- In der c't 3/2021 wird im Titelthema ["Abhörsicher Kommunizieren"](https://www.heise.de/select/ct/2021/3) alles wissenswerte Rund um das Thema gut verständlich und sehr ausführlich erklärt. Wem das hier zu oberflächlich ist, sollte da mal reinschauen.
- Bis einschließlich Version 68 benötigte man in Thunderbird das Plugin Enigmail, um verschlüsselte Mails zu schreiben. Erst in den späteren Versionen (ab Sommer 2020) wurde diese Funktion direkt in Thunderbird integriert, so dass keine weiteren Plugins mehr notwendig sind. Sollten Sie also im Internet nach besseren Anleitungen als dieser suchen, achten Sie bitte darauf, dass diese zu der von Ihnen verwendeten Version passen.
- Nutzen Sie einen Schlüssel nicht für immer. Im Optimalfall wechseln Sie für einen Kommunikationskanal spätestens nach ein oder zwei Jahren den Schlüssel!

# 7 Das Kleingedruckte
## 7.1 Fehlerteufel
Diese Anleitung wurde nach bestem Wissen und Gewissen erstellt. Wir haben die feste Absicht, diese im Laufe der Zeit an Änderungen der erwähnten Software anzupassen und um weitere Aspekte zu ergänzen.

Ihnen sind Fehler aufgefallen? Sie haben Verbesserungs- oder Änderungswünsche? Dann nehmen Sie gerne Kontakt mit uns auf. Wir sind für jedes Feedback dankbar!

## 7.2 Lizenz
Dieser Text steht unter einer CC-Lizenz, ist also quasi schöpferisches Gemeingut.

Sie dürfen:
- **Teilen** das Material in jedwedem Format oder Medium vervielfältigen und weiterverbreiten
- **Bearbeiten** das Material remixen, verändern und darauf aufbauen

Der Lizenzgeber kann diese Freiheiten nicht widerrufen solange Sie sich an die Lizenzbedingungen halten.

Unter folgenden Bedingungen:
- **Namensnennung** Sie müssen angemessene Urheber- und Rechteangaben machen, einen Link zur Lizenz beifügen und angeben, ob Änderungen vorgenommen wurden. Diese Angaben dürfen in jeder angemessenen Art und Weise gemacht werden, allerdings nicht so, dass der Eindruck entsteht, der Lizenzgeber unterstütze gerade Sie oder Ihre Nutzung besonders.
- **Nicht kommerziell** Sie dürfen das Material nicht für kommerzielle Zwecke nutzen. 
- **Weitergabe unter gleichen Bedingungen** Wenn Sie das Material remixen, verändern oder anderweitig direkt darauf aufbauen, dürfen Sie Ihre Beiträge nur unter derselben Lizenz wie das Original verbreiten. 
- **Keine weiteren Einschränkungen** Sie dürfen keine zusätzlichen Klauseln oder technische Verfahren einsetzen, die anderen rechtlich irgendetwas untersagen, was die Lizenz erlaubt. 

Hinweise:
- Sie müssen sich nicht an diese Lizenz halten hinsichtlich solcher Teile des Materials, die gemeinfrei sind, oder soweit Ihre Nutzungshandlungen durch Ausnahmen und Schranken des Urheberrechts gedeckt sind.
- Es werden keine Garantien gegeben und auch keine Gewähr geleistet. Die Lizenz verschafft Ihnen möglicherweise nicht alle Erlaubnisse, die Sie für die jeweilige Nutzung brauchen. Es können beispielsweise andere Rechte wie Persönlichkeits- und Datenschutzrechte zu beachten sein, die Ihre Nutzung des Materials entsprechend beschränken.

*Dies war eine allgemeinverständliche Zusammenfassung der [Lizenz](https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode), die diese nicht ersetzt.*

## 7.3 Externe Links
Bitte erlauben Sie uns auch noch ein paar Wörter zu den auf dieser Seite gesetzten Links, wie sie von [eRecht24](https://www.e-recht24.de/muster-disclaimer.html) empfohlen werden:

Unser Angebot enthält Links zu externen Websites Dritter, auf deren Inhalte wir keinen Einfluss haben. Deshalb können wir für diese fremden Inhalte auch keine Gewähr übernehmen. Für die Inhalte der verlinkten Seiten ist stets der jeweilige Anbieter oder Betreiber der Seiten verantwortlich. Die verlinkten Seiten wurden zum Zeitpunkt der Verlinkung auf mögliche Rechtsverstöße überprüft. Rechtswidrige Inhalte waren zum Zeitpunkt der Verlinkung nicht erkennbar. Eine permanente inhaltliche Kontrolle der verlinkten Seiten ist jedoch ohne konkrete Anhaltspunkte einer Rechtsverletzung nicht zumutbar. Bei Bekanntwerden von Rechtsverletzungen werden wir derartige Links umgehend entfernen.
