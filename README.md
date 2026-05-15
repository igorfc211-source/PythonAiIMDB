# 🎬 Sistema de Recomendação de Filmes com Gemini + FuzzyWuzzy

## 📌 Visão Geral

Este projeto implementa um sistema inteligente de recomendação de filmes utilizando:

- **Python**
- **Pandas**
- **KaggleHub**
- **FuzzyWuzzy**
- **Gemini LLM (Google AI)**

O sistema permite que o usuário digite nomes aproximados de filmes e, com base nas escolhas, gera recomendações automáticas utilizando:

1. Similaridade textual (`Fuzzy Matching`)
2. Gêneros favoritos
3. Média de avaliações (`score`)
4. Recomendações contextuais via LLM Gemini

---

## 🚀 Funcionalidades

- Download automático do dataset de filmes via KaggleHub
- Busca aproximada de nomes de filmes usando FuzzyWuzzy
- Correção de erros de digitação
- Recomendações automáticas baseadas em:
  - gênero
  - score
- Recomendações avançadas usando IA generativa (Gemini)
- Integração com variáveis de ambiente para segurança da API Key

---

## 🛠 Tecnologias Utilizadas

| Tecnologia | Função |
|---|---|
| Python | Linguagem principal |
| Pandas | Manipulação de dados |
| KaggleHub | Download do dataset |
| FuzzyWuzzy | Similaridade textual |
| Gemini API | Recomendações inteligentes |
| Google Colab | Ambiente de execução |

---

## 📂 Dataset Utilizado

Dataset do Kaggle:

- Dataset: `danielgrijalvas/movies`

Contém informações como:

- Nome do filme
- Ano
- Gênero
- Avaliação (`score`)

---

## 📦 Instalação das Dependências

```bash
pip install kagglehub pandas fuzzywuzzy googletrans==4.0.0-rc1

## 🔐 Configuração da API Gemini

A chave da API é armazenada usando variáveis de ambiente do Google Colab.

from google.colab import userdata
import os

os.environ["GOOGLE_API_KEY"] = userdata.get('ImdbAPI')

)

## 📥 Download do Dataset
import kagglehub

path = kagglehub.dataset_download("danielgrijalvas/movies")

## 📊 Carregamento do Dataset
import pandas as pd

df = pd.read_csv(f"{path}/movies.csv")

## 🧹 Seleção das Colunas

O projeto utiliza apenas as colunas relevantes para recomendação.

df_filmes = df[['year', 'name', 'genre', 'score']]

## Colunas Utilizadas
Coluna

- Descrição
- year	Ano do filme
- name	Nome do filme
- genre	Gênero
- score	Avaliação

print("Path to dataset files:", path)


## 🔎 Busca Aproximada com FuzzyWuzzy

O usuário pode digitar o nome do filme mesmo com erros de escrita.

from fuzzywuzzy import process

resultados = process.extract(
    consulta,
    df_filmes["name"].tolist(),
    limit=5
)

## 👤 Entrada do Usuário

O sistema solicita 4 filmes ao usuário.

entrada = []

for i in range(4):
    consulta = input(f"Digite o nome do filme {i+1}: ")

## 🎯 Seleção Inteligente

O sistema apresenta as opções mais parecidas.

Exemplo:

1. Rocky III
2. Rock & Rule
3. Body Rock
4. Rocky IV

O usuário escolhe o filme correto pelo índice.

## 🧠 Processamento das Preferências

Após selecionar os filmes:

os gêneros favoritos são identificados
a média de score é calculada
perfil = df_filmes[df_filmes["name"].isin(filmes_escolhidos)]

generos_preferidos = perfil["genre"].value_counts().index.tolist()
score_medio = perfil["score"].mean()

## 🎬 Recomendações Automáticas

O sistema filtra:

filmes do mesmo gênero
score maior ou igual à média
filmes ainda não escolhidos
recomendados = df_filmes[
    (~df_filmes["name"].isin(filmes_escolhidos)) &
    (df_filmes["genre"].isin(generos_preferidos)) &
    (df_filmes["score"] >= score_medio)
].sort_values(by="score", ascending=False)

)

## 🤖 Recomendações com Gemini

O projeto utiliza uma LLM Gemini para gerar recomendações mais contextuais.

Critérios utilizados pela IA
gênero
diretor
ano
estilo do filme
contexto narrativo

## 📨 Prompt Enviado ao Gemini
prompt = f"""
Sou um sistema de recomendação de filmes.

O usuário escolheu os filmes:
{', '.join(filmes_escolhidos)}.

Com base nesses títulos, recomende 10 filmes
que o usuário provavelmente vai gostar.
"""

## ⚡ Chamada da API Gemini

from google import genai

client = genai.Client()

chat = client.chats.create(
    model="gemini-2.5-flash"
)

resposta = chat.send_message(prompt)

## 📌 Exemplo de Saída
Recomendações automáticas
The Shawshank Redemption
Fight Club
Forrest Gump
Parasite
Cinema Paradiso
Recomendações do Gemini
1. Laços de Ternura - Drama
2. Flashdance - Romance
3. Rain Man - Drama
4. Instinto Selvagem - Thriller

## 🔄 Fluxo do Sistema
Usuário digita filme
        ↓
FuzzyWuzzy encontra similares
        ↓
Usuário escolhe o correto
        ↓
Sistema identifica preferências
        ↓
Recomendação automática
        ↓
Gemini gera recomendações inteligentes

## 📈 Possíveis Melhorias

-Interface gráfica
-API REST
-Recomendações por ator/diretor
-Sistema de usuários
-Histórico de recomendações
-Machine Learning com embeddings
-Banco de dados para persistência
-Deploy online
## 📚 Conceitos Aplicados

- NLP (Natural Language Processing)
- Fuzzy Matching
- Recomendação baseada em conteúdo
- IA Generativa
- Manipulação de datasets
- Engenharia de Prompt

## 👨‍💻 Autor

Projeto desenvolvido para estudos de:

Inteligência Artificial
Sistemas de Recomendação
Integração com LLMs
Ciência de Dados
