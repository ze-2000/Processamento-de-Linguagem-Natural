# Processamento-de-Linguagem-Natural

 Ubirajara – Lenda Tupi, de José de Alencar
Nota: O conteúdo completo do livro foi extraído do Projeto Gutenberg e está em domínio público. Como ele é extenso, para facilitar, você pode colar apenas trechos relevantes no seu código Python, ou carregar o arquivo Ubirajara.txt no Google Colab.

🧪 Passo a Passo Detalhado – Análise de Texto com Python (Google Colab)
Este guia te ajudará a analisar o conteúdo textual de Ubirajara usando técnicas básicas de Processamento de Linguagem Natural (PLN) em Python.

✅ Etapa 1 – Leitura do Arquivo
Objetivo: Carregar o conteúdo do livro de um arquivo .txt.

python
Copiar
Editar
def ler_arquivo(caminho):
    try:
        with open(caminho, 'r', encoding='utf-8') as arquivo:
            return arquivo.read()
    except FileNotFoundError:
        print("Arquivo não encontrado.")
        return ""
🔸 Exemplo de uso:

python
Copiar
Editar
texto = ler_arquivo("Ubirajara.txt")
print(texto[:1000])  # Exibe os primeiros 1000 caracteres
🔍 Etapa 2 – Buscador de Palavras com Contexto
Objetivo: Buscar uma palavra no texto, exibindo um trecho ao redor como contexto.

python
Copiar
Editar
def buscar_palavra(texto, palavra, contexto=40):
    texto_lower = texto.lower()
    palavra_lower = palavra.lower()
    ocorrencias = []
    pos = texto_lower.find(palavra_lower)
    while pos != -1:
        inicio = max(0, pos - contexto)
        fim = pos + len(palavra_lower) + contexto
        trecho = texto[inicio:fim]
        ocorrencias.append(trecho)
        pos = texto_lower.find(palavra_lower, pos + 1)
    print("Total de ocorrências:", len(ocorrencias))
    return ocorrencias
🔸 Exemplo:

python
Copiar
Editar
trechos = buscar_palavra(texto, "guerreiro")
for trecho in trechos[:5]:
    print("...", trecho, "...\n")
🧹 Etapa 3 – Limpeza e Pré-processamento do Texto
Objetivo: Normalizar o texto e remover pontuações, números e stopwords (palavras comuns como “de”, “a”, “e”).

python
Copiar
Editar
import re
import nltk
from nltk.corpus import stopwords

nltk.download('stopwords')

def limpar_texto(texto):
    texto = texto.lower()
    texto = re.sub(r'[^\w\s]', '', texto)  # Remove pontuações
    palavras = texto.split()
    palavras = [p for p in palavras if p.isalpha()]  # Remove números
    palavras = [p for p in palavras if p not in stopwords.words('portuguese')]  # Remove stopwords
    return palavras
🔸 Exemplo:

python
Copiar
Editar
palavras_limpo = limpar_texto(texto)
print(palavras_limpo[:20])
📊 Etapa 4 – Análise de Frequência de Palavras
Objetivo: Contar as palavras mais frequentes no texto processado.

python
Copiar
Editar
from collections import Counter

def frequencia_palavras(lista_palavras, top_n=20):
    contador = Counter(lista_palavras)
    return contador.most_common(top_n)
🔸 Exemplo:

python
Copiar
Editar
mais_frequentes = frequencia_palavras(palavras_limpo)
for palavra, freq in mais_frequentes:
    print(f"{palavra}: {freq}")
📈 Etapa Extra – Visualização Gráfica (opcional)
Objetivo: Visualizar as palavras mais frequentes com um gráfico de barras.

python
Copiar
Editar
import matplotlib.pyplot as plt

def plotar_frequencia(palavras_freq):
    palavras, frequencias = zip(*palavras_freq)
    plt.figure(figsize=(10,6))
    plt.bar(palavras, frequencias, color='skyblue')
    plt.title("Palavras mais frequentes")
    plt.xticks(rotation=45)
    plt.show()
🔸 Exemplo:

python
Copiar
Editar
plotar_frequencia(mais_frequentes)
