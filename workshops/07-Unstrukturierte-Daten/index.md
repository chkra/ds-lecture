---
title: "Workshop 07: Unstrukturierte Daten"
layout: single
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
author_profile: true
author: Christina Kratsch
lecture_name: "Data Science"
lecture_desc: "Grundlegende Methoden für die Exploration und das Management von Daten."
licence: "CC-BY"
licence_desc: 2024 | HTW Berlin 
classes: wide
---


Die heutigen beiden Challenges sind beide etwas anspruchsvoller. Das Szenario, das wir heute üben wollen, ist aber ein ganz typisches: Sie haben eine grobe Aufgabenstellung und finden im Netz ein Tutorial, das *ähnlich*, aber auch *kompliziert* und stellenweise *völlig unverständlich* ist. Das ist eine ganz alltägliche Situation für einen Data Scientist. Versuchen Sie einfach, so weit wie möglich in den unten gelisteten Challenges zu kommen.


### 🚀 Challenge #1: Fraud Detection mit Neo4J

**Fraud Detection** bezieht sich auf die Maßnahmen und Techniken, die Unternehmen einsetzen, um Vermögenswerte, Identitäten, Kundendaten, Geschäftsinformationen, Konten und Transaktionen vor Betrügern zu schützen. Dies geschieht hauptsächlich durch die Analyse von Benutzeraktivitäten und Verhaltensmustern, die mit einem Baseline- oder Profil verglichen werden, das das normale Benutzerverhalten repräsentieren. Ein typisches Beispiel ist das Erkennen von Kreditkartenbetrügern in Onlineshops, bevor diese den Kauf ihres Warenkorbs abschließen können. Manchmal liegen für diese Accounts oder Kreditkarten weitere externe Zahlungsdaten vor.

[Dieser Artikel im Neo4J Developer Blog](https://neo4j.com/developer-blog/exploring-fraud-detection-neo4j-graph-data-science-part-1/) zeigt, wie Sie mit Hilfe von Graph-Datenbanken und einem Machine Learning-Algorithmus zur Klassifikation Kreditkartenbetrüger identifizieren können. Der Artikel nutzt einige (komplexe, fast esoterische) Algorithmen, der Erkenntnisgewinn entsteht aber vor allem aus einer detailierten Datananalyse.


**Aufgabe:** Arbeiten Sie sich, so gut es Ihnen möglich ist, durch die Anleitung. Sie können, müssen aber nicht den Code nachbauen. Am Ende sollten Sie in der Lage sein, folgende Fragen zu beantworten:
* Wie ist der Datensatz grundsätzlich aufgebaut?
* Beschreiben Sie das grundsätzliche vorgehen des Artikeln, ohne komplizierte Algorithmen-Namen. Formulieren Sie eher so: "1. Es werden Gruppen von User-Accounts gefunden. 2. Diese werden sortiert nach Betrugswahrscheinlichkeit...")
{: .notice--warning} 



### 🚀 Challenge #2: Klassifikation von Bildern

PyTorch, eine leistungsstarke Bibliothek für neuronale Netzwerke, ermöglicht es, Modelle zur Bildklassifizierung zu erstellen und zu trainieren. In diesem Prozess werden Bilder anhand ihrer Merkmale in verschiedene Klassen eingeteilt. Ein typisches Vorgehen umfasst das Laden der Daten, die Definition eines neuronalen Konvolutionsnetzwerks (CNN), die Festlegung einer Verlustfunktion und das Training des Modells mit Trainingsdaten. PyTorch bietet eine flexible und intuitive Umgebung, um fortschrittliche Bildklassifikationsmodelle zu entwickeln und zu optimieren.


[Dieser Artikel auf Towards Data Science](https://towardsdatascience.com/pytorch-image-classification-tutorial-for-beginners-94ea13f56f2) beschreibt, wie Sie mit Hilfe von PyTorch ein bestehendes CNN so erweitern können, dass es in der Lage ist, Ihre individuelle Art von Bildern zu klassifizieren.

**Aufgabe:** Arbeiten Sie sich, so gut es Ihnen möglich ist, durch die Anleitung. Es wird vermutlich nicht ohne größere Vorbereitung möglich sein, den Code persönlich nachzubauen, deshalb sollten Sie sich auf das Lesen des Artikels beschränken. Am Ende sollten Sie in der Lage sein, folgende Fragen zu beantworten:
* Wie ist der Datensatz grundsätzlich aufgebaut?
* Beschreiben Sie das grundsätzliche vorgehen des Artikeln, ohne komplizierte Algorithmen-Namen. Formulieren Sie eher so: "1. Es wird eine Pipeline zur Verarbeitung der Daten definiert. Darin ... 2. Anschließend wird das Modell verbessert, indem ...")
{: .notice--warning} 

 ([Eine lokale Kopie des Artikels finden Sie hier](./img/PyTorch-Image-Classification-Tutorial.mhtml))