# Formation Dynatrace - Utilisateur Debutant

**OneAgent | Kubernetes | Cloud | Dashboards**  
**Duree totale : 3 heures | Niveau : Debutant | Format : Distanciel**  
**Version : 6 mai 2026**

Ce document accompagne la formation Dynatrace et a pour objectif de vous faire monter en competence sur les fonctionnalites essentielles de la plateforme.  
Il contient le support de cours, les exercices pratiques et les fiches de reference rapide.

---

## Programme de la formation

Cette formation de 3 heures est structuree en 6 modules progressifs.  
Chaque module alterne theorie courte et pratique guidee.

| Module | Horaire |
|---|---|
| Module 1 - Accueil & Introduction | 0h00 - 0h25 (25 min) |
| Module 2 - Naviguer dans Dynatrace | 0h25 - 1h15 (50 min) |
| Module 3 - Pause | 1h15 - 1h30 (15 min) |
| Module 4 - Logs, Metriques & Alertes | 1h30 - 2h15 (45 min) |
| Module 5 - Creer un Dashboard | 2h15 - 2h50 (35 min) |
| Module 6 - Bilan & Questions | 2h50 - 3h00 (10 min) |

## Objectifs pedagogiques

A l'issue de cette formation, le stagiaire sera capable de :
- naviguer dans l'interface Dynatrace
- consulter les logs et metriques de son environnement
- comprendre les alertes generees par Davis AI
- creer un dashboard de supervision personnalise

## Prerequis

- Avoir un compte Dynatrace actif (tenant fourni par le formateur)
- Acces a un navigateur web moderne (Chrome, Firefox, Edge)
- Aucune connaissance prealable de Dynatrace n'est requise
- Une connaissance de base des concepts d'application web et de serveur est un plus

---

## Module 1 - Accueil & Introduction a Dynatrace (25 min)

### 1.1 Qu'est-ce que Dynatrace ?

Imaginez que votre application est une voiture. Dynatrace, c'est le tableau de bord complet : vitesse, temperature moteur, niveau d'huile, GPS... tout en un seul regard, en temps reel.

En termes techniques, Dynatrace est une plateforme d'observabilite. Elle surveille automatiquement :
- vos applications et services
- l'infrastructure (serveurs, conteneurs, cloud)
- les transactions de vos utilisateurs de bout en bout
- les logs, metriques et traces, unifies dans une seule interface

### Davis AI - l'intelligence artificielle de Dynatrace

Davis est le moteur IA integre. Il analyse en permanence toutes les donnees et vous alerte automatiquement en cas d'anomalie.  
Il identifie aussi la cause racine du probleme - pas juste les symptomes.

### 1.2 Pourquoi utiliser Dynatrace ?

| Sans Dynatrace | Avec Dynatrace |
|---|---|
| Decouverte des incidents par les utilisateurs | Detection automatique avant l'impact utilisateur |
| Analyse manuelle dans plusieurs outils | Tout centralise dans une interface unique |
| Difficile d'identifier la cause racine | Davis AI identifie la cause en quelques secondes |
| Dashboards crees a la main | Topologie et relations detectees automatiquement |

### 1.3 Les quatre types de donnees

| Type de donnee | Ce que c'est en pratique |
|---|---|
| Metriques | Valeurs numeriques dans le temps - CPU a 85%, latence a 240ms |
| Logs | Messages texte horodates - erreurs, evenements, debogage |
| Traces | Chemin complet d'une requete a travers les services |
| Topologie | Carte des relations entre tous vos services et hotes |

### EXERCICE 1 - Se connecter et explorer l'interface

Prenez 5 minutes pour vous connecter et reperer les grandes zones de l'interface.

1. Ouvrir votre navigateur et aller sur l'URL de votre tenant Dynatrace (fournie par le formateur)
2. Se connecter avec vos identifiants
3. Reperer le menu lateral gauche : Infrastructure, Applications, Logs, Dashboards
4. Cliquer sur Infrastructure -> Hosts et observer la liste des hotes
5. Cliquer sur un hote au hasard et observer les metriques affichees

Ne cherchez pas a tout comprendre maintenant : l'objectif est de se reperer dans l'espace.

---

## Module 2 - Naviguer dans Dynatrace (50 min)

