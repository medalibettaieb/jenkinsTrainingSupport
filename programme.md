# Programme de Formation – Jenkins (3 jours)
## GFP Tech – Présentiel

---

# 1 — Pipelines : mise en place
- Présentation de l’approche, bénéfices et cas d’usage  
- Groovy et DSL  
- Les syntaxes : déclarative ou de script  
- Le fichier Jenkinsfile : pipeline-as-code  
- Sections et étapes d’un pipeline  
- Créer et exécuter un pipeline déclaratif  
- Visualisation des logs  
- Modifier et rejouer un pipeline  
- Gestion des chaînes de caractères (strings)  

**Travaux pratiques :**  
- Création de pipelines  
- Utilisation de la syntaxe déclarative  
- Modification de pipelines  

---

# 2 — Pipelines : configuration avancée
- Présentation des plugins Jenkins  
- Les propriétés globales (interface de Jenkins)  
- Les paramètres  
- Les variables d'environnement  
- Les artefacts  
- Les empreintes  
- Les identifiants (secrets / credentials)  
- Relation entre les jobs  
- Gérer les erreurs (post actions...)  
- Paralléliser des tâches  
- Pipeline multi configurés (matrix)  
- Utiliser des images Docker comme environnement d’exécution pour un pipeline  
- Introduction aux librairies partagées  

**Travaux pratiques :**  
- Mise en place de tâches parallèles  
- Exécution avec Docker  
- Gestion des erreurs  

---

# 4 — Gestion de branches avec GitLab  
- Comprendre les stratégies de gestion de branches adaptées aux pipelines Jenkins  
- Configurer Jenkins pour s’intégrer avec GitLab  
  - Webhooks  
  - Tokens  
  - Multibranch pipelines  
- Mettre en œuvre des pipelines différenciés selon le type de branche : feature, release, hotfix  
- Automatiser les déploiements et les validations selon le type de branche  

**Travaux pratiques :**  
- Pipeline multibranches  
- Simulation de création de branches et merge requests  

---

# 5 — Automatisation des tests
- Introduction, terminologie du test  
- Automatisation des tests unitaires et d'intégration  
- Configuration des rapports  
- Mesurer la couverture de test  
- Automatisation des tests d’acceptance  
- Automatisation des tests de performance avec JMeter  
- Optimiser les temps d'exécution des tests  

**Travaux pratiques :**  
- Intégration JUnit  
- Suivi des tests de performance avec JMeter  

---

# 6 — Automatisation du déploiement
- Mise en place du script de déploiement  
- Mise à jour des bases de données  
- Tests minimaux  
- Retour en arrière (rollback)  

**Travaux pratiques :**  
- Automatisation du déploiement de l'artefact construit  

---

# 3 — Mutualisation des pipelines
- Les librairies de pipeline partagées  
- Structure des librairies  
- Tests unitaires des librairies  

**Travaux pratiques :**  
- Création d’une bibliothèque de pipeline Groovy  
- Fonction réutilisable (ex : notification Slack)  

---

# 7 — Administration d’un serveur Jenkins
- Activation de la sécurité  
- Types de bases utilisateurs  
- Gestion des autorisations et des rôles  
- Journalisation des actions utilisateur  
- Gestion de l'espace disque  
- Monitoring de la charge CPU  
- Sauvegarde de la configuration  

---

# 8 — Installation d’agents dans le cluster Jenkins
- Échanges de clés SSH  
- Stratégie de répartition des outils entre les agents  
- Dimensionnement du cluster  
- Espace disque partagé entre les instances  

**Travaux pratiques :**  
- Configuration d’un agent Jenkins distant via SSH  

---

# 9 — Stratégie de sauvegarde
- Anatomie du répertoire $JENKINS_HOME  
- Choix de la stratégie de sauvegarde  
- Définition du plan de reprise d’activité (PRA)  

**Travaux pratiques :**  
- Configuration d’une tâche cron de sauvegarde régulière  
