Grundsätzliche Vorgehensweise für Nutzung von Datenbankzugriffen (hier SQLite)

# SQLite Basics

Die Nutzung von Datenbanken ist in Python exzellent unterstützt. Für die gängisten Arten von Datenbanken ist die Vorgehensweise ähnlich. In diesem Modul zeigen wir die Grundlagen für Pythonentwicklung mit SQLite, da es einen exzellenten Kompromiss aus Mächtigkeit und Einfachheit in der Bedienung bietet.

Dieses Modul geht davon aus, dass der Leser mit den wesentlichen Grundkonzepten des Relationalen Datenbankmodells und der Verwendung von SQL vertraut ist und konzentriert sich auf die Demonstration einer Umsetzung mit Python und demonstriert die notwendige Syntax. Für eine grundsätzliche Einführung in das Thema findet sich am Ende des Kapitels eine Literaturübersicht. @todo

## Grundlegender Umgang mit Datenbanken

Die folgenden Schritte sind für die Interaktion mit Datenbanken meistens notwendig:

* connection zur Datenbank herstellen
* Referenz (Cursor-Objekt) zum Zugriff auf die Datenbank erstellen
* SQL-Query übergeben
* SQL-Query bestäitgen (commit)
* Rückgabe/Daten verwerten
* Schließen der Datenbankconnection

Diese Schritte werden wir im Folgenden demonstrieren.

### 1. connection zur Datenbank aufbauen

```python
import sqlite3

connection = sqlite3.connect("geburtstage.db")
```
Alle wesentliche Funktionalität ist im Modul `sqlite3` umgesetzt. Wir stellen eine connection zur Datenbank `geburtstage.db` her. Diese wird als Datei auf der Festplatte abgelegt.  Gibt es diese Datenbank noch nicht, wird sie automatisch beim ersten Aufruf erzeugt.

### 2. Cursor-Objekt cursor()

Der Cursor ist der zentrale Zugriffspunkt auf die Datenbank. Er zeigt die aktuelle Position beim Lesen bzw. Schreiben von Datensätzen.

```python
cursor = connection.cursor()
```

### 3. SQL-Code erstellen und an Datenbank senden

Die Datenbank existiert. Jetzt können wir unsere SQL-Anweisung an die Datenbank übergeben, die Übergabe läuft als String ab. Mit der Anweisung `execute()` wird die SQL-Anweisung ausgeführt.

Aktuell ist unsere DB allerdings noch leer, wir legen deshalb zuerst unsere gewünschten Tabellen an. 
Die übergebene Anweisung enthält für jede Spalte der neuen Tablle
* einen Namen (damit wir die „Spalte“ ansprechen können)
* die Art der Inhalte (String, Integer, Datum etc.)
* die Feldlänge
  
```python
sql_stmnt = """
CREATE TABLE personen (
vorname VARCHAR(20), 
nachname VARCHAR(30), 
geburtstag DATE
);"""

cursor.execute(sql_stmnt)
```

Anmerkung: es ist gute Praxis, eine SQL-Anweisung  als String vorzubereiten und dann als String an `execute` zu übergeben.

4. Anweisung ausführen lassen mit commit()

Beim Verändern von Daten in der Datenbank ist eine weitere Bestätigung zum Ausführen notwendig. Die übergebene SQL-Anweisung muss nun ausgeführt werden. Dazu wird über den Befehl `commit()` dem Datenbanksystem mitgeteilt, dass endgültig die Anweisung ausgeführt werden darf.

```python
cursor.execute(sql_stmnt)
```

5. connection schließen mit close()
Wir schließen die connection nach getaner Arbeit über die Anweisung `close()`

```python
connection.close()
```

### Tipp für die Entwicklung

Lassen wir den Code nochmals ausführen, bekommen wir eine Fehlermeldung:

```python
sqlite3.OperationalError: table personen already exists
```

