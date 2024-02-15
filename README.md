# projet_M2_recherche
Pour coder des tests d'intégration pour des endpoints créés avec FastAPI en Python, vous allez typiquement suivre ces étapes :

1. **Installer les dépendances nécessaires** : Assurez-vous d'avoir installé FastAPI, un ASGI server comme Uvicorn pour exécuter votre application, et `pytest` pour écrire et exécuter vos tests. Vous pourriez également vouloir utiliser `httpx` pour les requêtes HTTP dans vos tests.

2. **Configurer votre environnement de test** : Configurez votre application FastAPI pour qu'elle soit prête à être testée. Cela peut inclure la configuration d'une base de données de test, la mise en place de variables d'environnement spécifiques aux tests, etc.

3. **Écrire les tests d'intégration** : Utilisez le framework `pytest` pour écrire des tests. Créez des fonctions de test qui exécutent des requêtes HTTP vers votre application FastAPI en utilisant `httpx` ou le `TestClient` de FastAPI. Vérifiez les réponses pour s'assurer qu'elles sont correctes.

4. **Exécuter les tests** : Utilisez la commande `pytest` pour exécuter vos tests d'intégration et vérifier que tout fonctionne comme prévu.

Voici un exemple de base pour illustrer ces étapes :

### Étape 1 : Installer les dépendances

Assurez-vous d'avoir `fastapi`, `uvicorn`, `pytest`, et `httpx` installés. Vous pouvez les installer via pip :

```bash
pip install fastapi uvicorn pytest httpx
```

### Étape 2 : Configurer l'environnement de test

Supposons que vous avez une application FastAPI simple :

```python
# app/main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"Hello": "World"}
```

### Étape 3 : Écrire les tests d'intégration

Créez un fichier de test, par exemple `test_main.py`, et utilisez le `TestClient` pour tester votre endpoint :

```python
# tests/test_main.py
from httpx import AsyncClient
import pytest
from app.main import app

@pytest.mark.anyio
async def test_read_root():
    async with AsyncClient(app=app, base_url="http://test") as ac:
        response = await ac.get("/")
        assert response.status_code == 200
        assert response.json() == {"Hello": "World"}
```

### Étape 4 : Exécuter les tests

Exécutez vos tests en utilisant la commande `pytest` dans votre terminal :

```bash
pytest
```

Cette approche simple vous permet de commencer avec les tests d'intégration pour FastAPI. Vous pouvez étendre cela en testant des endpoints plus complexes, en utilisant des bases de données de test, et en configurant des environnements de test plus avancés selon vos besoins.