### 2.1 Le menu principal

Le menu lateral gauche est votre point d'entree vers toutes les fonctionnalites. Il est organise par domaine :

| Section | Ce qu'on y trouve |
|---|---|
| Infrastructure | Hotes, conteneurs, reseau, processus |
| Applications | Services, applications web, monitoring utilisateurs |
| Kubernetes | Clusters, namespaces, workloads, pods |
| Logs | Recherche et analyse des logs en temps reel |
| Dashboards | Tableaux de bord personnalises |
| Alertes (Problems) | Incidents detectes par Davis AI |
| Settings | Configuration de l'environnement |

### 2.2 OneAgent - composant essentiel Dynatrace

OneAgent est l'agent de collecte principal de Dynatrace.  
Il s'installe sur les hotes (VM, bare metal, conteneurs) et detecte automatiquement :

- les processus et services
- les applications et dependances
- les metriques systeme (CPU, memoire, disque, reseau)
- les traces distribuees
- les logs (selon la configuration)

Pourquoi c'est essentiel :
- Sans OneAgent, Dynatrace a une visibilite partielle de votre environnement.
- Avec OneAgent, la topologie, le service flow et l'analyse Davis AI sont beaucoup plus precis.
- Il reduit les configurations manuelles grace a l'auto-discovery.

Verification rapide de la sante OneAgent :
1. Aller dans `Infrastructure -> Hosts`
2. Ouvrir un hote
3. Verifier le statut de monitoring et la remontee des metriques
4. Controler que des services sont detectes dans `Applications -> Services`

### 2.3 La vue Infrastructure - Hotes

1. Aller dans Infrastructure -> Hosts
2. Observer la liste des hotes avec leur etat (vert = OK, orange/rouge = probleme)
3. Cliquer sur un hote pour acceder a sa fiche detaillee
4. Explorer les onglets : Overview, Processes, Logs, Network, Events

Lecture des metriques hote : sur la fiche d'un hote, les graphiques CPU et memoire montrent l'evolution dans le temps. Le selecteur de periode en haut a droite (2h, 6h, 1d, 1w) ajuste la fenetre temporelle affichee.

### 2.4 La vue Services

Les services representent vos applications (APIs, microservices, bases de donnees). Dynatrace les detecte automatiquement via OneAgent.

5. Aller dans Applications -> Services
6. Observer les colonnes : nom du service, requetes/min, taux d'erreur, temps de reponse
7. Cliquer sur un service pour voir sa fiche detaillee
8. Explorer l'onglet Service flow (chemin des requetes entre services)

### 2.5 La Smartscape - carte de topologie

- Accessible depuis le menu : Infrastructure -> Smartscape
- Zoomer et deplacer la carte avec la souris
- Cliquer sur une entite pour voir ses connexions
- Utile pour comprendre l'impact d'une panne sur les autres services

### EXERCICE 2 - Explorer un service et sa topologie

1. Aller dans Applications -> Services
2. Cliquer sur le service avec le plus de requetes (colonne Requests/min)
3. Noter le temps de reponse moyen et le taux d'erreur affiche
4. Cliquer sur l'onglet `Service flow` et observer les services appeles
5. Revenir a la fiche principale, cliquer sur `...` -> `View in Smartscape`
6. Observer les connexions entrantes et sortantes du service

Le Service flow vous permet de voir en un coup d'oeil quels autres services sont impactes si celui-ci tombe.

### 2.6 La vue Problems - alertes Davis AI

La vue Problems liste tous les incidents detectes automatiquement par Davis AI. C'est votre centre de commandement en cas d'incident.

| Statut / Element | Signification |
|---|---|
| Open | Incident en cours - necessite une action |
| Resolved | Incident resolu automatiquement ou manuellement |
| Root cause | Cause racine identifiee par Davis AI |
| Affected entities | Liste des services/hotes impactes par l'incident |

Comment lire un Problem : chaque Problem contient (1) le titre de l'anomalie, (2) les entites affectees, (3) la cause racine identifiee par Davis, (4) la timeline de l'incident.

### EXERCICE 3 - Analyser un Problem (si disponible)

