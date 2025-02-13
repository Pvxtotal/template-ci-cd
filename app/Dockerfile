# Usa uma imagem Python reduzida para minimizar vulnerabilidades
FROM python:3.10-slim

# Definir diretório de trabalho
WORKDIR /app

# Atualiza pacotes do sistema e remove arquivos desnecessários
RUN apt-get update && apt-get upgrade -y && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copia os arquivos da aplicação
COPY . /app

# Instala dependências de forma otimizada
RUN pip install --no-cache-dir --upgrade pip setuptools && pip install --no-cache-dir -r requirements.txt

# Criar usuário não-root para segurança
RUN useradd -m appuser
USER appuser

# Expor a porta correta do container
EXPOSE 8000

# Executar a aplicação usando Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "app:app"]
