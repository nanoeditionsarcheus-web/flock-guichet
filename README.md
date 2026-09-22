# Test d'hybridation en présence de génotypes multiploïdes

Un outil qui compare des génotypes « testés » à deux lignées parentales de référence et signale les hybrides probables — y compris lorsque certains locus portent 3 ou 4 allèles.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/flock-guichet/)**

---

## Ce que ça fait

On choisit **deux espèces parentales** de référence (parmi les cinq catostomidés). L'outil calcule, pour chaque génotype, sa **log-vraisemblance** sous chaque lignée, puis mène l'analyse en **deux étapes** :

**Étape 1 — Y a-t-il un signal d'hybridation ?**
Deux graphes, un par lignée de référence, classent les vraisemblances en ordre croissant, avec les deux courbes parentales en repères et le groupe testé par-dessus. L'outil indique automatiquement si le nuage des testés se place *entre* les deux lignées (signal d'hybridation possible) ou s'il *suit* une lignée parentale (pas de signal — le groupe ressemble simplement à cette espèce). **Si aucun signal n'apparaît, le pointage des candidats n'est pas pertinent et l'analyse devrait s'arrêter là.**

**Étape 2 — Pointage des candidats-hybrides.**
Lorsque l'étape 1 montre un signal, l'outil signale les testés dont la vraisemblance moyenne tombe entre les deux lignées (voir le critère plus bas).

À cela s'ajoutent :

- **Les portraits des groupes** : effectifs et composition de ploïdie locus par locus (combien de génotypes ont 2, 3 ou 4 allèles à chaque locus).
- **L'heure d'exécution**, pour toujours savoir qu'on regarde la dernière version.

Un curseur règle le **nombre d'itérations** : à chaque itération, un locus à 3 ou 4 allèles est réduit à 2 allèles tirés au hasard, ce qui donne une courbe par itération et rend visible l'incertitude allélique.

## La méthode

Vraisemblance multilocus **« à la Paetkau » (1995)** — probabilité de génotype sous Hardy-Weinberg — avec **procédure leave-one-out** et un plancher de **1/(2N+1)** pour les allèles absents d'une lignée, en **log base 10**. Cette méthode reproduit les **classifications** de FLOCK (vérifié sur un jeu de validation : 14 génotypes sur 14 classés à l'identique). Les magnitudes exactes ne cherchent pas à copier FLOCK au centième — c'est la classification, et la position relative des testés entre les deux parents, qui portent le signal d'hybridation.

## Le critère de pointage : un paramètre de stringence par centiles

Un testé est retenu comme candidat si la **moyenne** de ses vraisemblances (sur les itérations) tombe au-dessus du centile *(100 − P)* de l'autre lignée et sous le centile *P* de la lignée de référence — la zone franche entre les deux nuages.

Le **centile P** est un curseur de stringence :

- **P = 0** : min/max, le plus strict, mais sensible aux génotypes singuliers (outliers) des groupes parentaux.
- **Monter P** élargit l'intervalle et retient davantage de candidats. Une **hausse brutale** du nombre de candidats à un certain niveau trahit l'effet de quelques outliers parentaux.
- **Valeur suggérée : 5** (neutralise les 5 % extrêmes de chaque lignée).

Les génotypes signalés sous les **deux** références sont les candidats hybrides les plus solides.

*(Note : une version antérieure proposait aussi un « critère relâché » fondé sur les moyennes. Il s'est révélé trop permissif — trop de faux positifs — et a été retiré.)*

## À garder en tête pour l'interprétation

- Le pointage des candidats n'a de sens qu'après un signal d'hybridation à l'étape 1. Sans signal, les candidats sont vraisemblablement des faux positifs.
- Les tailles des échantillons de référence influencent l'échelle des vraisemblances : une lignée riche en allèles produit des vraisemblances plus basses. Comparer des références de tailles très différentes n'est pas tout à fait à armes égales.

## Vos données restent chez vous

Tout le calcul se fait dans le navigateur. Aucune donnée n'est envoyée nulle part ; la page fonctionne hors ligne, sur Mac comme sur PC.

## Origine

Méthode et démarche de **Pierre Duchesne**, auteur de FLOCK (Duchesne & Turgeon 2009, 2012) et de la procédure de test proposée ici. Conçu pour les travaux de **Nathalie Tessier** sur l'assignation d'espèce et l'hybridation chez les chevaliers.

## Écriture

Cet outil a été écrit par **Claude** (Anthropic), dans le cadre d'un échange avec Éleine Leblanc.
