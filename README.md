# Análise de Sentimento de Tweets

Este projeto realiza uma análise de sentimento em um conjunto de dados de tweets. Utilizamos várias bibliotecas de Python para manipulação de dados, processamento de texto e visualização de dados. A análise de sentimento é realizada utilizando a biblioteca `TextBlob`.

## Estrutura do Projeto

- **Tweets.csv**: Arquivo CSV contendo os dados dos tweets.
- **analyze_sentiment.py**: Script Python que realiza a análise de sentimento e plota os resultados.
- **README.md**: Documento explicativo do projeto.

## Dependências

- Python 3.x
- Pandas
- Numpy
- Matplotlib
- Seaborn
- TextBlob
- NLTK

## Instalação

1. Clone este repositório:
    ```bash
    git clone https://github.com/seu-usuario/analise-sentimento-tweets.git
    ```

2. Navegue até o diretório do projeto:
    ```bash
    cd analise-sentimento-tweets
    ```

3. Instale as dependências:
    ```bash
    pip install pandas numpy matplotlib seaborn textblob nltk
    ```

4. Baixe os recursos necessários do NLTK:
    ```python
    import nltk
    nltk.download('punkt')
    ```

## Uso

1. Coloque o arquivo `Tweets.csv` no diretório do projeto.
2. Execute o script de análise de sentimento:
    ```bash
    python analyze_sentiment.py
    ```
3. O script irá carregar o dataset, limpar o texto dos tweets, realizar a análise de sentimento e exibir um gráfico de barras mostrando a distribuição dos sentimentos.

## Estrutura do Script

- **Carregamento e inspeção dos dados**:
    Utilizamos a biblioteca `Pandas` para carregar e inspecionar o dataset.
    ```python
    df = pd.read_csv('Tweets.csv')
    ```

- **Pré-processamento de texto**:
    Limpeza e preparação do texto usando `NLTK`.
    ```python
    def clean_text(text):
        text = text.lower()
        text = nltk.RegexpTokenizer(r'\w+').tokenize(text)
        text = " ".join(text)
        return text
    df['clean_text'] = df['text'].apply(clean_text)
    ```

- **Análise de Sentimento**:
    Utilizamos `TextBlob` para realizar a análise de sentimento dos tweets.
    ```python
    def get_sentiment(text):
        analysis = TextBlob(text)
        return analysis.sentiment.polarity
    df['sentiment'] = df['clean_text'].apply(get_sentiment)
    ```

- **Classificação dos Sentimentos**:
    Classificamos os sentimentos em positivo, negativo e neutro.
    ```python
    def classify_sentiment(polarity):
        if polarity > 0:
            return 'positive'
        elif polarity < 0:
            return 'negative'
        else:
            return 'neutral'
    df['sentiment_class'] = df['sentiment'].apply(classify_sentiment)
    ```

- **Visualização dos dados**:
    Utilizamos `Matplotlib` e `Seaborn` para criar gráficos de visualização.
    ```python
    sentiment_counts = df['sentiment_class'].value_counts()
    plt.figure(figsize=(10, 6))
    sns.barplot(x=sentiment_counts.index, y=sentiment_counts.values, palette='viridis')
    plt.title('Distribuição dos Sentimentos')
    plt.xlabel('Sentimento')
    plt.ylabel('Contagem')
    plt.show()
    ```

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

## Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo `LICENSE` para mais detalhes.