1. Aller dans Alerts -> Problems dans le menu gauche
2. Si un incident est visible, cliquer dessus pour l'ouvrir
3. Lire le titre et la description generee par Davis AI
4. Identifier les entites affectees (services, hotes)
5. Observer la timeline : quand a-t-il commence ? Quelle est la cause racine ?

S'il n'y a pas d'incident ouvert, consultez les incidents resolus (filtre `Status: Resolved`).

---

## Module 3 - Pause (15 min)

Retour a 1h30.

Avant de reprendre, faire un tour de table rapide : qu'est-ce qui etait le plus clair ? Le plus flou ?

---

## Module 4 - Logs, Metriques & Alertes (45 min)

### 4.1 Consulter les logs

9. Aller dans Logs dans le menu gauche
10. Observer le volume de logs dans le graphique temporel
11. Utiliser la barre de recherche pour filtrer par mot-cle : `ERROR`
12. Observer les logs filtres - noter le service et le message d'erreur
13. Cliquer sur un log pour voir son detail complet

Filtres essentiels :

| Filtre | Effet |
|---|---|
| `loglevel == "ERROR"` | Afficher uniquement les erreurs |
| `loglevel == "WARN"` | Afficher les avertissements |
| `service == "nom-du-service"` | Filtrer par service specifique |
| `contains(content, "timeout")` | Chercher un mot dans le contenu |

### 4.2 Introduction a DQL

DQL (Data Query Language) est le langage de requete de Dynatrace.  
Structure type d'une requete DQL :

```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count()
| sort timestamp desc
| limit 10
```

Mes 5 premieres requetes DQL :

**Requete 1 - Compter les erreurs**
```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count()
```

**Requete 2 - Voir les dernieres erreurs**
```dql
fetch logs
| filter loglevel == "ERROR"
| fields timestamp, service, content
| sort timestamp desc
| limit 20
```

**Requete 3 - Erreurs par service**
```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count(), by: {service}
| sort count() desc
```

**Requete 4 - Erreurs dans le temps**
```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count(), by: {bin(timestamp, 5m)}
| sort timestamp asc
```

**Requete 5 - Chercher un mot dans les logs**
```dql
fetch logs
| filter contains(content, "timeout")
| fields timestamp, service, content
| sort timestamp desc
| limit 30
```

### EXERCICE 4 - Mes premieres requetes DQL

1. Aller dans Logs -> cliquer sur `Open in Notebooks` (ou utiliser un tile DQL dans un dashboard)
2. Executer la requete 1
3. Executer la requete 3 et identifier le service le plus problematique
4. Executer la requete 4 et passer la visualisation en `Line chart`
5. Modifier la requete 5 : remplacer `timeout` par un mot de votre choix

L'editeur DQL propose de l'autocompletion (`Ctrl+Espace`).

### 4.3 Metriques & alertes

Consulter les metriques d'un hote :

14. Aller dans Infrastructure -> Hosts
15. Cliquer sur un hote
16. Observer les graphiques CPU Usage et Memory Usage
17. Passer la souris sur les graphiques pour voir les valeurs exactes
18. Cliquer sur `Pin to dashboard` pour ajouter un graphique a un dashboard

Configurer un seuil d'alerte :

19. Aller dans Settings -> Anomaly detection -> Infrastructure
20. Choisir le type de metrique (ex : CPU usage)
21. Definir un seuil (ex : alerter si CPU > 80% pendant 5 minutes)
22. Cliquer sur `Save`

Bonne pratique : commencer avec des seuils larges (ex : CPU > 90%) puis affiner.

---

## Module 5 - Creer son premier Dashboard (35 min)

### 5.1 Pourquoi creer un dashboard ?

| Type | Objectif |
|---|---|
| Dashboard operationnel | Vue temps reel pour l'equipe de supervision |
| Dashboard developpeur | Taux d'erreur et performance de ses propres services |
| Dashboard management | KPIs business : disponibilite, SLA, incidents du mois |

### 5.2 Creer un dashboard etape par etape

**Etape 1 - Creer le dashboard**
23. Aller dans Dashboards
24. Cliquer sur `+ New dashboard`
25. Nommer : `Mon dashboard de supervision`
26. Cliquer sur `Create`

**Etape 2 - Ajouter un tile Single Value (KPI)**
27. Cliquer sur `Edit` puis `+ Add tile`
28. Choisir le type DQL
29. Coller :

