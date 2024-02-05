# Vorlesung Data Science

Dieses Repository enthält die Unterlagen zum Kurs <em>Data Science</em> im Master Informatik in den Ingenieurwissenschaften an der HTW Berlin. Dieses Repository ist work-in-progress.


## Aufbau des Repositories

Das Repsitory basiert auf dem Jekyll Template [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) von Michael Rose. Alle technischen Ordner entstammen dem Template mit ggf. minimalen ästhetischen Anpassungen (z.B. Code Syntax Highlighting).

Folgende Ordner enthalten den Content:

* `/lectures` enthält die Einstiegsseiten und Übersichten für die theoretischen Inhalte der wöchentlichen Lektionen
* `/modules` enthält Ordner, die fachlich getrennt unterschiedliche Themen beinhalten. Eine wöchtenliche Lektion kann mehrere Module umfassen.
* `/workshops` enthält praktischen Aufgaben und Materialien für die wöchentlichen Gruppenarbeiten vor Ort.


## Seiteninhalte erzeugen

Diese Seite wurde mit Jekyll erstellt. Die erzeugten Inhalte sind mit eingecheckt. Zur Vorbereitung ist auf einem System, das eine aktuelle Version von Ruby benötigt, folgendes auszuführen:

```bash
# install gem manager, may need sudo
gem install bundler

# install all requirements listed in Gemfile
bundle install
```

Zum Bauen der Lösung folgende Befehle ausführen:

```bash
# build all pages
bundle exec jekyll build
# or build and serve all pages at a local webserver
bundle exec jekyll serve
```

Der Output findet sich als HTML-Seite im Unterordner `/site`. 

## Copyright

Alle Rechte vorbehalten | 2024 | KI Werkstatt @ HTW Berlin / CK.
