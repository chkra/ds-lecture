


## Word Embeddings  - eine erste Intuition

*Natural Language Processing* (NLP) ist ein sehr breites Anwendungsfeld, das sich mit der Verarbreitung natürlicher Sprache beschäftigt. Eine weit verbreitete Grundlage vieler NLP-Ansätze ist die Abbildung eines Wortes/ Tokens/ Symbols $w \in V$ auf eine Zahl bzw. einen Vektor $v \in \R^n$. Dafür gibt es [viele verschiedene Ansätze](https://de.wikipedia.org/wiki/Worteinbettung). Die denkbar einfachste Methode ist es, alle bekannten Wörter im Vokabular $V$ einfach durchzunummerieren: $f: V \rightarrow \N$. Aufgrund der großen Komplexität natürlicher Sprache wird dieser Ansatz aber kaum gewählt.

Einer der berühmtesten  Ansätze ist die **word2vec** Methode[^1], eine Form des **Word Embeddings** $f: V \rightarrow \R^n$. Diese zeichnet sich insbesondere dadurch aus, dass Abstände im Ziel-Vektorraum semantische Bedeutung haben, so dass abstrakte Berechnungen wie 
$v$(Arzt) + $v$(Frau) = $v$(Ärztin) möglich sind:

![](./images/word2vec1.png)
*Semantische Äquivalenz bei word2vec: gleiche Konzepte haben gleiche Distanzen*

![](./images/word2vec2.png)
*Semantische Äquivalenz bei word2vec: gleiche Tempora haben gleiche Distanzen*

Wie kann man aber einen Satz (ein Wort, einen Absatz, ein Dokument) in einen Vektor umwandeln? D 
