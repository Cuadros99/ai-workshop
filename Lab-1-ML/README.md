# 🧠 AI Workshop – Laboratório de Machine Learning

Este ambiente contém o notebook do laboratório de aprendizado de máquina.  
Siga as instruções abaixo para **construir e executar** o container Docker com o Jupyter Notebook.

---

## 🎲 1. Baixar dataset

Baixar o dataset no link https://www.kaggle.com/datasets/solarmainframe/ids-intrusion-csv?select=02-15-2018.csv

Armazená-lo na pasta dataset

```bash
mkdir dataset
```


## 🧱 2. Construir a imagem

No terminal, dentro da pasta do projeto, execute:

```bash
sudo docker build -t lab-1-image .
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
  --name lab-1-container \
  -p 8888:8888 \
  --memory="7g" \
  -v "$(pwd)/output":/app/output \
  lab-1-image
```

## 📊 5. Acessar o Jupyter Notebook

Após o container iniciar, o terminal exibirá uma URL parecida com:

```bash
http://127.0.0.1:8888/?token=<seu_token_aqui>
```

## 🧩 6. (Opcional) Monitorar o uso de recursos

Para verificar o consumo de CPU e memória dentro do container:

```bash
sudo docker exec -it lab-1-container /bin/bash
htop
```

## ✅ Observações

- O container é temporário (--rm), ou seja, será removido automaticamente ao encerrar.
- Todos os arquivos gerados pelo notebook serão salvos na pasta local output/.

## 📘 Pronto!

Agora você pode abrir o Jupyter Notebook e seguir as instruções do laboratório.


