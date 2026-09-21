# Test d'hybridation en présence de génotypes multiploïdes

Un outil qui compare des génotypes « testés » à deux lignées parentales de référence et signale les hybrides probables — y compris lorsque certains locus portent 3 ou 4 allèles.

**→ [Ouvrir l'outil](https://nanoeditionsarcheus-web.github.io/flock-guichet/)**

---

## Ce que ça fait

On choisit **deux espèces parentales** de référence (parmi les cinq catostomidés). L'outil calcule, pour chaque génotype, sa **log-vraisemblance** sous chaque lignée, puis produit :

- **Deux graphes**, un par lignée de référence : les vraisemblances classées en ordre croissant, avec les deux courbes parentales en repères et le groupe testé par-dessus. Un hybride se place *entre* les deux parents dans les deux graphes.
- **Les portraits des groupes** : effectifs et composition de ploïdie locus par locus (combien de génotypes ont 2, 3 ou 4 allèles à chaque locus).
- **Un bilan des hybrides probables**, selon deux critères (voir plus bas).
- **L'heure d'exécution**, pour toujours savoir qu'on regarde la dernière version.

Un curseur règle le **nombre d'itérations** : à chaque itération, un locus à 3 ou 4 allèles est réduit à 2 allèles tirés au hasard, ce qui donne une courbe par itération et rend visible l'incertitude allélique.

## La méthode

Vraisemblance multilocus **« à la Paetkau » (1995)** — probabilité de génotype sous Hardy-Weinberg — avec **procédure leave-one-out** et un plancher de **1/(2N+1)** pour les allèles absents d'une lignée, en **log base 10**. Cette méthode reproduit les **classifications** de FLOCK (vérifié sur un jeu de validation : 14 génotypes sur 14 classés à l'identique). Les magnitudes exactes ne cherchent pas à copier FLOCK au centième — c'est la classification, et la position relative des testés entre les deux parents, qui portent le signal d'hybridation.

## Les deux critères du bilan

- **Critère strict** : la moyenne des vraisemblances du testé (sur les itérations) est supérieure au **maximum** de l'autre lignée et inférieure au **minimum** de la lignée de référence — la zone franche entre les deux nuages.
- **Critère relâché (moyennes)** : la moyenne du testé se situe entre la **moyenne** de chaque lignée parentale — plus robuste lorsque les nuages se chevauchent.

Les génotypes signalés sous les **deux** références sont les candidats hybrides les plus solides.

## À garder en tête pour l'interprétation

- Le critère strict, fondé sur min/max, se referme facilement dès qu'une lignée de référence est grande et hétérogène (quelques individus atypiques suffisent à écraser le minimum).
- Les tailles des échantillons de référence influencent l'échelle des vraisemblances : une lignée riche en allèles produit des vraisemblances plus basses. Comparer des références de tailles très différentes n'est pas tout à fait à armes égales.

## Vos données restent chez vous

Tout le calcul se fait dans le navigateur. Aucune donnée n'est envoyée nulle part ; la page fonctionne hors ligne, sur Mac comme sur PC.

## Origine

Méthode et démarche de **Pierre Duchesne**, auteur de FLOCK (Duchesne & Turgeon 2009, 2012) et de la procédure de test proposée ici. Conçu pour les travaux de **Nathalie Tessier** sur l'assignation d'espèce et l'hybridation chez les chevaliers.

## Écriture

Cet outil a été écrit par **Claude** (Anthropic), dans le cadre d'un échange avec Éleine Leblanc.
