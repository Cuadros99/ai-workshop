# 🧠 AI Workshop

Para conseguirmos executar as atividades planejadas para esse workshop será necessário seguir as instruções abaixo.

Antes de partir para os preparativos de cada laboratório vamos precisar garantir que o Docker está instalado nas máquinas.

```bash
docker --version
```

**Resultado esperado:**
- Se estiver instalado, o terminal exibirá a versão do Docker (ex: `Docker version 24.0.6, build 240ee23`).
- Se não estiver instalado, o terminal retornará um erro como: `command not found: docker`

## ⚠️ Atenção

Caso você já passua o Docker instalado, pode **pular para a etapa** de preparação do Laboratório de Machine Learning, **caso contrário, siga as instruções abaixo de instalação do Docker**

---

## 🐳 Instalação do Docker


**Passo 1: Atualizar o repositório de pacotes**
```bash
sudo apt-get update
sudo apt-get upgrade -y
```

**Passo 2: Instalar dependências necessárias**
```bash
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

**Passo 3: Adicionar a chave GPG oficial do Docker**
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

**Passo 4: Adicionar o repositório do Docker ao APT**
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Passo 5: Atualizar o repositório de pacotes novamente**
```bash
sudo apt-get update
```

**Passo 6: Instalar o Docker Engine**
```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**Verificar a instalação**
Depois de instalar, verifique a versão do Docker:

```bash
docker --version
```

---

## 🔬 A - Laboratório de Machine Learning

Este ambiente contém o notebook do laboratório de aprendizado de máquina.  
Siga as instruções abaixo para **construir e executar** o container Docker com o Jupyter Notebook.

---

### 🎲 1. Baixar dataset

Baixar o dataset no link https://drive.google.com/file/d/1rA7IL03JcvlhEGai5Zk6s4SPktBRwKca/view?usp=sharing

Armazená-lo na pasta **dataset** do diretório do projeto.


### 🧱 2. Construir a imagem

Entrar na pasta do laboratório

```bash
cd Lab-1-ML  
```

No terminal, dentro da pasta do laboratório, execute:

```bash
sudo docker build -t lab-1-image .
```

### 📂 3. Criar a pasta de saída

Esta pasta armazenará os artefatos e resultados gerados pelo notebook.

```bash
mkdir -p output
```

### 🚀 4. Executar o container

Rode o container com o comando abaixo:

```bash
sudo docker run --rm -it \
  --name lab-1-container \
  -p 8888:8888 \
  --memory="7g" \
  -v "$(pwd)/output":/app/output \
  lab-1-image
```

### 📊 5. Acessar o Jupyter Notebook

Após o container iniciar, o terminal exibirá uma URL parecida com:

```bash
http://127.0.0.1:8888/?token=<seu_token_aqui>
```

### 🧩 6. (Opcional) Monitorar o uso de recursos

Para verificar o consumo de CPU e memória dentro do container:

```bash
sudo docker exec -it lab-1-container /bin/bash
```

```bash
htop
```

### ✅ Observações

- O container é temporário (--rm), ou seja, será removido automaticamente ao encerrar.
- Todos os arquivos gerados pelo notebook serão salvos na pasta local output/.
- Em caso de erro pelo Docker não estar ativo, rode o seguinte comando:

    ```bash
    sudo systemctl start docker
    ```

    E para habilitar o Docker iniciar automaticamente no boot:

    ```bash
    sudo systemctl enable docker
    ```



### 📘 Pronto!

Agora você pode abrir o Jupyter Notebook e seguir as instruções do laboratório.


## 🔬 B - Laboratório de LLMs

Este ambiente contém o notebook do laboratório de RAG.  
Siga as instruções abaixo para **construir e executar** o container Docker com o Jupyter Notebook.

---

### 🔒 1. Preencher .env

Entrar na pasta do laboratório

```bash
cd Lab-2-RAG
```

No terminal, dentro da pasta do laboratório, execute:

```bash
mv .env-example .env
```

Agora vamos preencher o .env com a chave de API da OpenAI

```bash
nano .env
```


### 🧱 2. Construir a imagem

No terminal, dentro da pasta do projeto, execute:

```bash
sudo docker build -t lab-2-image .
```

### 📂 3. Criar a pasta de saída

Esta pasta armazenará os artefatos e resultados gerados pelo notebook.

```bash
mkdir -p output
```

### 🚀 4. Executar o container

Rode o container com o comando abaixo:

```bash
sudo docker run --rm -it \
  --env-file .env\
  --name lab-2-container \
  -p 8888:8888 \
  --memory="7g" \
  -v "$(pwd)/output":/app/output \
  lab-2-image
```

### 📊 5. Acessar o Jupyter Notebook

Após o container iniciar, o terminal exibirá uma URL parecida com:

```bash
http://127.0.0.1:8888/?token=<seu_token_aqui>
```

### 🧩 6. (Opcional) Monitorar o uso de recursos

Para verificar o consumo de CPU e memória dentro do container:

```bash
sudo docker exec -it lab-2-container /bin/bash
```

```bash
htop
```

### 🧩 7. (Opcional) Rodar modelo localmente (Ollama)

Instalar Ollama na máquina

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Verificar se foi instalado com sucesso

```bash
ollama --version
```

Iniciar o serviço

```bash
ollama serve
```

Baixar pesos de um modelo open source

```bash
ollama pull qwen3:4b
```

Rodar o modelo

```bash
ollama run qwen3
```




### ✅ Observações

- O container é temporário (--rm), ou seja, será removido automaticamente ao encerrar.
- Todos os arquivos gerados pelo notebook serão salvos na pasta local output/.
- Em caso de erro para fazer o pull da imagem python:3.11, rodar o seguinte comando:

```bash
docker pull python:3.11
```


### 📘 Pronto!

Agora você pode abrir o Jupyter Notebook e seguir as instruções do laboratório.




