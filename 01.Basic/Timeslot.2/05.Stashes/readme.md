# Stashes


## Definition
Damit können Änderungen gesichert werden ohne sie zu commiten.
Ein Anwendungsszenario wäre zum Beispiel wenn du mitten in der Implementierung eines neuen Features bist, aber ein Bug reinkommt der zuerst bearbeitet werden muss. Du willst aber deine Änderungen noch nicht commiten, da sie noch nicht vollständig sind (und du willst auch keinen WIP Commit machen ;)). Durch den Stash kannst du deine Änderungen einfach speichern und kannst hast ein sauberen Stand und kannst den Branch wechseln. 
**Beachte das Stashes nur lokal vorhanden ist!**


## Anlegen eines Stashes
Mit dem Befehl

    git stash

werden alle Änderungen, egal ob Stage oder nicht, weg gespeichert und von der working copy entfernt. 
**Außer:**
- **von nicht verfolgten Dateien**
- **von ignorierten Dateien**


### Partielle Stashes
Man kann auch nur bestimmte Dateien, oder gar nur bestimmte Änderungen aus Dateien stashen.

    git stash -p

Command|Beschreibung
---|---
/ | mit Regex nach Hunk suchen
? | Hilfe
n | Hunk nicht in Stash aufnehmen
q | beenden
s | Hunk aufteilen
y | Hunk in Stash aufnehmen


### Nicht verfolgte oder ignorierte Dateien
Es kann auch bewusst nicht verfolgte Dateien im Stash mit berücksichtigt werden.

    git stash -u

Oder auch Änderungen an ignorierten Dateien.

    git stash -a


## Verwalten mehrerer Stashes
Um einen spezifischen Stash wieder anzuwenden, kann man sich mit

    git stash list

alle Stahes anzeigen lassen. 


## Diff mit Stash
Mit 

    git stash show <stash>

kann man sich einen spezifischen Stash dann genauer anschauen. Dabei kann die Stash Bezeichnung aus der vorher angeschauten Liste genommen werden.


## Wiederverwenden eines Stashes
Gespeicherten Stash auf working copy anwenden und aus Stash-Sammulung entfernen.

    git stash pop

Bei keiner Angabe welcher Stash angewendet werden soll, wird immer der zuletzt hinzugefügte Stash genommen, ähnlich wie bei einen Stack.

Es kann aber auch ein Stash angewendet werden ohne diesen aus der Stash-Sammlung zu entfernen.

    git stash apply

Die Befehle pop oder apply können auch auf einen speziellen Stash angewendet werden.

    git stash pop <stash>
    git stash apply <stash>


### Branch erstellen
Man kann auch direkt mit einen Stash einen neuen Branch erstellen.

    git stash branch <branch-name>

## Stash bereinigen
Nicht mehr benötigte Stashes können gelöscht werden, wenn kein expliziter Stash angegeben wird, greift wieder das "Stack-Verhalten" und der zuletzt hinzugefügte Stash wird gelöscht.

    git stash drop <stash>

Oder komplett alle Stashes löschen.

    git stash clear


## Stash Commands

    usage: git stash list [<options>]
        or: git stash show [<options>] [<stash>]
        or: git stash drop [-q|--quiet] [<stash>]
        or: git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
        or: git stash branch <branchname> [<stash>]
        or: git stash clear
        or: git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
          [-u|--include-untracked] [-a|--all] [-m|--message <message>]
          [--pathspec-from-file=<file> [--pathspec-file-nul]]
          [--] [<pathspec>...]]
        or: git stash save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
          [-u|--include-untracked] [-a|--all] [<message>]


## Fahrplan Schulung

- git stash
    - Beachte neue und ignorierte Files
- git pop
- git stash -p
- git stash
- git pop
    - letzter Stash wird genommen
- git stash
- git stash list
- git stash show 0
- git apply 0
- git stash branch new-branch
- git stash 
- git stash 
- git stash 
- git stash list
- git drop
- git stash list
- git clear
- git stash list