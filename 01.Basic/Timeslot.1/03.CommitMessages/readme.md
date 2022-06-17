# Commit Messages 

![As a project drags on, my git commit message get less and less informative.][logo]
_[Logo: xkcd 1296](https://xkcd.com/1296)_

Unser Version Control System (VCS) ermöglicht es uns Schnappschüsse von
Daten zu verwalten. Anhand des Schnappschusses zeigt uns git als Inhalt
den Unterschied zu der vorhergehenden oder einer anderen Version. Diese
Änderung Bedeutung zu geben liegt damit ganz bei uns.

In einem Projekt sind immer mindestens zwei Personen beteiligt. Der
initiale Ersteller und jemand der den Inhalt später ließt.

## Vorbereitung

Um bestmöglich Commit[^1]-Nachrichten erstellen zu können sollten wir das
meiste aus unserem Tooling herausholen. Zwar gibt es viele Programme
(IDEs) welche eine Integration von git anbieten aber die genauen
Aktionen lassen sich sehr gut nachvollziehen und ausführen über das
Command Line Interface (CLI).

Dafür hinterlegen wir in unserem System einen Editor unserer Wahl:

1. Notepad++ [Windows]

``` bash
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

2. Visual Studio code (vscode) [Cross-Platform]

``` bash
$ git config --global core.editor "code --wait"
```

3. Vim [Cross-Platform]

``` bash
$ git config --global core.editor "vim --nofork"
$ cat ~/.vimrc
[...]
au BufRead */.git/* set colorcolumn=73 textwidth=72 spell spelllang=en
[...]
```

---

Wir unterscheiden bei einer Commit[^1]-Nachricht zwischen dem Betreff
(subject[^2]) und dem Inhalt (body[^3]).

## Betreff

Der Betreff[^2] wird knapp formuliert und im Imperativ geschrieben!

Das hat den Hintergrund das dieser in vielen Tools angezeigt wird ohne
den gesamten Inhalt[^3] darzustellen.

(Manche Projekte haben spezielle Vorgaben z.B. Präfix:)

``` bash
$ git log
[...]
commit ce18a30bb78720d90df42b9d9ee6b8b7dd33d7e6
Author: Fabian Stelzer <fs@gigacodes.de>
Commit: Junio C Hamano <gitster@pobox.com>

gpg docs: explain better use of ssh.defaultKeyCommand

Using `ssh-add -L` for gpg.ssh.defaultKeyCommand is not a good
recommendation. It might switch keys depending on the order of known
keys and it only supports ssh-* and no ecdsa or other keys.
Clarify that we expect a literal key prefixed by `key::`, give valid
example use cases and refer to `user.signingKey` as the preferred
option.

Signed-off-by: Fabian Stelzer <fs@gigacodes.de>
Signed-off-by: Junio C Hamano <gitster@pobox.com>
[...]
```
Ursprung  https://lore.kernel.org/git/20220608152437.126276-1-fs@gigacodes.de/
Das Beispiel ist direkt aus dem git Projekt (einer der letzten Commits).

``` bash
$ git log --oneline
[...]
ce18a30bb7 gpg docs: explain better use of ssh.defaultKeyCommand
[...]
```

``` bash
$ git shortlog
[...]
Fabian Stelzer (29):
[...]
gpg-interface/gpgsm: fix for v2.3
gpg docs: explain better use of ssh.defaultKeyCommand
[...]
```

Der shortlog und anderes Tooling kann verwendet werden um ordentliche
Release notes zu erstellen. Wenn die Commits sauber gepflegt sind
lassen sich durch den Maintainer alle notwendigen Informationen
herausziehen.
_[keep a changelog: Don’t let your friends dump git logs into changelogs.][keep_a_changelog]_

Jetzt haben wir an drei verschiedene Stellen den selben Commit[^1]
gesehen. Ohne uns die tatsächliche Änderung zu betrachten wissen wir
bereits viel über diese Änderung und können anhand der Nachricht
entscheiden wie relevant diese Änderung gerade für uns ist.

Dadurch das der Betreff auf 50 bis 72 Zeichen begrenzt ist sind die
Programme die diesen Teil der Nachricht anzeigen auch darauf optimiert.
Auch grafische Programme verlassen sich auf diese Eigenschaft (GitHub,
Azure DevOps, Gitk, Visual Studio und viele mehr).

Generell sollte der Betreff[^2] in dieses Schema passen:
`If applied, this commit will ________`

Damit ergibt es auch Sinn den Betreff im Imperativ zu formulieren.

Beispiele:
 - `If applied, this commit will _refactor subsystem X for readability_`
 - `If applied, this commit will _remove deprecated methods_`

## Inhalt

Wie oben bereits in der Ausgabe zu sehen ist gibt der Inhalt[^3]
weitere Auskunft über die Änderung:

> gpg docs: explain better use of ssh.defaultKeyCommand
>
> Using `ssh-add -L` for gpg.ssh.defaultKeyCommand is not a good
> recommendation. It might switch keys depending on the order of known
> keys and it only supports ssh-* and no ecdsa or other keys.
> Clarify that we expect a literal key prefixed by `key::`, give valid
> example use cases and refer to `user.signingKey` as the preferred
> option.

Durch diesen Text werden wichtige Fragen geklärt:
 - Warum ist diese Anpassung notwendig?
 - Wie wird das genannte Problem angegangen?
 - Was ist von dieser Änderung betroffen?

Unabhängig vom verwendeten System sollte jeder Gutachter die Änderung
genau verstehen bevor die tatsächlich angepassten Textstellen
betrachtet werden müssen.

Eine gute Daumenregel ist das jeder Commit[^1] nur eine logische
Änderung enthalten sollte. Ein anderer Entwickler sollte in der Lage
sein nur anhand des Betreffs[^2] und des Inhalts[^3] den Patch
innerhalb einer angemessenen Zeit zu implementieren.

Die tatsächliche Anpassung kann durch Code, einen Kommentar, oder
Dokumentation gelöst sein, was aber nicht Teil der Commit[^1]-Nachricht
ist. Wenn sich durch die Nachricht herausstellt das die eigentliche
Anpassung relevant wird kann diese z.B. mit `git show #hash#`
eingesehen werden.

## Zusammenfassung der Regeln

Es gibt einige Regeln auf die sich allgemein in der Community geeinigt
wurde:
1. Betreff[^2] vom Inhalt[^3] mit einer Leerzeile
trennen
2. Betreff[^2] auf 50 Zeichen begrenzen
3. Kapitalisierung des Betreff[^2]
4. Der Betreff endet nicht mit einem Punkt
5. Schreibe den Betreff[^2] im Imperativ
6. Inhalt[^3] auf 72 Zeichen pro Zeile begrenzen
7. Der Inhalt[^3] beschreibt __Was__ angepasst wurde und __Warum__ diese
Anpassung notwendig ist

Einiger dieser Punkte kommen direkt als Vorschlag von git selbst [^4]
und haben sich in der Praxis gut bewährt.

Den Kontext zu einer Änderung wiederherzustellen ist sehr zeitaufwendig.
Diese Zeit kann minimiert werden durch gute Commits[^1]. Deshalb
zeichnen gute Commits[^1] einen guten Teamplayer aus. Andere Entwickler
und dein zukünftiges Selbst werden es dir Danken.

## Hands on

[![asciicast - Git commit](https://asciinema.org/a/502382.svg)](https://asciinema.org/a/502382)

Bei euch wird sich der konfigurierte Editor öffnen. Die Variante von
`git commit -v` gibt zusätzlich noch die Änderung in der Datei aus,
sodass der Commit nur das enthält was gewünscht ist. Diese Option kann
auch immer aktiv gesetzt werden mit `git config --global commit.verbose true`.

## Beispiele aus öffentlichen Projekten

 - Bitcoin Core [eb0b56b][bitcoin_simplify_serializeh_exception_handling]
 - [Linux kernel][linux_kernel]
 - [Git itself][git]
 - [Spring boot][spring_boot]
 - [Repositories][gh_tim_pope] by Tim Pope

Sources:
 - Gustavsson, B. (2021, June 5). Writing good commit messages. Erlang/otp. [https://github.com/erlang/otp/wiki/writing-good-commit-messages][gustavsson2021]
 - Pope, T. (2008, April 19). A Note About Git Commit Messages. tpope blogs here, when he blogs. [https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html][pope2008]
 - Hutterer, P. (2009, December 28). On commit messages. Who-T. [http://who-t.blogspot.com/2009/12/on-commit-messages.html][hutterer2009]
 - How to Write a Git Commit Message. (2014, August 31). cbeams. [https://cbea.ms/git-commit/][cbeams2014]
 - Thompson, D. (2019, August 30). My favourite Git commit. dhwthompson.com. [https://dhwthompson.com/2019/my-favourite-git-commit][thompson2019]
 - O'Leary, R. (2020, September 15). How to use VS Code as your Git editor, difftool, and mergetool. roboleary.net. [https://www.roboleary.net/vscode/2020/09/15/vscode-git.html][oleary2020]
 - Chacon, S., & Straub, B. (2014) Pro Git: Everthing you need to know about Git. Apress. [https://git-scm.com/book/en/v2][chaconstraub2014]

[logo]: https://imgs.xkcd.com/comics/git_commit.png "Git commit"
[gustavsson2021]: https://github.com/erlang/otp/wiki/writing-good-commit-messages
[pope2008]: https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[hutterer2009]: http://who-t.blogspot.com/2009/12/on-commit-messages.html
[cbeams2014]: https://cbea.ms/git-commit/
[thompson2019]: https://dhwthompson.com/2019/my-favourite-git-commit
[oleary2020]: https://www.roboleary.net/vscode/2020/09/15/vscode-git.html
[chaconstraub2014]: https://git-scm.com/book/en/v2

[git_glossary_commit]: https://git-scm.com/docs/gitglossary#Documentation/gitglossary.txt-aiddefcommitacommit
[git_commit_discussion]: https://git-scm.com/docs/git-commit#_discussion
[bitcoin_simplify_serializeh_exception_handling]: https://github.com/bitcoin/bitcoin/commit/eb0b56b19017ab5c16c745e6da39c53126924ed6
[linux_kernel]: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/
[git]: https://git.kernel.org/pub/scm/git/git.git/log/
[spring_boot]: https://github.com/spring-projects/spring-boot/commits/main
[gh_tim_pope]: https://github.com/tpope
[keep_a_changelog]: https://keepachangelog.com/en/1.0.0/

[^1]: [Commit - Glossar][git_glossary_commit]
    > As a noun: A single point in the Git history; the entire history
    > of a project is represented as a set of interrelated commits. The
    > word "commit" is often used by Git in the same places other
    > revision control systems use the words "revision" or "version".
    > Also used as a short hand for commit object.

    > As a verb: The action of storing a new snapshot of the project’s
    > state in the Git history, by creating a new commit representing
    > the current state of the index and advancing HEAD to point at the
    > new commit.
[^2]: Subject -> der Betreff der Commit-Nachricht
[^3]: Body -> der Inhalt der Commit-Nachricht
[^4]: Vorschläge zur Konvention zu Commit-Nachrichten [git commit - Diskussion][git_commit_discussion]

