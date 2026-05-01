# 🚌 Analyse du transport public dans le Grand Tunis

Projet académique : M1 AI, Data, Agentics - Dauphine Tunis  
Cours : Analyse de données

**Toutes les analyses et interprétations sont rédigées en français**

## Contexte

Ce projet porte sur l'usage et la perception du transport public dans le Grand Tunis. **Les données ont été collectées directement** via un questionnaire Google Forms diffusé entre octobre et décembre 2025.

La base de données finale compte **77 répondants** et **38 variables** couvrant les habitudes de déplacement, les modes de transport utilisés, et les évaluations de qualité (confort, sécurité, ponctualité, coût, accessibilité...).

Les données ont été anonymisées avant publication : aucune information personnelle identifiante n'est présente dans le fichier `transport.csv`.

## Problématique

**Quels facteurs encouragent ou freinent l'utilisation du transport public dans le Grand Tunis, et comment les usagers en évaluent-ils la qualité ?**

## Questionnaire

### Informations générales
1. Quel est votre âge ?  
  \<18 / 18–35 / 35–60 / \>60  

2. Quel est votre sexe ?  
   Homme / Femme  

3. Dans quelle gouvernorat du Grand Tunis résidez-vous ?  
   Ariana / Ben Arous / Manouba / Tunis

4. Quelle est votre profession ?  
   Étudiant / Cadre / Profession libérale / Chômeur / Retraité  

5. Possédez-vous un véhicule personnel ?  
   Oui / Non  
 
### Habitudes de transport  
Echelle de Likert de 1 à 5

6. J’utilise les transports publics plusieurs fois par semaine.  
7. Je prends le transport public aux heures de pointe.  
8. Je me déplace régulièrement en transport public pour le travail ou les études.  
9. Mes déplacements en transport public suivent une routine hebdomadaire.
10. J’utilise fréquemment le métro, le bus ou le train pour mes déplacements.  
11. Je combine différents modes de transport pour mes trajets.  
12. Je privilégie le transport public plutôt que le taxi ou la voiture personnelle.  
13. Je planifie mes trajets à l’avance selon le mode de transport.
14. Les stations ou arrêts sont proches de chez moi.  
15. Les correspondances entre lignes sont faciles à effectuer.  
16. Les horaires des transports publics correspondent à mes besoins.  
17. Les transports publics desservent les zones que je fréquente.  
18. J’adapte mes trajets aux contraintes des transports publics.  

### Satisfaction et perception  
Echelle de Likert de 1 à 5

19. Les véhicules de transport public sont en bon état.  
20. Le confort à bord (sièges, climatisation, propreté) est satisfaisant.  
21. Les stations et arrêts sont propres et bien entretenus.  
22. Les transports publics sont ponctuels.
23. Je me sens en sécurité dans les transports publics.  
24. Les chauffeurs conduisent prudemment et respectent le code de la route.  
25. Le risque de vol ou d’agression est faible.  
26. Les pannes et incidents techniques sont rares.  
27. Je fais confiance à la fiabilité du service.
28. Le coût des transports publics est raisonnable.  
29. Je recommande l’utilisation du transport public à mes proches.  
30. Les transports publics sont accessibles aux personnes à mobilité réduite.  
31. Je suis globalement satisfait(e) du service offert.  

### Questions Oui / Non
32. Avez-vous un abonnement de transport (bus, métro, train) ?  
33. Avez-vous déjà été victime d’un vol ou de harcèlement dans les transports ?  
34. Avez-vous déjà dû renoncer à un déplacement faute de transport disponible ?  
35. Votre employeur/école propose-t-il des avantages liés au transport ?  
36. Avez-vous utilisé une application de transport (Bolt, InDrive, Wassalni, etc.) ?  
37. Transportez-vous souvent des passagers (famille, amis, colocataires) ?

## Pipeline d'analyse

| Étape | Description |
|-------|-------------|
| **Statistique descriptive** | Profil des répondants : âge, profession, possession d'un véhicule personnel |
| **Prétraitement** | Renommage des colonnes, conversion des variables qualitatives en facteurs |
| **ACP** | Analyse en Composantes Principales sur les variables d'évaluation (Likert) |
| **ACM** | Analyse des Correspondances Multiples sur les variables binaires (Oui/Non) |
| **HCPC** | Classification hiérarchique sur les coordonnées ACP : 4 clusters identifiés |

## Résultats clés

**ACP : Variables d'évaluation (13 variables de Likert) :**
- **Axe 1** (≈ 47% de variance) : Qualité perçue du transport : état des véhicules, propreté, ponctualité, satisfaction globale
- **Axe 2** (≈ 19% de variance) : Sécurité et risque perçus : sécurité, risque de vol, conduite prudente
- Les 2 premiers axes expliquent **~66%** de la variance totale

**ACM : Variables comportementales (7 variables Oui/Non) :**
- **Axe 1** : oppose les *utilisateurs réguliers du transport public* (abonnés, sans véhicule) aux *utilisateurs de véhicule personnel*
- **Axe 2** : reflète l'*accès aux avantages liés au transport* (avantages employeur, possession de véhicule)

**HCPC : 4 profils d'usagers identifiés :**

| Cluster | Profil |
|---------|--------|
| 1 | Insatisfaits : perçoivent des pannes fréquentes, mauvaise ponctualité |
| 2 | Neutres : perception modérée de la qualité et de la sécurité |
| 3 | Satisfaits : se sentent en sécurité, jugent le service ponctuel et en bon état |
| 4 | Mitigés : satisfaits de la qualité mais inquiets pour leur sécurité |

## 🛠️ Stack technique

- **Langage :** R
- **Analyse multivariée :** `FactoMineR`, `factoextra`
- **Visualisation :** `ggplot2`, `corrplot`
- **Manipulation des données :** `dplyr`, `readr`
