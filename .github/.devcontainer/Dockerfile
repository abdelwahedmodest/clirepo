# Utiliser une image Python comme base pour Django
FROM python:3.10-slim

# Installer PostgreSQL et les dépendances requises
RUN apt-get update && apt-get install -y \
    postgresql postgresql-contrib libpq-dev build-essential

# Configurer PostgreSQL
USER postgres
RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER postgres WITH SUPERUSER PASSWORD 'postgres';" && \
    createdb -O postgres postgres

# Retour à l'utilisateur root pour continuer l'installation
USER root

# Installer les dépendances de votre projet
COPY requirements.txt /workspace/requirements.txt
RUN pip install -r /workspace/requirements.txt

# Exposer les ports pour Django et PostgreSQL
EXPOSE 5432 8000

# Commande de démarrage par défaut
CMD service postgresql start && bash
