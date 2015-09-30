Einführung in Bash und UNIX-Werkzeuge für die Nut Shell
=======================================================

Dieses Repository enthält Lektionsdateien für den Vorkurs Informatik an der TU Braunschweig, die Mithilfe der Nut Shell gestartet werden können.

Setup
-----

Auf dem `gh-pages`-branch in diesem Repository liegen eine HTML-Seite mit Installationsanleitungen sowie Installationskripte. GitHub veröffentlicht die HTML-Seite automatisch auf <https://tubs-ips.github.io/nutsh-vorkurs/>.

Der Installationsprozess läuft dann wie folgt: Der Benutzer führt das `setup`-Skript aus, welches das `nutsh`-Skript herunterlädt, im Ordner `~/.vorkurs/` speichert und ausführt. Dieses sorgt bei jeder Ausführung für eine Aktualisierung der Nut Shell und der Lektionen und startet dann das `run`-Skript. Dieses komplizierte Setup stellt sicher, dass sämtliche Komponenten (inklusive des `run`-Skriptes) bei Problemen angepasst werden können und beim Neustart der Nut Shell aktualisiert werden.

Lektions-Stückelung
-------------------

In der Datei [info.yaml](info.yaml) steht, zu welchem Datum welche Lektionen freigeschaltet werden. Soll zum Beispiel am 8. Oktober 2015 alles bis inklusive der fünften Lektion freigeschaltet werden, lautet der Eintrag: `2015-10-08: 5`

Mit folgendem Befehl können (zum Testen, oder für besonders schnelle Teilnehmer) sämtliche Lektionen freigeschaltet werden: `touch ~/.vorkurs/nutsh-vorkurs/all`

Syntax der Lektions-Dateien
---------------------------

Die Syntaxelemente sind in [diesem Blogpost](http://morr.cc/bachelorarbeit-woche-9/) locker dokumentiert. Die [Bachelorarbeit](http://morr.cc/bachelor-thesis/) enthält zusätzlich eine sehr detaillierte Beschreibung.

Die Datei `common.nutsh` enthält Funktionen, die von allen Lektionsdateien benutzt werden können.

Achtung: Die Nummerierung der Lektionsdateien beginnt bei 0, die Nummerierung im Auswahlmenü jedoch bei 1.

Automatisiertes Testen
----------------------

Der `expect`-Befehl ist der verwirrendste und soll hier deshalb an folgendem Beispiel nochmal beschrieben werden:

```
"Remove `file` from your home directory."

prompt {
    if ! file("$HOME/file") {
        expect("rm $HOME/file")
        expect("mv $HOME/file /tmp")
        "Well done!"
        break
    }
}
```

Die `expect`-Befehle haben bei normaler Ausführung der Nut Shell keine Bedeutung, sie sind dafür da, automatisierte Tests durchführen zu können. Die Semantik ist folgende: Der Test überprüft für jeden `expect`-Befehl, ob, wenn dieser Befehl bei dem umschließenden Prompt eingegeben wird, der Programmfluss an der Stelle landet, wo das `expect` steht. Anders gesagt: Der Test scheitert, wenn der `expect`-Beefhl nicht die richtige (oder keine) `if`-Bedingung erfüllt.

Folgender Befehl überprüft automatisch sämtliche Lektionen auf korrekte Funktionsweise: `~/.vorkurs/go/bin/nutsh test ~/.vorkurs/nutsh-vorkurs/` (Das dauert etwas, weil alle expect-Befehle tatsächlich ausgeführt werden.) Es empfiehlt sich, diesen Test in jedem Raum, in dem der Vorkurs stattfinden soll, einmal laufen zu lassen. Um einzelne Lektionen zu testen, kann folgender Befehl verwendet werden: `~/.vorkurs/go/bin/nutsh test ~/.vorkurs/nutsh-vorkurs/ <Name der Lektionsdatei ohne Dateiendung>`
