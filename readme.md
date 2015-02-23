# Git Workflow Web / Bonnes pratiques
### 3 branches d'environnements :
1. Master (Développement)
2. Staging (Contrôle Qualité & Test)
3. Production

### Bonnes pratiques pour les branches Features et Bug
* Ne pas faire de commit d'un travail non finalisé dans la branche de travail par défaut (develop).
* Créer une branche chaque fois que l'on travaille sur une **feature** ou un **bugfix**.
* Quel que soit le niveau et le type de bug, une nouvelle branche sera créée afin de le corriger.
* Ne pas oublier d'effacer les branches **features** et **bugfixes** dès qu'elles ont été fusionné **(merge)** dans une branche stable. Votre repo(siroty) restera propre.

### Bénéfices d'utiliser des branches: Branches d'Environnement Serveur
Les branches d'environnement permettent de séparer le code sur lequel vous travaillez du code stable.
Utiliser des branches d'environnement et déployer à partir de ces branches signifie que nous savons quel code tourne sur les serveurs de chaque environnement.

### Le Workflow
Le déploiement fait entièrement partie du workflow de développement.
Le workflow intègre 3 environnements de développement: **Development**, **Staging** et **Production**.
* Les développeurs travaillent sur des bugs ou des features (fonctionnalités) dans des branches séparées. Les mises à jour vraiment mineures peuvent être committer directement dans la branche stable de développement (**master**).
* Une fois qu'une feature est créée, elle est fusionné (merge) avec la branche staging et déployé dans l'environnement Staging pour le Contrôle Qualité et Tests (quality assurance and test).
* Après avoir été testée, la feature est fusionnée dans la branche de développement (master).
* La branche de développement (master) est fusionnée avec la branche production qui est déployée dans l'environnement Production

### Development Environment (master)
Chaque développeur possède son propre environnement local et peut tester l'application web sur son ordinateur.

### Staging Environnement
Dès qu'une feature est implémentée et est considérée comme suffisament stable, une pull-request est envoyé. La prise en charge d'une **pull-request est de 48h maximum**. Après validation du pull-request la feature est fusionnée dans la branche staging qui est automatiquement déployée dans l'environnement Staging. C'est là qu'intervient le Contrôle Qualité: les testeurs vont sur les serveurs de test afin de vérifier que le code fonctionne comme prévu.

**Le déploiement dans l'environnement Staging est automatique à chaque validation de pull-request**

### Production Environment
Une fois que la feature est implémentée et testée, elle peut être déployée en production. La feature doit d'abord être fusionnée dans la branche stable de développment (master). La branche de la feature doit être ensuite effacée après le merge pour éviter toute confusion entre les membres de l'équipe.

L'étape suivante est de faire un diff entre les branches production development (master) afin de jeter un coup d'oeil rapide sur le code qui va être déployé en production. Ca donne une dernière chance de repérer quelque chose non finalisé ou non destiné à la production. Des choses comme des breakpoints du debugger, connexion en mode verbose ou des features incomplètes.

Une fois l'analyse diff finie, on peut merger la branche development dans la branche production et initialiser un déploiement de la branche production dans l'environnement Production. Il faut écrire un message pertinent pour le déploiement de sorte que l'équipe sache exactement ce qui a été déployé.

Il est recommandé de toujours déployer les releases majeures en production à une heure prévue (quand l'application web est le moins sollicité), que toute l'équipe connaitra. S'assurer qu'il ne soit pas trop tard, car quelqu'un soit être présent et disponible au moins pour quelques heures pour monitorer/surveiller l'application web et s'assurer que tout c'est bien déroulé. Les corrections urgentes de bugs sur la production peuvent être déployées à n'importe quel moment.

A la fin du déploiement il faut vérifier l'application web. Il vaut mieux tester toutes les features ou corrections de bugs qui ont été déployées pour s'assurer de leur bon fonctionnement. L'outil de déploiement peut envoyer à tous les membres de l'équipe un email indiquant les modifications après tous les déploiements.

![Stage 1. Developing a new feature.](http://guides.beanstalkapp.com/version-control/branching-best-practices/stage-1.png)
_Stage 1. Developing a new feature._
![Stage 2. Feature is completed and tested.](http://guides.beanstalkapp.com/version-control/branching-best-practices/stage-3.png)
_Stage 2. Feature is completed and tested._
![Stage 3. Feature is being released.](http://guides.beanstalkapp.com/version-control/branching-best-practices/stage-3.png)
_Stage 3. Feature is being released._

### Ne jamais fusionner dans une branche d'environnement staging ou production sans déployer
Afin de garder les branches d'environnement synchronisées avec les environnements, il vaut mieux effectuer un déploiement après un merge.