```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count()
```

30. Dans Visualization, choisir `Single value`
31. Nommer le tile : `Erreurs (30 dernieres minutes)`
32. Cliquer sur `Save tile`

**Etape 3 - Ajouter un graphique d'evolution**
33. `+ Add tile` -> DQL
34. Coller :

```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count(), by: {bin(timestamp, 5m)}
| sort timestamp asc
```

35. Choisir `Line chart`
36. Nommer : `Evolution des erreurs`
37. Sauvegarder

**Etape 4 - Ajouter un tableau Top Services**
38. Ajouter un nouveau tile DQL :

```dql
fetch logs
| filter loglevel == "ERROR"
| summarize erreurs = count(), by: {service}
| sort erreurs desc
| limit 5
```

39. Choisir `Table`
40. Nommer : `Top 5 services en erreur`

### 5.3 Rendre le dashboard dynamique

Creer une variable `$service` :

41. Mode Edit -> Variables -> `+ Add variable`
42. Nom : `service` | Type : `Query`
43. Coller :

```dql
fetch logs
| summarize by: {service}
| fields service
| sort service
```

44. Activer `Allow all values` (option `All`)
45. Cliquer sur `Save`

Utiliser la variable dans les tiles :

```dql
fetch logs
| filter service == "{{$service}}"
| filter loglevel == "ERROR"
| summarize count()
```

Resultat attendu : un menu deroulant apparait en haut du dashboard et filtre tous les tiles qui utilisent `{{$service}}`.

### EXERCICE 5 - Assembler le dashboard complet

1. Creer un nouveau dashboard nomme `Supervision [votre prenom]`
2. Ajouter le tile Single Value : nombre d'erreurs totales
3. Ajouter le tile Line chart : evolution des erreurs
4. Ajouter le tile Table : top 5 services en erreur
5. Creer la variable `$service` et l'integrer dans les 3 requetes
6. Tester : changer la variable et verifier la mise a jour des tiles
7. Sauvegarder et partager le lien

Bonus : ajouter une variable `$env` pour filtrer par environnement (production, staging, dev).

---

## Module 6 - Bilan & Questions (10 min)

### 6.1 Ce que vous avez appris aujourd'hui

| Competence | Acquis |
|---|---|
| Interface Dynatrace | Navigation dans Infrastructure, Services, Logs, Dashboards |
| OneAgent | Role de l'agent de collecte installe sur les serveurs |
| Problems & Davis AI | Lire et interpreter les incidents detectes automatiquement |
| Logs & DQL | Rechercher, filtrer et requeter les logs |
| Metriques | Consulter CPU, memoire, temps de reponse |
| Dashboards | Creer, organiser et rendre interactif un dashboard |

### 6.2 Quiz de validation

46. Qu'est-ce que Davis AI et a quoi sert-il ?  
47. Comment afficher uniquement les logs en erreur dans la vue Logs ?  
48. Quelle commande DQL permet de compter les erreurs par service ?  
49. Comment creer une variable de dashboard et l'utiliser dans une requete ?  
50. Quelle est la difference entre un Problem et une alerte de seuil ?

Reponses courtes :
1. Davis AI detecte les anomalies et la cause racine automatiquement.
2. Utiliser `loglevel == "ERROR"`.
3. `summarize count(), by: {service}`.
4. Variables -> Query DQL -> utiliser `{{$nom}}` dans la requete.
5. Un Problem est detecte automatiquement par IA ; une alerte de seuil est basee sur une valeur fixe configuree.

### 6.3 Pour aller plus loin

