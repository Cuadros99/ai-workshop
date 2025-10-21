FROM python:3.11

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Atualiza pacotes e instala utilitários do sistema
# ✅ Inclui o htop para monitorar uso de CPU e memória
RUN apt-get update && apt-get install -y \
    htop \
 && rm -rf /var/lib/apt/lists/*

# Copia o arquivo de requisitos para o container
COPY requirements-lab-2.txt .

# Instala as dependências do arquivo de requisitos
RUN pip install --no-cache-dir -r requirements-lab-2.txt

# ✅ Instala o Jupyter Notebook explicitamente
RUN pip install --no-cache-dir jupyter notebook

# Copia o arquivo main.ipynb para o diretório de trabalho do container
COPY main.ipynb .

# Cria a pasta 'output' dentro do container para arquivos que devem ser persistidos
RUN mkdir -p /app/output

# (Opcional) Comando para rodar o Jupyter Notebook, se desejar
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]