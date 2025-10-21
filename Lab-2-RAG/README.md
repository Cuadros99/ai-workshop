# 🧠 AI Workshop – Laboratório de RAG

Este ambiente contém o notebook do laboratório de RAG.  
Siga as instruções abaixo para **construir e executar** o container Docker com o Jupyter Notebook.

---

## 🔒 1. Preencher .env

No terminal, dentro da pasta do projeto, execute:

```bash
mv .env-example .env
```

Agora vamos preencher o .env com a chave de API da OpenAI

```bash
nano .env
```


## 🧱 2. Construir a imagem

No terminal, dentro da pasta do projeto, execute:

```bash
sudo docker build -t lab-2-image .
```

## 📂 3. Criar a pasta de saída

Esta pasta armazenará os artefatos e resultados gerados pelo notebook.

```bash
mkdir -p output
```

## 🚀 4. Executar o container

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

## 📊 5. Acessar o Jupyter Notebook

Após o container iniciar, o terminal exibirá uma URL parecida com:

```bash
http://127.0.0.1:8888/?token=<seu_token_aqui>
```

## 🧩 6. (Opcional) Monitorar o uso de recursos

Para verificar o consumo de CPU e memória dentro do container:

```bash
sudo docker exec -it lab-2-container /bin/bash
```

```bash
htop
```

## ✅ Observações

- O container é temporário (--rm), ou seja, será removido automaticamente ao encerrar.
- Todos os arquivos gerados pelo notebook serão salvos na pasta local output/.
- Em caso de erro para fazer o pull da imagem python:3.11, rodar o seguinte comando:

```bash
docker pull python:3.11
```


## 📘 Pronto!

Agora você pode abrir o Jupyter Notebook e seguir as instruções do laboratório.


