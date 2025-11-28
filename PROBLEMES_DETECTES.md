## Recensement des problèmes détectés

**Infos**
🎨 **Formatage** : Espaces, lignes trop longues, indentation
🔒 **Sécurité** : Secrets en dur, mots de passe, clés API
📦 **Imports** : Inutilisés, mal ordonnés, dupliqués
🏷️ **Types** : Fonctions non typées, any implicites
📝 **Documentation** : Docstrings manquantes ou incomplètes
♻️ **Code mort** : Variables inutilisées, fonctions obsolètes, code commenté


### main.py
- **Formatage** : la variable very_long_variable_name_that_exceeds_line_length est trop longue.
- **sécurité** : Clé API (API_KEY) et la variable "secret" en clairs.
- **imports** : "from typing import Dict, Any" non utilisé. "import os" non utilisé. "import json" non utilisé. 
- **Types** :
- **Documentation** :
- **Codes morts** : Les variables UNUSED_VAR et DEBUG_MODE non-utilisées.

### database.py
- **Formatage** :
- **sécurité** :
- **imports** : "from typing import Generator" et "import sys" non utlisés.
- **Types** :
- **Documentation** :
- **Codes morts** : la variable POOL_SIZE non-utilisée.

### models/items.py
- **Formatage** :
- **sécurité** :
- **imports** : "from typing import Optional" non-utlisé. 
- **Types** :
- **Documentation** :
- **Codes morts** : "def _legacy_method" inutile.

### routes/items.py
- **Formatage** :
- **sécurité** :
- **imports** : import "ItemCreate", "List" non utilisés. "import datetime" non-utilisé. "from app.schemas.item import ItemCreate" non utilisé.
- **Types** :
- **Documentation** : docstrings manquantes pour les fonctions "get_item", "create_item", "update_item", "delete_item" ;
- **Codes morts** :  La variable "MAX_ITEMS_PER_PAGE" non-utilisée. La fonction "_old_helper_function" n'est pas utilisée.

### schemas/items.py 
- **Formatage** :
- **sécurité** :
- **imports** : "from typing import Optional" non utilisé.
- **Types** :
- **Documentation** :
- **Codes morts** : "class ItemCreate" inutile. 

### services/items.py
- **Formatage** :
- **sécurité** :
- **imports** :
- **Types** :
- **Documentation** :
- **Codes morts** :


## 🔍 Phase 1 : Découverte du Projet

### Questions de réflexion

1. **Le code fonctionne, mais** :
   - Est-il maintenable ?
   - Est-il sécurisé ?
   - Est-il bien documenté ?

2. **Comment détecter ces problèmes automatiquement ?**
   - Quels outils utiliser ?
   - À quel moment les exécuter ?

3. **Comment empêcher ces problèmes à l'avenir ?**


### ✅ Validation Phase 1

- [ ] L'application fonctionne localement
- [ ] Vous avez testé tous les endpoints
- [ ] ✅ `PROBLEMES_DETECTES.md` contient au moins 20 problèmes identifiés
- [ ] ✅ Vous comprenez la structure du projet


## 🌿 Phase 2 : Stratégie de Branches & Conventional Commits

### ❓ Questions de réflexion

1. **Pourquoi protéger les branches ?**
   - Que se passerait-il sans protection ?

2. **Pourquoi Conventional Commits ?**
   - Avantages pour l'équipe
   - Avantages pour le versionnage automatique

3. **Différence entre develop et main ?**
   - Quand merger dans develop ?
   - Quand merger dans main ?

### ✅ Validation Phase 2

- [ ] ✅ Branches `main` et `develop` créées
- [ ] ✅ Protection de branches configurée sur GitHub
- [ ] ✅ Au moins 1 PR créée avec Conventional Commit
- [ ] ✅ Vous comprenez le workflow GitFlow


## 🧪 Phase 3 : CI Pipeline - Tests, Quality & Security

