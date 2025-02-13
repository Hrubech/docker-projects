# Containerized web app
**Objectif** : Apprendre les bases de Docker en conteneurisant une simple application web.<br>
**Tech Stack** :<br>
  - Python (Flask)<br>
  - Docker
## 🛠️ 1. Créer un environnement virtuel

Assurez-vous que Python est installé :
```bash
    python3 --version
```
### ▶️ Création de l'environnement
```bash
    # Créer un environnement virtuel nommé "flask"
    python -m venv flask
```
### ▶️ Activer l'environnement
```bash
    source flask/bin/activate
```
Vous devriez voir (flask) devant votre prompt, indiquant que l'environnement est activé.

## 📦 2. Installer les dépendances

Dans l'environnement activé, installez les paquets nécessaires :
```bash
    pip3 install flask
```

## 📤 3. Extraire les dépendances dans un fichier
Une fois tous vos paquets installés, utilisez :
```bash
    pip3 freeze > requirements.txt
```
Cela générera un fichier contenant toutes les dépendances et leurs versions, par exemple :
```bash
    # requirements.txt
    flask==3.0.0
```

## 4. Configuration de l'application Web

Créer une application Flask simple.
```bash
    # app.py
    from flask import Flask
    app = Flask(__name__)

    @app.route("/")
    def home():
      return "Hello, Docker!"

    if __name__ == "__main__":
      app.run(host="0.0.0.0", port=5000)
```

## 5. Écrire un Dockerfile

Créer un fichier Dockerfile à la racine du projet :
```
    # Dockerfile
    FROM python:3.11-slim
    WORKDIR /app

    # Installer les dépendances
    COPY requirements.txt .
    RUN pip3 install -r requirements.txt

    # Copier le code de l'application
    COPY . .

    # Lancer l'application Flask
    CMD ["python3","app.py"]
```

## 6. Créer et exécuter l'image Docker

- Build de l'image Docker :
  ```bash
    docker build -t flask-app .
  ```
- Run du container
  ```bash
    docker run -p 5000:5000 flask-app
  ```

## 7. Vérifier l'application

- Ouvrir http://localhost:5000 dans votre navigateur.