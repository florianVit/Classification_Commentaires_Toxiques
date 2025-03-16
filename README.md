# Classification de Commentaires
Florian VITOUX et Mathéo STEPHAN

## 1. Présentation du Projet

Dans le cadre de ce projet, l'objectif est de créer un modèle de classification de commentaires laissés par les utilisateurs sur une plateforme. Ces commentaires peuvent être variés et contenir des propos toxiques, injurieux, menaçant, etc...
La classification automatique des commentaires permet de prendre des mesures adéquates et d'identifier les contenus problématiques rapidement.

## 2. Objectifs

- Créer un modèle permettant de classifier des commentaires dans différentes catégories (par exemple : toxiques, non toxiques, etc.).
- Mettre en place un modèle basé sur du Random Forest et itérer vers une solution plus avancée avec BERT pour améliorer les performances.
- Développer un pipeline complet de traitement de texte et de classification de commentaires.

Ce README sert de mise en bouche pour avoir une idée des étapes suivies durant le projet. Les explications de code et de choix seront présent dans le rapport
## 3. Analyse de données
   Nous allons avant d'entrainer les modéles, analyser les données pour mieux comprendre celle-ci et donc mieux préparer les modéles :
   
***Répartition des Classes de Toxicité*** :
   - L'objectif ici est de comprendre comment les différentes catégories de toxicité sont réparties dans le jeu de données. Cela permet d'identifier si certaines classes sont plus fréquentes que d'autres, ce qui pourrait influencer la performance du modèle.

***Analyse du Pourcentage de Commentaires Non Toxiques*** :
   - Cette analyse consiste à calculer la proportion de commentaires jugés non toxiques. Cela donne un aperçu global de la quantité de contenu "propre" dans le jeu de données par rapport aux commentaires toxiques.

***Visualisation de Commentaires Exemples*** :
   - Il est important de visualiser des exemples de commentaires toxiques et non toxiques pour mieux comprendre le contenu textuel du jeu de données. Cela permet de mieux saisir la nature des commentaires et d'ajuster les prétraitements et le modèle en conséquence.

***Vérification des Données Manquantes*** :
   - Avant d'entraîner un modèle, il est essentiel de vérifier s'il y a des données manquantes (valeurs nulles). Cela garantit que le modèle recevra des données complètes, et permet de décider des actions à entreprendre en cas de données manquantes (par exemple, les supprimer ou les imputer).

***Analyse des Longueurs de Commentaires*** :
   - L'analyse des longueurs des commentaires permet de comprendre si la taille des commentaires varie considérablement et s'il existe des différences notables entre les commentaires toxiques et non toxiques. Cela peut également aider à choisir la manière dont les commentaires sont traités par le modèle.

***Nuage de Mots des Commentaires Toxiques*** :
   - Un nuage de mots est généré à partir des commentaires toxiques pour identifier les termes les plus fréquemment utilisés. Cette analyse textuelle permet de repérer des patterns récurrents et des mots clés associés à la toxicité.

## 4. Random Forest

1. **Choix du Modèle: Random Forest**  
   Pour commencer, nous avons choisit d'utiliser un modèle Random Forest. Ce choix a été motivé par sa simplicité, sa robustesse et son efficacité pour des problèmes de classification sur des données tabulaires comme celles-ci. Random Forest est particulièrement adapté pour gérer des données où les relations entre les variables ne sont pas linéaires.

3. **Entraînement du Modèle Random Forest**  
   Le modèle Random Forest a été entraîné sur une petite portion du jeu de données (0.10 puis 0.5 pour tester d'autres mots) pour observer la performance de base. L'utilisation de Random Forest permet d'obtenir rapidement une solution de référence avec relativement peu d'efforts.

----

   Malheuresement, malgré son efficacité, le Random Forest ne capturent pas bien le contexte sémantique ou la relation entre les mots dans une phrase. C'est pour cela que nous nous tournons pour cette deuxième partie vers le modèle BERT.
   Etant conçu pour comprendre le contexte des mots dans une phrase grâce à son architecture de type Transformer. Il est bidirectionnel, ce qui signifie qu'il prend en compte le contexte des mots à la fois avant et après un mot donné. Cela lui permet de saisir des relations complexes et des nuances dans le texte, ce qui est essentiel pour des tâches comme la classification de toxicité où le contexte fait souvent la différence entre un commentaire agressif et un commentaire neutre, ce qui en fait un choix parfait pour notre objectif.

----

## 5. BERT

### Choix du Modèle: BERT  
Après avoir testé Random Forest, nous avons décidé d'explorer **BERT** (Bidirectional Encoder Representations from Transformers), un modèle de traitement du langage naturel basé sur l'architecture Transformer.

### Entraînement du Modèle BERT  
Nous avons utilisé une version pré-entraînée de BERT, que nous avons fine-tuné sur notre jeu de données. Contrairement à Random Forest, l'entraînement de BERT nécessite des ressources plus importantes (notamment un GPU) et un temps d'entraînement plus long. Cependant, il permet d'obtenir des performances nettement supérieures en termes de compréhension du langage et de précision des prédictions.  

### Optimisation avec DistilBERT  
BERT étant un modèle lourd en calcul, nous avons également testé **DistilBERT**, une version optimisée et plus légère, qui conserve une grande partie des performances de BERT tout en réduisant le temps d'entraînement et l'utilisation des ressources. Cette approche nous permet d'obtenir un bon équilibre entre **précision** et **efficacité computationnelle**.  

Grâce à BERT et DistilBERT, notre modèle est capable de mieux comprendre le **sens global des commentaires**, améliorant ainsi la détection des propos toxiques de manière plus fiable et contextuelle.

Attention, suite à des problèmes avec collab (limite atteinte, nous n'avons pas pu l'entrainer longtemps mais nous avons eu de bon résultat avant d'atteindre cette limite)

