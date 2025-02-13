FROM python:3.11-slim
WORKDIR /app

# Installer les dépendances
COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Copier le code de l'application
COPY . .

# Lancer l'application Flask
CMD ["python3","app.py"]
