# AI Stock Analyst : Alternative privée et locale à Manus.

<p align="center">
<img align="center" src="./media/ai_stock_analyst_logo.png" width="300" height="300" alt="AI Stock Analyst Logo">
<p>

    [English](./README.md) | [中文](./README_CHS.md) | [繁體中文](./README_CHT.md) | Français | [日本語](./README_JP.md) | [Português (Brasil)](./README_PTBR.md)

*Une **alternative 100% locale à Manus AI**, cet assistant vocal autonome navigue sur le web, écrit du code et planifie des tâches tout en gardant toutes les données sur votre appareil. Conçu pour les modèles de raisonnement locaux, il fonctionne entièrement sur votre matériel, garantissant une confidentialité totale et aucune dépendance au cloud.*

[![Visiter AI Stock Analyst](https://img.shields.io/static/v1?label=Website&message=AI%20Stock%20Analyst&color=blue&style=flat-square)](#) ![Licence](https://img.shields.io/badge/license-GPL--3.0-green) [![GitHub stars](https://img.shields.io/github/stars/ServOps117/agenticSeek?style=social)](https://github.com/ServOps117/agenticSeek/stargazers)

### Pourquoi AI Stock Analyst ?

* 🔒 100% Local & Privé – Tout fonctionne sur votre machine : pas de cloud, pas de partage de données. Vos fichiers, conversations et recherches restent privés.

* 🌐 Navigation Web Intelligente – AI Stock Analyst peut naviguer sur Internet de façon autonome : recherche, lecture, extraction d'informations, remplissage de formulaires web — tout cela sans intervention.n.

* 💻 Assistant de Codage Autonome – Besoin de code ? Il peut écrire, déboguer et exécuter des programmes en Python, C, Go, Java, et plus — sans supervision.

* 🧠 Sélection Intelligente d’Agent – Vous demandez, il choisit automatiquement le meilleur agent pour la tâche. Comme une équipe d’experts à disposition.

* 📋 Planifie & Exécute des Tâches Complexes – De la planification de voyage à la gestion de projets complexes : il divise les grandes tâches en étapes et les réalise avec plusieurs agents IA.

* 🎙️ Contrôle Vocal – Voix et reconnaissance vocale rapides et futuristes, permettant de dialoguer comme avec une IA de film de science-fiction. (En développement)

### **Démo**

> *Peux-tu rechercher le projet AI Stock Analyst, découvrir les compétences requises, puis ouvrir le fichier CV_candidates.zip et me dire lesquels correspondent le mieux au projet ?*

https://github.com/user-attachments/assets/b8ca60e9-7b3b-4533-840e-08f9ac426316

Avertissement : Cette démo, y compris tous les fichiers affichés (ex : CV_candidates.zip), est entièrement fictive. Nous ne sommes pas une entreprise, nous recherchons des contributeurs open-source, pas des candidats.

> 🛠⚠️️ **Travail en cours**

> 🙏 Ce projet a commencé comme un projet annexe sans feuille de route ni financement. Il a dépassé toutes nos attentes en finissant dans GitHub Trending. Les contributions, retours et votre patience sont grandement appréciés.

## Prérequis

Assurez-vous d’avoir chrome driver, docker et python3.10 installés.

Pour les problèmes liés à chrome driver, voir la section **Chromedriver**.

### 1. **Cloner le dépôt et configurer**

```sh
git clone https://github.com/ServOps117/agenticSeek.git
cd agenticSeek
mv .env.example .env
```

### 2. Modifier le contenu du fichier .env

```sh
SEARXNG_BASE_URL="http://127.0.0.1:8080"
REDIS_BASE_URL="redis://redis:6379/0"
WORK_DIR="/Users/mlg/Documents/workspace_for_ai"
OLLAMA_PORT="11434"
LM_STUDIO_PORT="1234"
CUSTOM_ADDITIONAL_LLM_PORT="11435"
OPENAI_API_KEY='optionnel'
DEEPSEEK_API_KEY='optionnel'
OPENROUTER_API_KEY='optionnel'
TOGETHER_API_KEY='optionnel'
GOOGLE_API_KEY='optionnel'
ANTHROPIC_API_KEY='optionnel'
```

**Les clés API sont totalement optionnelles pour les utilisateurs qui choisissent d’exécuter le LLM localement. Ce qui est le but principal du projet. Laissez vide si vous avez le matériel suffisant.**

Les variables d’environnement suivantes configurent les connexions et clés API de votre application.

Mettez à jour le fichier `.env` avec vos propres valeurs si besoin :

- **SEARXNG_BASE_URL** : Laisser inchangé
- **REDIS_BASE_URL** : Laisser inchangé
- **WORK_DIR** : Chemin vers votre dossier de travail local. AI Stock Analyst pourra lire et interagir avec ces fichiers.
- **OLLAMA_PORT** : Port pour le service Ollama.
- **LM_STUDIO_PORT** : Port pour le service LM Studio.
- **CUSTOM_ADDITIONAL_LLM_PORT** : Port pour tout service LLM personnalisé.

Toutes les variables d’environnement de clé API ci-dessous sont **optionnelles**. Vous n’avez à les fournir que si vous souhaitez utiliser des API externes au lieu d’exécuter les LLM localement.

### 3. **Démarrer Docker**

Assurez-vous que Docker est installé et en cours d’exécution sur votre système. Vous pouvez démarrer Docker avec les commandes suivantes :

- **Sur Linux/macOS :**  
        Ouvrez un terminal et lancez :
        ```sh
        sudo systemctl start docker
        ```
        Ou lancez Docker Desktop depuis votre menu d’applications si installé.

- **Sur Windows :**  
        Lancez Docker Desktop depuis le menu Démarrer.

Vous pouvez vérifier que Docker fonctionne avec :
```sh
docker info
```
Si vous voyez des informations sur votre installation Docker, c’est que tout fonctionne.

---

## Configuration pour exécuter un LLM localement

**Configuration matérielle requise :**

Pour exécuter des LLM localement, il vous faut un matériel suffisant. Au minimum, un GPU capable d’exécuter Qwen/Deepseek 14B est requis. Voir la FAQ pour des recommandations détaillées.

**Démarrer votre fournisseur local**

Démarrez votre fournisseur local, par exemple avec ollama :

```sh
ollama serve
```

Voir ci-dessous la liste des fournisseurs locaux supportés.

**Mettre à jour le config.ini**

Modifiez le fichier config.ini pour définir provider_name sur un fournisseur supporté et provider_model sur un modèle LLM supporté par votre fournisseur. Nous recommandons des modèles de raisonnement comme *Qwen* ou *Deepseek*.

Voir la **FAQ** à la fin du README pour le matériel requis.

```sh
[MAIN]
is_local = True # Si vous exécutez localement ou avec un fournisseur distant.
provider_name = ollama # ou lm-studio, openai, etc.
provider_model = deepseek-r1:14b # choisissez un modèle adapté à votre matériel
provider_server_address = 127.0.0.1:11434
agent_name = Jarvis # nom de votre IA
recover_last_session = True # reprendre la session précédente
save_session = True # mémoriser la session actuelle
speak = False # synthèse vocale
listen = False # Reconnaissance vocale, uniquement pour CLI, expérimental
jarvis_personality = False # Personnalité "Jarvis" (expérimental)
languages = en zh # Liste des langues, la synthèse vocale prendra la première par défaut
[BROWSER]
headless_browser = True # laisser inchangé sauf si utilisation CLI sur l’hôte.
stealth_mode = True # Utilise selenium indétectable pour réduire la détection
```

**Attention** :

- Le format du fichier `config.ini` ne supporte pas les commentaires.
Ne copiez/collez pas la configuration d’exemple directement, car les commentaires provoqueront des erreurs. Modifiez manuellement le fichier `config.ini` avec vos paramètres, sans commentaires.

- Ne mettez *pas* provider_name à `openai` si vous utilisez LM-studio pour exécuter les LLM. Mettez-le à `lm-studio`.

- Certains fournisseurs (ex : lm-studio) nécessitent `http://` devant l’IP. Par exemple `http://127.0.0.1:1234`

**Liste des fournisseurs locaux**

| Fournisseur  | Local ? | Description                                               |
|--------------|---------|----------------------------------------------------------|
| ollama       | Oui     | Exécutez des LLM localement facilement avec ollama       |
| lm-studio    | Oui     | Exécutez un LLM localement avec LM studio (`lm-studio`)  |
| openai       | Oui     | Utilise une API compatible openai (ex : serveur llama.cpp)|

Étape suivante : [Démarrer les services et lancer AI Stock Analyst](#Start-services-and-Run)

*Voir la section **Problèmes connus** en cas de souci*

*Voir la section **Utiliser une API** si votre matériel ne peut pas exécuter deepseek localement*

*Voir la section **Config** pour une explication détaillée du fichier de configuration.*

---

## Configuration pour utiliser une API

**L’utilisation d’une API est optionnelle, voir ci-dessus pour l’exécution locale.**

Définissez le fournisseur désiré dans le `config.ini`. Voir ci-dessous la liste des fournisseurs API.

```sh
[MAIN]
is_local = False
provider_name = google
provider_model = gemini-2.0-flash
provider_server_address = 127.0.0.1:5000 # sans importance
```
Attention : Ne laissez pas d’espace à la fin de la config.

Exportez votre clé API : `export <<PROVIDER>>_API_KEY="xxx"`

Exemple : export `TOGETHER_API_KEY="xxxxx"`

**Liste des fournisseurs API**
    
| Fournisseur  | Local ? | Description                                               |
|--------------|---------|----------------------------------------------------------|
| openai       | Selon   | Utilise l’API ChatGPT  |
| deepseek     | Non     | API Deepseek (non privé)                            |
| huggingface  | Non     | API Hugging-Face (non privé)                            |
| togetherAI   | Non     | Utilise l’API together AI (non privé)                   |
| google       | Non     | Utilise l’API gemini de Google (non privé)              |

Notez que le codage/bash peut échouer avec gemini, qui ignore parfois le format demandé, optimisé pour deepseek r1. Les modèles comme gpt-4o donnent aussi de moins bons résultats avec notre prompt.

Étape suivante : [Démarrer les services et lancer AI Stock Analyst](#Start-services-and-Run)

*Voir la section **Problèmes connus** en cas de souci*

*Voir la section **Config** pour une explication détaillée du fichier de configuration.*

---

## Démarrer les services et lancer AI Stock Analyst

Démarrez les services requis. Cela lancera tous les services du docker-compose.yml, dont :
        - searxng
        - redis (requis par searxng)
        - frontend
        - backend (si vous utilisez `full`)

```sh
./start_services.sh full # MacOS
start ./start_services.cmd full # Windows
```

**Attention :** Cette étape téléchargera et chargera toutes les images Docker, ce qui peut prendre jusqu’à 30 minutes. Après le démarrage, attendez que le backend soit bien lancé (vous devriez voir backend: <info> dans les logs) avant d’envoyer des messages. Le backend peut mettre plus de temps à démarrer.

Allez sur `http://localhost:3000/` pour accéder à l’interface web.

**Optionnel : Utiliser l’interface CLI :**

Pour utiliser le mode CLI, vous devrez installer les paquets sur l’hôte :

```sh
./install.sh
./install.bat # windows
```

Démarrez les services :

```sh
./start_services.sh # MacOS
start ./start_services.cmd # Windows
```

Puis lancez : `uv run cli.py`

---

## Utilisation

Assurez-vous que les services sont lancés avec `./start_services.sh full` et allez sur `localhost:3000` pour l’interface web.

Vous pouvez aussi utiliser la reconnaissance vocale en mettant `listen = True` dans la config (mode CLI uniquement).

Pour quitter, dites/tapez simplement `goodbye`.

Exemples d’utilisation :

> *Fais un jeu du serpent en python !*

> *Recherche les meilleurs cafés à Rennes, France, et enregistre une liste de trois avec leurs adresses dans rennes_cafes.txt.*

> *Écris un programme Go pour calculer la factorielle d’un nombre, sauvegarde-le sous factorial.go dans ton espace de travail*

> *Cherche dans mon dossier summer_pictures tous les fichiers JPG, renomme-les avec la date du jour, et enregistre la liste dans photos_list.txt*

> *Recherche en ligne les films de science-fiction populaires de 2024 et choisis-en trois à regarder ce soir. Sauvegarde la liste dans movie_night.txt.*

> *Recherche les derniers articles d’actualité sur l’IA de 2025, sélectionne-en trois, et écris un script Python pour extraire leurs titres et résumés. Sauvegarde le script sous news_scraper.py et les résumés dans ai_news.txt dans /home/projects*

> *Vendredi, cherche une API gratuite de prix d’actions, inscris-toi avec supersuper7434567@gmail.com puis écris un script Python pour récupérer les prix quotidiens de Tesla, et sauvegarde les résultats dans stock_prices.csv*

*Note : le remplissage de formulaires est encore expérimental et peut échouer.*

Après avoir saisi votre requête, AI Stock Analyst choisira le meilleur agent pour la tâche.

Comme il s’agit d’un prototype, le système de routage d’agent peut ne pas toujours choisir le bon agent selon votre requête.

Soyez donc explicite sur ce que vous voulez et comment l’IA doit procéder. Par exemple, pour une recherche web, ne dites pas :

`Connais-tu de bons pays pour voyager en solo ?`

Dites plutôt :

`Fais une recherche web et trouve les meilleurs pays pour voyager en solo`

---

## **Exécuter le LLM sur votre propre serveur**

Si vous avez un ordinateur ou un serveur puissant, mais souhaitez l’utiliser depuis votre laptop, vous pouvez exécuter le LLM sur un serveur distant via notre serveur LLM personnalisé.

Sur votre "serveur" qui exécutera le modèle IA, récupérez l’adresse IP :

```sh
ip a | grep "inet " | grep -v 127.0.0.1 | awk '{print $2}' | cut -d/ -f1 # ip locale
curl https://ipinfo.io/ip # ip publique
```

Note : Sous Windows ou macOS, utilisez ipconfig ou ifconfig pour trouver l’adresse IP.

Clonez le dépôt et entrez dans le dossier `server/` :

```sh
git clone --depth 1 https://github.com/ServOps117/agenticSeek.git
cd agenticSeek/llm_server/
```

Installez les dépendances spécifiques au serveur :

```sh
pip3 install -r requirements.txt
```

Lancez le script serveur :

```sh
python3 app.py --provider ollama --port 3333
```

Vous pouvez choisir entre `ollama` et `llamacpp` comme service LLM.

Sur votre ordinateur personnel :

Modifiez le fichier `config.ini` pour mettre `provider_name` à `server` et `provider_model` à `deepseek-r1:xxb`.
Mettez `provider_server_address` à l’adresse IP de la machine qui exécute le modèle.

```sh
[MAIN]
is_local = False
provider_name = server
provider_model = deepseek-r1:70b
provider_server_address = x.x.x.x:3333
```

Étape suivante : [Démarrer les services et lancer AI Stock Analyst](#Start-services-and-Run)

---

## Reconnaissance Vocale

Attention : la reconnaissance vocale ne fonctionne qu’en mode CLI pour l’instant.

Notez qu’actuellement la reconnaissance vocale ne fonctionne qu’en anglais.

La fonctionnalité de reconnaissance vocale est désactivée par défaut. Pour l’activer, mettez listen à True dans le fichier config.ini :

```
listen = True
```

Quand activée, la reconnaissance vocale attend un mot-clé déclencheur, qui est le nom de l’agent, avant de commencer à traiter votre entrée. Vous pouvez personnaliser le nom de l’agent via `agent_name` dans *config.ini* :

```
agent_name = Friday
```

Pour une reconnaissance optimale, nous recommandons d’utiliser un prénom anglais courant comme "John" ou "Emma" comme nom d’agent.

Une fois la transcription affichée, dites le nom de l’agent à voix haute pour le réveiller (ex : "Friday").

Énoncez clairement votre requête.

Terminez votre demande par une phrase de confirmation pour signaler au système de procéder. Exemples :
```
"do it", "go ahead", "execute", "run", "start", "thanks", "would ya", "please", "okay?", "proceed", "continue", "go on", "do that", "go it", "do you understand?"
```

## Config

Exemple de config :
```
[MAIN]
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:11434
agent_name = Friday
recover_last_session = False
save_session = False
speak = False
listen = False
jarvis_personality = False
languages = en zh
[BROWSER]
headless_browser = False
stealth_mode = False
```

**Explications** :

- is_local -> Exécute l’agent localement (True) ou sur un serveur distant (False).

- provider_name -> Fournisseur à utiliser (parmi : `ollama`, `server`, `lm-studio`, `deepseek-api`)

- provider_model -> Modèle utilisé, ex : deepseek-r1:32b.

- provider_server_address -> Adresse du serveur, ex : 127.0.0.1:11434 pour local. Mettre n’importe quoi pour une API non locale.

- agent_name -> Nom de l’agent, ex : Friday. Utilisé comme mot-clé pour la reconnaissance vocale.

- recover_last_session -> Reprend la dernière session (True) ou non (False).

- save_session -> Sauvegarde la session (True) ou non (False).

- speak -> Active la synthèse vocale (True) ou non (False).

- listen -> Active la reconnaissance vocale (True) ou non (False).

- jarvis_personality -> Utilise une personnalité type JARVIS (True) ou non (False). Change simplement le prompt.

- languages -> Liste des langues supportées, nécessaire pour le routage des agents. Évitez d’en mettre trop ou des langues trop similaires.

- headless_browser -> Lance le navigateur sans fenêtre visible (True) ou non (False).

- stealth_mode -> Rend la détection par les bots plus difficile. Nécessite d’installer l’extension anticaptcha manuellement.

- languages -> Liste des langues supportées. Requis pour le système de routage. Plus la liste est longue, plus de modèles seront téléchargés.

## Fournisseurs

Tableau des fournisseurs disponibles :

| Fournisseur  | Local ? | Description                                               |
|--------------|---------|----------------------------------------------------------|
| ollama       | Oui     | Exécutez des LLM localement avec ollama                  |
| server       | Oui     | Hébergez le modèle sur une autre machine                 |
| lm-studio    | Oui     | Exécutez un LLM localement avec LM studio (`lm-studio`)  |
| openai       | Selon   | Utilise l’API ChatGPT (non privé) ou API compatible openai|
| deepseek-api | Non     | API Deepseek (non privé)                                 |
| huggingface  | Non     | API Hugging-Face (non privé)                             |
| togetherAI   | Non     | Utilise l’API together AI (non privé)                    |
| google       | Non     | Utilise l’API gemini de Google (non privé)               |

Pour sélectionner un fournisseur, modifiez le config.ini :

```
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:5000
```
`is_local` : doit être True pour tout LLM local, sinon False.

`provider_name` : Sélectionnez le fournisseur par son nom, voir la liste ci-dessus.

`provider_model` : Modèle à utiliser par l’agent.

`provider_server_address` : Peut être n’importe quoi si vous n’utilisez pas le fournisseur server.

# Problèmes connus

## Problèmes avec Chromedriver

**Erreur connue #1 :** *chromedriver mismatch*

`Exception: Failed to initialize browser: Message: session not created: This version of ChromeDriver only supports Chrome version 113
Current browser version is 134.0.6998.89 with binary path`

Cela arrive s’il y a un décalage entre la version de votre navigateur et celle de chromedriver.

Téléchargez la dernière version ici :

https://developer.chrome.com/docs/chromedriver/downloads

Si vous utilisez Chrome version 115 ou plus, allez sur :

https://googlechromelabs.github.io/chrome-for-testing/

Et téléchargez la version de chromedriver correspondant à votre OS.

![alt text](./media/chromedriver_readme.png)

Si cette section est incomplète, ouvrez une issue.

## Problèmes d’adaptateurs de connexion

```
Exception: Provider lm-studio failed: HTTP request failed: No connection adapters were found for '127.0.0.1:11434/v1/chat/completions'
```

Assurez-vous d’avoir `http://` devant l’adresse IP du fournisseur :

`provider_server_address = http://127.0.0.1:11434`

## SearxNG base URL doit être fourni

```
raise ValueError("SearxNG base URL must be provided either as an argument or via the SEARXNG_BASE_URL environment variable.")
ValueError: SearxNG base URL must be provided either as an argument or via the SEARXNG_BASE_URL environment variable.
```

Peut-être n’avez-vous pas renommé `.env.example` en `.env` ? Vous pouvez aussi exporter SEARXNG_BASE_URL :

`export  SEARXNG_BASE_URL="http://127.0.0.1:8080"`

## FAQ

**Q : Quel matériel est nécessaire ?**  

| Taille du modèle | GPU           | Commentaire                                                                 |
|------------------|---------------|-----------------------------------------------------------------------------|
| 7B               | 8 Go Vram     | ⚠️ Non recommandé. Performances faibles, hallucinations fréquentes, échec probable des agents planificateurs. |
| 14B              | 12 Go VRAM    | ✅ Utilisable pour des tâches simples. Peut avoir du mal avec la navigation web et la planification. |
| 32B              | 24+ Go VRAM   | 🚀 Réussite sur la plupart des tâches, peut encore avoir du mal avec la planification |
| 70B+             | 48+ Go Vram   | 💪 Excellent. Recommandé pour les cas avancés.                              |

**Q : Pourquoi Deepseek R1 plutôt qu’un autre modèle ?**  

Deepseek R1 excelle en raisonnement et utilisation d’outils pour sa taille. Nous pensons que c’est un bon choix, d’autres modèles fonctionnent aussi, mais Deepseek est notre favori.

**Q : J’ai une erreur en lançant `cli.py`. Que faire ?**  

Assurez-vous que le local est lancé (`ollama serve`), que votre `config.ini` correspond à votre fournisseur, et que les dépendances sont installées. Si rien ne marche, ouvrez une issue.

**Q : Peut-on vraiment tout faire tourner en local ?**  

Oui, avec Ollama, lm-studio ou server, tout (reconnaissance vocale, LLM, synthèse vocale) fonctionne localement. Les options non-locales (OpenAI ou autres API) sont optionnelles.

**Q : Pourquoi utiliser AI Stock Analyst alors que j'ai Manus ?****

Ce projet est né d’un intérêt pour les agents IA. Ce qui le rend spécial, c’est la volonté d’utiliser des modèles locaux et d’éviter les API.
Nous nous inspirons de Jarvis et Friday (Iron Man) pour le côté "cool", mais pour la fonctionnalité, c’est Manus qui nous inspire, car c’est ce que les gens recherchent : une alternative locale à Manus.
Contrairement à Manus, AI Stock Analyst privilégie l'indépendance vis-à-vis des systèmes externes, vous donnant plus de contrôle, de confidentialité et évitant les coûts d'API.API.

## Contribuer

Nous recherchons des développeurs pour améliorer AI Stock Analyst ! Consultez les issues ou discussions ouvertes.

[Guide de contribution](./docs/CONTRIBUTING.md)

[![Star History Chart](https://api.star-history.com/svg?repos=Fosowl/ai-stock-analyst&type=Date)](https://www.star-history.com/#Fosowl/ai-stock-analyst&Date)

## Mainteneurs :

 > [Fosowl](https://github.com/Fosowl) | Heure de Paris 

 > [antoineVIVIES](https://github.com/antoineVIVIES) | Heure de Taipei 

 > [steveh8758](https://github.com/steveh8758) | Heure de Taipei 

## Remerciements :

 > [tcsenpai](https://github.com/tcsenpai) et [plitc](https://github.com/plitc) pour l’aide à la dockerisation du backend

