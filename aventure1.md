~~~{"variant":"standard","title":"Étape 1 – Storytelling pour les participants","id":"71001"}
# Étape 1 – L’aventure classique : l’équipage de base

## Storytelling détaillé / présentation

Bienvenue dans notre startup GFP Tech !  
Vous êtes les fondateurs du projet et notre mission est de construire **notre première application Java** avec un pipeline CI/CD simple.  

### Contexte narratif
Au début, l’équipe est petite. Vous êtes tous dans un petit bureau, chacun ayant un rôle précis :  
- Développeur : écrit du code et des tests unitaires  
- DevOps : configure le pipeline Jenkins et le build Docker  
- Chef de projet : surveille l’avancement et valide les builds  

Vous allez apprendre à automatiser le processus de compilation et de test, puis à créer vos premiers artefacts.  
Pour rendre les choses intéressantes, vous disposez de **pouvoirs spéciaux** : les **paramètres et variables** du pipeline Jenkins.  

### Vos missions
1. **Compiler le projet Maven** et générer les artefacts (`.jar`/`.war`)  
2. **Exécuter les tests unitaires** pour garantir que le code fonctionne  
3. **Construire un container Docker** avec l’application  
4. **Activer vos pouvoirs spéciaux** pour contrôler le pipeline :  
   - Activer/désactiver les tests (`RUN_TESTS`)  
   - Activer/désactiver l’analyse SonarQube (`RUN_SONAR`)  
   - Activer/désactiver le build Docker (`RUN_DOCKER_BUILD`)  
   - Configurer les notifications Slack/Email (`NOTIFY`)  
   - Choisir l’environnement (`ENV`) : dev / staging / prod  

### Objectifs pédagogiques
- Découvrir la structure d’un pipeline Jenkins simple  
- Comprendre l’utilité des paramètres et variables  
- Exécuter un pipeline complet : code → build → Docker  
- Prendre confiance avant d’aborder les pipelines multibranch
~~~

markdown
Copy code
~~~{"variant":"standard","title":"Étape 1 – Pense-bête / Guide pour les participants","id":"71004"}
# Étape 1 – Pipeline classique : guide rapide pour les participants

Ce guide est à utiliser uniquement si vous êtes bloqués. Il contient **des étapes simples pour avancer sans tout révéler**.

---

## 1. Pipeline simple
- Branche : `main` ou `develop`  
- Stages principaux :  
  1. Checkout du code  
  2. Build Maven (`mvn clean package`)  
  3. Tests unitaires (JUnit)  
  4. Docker build

---

## 2. Paramètres / pouvoirs spéciaux
- `RUN_TESTS` → activer ou désactiver les tests  
- `RUN_SONAR` → activer ou désactiver l’analyse SonarQube  
- `RUN_DOCKER_BUILD` → activer ou désactiver le build Docker  
- `NOTIFY` → activer ou désactiver les notifications Slack/Email  
- `ENV` → choisir l’environnement : `dev`, `staging`, `prod`

💡 **Astuce** : changer la valeur d’un paramètre ne modifie pas le code, seulement le comportement du pipeline.

---

## 3. Artefacts et logs
- Artefacts Maven dans `target/`  
- Logs visibles dans Jenkins → vérifier compilation, tests, build Docker  
- SonarQube : si activé, analyser les résultats via l’interface web

---

## 4. Débogage rapide
- Maven échoue ? → vérifier dépendances et `pom.xml`  
- Tests KO ? → lire le log JUnit pour identifier la classe ou le test qui échoue  
- Docker build échoue ? → vérifier le Dockerfile et le tag image

---

## 5. Bonnes pratiques
- Exécuter le pipeline d’abord avec tous les paramètres activés  
- Modifier un paramètre à la fois pour comprendre l’effet  
- Observer les logs et artefacts à chaque étape  
- Posez des questions si vous ne comprenez pas, puis consultez ce guide
~~~

markdown
Copy code
~~~{"variant":"standard","title":"Étape 1 – Correction technique détaillée","id":"71003"}
# Étape 1 – Correction technique détaillée / Solution pipeline

## Exemple de Jenkinsfile pour l’étape 1

```groovy
pipeline {
    agent any

    parameters {
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Exécuter les tests unitaires')
        booleanParam(name: 'RUN_SONAR', defaultValue: false, description: 'Exécuter l’analyse SonarQube')
        booleanParam(name: 'RUN_DOCKER_BUILD', defaultValue: true, description: 'Construire l’image Docker')
        booleanParam(name: 'NOTIFY', defaultValue: true, description: 'Activer notifications Slack/Email')
        choice(name: 'ENV', choices: ['dev','staging','prod'], description: 'Choisir l’environnement')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://gitlab.com/votre-projet.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Tests') {
            when {
                expression { params.RUN_TESTS }
            }
            steps {
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('Analyse SonarQube') {
            when {
                expression { params.RUN_SONAR }
            }
            steps {
                sh 'mvn sonar:sonar'
            }
        }

        stage('Docker Build') {
            when {
                expression { params.RUN_DOCKER_BUILD }
            }
            steps {
                script {
                    def imageTag = "${params.ENV}-latest"
                    sh "docker build -t gfptech/app:${imageTag} ."
                }
            }
        }

        stage('Notifications') {
            when {
                expression { params.NOTIFY }
            }
            steps {
                echo "Notifier l'équipe pour le build terminé."
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé"
        }
    }
}
```

## Points de correction
- Tous les stages doivent être conditionnels selon les paramètres  
- Les artefacts Maven sont générés dans `target/` et visibles via Jenkins  
- Les logs doivent être clairs et faciles à interpréter  
- Le Dockerfile doit être simple mais fonctionnel pour construire l’image  
- L’activation/désactivation des tests et SonarQube fonctionne via les paramètres  

💡 Astuce : ce Jenkinsfile est prêt à évoluer vers multibranch pour l’étape suivante.
~~~
