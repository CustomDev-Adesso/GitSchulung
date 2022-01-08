# Cherry-Pick


## Definition
Mit Cherry-Pick kannst du einen Commit eines Branches auf einen anderen Branch anwenden.
Es gibt einige Szenarien bei denen man Cherry-Pick benutzen kann, wobei beachtet werden muss, dass dadurch Commits dupliziert werden können. Hilfreich kann es durchaus sein wenn während der Entwicklung ein Bug gefunden wird und dieser per expliziten Commit gepacht wird, dann kann per Cherry-Pick der Commit auch direkt auf den Main-Branch angewendet werden

## Verwendung
Ziel-Branch auschecken und folgenden Befehl ausführen, dabei ist "commitSha" der Hash des Commits der geholt werden soll.

    git cherry-pick <commitSha>

Nach der Ausführung des Befehls gibt es im ausgecheckten Branch einen Commit mit dem gleichen Inhalt wie der ausgewählte Commit.


### --no-commit
Wenn man den Commit nicht direkt im Ziel-Branch commiten will sondern davor noch bearbeiten will kann man mittels

    git cherry-pick <commitSha> -n

den Inhalt des Commits auch einfach ins kopieren lassen.


### --edit
Beim Cherry-Pick kann auch die Commit Message angepasst werden

    git cherry-pick <commitSha> -e


## git log
Um schnell und einfach den Hash des Commits rauszufinden den man sich holen will, kann man sich mit folgenden Befehl sich die Commits des Branches anschauen in dem der Commit liegt

    git log <branch> --pretty=oneline


## Cherry-Pick Commands

    usage: git cherry-pick [<options>] <commit-ish>...
        or: git cherry-pick <subcommand>

            --quit                end revert or cherry-pick sequence
            --continue            resume revert or cherry-pick sequence
            --abort               cancel revert or cherry-pick sequence
            --skip                skip current commit and continue
            --cleanup <mode>      how to strip spaces and #comments from message
            -n, --no-commit       don't automatically commit
            -e, --edit            edit the commit message
            -s, --signoff         add Signed-off-by:
            -m, --mainline <parent-number>
                                  select mainline parent
            --rerere-autoupdate   update the index with reused conflict resolution if possible
            --strategy <strategy>
                                  merge strategy
            -X, --strategy-option <option>
                                  option for merge strategy
            -S, --gpg-sign[=<key-id>]
                                  GPG sign commit
            -x                    append commit name
            --ff                  allow fast-forward
            --allow-empty         preserve initially empty commits
            --allow-empty-message
                                  allow commits with empty messages
            --keep-redundant-commits
                                  keep redundant, empty commits


## Fahrplan Schulung

- Vorbereitung:

    Repository mit folgender Struktur

        main:    a - b - c - d - h
                  \
        feature:   e - f - g  

    Dabei ist der Commit "h" fälschlicherweise auf "main" commited worden und nicht wie geplant auf den "feature" Branch

- Commands
  - Commit Hash rausfinden: git log master
  - Sicherstellen das man auf auf den Zielbranch "feature" ist
  - Cherry-pick: git cherry-pick "commitSha"