- Dynatrace University : [https://university.dynatrace.com](https://university.dynatrace.com)
- Documentation officielle : [https://docs.dynatrace.com](https://docs.dynatrace.com)
- Dynatrace Community : [https://community.dynatrace.com](https://community.dynatrace.com)
- Certification Dynatrace Associate

---

## Fiche de reference rapide

### Navigation rapide

| Objectif | Ou aller |
|---|---|
| Hotes & serveurs | Infrastructure -> Hosts |
| Services & APIs | Applications -> Services |
| Kubernetes | Infrastructure -> Kubernetes |
| Logs | Logs |
| Incidents & alertes | Alerts -> Problems |
| Dashboards | Dashboards |
| Topologie | Infrastructure -> Smartscape |
| Metriques custom | Metrics |

### Les 5 requetes DQL a retenir

**1 - Logs en erreur**
```dql
fetch logs
| filter loglevel == "ERROR"
| fields timestamp, service, content
| sort timestamp desc
| limit 20
```

**2 - Erreurs par service**
```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count(), by: {service}
| sort count() desc
```

**3 - Evolution dans le temps**
```dql
fetch logs
| filter loglevel == "ERROR"
| summarize count(), by: {bin(timestamp, 5m)}
| sort timestamp asc
```

**4 - Recherche par mot-cle**
```dql
fetch logs
| filter contains(content, "MOT_CLE")
| fields timestamp, service, content
| limit 30
```

**5 - Dashboard avec variable**
```dql
fetch logs
| filter service == "{{$service}}"
| filter loglevel == "ERROR"
| summarize count()
```

### Syntaxe DQL essentielle

| Commande DQL | Ce que ca fait |
|---|---|
| `fetch logs` | Source des donnees : logs |
| `fetch metrics` | Source des donnees : metriques |
| `\| filter X == "valeur"` | Filtrer sur une valeur exacte |
| `\| filter contains(X, "mot")` | Filtrer si un champ contient un mot |
| `\| summarize count()` | Compter le nombre de resultats |
| `\| summarize avg(value)` | Calculer une moyenne |
| `\| summarize count(), by: {col}` | Compter par groupe |
| `\| sort col desc` | Trier par colonne decroissante |
| `\| limit 10` | Limiter a 10 resultats |
| `\| fields col1, col2` | Selectionner des colonnes |

### Variables de dashboard

| Variable | Usage dans la requete DQL |
|---|---|
| `{{$service}}` | Filtre par service selectionne |
| `{{$env}}` | Filtre par environnement |
| `{{$interval}}` | Intervalle de groupement temporel |

---

## Atelier Kubernetes + Dynatrace (creation de pods)

Cette section permet de creer rapidement des pods Kubernetes visibles dans Dynatrace.

### Prerequis

- Un cluster Kubernetes accessible (`kubectl` configure)
- Dynatrace Operator installe sur le cluster
- Injection OneAgent active via admission controller

### Installation rapide de l'environnement local (WSL Ubuntu)

Si vous n'avez pas encore `kubectl` et `minikube`, utilisez ces commandes :

```bash
sudo apt update
sudo apt install -y curl ca-certificates apt-transport-https gpg docker.io
sudo usermod -aG docker $USER
newgrp docker
```

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt update
sudo apt install -y kubectl
kubectl version --client
```

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
minikube start --driver=docker
kubectl get nodes
```

Activer l'ingress NGINX :

```bash
minikube addons enable ingress
kubectl get pods -n ingress-nginx
```

### Fichiers manifests

- `k8s/namespace.yaml`
- `k8s/deployment.yaml`
- `k8s/service.yaml`
- `k8s/ingress.yaml`

Le `Deployment` cree 2 pods `nginx` avec les annotations Dynatrace :
- `oneagent.dynatrace.com/inject: "true"`
- `metadata-enrichment.dynatrace.com/inject: "true"`

### Deployer les pods

```bash
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/ingress.yaml
```

### Verifier le deploiement

```bash
kubectl get pods -n dynatrace-demo
kubectl get svc -n dynatrace-demo
kubectl get ingress -n dynatrace-demo
kubectl describe pod -n dynatrace-demo -l app=web-demo
```

### Tester depuis un navigateur

Si vous utilisez un ingress controller NGINX local (ex: minikube/kind), ajoutez une entree hosts :

```text
127.0.0.1 web-demo.local
```

Puis testez :

```bash
curl -H "Host: web-demo.local" http://$(minikube ip)/
```

Ou ouvrez directement `http://web-demo.local` dans votre navigateur (selon votre configuration ingress).

### Verification dans Dynatrace

1. Aller dans `Kubernetes` puis selectionner le cluster
2. Ouvrir le namespace `dynatrace-demo`
3. Verifier la presence du workload `web-demo`
4. Confirmer la remontee des metriques/traces/logs selon votre configuration
# Dynatrace Formation 

