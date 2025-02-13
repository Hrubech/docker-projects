# Multi-Container Application
**Objectif** : Apprendre à gérer des applications multi-conteneurs à l'aide de Docker Compose.<br>
**Tech Stack** :<br>
  - Python (Flask)<br>
  - PostgreSQL<br>
  - Docker Compose
## 🛠️ 1. Créer un environnement virtuel

Voir étape 1 à 3 de **Project1**.

## 2. Configuration de l'application Web et de la base de données

Créer une application web simple avec une connection à la base de données (Flask + PostgreSQL).
```bash
    # app.py
    import psycopg2
    from flask import Flask
    app = Flask(__name__)

    def connect_db():
        return psycopg2.connect(
            dbname="mydb",
            user="user",
            password="password",
            host="db"
        )

    @app.route("/")
    def home():
        conn = connect_db()
        return "Connected to DB!"

    if __name__ == "__main__":
      app.run(host="0.0.0.0", port=5000)
```

## 3. Écrire un Dockerfile

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

## 4. Créer le fichier docker-compose.yml

- Ajouter ce contenu dans le fichier docker-compose.yml :
  ```
    services:
        web:
            build: .
            ports: 
                - "5000:5000"
            depends_on:
                - db
        
        db:
            image: postgres
            environment:
                POSTGRES_USER: user
                POSTGRES_PASSWORD: password
                POSTGRES_DB: mydb
  ```

## 5. Exécuter avec Docker Compose

```bash
    docker compose up --build
```

## 6. Vérifier l'application

- Ouvrir http://localhost:5000 dans votre navigateur.