Diesen Fehler können wir vermeiden, indem wir die SQL-Anweisung nur ausführen lassen, wenn noch keine Tabelle existiert. Wir erweitern dazu unsere SQL-Anweisung um `IF NOT EXISTS`:

```python
sql_stmnt = """
CREATE TABLE IF NOT EXISTS personen (
vorname VARCHAR(20), 
nachname VARCHAR(30), 
geburtstag DATE
);"""
```

## Daten einfügen

Die SQL-Anweisung zum Eintragen von Daten in die Datenbank  lautet INSERT INTO. 

Wir fügen Daten in die Tabelle `personen` ein. Die Daten werden in der Reihenfolge eingegeben, wie wir die Felder festgelegt haben. 
```python
sql_stmnt = """
INSERT INTO personen VALUES ('Johann Wolfgang von', 'Goethe', '28.8.1749')
"""
```

**Achtung:** mit der hier verwendeten Schreibweise wird das Geburtsdatum von SQLite als String gespeichert, Datenoperationen auf der Zeitkompenente sind also nicht möglich.

### Variablen für INSERT nutzen

Etwas eleganter lassen sich Werte im SQL statement als Variablen übergeben:

```python
nachname   = "Schiller"
vorname    = "Friedrich"
geburtstag = "10.11.1759"

cursor.execute("""
                INSERT INTO personen 
                       VALUES (?,?,?)
               """, 
              (vorname, nachname, geburtstag)
              )

```

### Variablenlisten für INSERT

Für umfangreichere Datenmengen können Variablentupel als Liste übergeben werden. Der Befehl `execute_many` übernimmt dann die Ausführung:

```python
import sqlite3
connection = sqlite3.connect("geburtstage.db")
cursor = connection.cursor()

beruehmtheiten = [('Georg Wilhelm Friedrich', 'Hegel', '27.08.1770'), 
                  ('Johann Christian Friedrich', 'Hölderlin', '20.03.1770'), 
                  ('Rudolf Ludwig Carl', 'Virchow', '13.10.1821')]

cursor.executemany("""
                INSERT INTO personen 
                       VALUES (?,?,?)
                """, beruehmtheiten)

connection.commit()
```

### Dateien für INSERT

Im Data Science Umfeld müssen häufig Daten zwischen Verschiedenen Quellen und Formaten transferiert werden. Der folgende Code zeigt, wie eine Text-Datei direkt in eine Datenbank "gegossen" werden kann, ohne das zeilenweise Auslesen explizit zu formulieren.

Nehmen wir an, in einer Textdatei `adressen.csv` liegen Adressdaten separiert mit Semikolon vor:

```
nachname;vorname;geburtstag
Müller;Mike;05.03.80
Sommer;Elke;02.05.87
Schuster;Johanna;10.10.93
Trister;Theodor;08.03.87
```

Der folgende Code erlaubt das schnelle und elegante Einlesen:

```python
import csv
import sqlite3

# ... setup db here ...

# reading from csv
with open("adressen.csv") as csv_file:
    csv_reader_object = csv.reader(csv_file, delimiter=';')

    with sqlite3.connect("adressen.db") as connection:
        cursor = connection.cursor()
        cursor.executemany(sql_anweisung, csv_reader_object)
```



### SELECT, UPDATE und DELETE

Auslesen und Ändern von Daten erfolgt über die bekannten Mechanismen im SQL Statement:

```python
cursor.execute("SELECT nachname, geburtstag FROM personen")
inhalt = cursor.fetchall()
print(inhalt)
connection.close()
```

```python
nachname   = "Schiller"
vorname    = "Johann Christoph Friedrich"

cursor.execute("UPDATE personen SET vorname=? WHERE nachname=?", (vorname, nachname))
connection.commit()
```

```python
cursor.execute("DELETE FROM personen WHERE nachname=?, geburtstag=?", ('Goethe', '28.8.1749'))
```


# Furter Reading

* [SQLite und Datetime](https://www.sqlite.org/lang_datefunc.html)

# Quelle
https://www.python-lernen.de/sqlite-vorgehensweise.htm