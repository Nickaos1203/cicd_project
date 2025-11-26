## Mission 1 : Comprendre le CI/CD

### 1. Qu’est-ce que la CI (Continuous Integration) ?

La CI, ou "Intégration Continue", est une pratique qui consiste à intégrer fréquemment (souvent plusieurs fois par jour) le code développé par différents membres d’une équipe dans un dépôt central.
Chaque intégration déclenche automatiquement une série de vérifications (compilation, tests unitaires, analyse qualité, etc.). L’objectif est de détecter les erreurs le plus tôt possible.

#### Quels problèmes la CI résout-elle ?
- **Réduction des conflits d’intégration :** Lorsque chaque développeur travaille plusieurs jours sur sa branche, l’intégration devient difficile (« integration hell »). La CI évite cela.
- **Détection rapide des bugs :** Les tests automatiques tournent à chaque commit → les erreurs apparaissent rapidement.
- **Stabilisation du code :** Le dépôt principal reste en état fonctionnel grâce aux contrôles automatiques.
- **Automatisation des tâches répétitives :** Build, tests, analyse statique, packaging, etc.

#### Quels sont les principes clés de la CI ?
- **Commit fréquents :** petites modifications intégrées souvent.
- **Builds automatisés :** compilation et tests se lancent automatiquement.
- **Pipeline unique et reproductible :** toujours le même processus de vérification.
- **Tests automatisés nombreux :** surtout tests unitaires rapides.
- **Transparence et feedback rapide :** les développeurs sont immédiatement alertés en cas de problème.
- **Codebase toujours déployable :** la branche principale doit rester stable.

#### Exemples d’outils de CI
Jenkins, GitLab CI/CD, GitHub Actions.


### 2. Qu’est-ce que le CD (Continuous Delivery / Continuous Deployment) ?

Le CD est la suite logique de la CI et concerne les étapes de mise en production.
- **Continuous Delivery :** Le logiciel est toujours prêt à être déployé, mais le déploiement nécessite une validation humaine.
- **Continuous Deployment :** Chaque modification validée par la CI est déployée automatiquement en production sans intervention humaine.

#### Différence entre Continuous Delivery et Continuous Deployment

| Aspect                  | Continious Delivery                 | Continious Deployment               |
| :---------------------- | :---------------------------------- | :---------------------------------- |
|Déploiement en production|Manuel                               |Automatique                          |
|Critère                  |Pipeline automatisé jusqu'au pré-prod|Pipeline jusqu'en prod               |
|Fréquence                |Régulière                            |Très élevée (plusieurs fois par jour)|
|Risque humain            |Contrôle final humain                |Aucun contrôle humain                |

#### Risques et bénéfices du CD

**Bénéfices :**
- Déploiements plus fréquents et plus fiables.
- Réduction du temps entre développement et valeur livrée au client.
- Moins d’erreurs humaines (automatisation).
Releases plus petites donc moins risquées.

**Risques :**
- Mauvaise configuration du pipeline → déploiement de bugs en production.
- Nécessite une excellente couverture de tests automatisés.
Demande une maturité technique et organisationnelle importante.

### 3. Pourquoi le CI/CD est important ?

#### Impact sur la qualité du code
- Détection précoce des bugs (moins coûteux à corriger).
- Analyses automatiques (lint, tests, sécurité).
- code plus stable, plus propre et mieux testé.

#### Impact sur la vitesse de développement
- Moins de temps consacré aux intégrations manuelles.
- Mise en production accélérée.
- Automatisation des tâches répétitives (gain de temps pour les développeurs).

#### Impact sur la collaboration en équipe
- Moins de conflits de merge.
- Pipeline commun (transparence sur l’état du code).
- Culture DevOps (responsabilité partagée du cycle de développement).

## Mission 2 : Maîtriser UV

### 1. Qu’est-ce que uv ?

UV est un outil Python développé par Astral (créateurs de Ruff). C’est un gestionnaire d’environnement et de dépendances ultra-rapide, écrit en Rust, qui vise à remplacer ou compléter :
- pip (installation de paquets),
- venv (création d’environnements virtuels),
- pip-tools (gestion de versions) et même des outils plus complets comme Poetry ou Pipenv.

**Son objectif principal :** offrir une alternative unifiée, moderne et très rapide pour la gestion de projets Python.

#### En quoi est-ce différent de pip / poetry / pipenv ?

| Fonction                          | pip     | pipenv  | poetry  | uv                            |
| --------------------------------- | ------- | ------- | ------- | ----------------------------- |
| Gestion des dépendances           | ✔       | ✔       | ✔       | ✔                             |
| Environnements virtuels           | ✖       | ✔       | ✔       | ✔                             |
| Lockfile                          | partiel | ✔       | ✔       | ✔ (super rapide)              |
| Vitesse                           | lente   | moyenne | moyenne | **extrêmement rapide** (Rust) |
| Build backend                     | ✖       | partiel | ✔       | ✔                             |
| Compatible pyproject              | ✔       | ✔       | ✔       | ✔                             |
| Installation d’outils (type pipx) | ✖       | ✖       | ✖       | ✔                             |
| Unification des workflows         | ✖       | partiel | ✔       | **✔ (plus complet)**          |

#### Avantages principaux de uv

- Rapidité (installation, création d’environnements, résolution de dépendances).
- Outil unique remplaçant pip, venv, pipx, etc.
- Compatible avec les standards Python : pyproject.toml, PEPs modernes.
- Cache global intelligent (valide entre projets).
- Usage simple mais puissant : uv add, uv run, uv sync.

### 3. Comment uv fonctionne avec pyproject.toml ? 

#### Structure du fichier
```
[project]
name = "mon_projet"
version = "0.1.0"
description = "Exemple d'utilisation d'uv"
authors = [{ name = "Alice", email = "alice@example.com" }]
requires-python = ">=3.10"

dependencies = [
    "requests",
    "pandas>=2.0",
]

[project.optional-dependencies]
dev = [
    "pytest",
    "ruff",
]

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

```

#### Gestion des dépendances
- Ajout d'une dépendance (exemple avec numpy) :
```
uv add numpy
```
- Synchroniser l'environnement (met à jour le uv.lock) :
```
uv sync
```

#### Build backend
(...)

### 3. Comment utiliser uv dans Github actions ?

#### Installation
- installer les dépendances (avec Python):
```
- name: Install uv + Python
  uses: astral-sh/setup-uv@v1
  with:
    python-version: "3.12"
```

#### Cache des dépendances
```
- name: Cache uv dependencies
  uses: actions/cache@v4
  with:
    path: ~/.cache/uv
    key: ${{ runner.os }}-uv-${{ hashFiles('**/uv.lock') }}
    restore-keys: |
      ${{ runner.os }}-uv-
```

#### Exécution des commandes

- Installation des dépendances :
```
- name: Install dependencies
  run: uv sync
```

- Lancer une commande Python via uv : 
```
- name: Run tests
  run: uv run pytest
```

- Lancer un script :
```
- name: Run script
  run: uv run python main.py
```
