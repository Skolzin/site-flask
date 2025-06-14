# Usa imagem base do Python
FROM python:3.11-slim

# Define diretório de trabalho
WORKDIR /app

# Copia os arquivos para o container
COPY . .

# Instala dependências
RUN pip install --no-cache-dir -r requirements.txt

# Cria pasta persistente para uploads
RUN mkdir -p /data
VOLUME ["/data"]

# Define variável de ambiente para uploads
ENV UPLOAD_FOLDER=/data

# Expõe a porta usada pela aplicação
EXPOSE 8080

# Comando para rodar o app com Gunicorn
CMD ["gunicorn", "-b", "0.0.0.0:8080", "app:app"]
