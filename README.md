# Test d'hybridation en présence de génotypes multiploïdes

Un outil qui compare des génotypes « testés » à deux lignées parentales de référence et signale les hybrides probables — y compris lorsque certains locus portent 3 ou 4 allèles.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/flock-guichet/)**

---

## Ce que ça fait

On choisit **deux espèces parentales** de référence. L'outil calcule, pour chaque génotype, sa **log-vraisemblance** sous chaque lignée, puis mène l'analyse en **deux étapes** :

**Étape 1 — Y a-t-il un signal d'hybridation ?**
Deux graphes, un par lignée de référence, classent les vraisemblances en ordre croissant, avec les deux courbes parentales en repères et le groupe testé par-dessus. C'est à l'usagère de juger visuellement les courbes : la page lui demande si elles montrent la présence probable d'hybrides. **Oui** affiche l'étape 2 ; **Non** arrête l'analyse, car le pointage des candidats ne serait pas pertinent et pourrait produire des faux positifs. La réponse peut être changée à tout moment.

**Étape 2 — Pointage des candidats-hybrides.**
Lorsque l'usagère a répondu Oui à l'étape 1, l'outil signale les testés dont la vraisemblance moyenne tombe entre les deux lignées (voir le critère plus bas).

À cela s'ajoutent les **portraits des groupes** (effectifs et composition de ploïdie locus par locus) et l'**heure d'exécution**. Un curseur règle le **nombre d'itérations** : à chaque itération, un locus à 3-4 allèles est réduit à 2 allèles tirés au hasard, ce qui donne une courbe par itération et rend visible l'incertitude allélique.

## Charger ses propres données

Par défaut, l'outil est livré avec un **jeu de test embarqué** et fonctionne dès l'ouverture. Pour analyser vos propres données, utilisez la carte **« Données »** en haut :

- **Références** : une matrice par espèce (disposition FLOCK — identifiant, puis deux colonnes par locus, une par allèle). Le nom du fichier (sans extension) devient le nom de l'espèce.
- **Testés** : le fichier des génotypes à tester, même disposition. Les lignes développées (`1987_A, 1987_B…`) sont **regroupées automatiquement** en un seul individu multi-allèle.
- Formats acceptés : `.xls`, `.xlsx`, `.csv`. Tous les fichiers doivent partager le **même panel de locus**.

Le bouton « Rétablir le jeu de test 2026 » revient aux données embarquées. Tout se fait dans le navigateur : aucun fichier n'est téléversé sur un serveur.

## La méthode

Vraisemblance multilocus **« à la Paetkau » (1995)** — probabilité de génotype sous Hardy-Weinberg — avec **procédure leave-one-out** et un plancher de **1/(2N+1)** pour les allèles absents d'une lignée, en **log base 10**. Cette méthode reproduit les **classifications** de FLOCK (vérifié sur un jeu de validation : 14 génotypes sur 14 classés à l'identique). Les magnitudes exactes ne cherchent pas à copier FLOCK au centième — c'est la classification, et la position relative des testés entre les deux parents, qui portent le signal d'hybridation.

## Le critère de pointage : un paramètre de stringence par centiles

Un testé est retenu si la **moyenne** de ses vraisemblances (sur les itérations) tombe au-dessus du centile *(100 − P)* de l'autre lignée et sous le centile *P* de la lignée de référence — la zone franche entre les deux nuages.

Le **centile P** est un curseur de stringence : **P = 0** correspond au min/max (le plus strict, sensible aux génotypes singuliers) ; monter P élargit l'intervalle et retient davantage de candidats. Une **hausse brutale** du nombre de candidats à un certain niveau trahit l'effet d'outliers parentaux. Valeur suggérée : **5**. Dans les résultats, un identifiant en **gras** est retenu pour cette référence seulement ; en **gras vert**, il est retenu pour les deux références.

## À garder en tête pour l'interprétation

- Le pointage des candidats n'a de sens qu'après un signal d'hybridation à l'étape 1. Sans signal, les candidats sont vraisemblablement des faux positifs.
- Les tailles des échantillons de référence influencent l'échelle des vraisemblances. Pour vérifier la robustesse à ce chapitre, trois sous-échantillons aléatoires fixes de 50 génotypes MOHU (MOHU-REC1/2/3) sont fournis dans le jeu embarqué.

## Origine

Méthode et démarche de **Pierre Duchesne**, auteur de FLOCK (Duchesne & Turgeon 2009, 2012) et de la procédure de test proposée ici. Conçu pour les travaux de **Nathalie Tessier** sur l'assignation d'espèce et l'hybridation chez les chevaliers.

## Écriture

Cet outil a été écrit par **Claude** (Anthropic), dans le cadre d'un échange avec Éleine Leblanc.
