FROM python:3.13-slim
WORKDIR /app

COPY app.py requirements.txt /app/


RUN pip install -r requirements.txt

# Créer un utilisateur dédié (sans privilèges)
RUN groupadd -r appgroup && useradd -r -g appgroup appuser

# Changer les permissions avant de changer d'utilisateur
RUN chown -R appuser:appgroup /app

# Passer à l'utilisateur non-root
USER appuser


ENV FLASK_APP=app.py

EXPOSE 5000

CMD ["python", "app.py"]


