---
title: "Methoden der Datenanalyse: Clustering"
layout: single
author_profile: true
author: Christina Kratsch
lecture_name: "Data Science"
lecture_desc: "Grundlegende Methoden für die Exploration und das Management von Daten."
licence: "CC-BY"
licence_desc: 2024 | HTW Berlin 
classes: wide
---

## Clustering im echten Leben

Der Künstler Urs Wehrli ist dafür bekannt, dass er sehr gern aufräumt. Nichts ist vor ihm sicher, nicht mal Kandisky. Die *Sendung mit der Maus* erklärt das sehr schön - [schauen Sie sich es gern im Video an](https://www.youtube.com/watch?v=GPeNVYKaYZE):

<a href="https://www.youtube.com/watch?v=GPeNVYKaYZE"><img src="./img/Wehrli.png"></a>


Dieses "Aufräumen", das Herr Wehrli da so gerne betreibt, ist letzten Endes eine besondere Form der Datenanalyse. Hier werden Entitäten in **Cluster** gruppiert, basierend auf ihren **Merkmalen**. 

**⚑ Quelle** <br> Wesentliche Teile der folgenden Ausführungen sind aus dem Kurs ["Machine Learning for Beginners"](https://github.com/microsoft/ML-For-Beginners/tree/main) entnommen. 
{: .notice--info}

## Was ist Clustering?

Clustering ist ein Typ des [Unüberwachten Lernens](https://de.wikipedia.org/wiki/Un%C3%BCberwachtes_Lernen), der davon ausgeht, dass ein Datensatz unbeschriftet ist oder dass seine Eingaben nicht mit vordefinierten Ausgaben übereinstimmen. Es verwendet verschiedene Algorithmen, um unbeschriftete Daten zu durchsuchen und **Gruppierungen** entsprechend der Muster zu erstellen, die es in den Daten erkennt. [Clustering](https://link.springer.com/referenceworkentry/10.1007%2F978-0-387-30164-8_124) ist sehr nützlich für die Datenexploration. Mal sehen, ob es helfen kann, Trends und Muster in der Art und Weise zu entdecken, wie das nigerianische Publikum Musik konsumiert.

✅ Nehmen Sie sich einen Moment Zeit, um über die Verwendungen von Clustering nachzudenken. Im wirklichen Leben tritt Clustering immer dann auf, wenn Sie einen Haufen Wäsche haben und die Kleidung Ihrer Familienmitglieder sortieren müssen 🧦👕👖🩲. In der Datenwissenschaft tritt Clustering auf, wenn man die Vorlieben eines Benutzers analysiert oder die Merkmale eines ungelabelten Datensatzes bestimmen möchte. Clustering hilft gewissermaßen dabei, aus dem Chaos Sinn zu machen, wie bei einer Sockenschublade.

In einem professionellen Umfeld kann Clustering verwendet werden, um Dinge wie Marktsegmentierung festzulegen, zum Beispiel um herauszufinden, welche Altersgruppen welche Artikel kaufen. Eine weitere Verwendung wäre die Anomalieerkennung, vielleicht um Betrug in einem Datensatz von Kreditkartentransaktionen zu erkennen. Oder Sie könnten Clustering verwenden, um Tumore in einer Reihe von medizinischen Scans zu bestimmen.

✅ Denken Sie einen Moment darüber nach, wie Sie Clustering bereits in einem Banken-, E-Commerce- oder Geschäftsumfeld erlebt haben könnten.

> 🎓 Interessanterweise entstand die Clusteranalyse in den 1930er Jahren in den Bereichen Anthropologie und Psychologie. Können Sie sich vorstellen, wie sie verwendet wurde?

Alternativ könnten Sie sie zur Gruppierung von Suchergebnissen verwenden - nach Einkaufslinks, Bildern oder Bewertungen zum Beispiel. Clustering ist nützlich, wenn Sie einen großen Datensatz haben, den Sie reduzieren und auf dem Sie eine genauere Analyse durchführen möchten, sodass die Technik verwendet werden kann, um Daten zu lernen, bevor andere Modelle erstellt werden.

✅ Sobald Ihre Daten in Clustern organisiert sind, weisen Sie ihnen eine Cluster-ID zu, und diese Technik kann nützlich sein, um die Privatsphäre eines Datensatzes zu bewahren; Sie können sich stattdessen auf einen Datenpunkt durch seine Cluster-ID beziehen, anstatt auf offenere identifizierbare Daten. Können Sie sich andere Gründe vorstellen, warum Sie sich auf eine Cluster-ID anstelle anderer Elemente des Clusters beziehen würden, um ihn zu identifizieren?


## Einstieg in das Clustering

[Scikit-learn bietet eine große Auswahl](https://scikit-learn.org/stable/modules/clustering.html) an Methoden zur Durchführung von Clustering an. Die Art, die Sie wählen, hängt von Ihrem Anwendungsfall ab. Laut der Dokumentation hat jede Methode verschiedene Vorteile. Hier ist eine vereinfachte Tabelle der von Scikit-learn unterstützten Methoden und ihrer geeigneten Anwendungsfälle:


| Methodenname                 | Anwendungsfall                                                          |
| :--------------------------- | :----------------------------------------------------------------------- |
| K-Means                      | allgemeiner Zweck, induktiv                                             |
| Affinity Propagation         | viele, ungleichmäßige Cluster, induktiv                                 |
| Mean-Shift                   | viele, ungleichmäßige Cluster, induktiv                                 |
| Spektrales Clustering        | wenige, gleichmäßige Cluster, transduktiv                               |
| Ward-hierarchisches Clustering | viele, eingeschränkte Cluster, transduktiv                              |
| Agglomeratives Clustering    | viele, eingeschränkte, nicht-euklidische Abstände, transduktiv          |
| DBSCAN                       | nicht-flache Geometrie, ungleichmäßige Cluster, transduktiv              |
| OPTICS                       | nicht-flache Geometrie, ungleichmäßige Cluster mit variabler Dichte, transduktiv |
| Gauß'sche Mischungen         | flache Geometrie, induktiv                                              |
| BIRCH                        | großer Datensatz mit Ausreißern, induktiv                               |

> 🎓 Wie wir Cluster erstellen, hängt stark davon ab, wie wir die Datenpunkte in Gruppen zusammenfassen. Lassen Sie uns einige Begriffe genauer betrachten:
>
> 🎓 ['Transduktiv' vs. 'induktiv'](https://de.wikipedia.org/wiki/Transduktive_Inferenz)
> 
> Transduktive Inferenz leitet sich von beobachteten Trainingsfällen ab, die spezifischen Testfällen entsprechen. Induktive Inferenz leitet sich von Trainingsfällen ab, die allgemeinen Regeln entsprechen, die dann nur auf Testfälle angewendet werden. 
> 
> Ein Beispiel: Stellen Sie sich vor, Sie haben einen Datensatz, der nur teilweise beschriftet ist. Einige Dinge sind 'Aufzeichnungen', einige 'CDs', und einige sind leer. Ihre Aufgabe ist es, Beschriftungen für die leeren Felder bereitzustellen. Wenn Sie einen induktiven Ansatz wählen, würden Sie ein Modell trainieren, das nach 'Aufzeichnungen' und 'CDs' sucht, und diese Beschriftungen auf Ihre unbeschrifteten Daten anwenden. Dieser Ansatz hat Schwierigkeiten, Dinge zu klassifizieren, die tatsächlich 'Kassetten' sind. Ein transduktiver Ansatz hingegen handhabt diese unbekannten Daten effektiver, indem er ähnliche Elemente gruppiert und dann einer Gruppe eine Beschriftung zuweist. In diesem Fall könnten Cluster 'runde musikalische Dinge' und 'quadratische musikalische Dinge' widerspiegeln. 
> 
> 🎓 ['Nicht-flache' vs. 'flache' Geometrie](https://datascience.stackexchange.com/questions/52260/terminology-flat-geometry-in-the-context-of-clustering)
> 
> Abgeleitet von mathematischer Terminologie bezieht sich nicht-flache vs. flache Geometrie auf die Messung von Abständen zwischen Punkten entweder durch 'flache' ([Euklidische](https://de.wikipedia.org/wiki/Euklidische_Geometrie)) oder 'nicht-flache' (nicht-euklidische) geometrische Methoden. 
>
> 'Flach' in diesem Zusammenhang bezieht sich auf die euklidische Geometrie (Teile davon werden als 'ebene' Geometrie unterrichtet), und nicht-flach bezieht sich auf nicht-euklidische Geometrie. Was hat Geometrie mit maschinellem Lernen zu tun? Nun, als zwei auf Mathematik basierende Felder muss es eine gemeinsame Möglichkeit geben, Abstände zwischen Punkten in Clustern zu messen, und das kann auf 'flache' oder 'nicht-flache' Weise geschehen, je nach Art der Daten. [Euklidische Abstände](https://de.wikipedia.org/wiki/Euklidischer_Abstand) werden als Länge eines Liniensegments zwischen zwei Punkten gemessen. [Nicht-euklidische Abstände](https://de.wikipedia.org/wiki/Nicht-euklidische_Geometrie) werden entlang einer Kurve gemessen. Wenn Ihre Daten, visualisiert, nicht auf einer Ebene zu existieren scheinen, müssen Sie möglicherweise einen spezialisierten Algorithmus verwenden, um damit umzugehen.
>
> ![Flache vs Nichtflache Geometrie Infografik](./images/flat-nonflat.png)
> Infografik von [Dasani Madipalli](https://twitter.com/dasani_decoded)
> 
> 🎓 ['Abstände'](https://web.stanford.edu/class/cs345a/slides/12-clustering.pdf)
> 
> Cluster werden durch ihre Distanzmatrix definiert, z.B. die Abstände zwischen Punkten. Diese Distanz kann auf verschiedene Arten gemessen werden. Euklidische Cluster werden durch den Durchschnitt der Punktwerte definiert und enthalten einen 'Schwerpunkt' oder Mittelpunkt. Die Abstände werden also durch die Entfernung zu diesem Schwerpunkt gemessen. Nicht-euklidische Abstände beziehen sich auf 'Clustroide', den Punkt, der am nächsten zu anderen Punkten liegt. Clustroide können wiederum auf verschiedene Arten definiert werden.
> 
> 🎓 ['Eingeschränkt'](https://de.wikipedia.org/wiki/Constrained_clustering)
> 
> [Eingeschränktes Clustering](https://web.cs.ucdavis.edu/~davidson/Publications/ICDMTutorial.pdf) führt 'halbüberwachtes' Lernen in diese unüberwachte Methode ein. Die Beziehungen zwischen den Punkten werden als 'kann nicht verknüpfen' oder 'muss verknüpfen' markiert, damit einige Regeln auf den Datensatz angewendet werden.
>
> Ein Beispiel: Wenn ein Algorithmus auf einen Satz von unbeschrifteten oder halb beschrifteten Daten losgelassen wird, können die von ihm erzeugten Cluster von schlechter Qualität sein. Im obigen Beispiel könnten die Cluster '

>
Ein Beispiel: Wenn ein Algorithmus auf einen Satz von unbeschrifteten oder halb beschrifteten Daten losgelassen wird, können die von ihm erzeugten Cluster von schlechter Qualität sein. Im obigen Beispiel könnten die Cluster 'runde Musikdinge' und 'quadratische Musikdinge' und 'dreieckige Dinge' und 'Kekse' gruppieren. Wenn einige Einschränkungen oder Regeln vorgegeben werden ("das Element muss aus Kunststoff sein", "das Element muss in der Lage sein, Musik zu produzieren"), kann dies dem Algorithmus helfen, bessere Entscheidungen zu treffen.
> 
> 🎓 'Dichte'
> 
> Daten, die 'rauschig' sind, gelten als 'dicht'. Die Abstände zwischen Punkten in jedem ihrer Cluster können sich bei genauerer Betrachtung als mehr oder weniger dicht oder 'überfüllt' erweisen, und daher müssen diese Daten mit der entsprechenden Clustering-Methode analysiert werden. [Dieser Artikel](https://www.kdnuggets.com/2020/02/understanding-density-based-clustering.html) zeigt den Unterschied zwischen der Verwendung von K-Means-Clustering und HDBSCAN-Algorithmen zur Exploration eines rauschigen Datensatzes mit ungleichmäßiger Clusterdichte.

## Clustering-Algorithmen

Es gibt über 100 Clustering-Algorithmen, und ihre Verwendung hängt von der Beschaffenheit der vorliegenden Daten ab. Lassen Sie uns einige der wichtigsten diskutieren:

- **Hierarchisches Clustering**. Wenn ein Objekt nach seiner Nähe zu einem nahe gelegenen Objekt klassifiziert wird, anstatt zu einem weiter entfernten, werden Cluster basierend auf der Entfernung ihrer Mitglieder zu und von anderen Objekten gebildet. Das hierarchische Clustering von Scikit-learn ist agglomerativ.

   ![Infografik zum hierarchischen Clustering](./images/hierarchical.png)
   > Infografik von [Dasani Madipalli](https://twitter.com/dasani_decoded)

- **Zentroid-Clustering**. Dieser beliebte Algorithmus erfordert die Wahl von 'k', oder die Anzahl der zu bildenden Cluster, wonach der Algorithmus den Mittelpunkt eines Clusters bestimmt und Daten um diesen Punkt sammelt. [K-Means-Clustering](https://de.wikipedia.org/wiki/K-means-Algorithmus) ist eine beliebte Version des Zentroid-Clustering. Der Mittelpunkt wird durch den nächsten Mittelwert bestimmt, daher der Name. Der quadrierte Abstand vom Cluster wird minimiert.

   ![Infografik zum Zentroid-Clustering](./images/centroid.png)
   > Infografik von [Dasani Madipalli](https://twitter.com/dasani_decoded)

- **Verteilungsbasiertes Clustering**. Basierend auf statistischer Modellierung konzentriert sich das verteilungsbasierte Clustering darauf, die Wahrscheinlichkeit zu bestimmen, dass ein Datenpunkt zu einem Cluster gehört, und ordnet ihn entsprechend zu. Gaußsche Mischmethoden gehören zu diesem Typ.

- **Dichtebasiertes Clustering**. Datenpunkte werden Clustern zugeordnet, basierend auf ihrer Dichte oder ihrem Gruppieren umeinander. Datenpunkte, die weit von der Gruppe entfernt sind, gelten als Ausreißer oder Rauschen. DBSCAN, Mean-Shift und OPTICS gehören zu diesem Clusteringtyp.

- **Gitterbasiertes Clustering**. Für mehrdimensionale Datensätze wird ein Raster erstellt und die Daten werden auf die Zellen des Rasters aufgeteilt, wodurch Cluster erstellt werden.




## Exercise - cluster your data

Clustering as a technique is greatly aided by proper visualization, so let's get started by visualizing our music data. This exercise will help us decide which of the methods of clustering we should most effectively use for the nature of this data.

1. Open the [_notebook.ipynb_](https://github.com/microsoft/ML-For-Beginners/blob/main/5-Clustering/1-Visualize/notebook.ipynb) file in this folder.

1. Import the `Seaborn` package for good data visualization.

    ```python
    !pip install seaborn
    ```

1. Append the song data from [_nigerian-songs.csv_](https://github.com/microsoft/ML-For-Beginners/blob/main/5-Clustering/data/nigerian-songs.csv). Load up a dataframe with some data about the songs. Get ready to explore this data by importing the libraries and dumping out the data:

    ```python
    import matplotlib.pyplot as plt
    import pandas as pd
    
    df = pd.read_csv("../data/nigerian-songs.csv")
    df.head()
    ```

    Check the first few lines of data:

    |     | name                     | album                        | artist              | artist_top_genre | release_date | length | popularity | danceability | acousticness | energy | instrumentalness | liveness | loudness | speechiness | tempo   | time_signature |
    | --- | ------------------------ | ---------------------------- | ------------------- | ---------------- | ------------ | ------ | ---------- | ------------ | ------------ | ------ | ---------------- | -------- | -------- | ----------- | ------- | -------------- |
    | 0   | Sparky                   | Mandy & The Jungle           | Cruel Santino       | alternative r&b  | 2019         | 144000 | 48         | 0.666        | 0.851        | 0.42   | 0.534            | 0.11     | -6.699   | 0.0829      | 133.015 | 5              |
    | 1   | shuga rush               | EVERYTHING YOU HEARD IS TRUE | Odunsi (The Engine) | afropop          | 2020         | 89488  | 30         | 0.71         | 0.0822       | 0.683  | 0.000169         | 0.101    | -5.64    | 0.36        | 129.993 | 3              |
    | 2   | LITT!                    | LITT!                        | AYLØ                | indie r&b        | 2018         | 207758 | 40         | 0.836        | 0.272        | 0.564  | 0.000537         | 0.11     | -7.127   | 0.0424      | 130.005 | 4              |
    | 3   | Confident / Feeling Cool | Enjoy Your Life              | Lady Donli          | nigerian pop     | 2019         | 175135 | 14         | 0.894        | 0.798        | 0.611  | 0.000187         | 0.0964   | -4.961   | 0.113       | 111.087 | 4              |
    | 4   | wanted you               | rare.                        | Odunsi (The Engine) | afropop          | 2018         | 152049 | 25         | 0.702        | 0.116        | 0.833  | 0.91             | 0.348    | -6.044   | 0.0447      | 105.115 | 4              |

1. Get some information about the dataframe, calling `info()`:

    ```python
    df.info()
    ```

   The output looking like so:

    ```output
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 530 entries, 0 to 529
    Data columns (total 16 columns):
     #   Column            Non-Null Count  Dtype  
    ---  ------            --------------  -----  
     0   name              530 non-null    object 
     1   album             530 non-null    object 
     2   artist            530 non-null    object 
     3   artist_top_genre  530 non-null    object 
     4   release_date      530 non-null    int64  
     5   length            530 non-null    int64  
     6   popularity        530 non-null    int64  
     7   danceability      530 non-null    float64
     8   acousticness      530 non-null    float64
     9   energy            530 non-null    float64
     10  instrumentalness  530 non-null    float64
     11  liveness          530 non-null    float64
     12  loudness          530 non-null    float64
     13  speechiness       530 non-null    float64
     14  tempo             530 non-null    float64
     15  time_signature    530 non-null    int64  
    dtypes: float64(8), int64(4), object(4)
    memory usage: 66.4+ KB
    ```

1. Double-check for null values, by calling `isnull()` and verifying the sum being 0:

    ```python
    df.isnull().sum()
    ```

    Looking good:

    ```output
    name                0
    album               0
    artist              0
    artist_top_genre    0
    release_date        0
    length              0
    popularity          0
    danceability        0
    acousticness        0
    energy              0
    instrumentalness    0
    liveness            0
    loudness            0
    speechiness         0
    tempo               0
    time_signature      0
    dtype: int64
    ```

1. Describe the data:

    ```python
    df.describe()
    ```

    |       | release_date | length      | popularity | danceability | acousticness | energy   | instrumentalness | liveness | loudness  | speechiness | tempo      | time_signature |
    | ----- | ------------ | ----------- | ---------- | ------------ | ------------ | -------- | ---------------- | -------- | --------- | ----------- | ---------- | -------------- |
    | count | 530          | 530         | 530        | 530          | 530          | 530      | 530              | 530      | 530       | 530         | 530        | 530            |
    | mean  | 2015.390566  | 222298.1698 | 17.507547  | 0.741619     | 0.265412     | 0.760623 | 0.016305         | 0.147308 | -4.953011 | 0.130748    | 116.487864 | 3.986792       |
    | std   | 3.131688     | 39696.82226 | 18.992212  | 0.117522     | 0.208342     | 0.148533 | 0.090321         | 0.123588 | 2.464186  | 0.092939    | 23.518601  | 0.333701       |
    | min   | 1998         | 89488       | 0          | 0.255        | 0.000665     | 0.111    | 0                | 0.0283   | -19.362   | 0.0278      | 61.695     | 3              |
    | 25%   | 2014         | 199305      | 0          | 0.681        | 0.089525     | 0.669    | 0                | 0.07565  | -6.29875  | 0.0591      | 102.96125  | 4              |
    | 50%   | 2016         | 218509      | 13         | 0.761        | 0.2205       | 0.7845   | 0.000004         | 0.1035   | -4.5585   | 0.09795     | 112.7145   | 4              |
    | 75%   | 2017         | 242098.5    | 31         | 0.8295       | 0.403        | 0.87575  | 0.000234         | 0.164    | -3.331    | 0.177       | 125.03925  | 4              |
    | max   | 2020         | 511738      | 73         | 0.966        | 0.954        | 0.995    | 0.91             | 0.811    | 0.582     | 0.514       | 206.007    | 5              |

> 🤔 If we are working with clustering, an unsupervised method that does not require labeled data, why are we showing this data with labels? In the data exploration phase, they come in handy, but they are not necessary for the clustering algorithms to work. You could just as well remove the column headers and refer to the data by column number. 

Look at the general values of the data. Note that popularity can be '0', which show songs that have no ranking. Let's remove those shortly.

1. Use a barplot to find out the most popular genres:

    ```python
    import seaborn as sns
    
    top = df['artist_top_genre'].value_counts()
    plt.figure(figsize=(10,7))
    sns.barplot(x=top[:5].index,y=top[:5].values)
    plt.xticks(rotation=45)
    plt.title('Top genres',color = 'blue')
    ```

    ![most popular](./images/popular.png)

✅ If you'd like to see more top values, change the top `[:5]` to a bigger value, or remove it to see all.

Note, when the top genre is described as 'Missing', that means that Spotify did not classify it, so let's get rid of it.

1. Get rid of missing data by filtering it out

    ```python
    df = df[df['artist_top_genre'] != 'Missing']
    top = df['artist_top_genre'].value_counts()
    plt.figure(figsize=(10,7))
    sns.barplot(x=top.index,y=top.values)
    plt.xticks(rotation=45)
    plt.title('Top genres',color = 'blue')
    ```

    Now recheck the genres:

    ![most popular](images/all-genres.png)

1. By far, the top three genres dominate this dataset. Let's concentrate on `afro dancehall`, `afropop`, and `nigerian pop`, additionally filter the dataset to remove anything with a 0 popularity value (meaning it was not classified with a popularity in the dataset and can be considered noise for our purposes):

    ```python
    df = df[(df['artist_top_genre'] == 'afro dancehall') | (df['artist_top_genre'] == 'afropop') | (df['artist_top_genre'] == 'nigerian pop')]
    df = df[(df['popularity'] > 0)]
    top = df['artist_top_genre'].value_counts()
    plt.figure(figsize=(10,7))
    sns.barplot(x=top.index,y=top.values)
    plt.xticks(rotation=45)
    plt.title('Top genres',color = 'blue')
    ```

1. Do a quick test to see if the data correlates in any particularly strong way:

    ```python
    corrmat = df.corr()
    f, ax = plt.subplots(figsize=(12, 9))
    sns.heatmap(corrmat, vmax=.8, square=True)
    ```

    ![correlations](images/correlation.png)

    The only strong correlation is between `energy` and `loudness`, which is not too surprising, given that loud music is usually pretty energetic. Otherwise, the correlations are relatively weak. It will be interesting to see what a clustering algorithm can make of this data.

    > 🎓 Note that correlation does not imply causation! We have proof of correlation but no proof of causation. An [amusing web site](https://tylervigen.com/spurious-correlations) has some visuals that emphasize this point.

Is there any convergence in this dataset around a song's perceived popularity and danceability? A FacetGrid shows that there are concentric circles that line up, regardless of genre. Could it be that Nigerian tastes converge at a certain level of danceability for this genre?  

✅ Try different datapoints (energy, loudness, speechiness) and more or different musical genres. What can you discover? Take a look at the `df.describe()` table to see the general spread of the data points.

### Exercise - data distribution

Are these three genres significantly different in the perception of their danceability, based on their popularity?

1. Examine our top three genres data distribution for popularity and danceability along a given x and y axis.

    ```python
    sns.set_theme(style="ticks")
    
    g = sns.jointplot(
        data=df,
        x="popularity", y="danceability", hue="artist_top_genre",
        kind="kde",
    )
    ```

    You can discover concentric circles around a general point of convergence, showing the distribution of points.

    > 🎓 Note that this example uses a KDE (Kernel Density Estimate) graph that represents the data using a continuous probability density curve. This allows us to interpret data when working with multiple distributions.

    In general, the three genres align loosely in terms of their popularity and danceability. Determining clusters in this loosely-aligned data will be a challenge:

    ![distribution](images/distribution.png)

1. Create a scatter plot:

    ```python
    sns.FacetGrid(df, hue="artist_top_genre", size=5) \
       .map(plt.scatter, "popularity", "danceability") \
       .add_legend()
    ```

    A scatterplot of the same axes shows a similar pattern of convergence

    ![Facetgrid](images/facetgrid.png)

In general, for clustering, you can use scatterplots to show clusters of data, so mastering this type of visualization is very useful. In the next lesson, we will take this filtered data and use k-means clustering to discover groups in this data that see to overlap in interesting ways.

---

## 🚀Challenge

In preparation for the next lesson, make a chart about the various clustering algorithms you might discover and use in a production environment. What kinds of problems is the clustering trying to address?

## [Post-lecture quiz](https://gray-sand-07a10f403.1.azurestaticapps.net/quiz/28/)

## Review & Self Study

Before you apply clustering algorithms, as we have learned, it's a good idea to understand the nature of your dataset. Read more on this topic [here](https://www.kdnuggets.com/2019/10/right-clustering-algorithm.html)

[This helpful article](https://www.freecodecamp.org/news/8-clustering-algorithms-in-machine-learning-that-all-data-scientists-should-know/) walks you through the different ways that various clustering algorithms behave, given different data shapes.

## Assignment

[Research other visualizations for clustering](assignment.md)