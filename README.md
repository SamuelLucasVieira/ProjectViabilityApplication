# Aplicativo de Viabilidade de Projetos

Este aplicativo simples usa regressão logística para avaliar a viabilidade de projetos com base em três características principais: valor do investimento, retorno esperado e pontuação de impacto. Você pode treinar o modelo com dados históricos de projetos e prever a viabilidade e a probabilidade de sucesso de novas propostas de projeto.

## Funcionalidades

* **Treino e Avaliação do Modelo**: Treine um modelo de regressão logística usando o scikit-learn e avalie seu desempenho com métricas de classificação.
* **Escalonamento de Características**: Padronize as variáveis de entrada (`investment`, `expected_return`, `impact_score`) usando `StandardScaler`.
* **Persistência**: Salve e carregue o modelo treinado, o escalonador e as métricas de avaliação com `joblib`.
* **API de Previsão**: Use a função `train_or_predict()` para treinar o modelo ou prever viabilidade de novos projetos.

## Instalação

1. **Clone o repositório**:

   ```bash
   git clone https://github.com/SamuelLucasVieira/ProjectViabilityApplication.git
   cd ProjectViabilityApplication
   ```
2. **Crie um ambiente virtual e instale as dependências**:

   ```bash
   python3 -m venv venv
   source venv/bin/activate    # No Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

## Uso

### 1. Treinando o Modelo

Execute a etapa de treinamento (sem novos projetos para prever):

```python
from viability import train_or_predict

# Treina o modelo e retorna métricas de avaliação
default_predictions, metrics = train_or_predict(new_projects=None)
print("Métricas de Avaliação do Modelo:")
print(metrics)
```

### 2. Prevendo Novos Projetos

Forneça uma lista de dicionários de projetos para receber previsões de viabilidade e probabilidades:

```python
from viability import train_or_predict

new_projects = [
    {"investment": 40000, "expected_return": 60000, "impact_score": 6},
    {"investment": 25000, "expected_return": 50000, "impact_score": 8},
]
predictions, metrics = train_or_predict(new_projects)
print("Previsões para Novos Projetos:")
print(predictions)
print("Métricas de Avaliação do Modelo:")
print(metrics)
```

## Dados

* **`projects_data.csv`**: Conjunto de dados históricos contendo:

  * `investment` (numérico)
  * `expected_return` (numérico)
  * `impact_score` (numérico)
  * `viability` (0 para não viável, 1 para viável)

Certifique-se de que este arquivo esteja na raiz do projeto antes de executar o treinamento.

## Metodologia

1. **Carregar Dados**: Leia `projects_data.csv` em um DataFrame do pandas.
2. **Seleção de Características**: Extraia as variáveis numéricas e a variável-alvo.
3. **Pré-processamento**: Padronize as características com `StandardScaler`.
4. **Treinamento do Modelo**:

   * Divida os dados em conjuntos de treino e teste usando `train_test_split`.
   * Treine um classificador `LogisticRegression`.
5. **Avaliação**: Gere um relatório de classificação com precisão, recall e F1-score.
6. **Persistência**: Salve o modelo treinado, o escalonador e as métricas para uso posterior.
7. **Previsão**: Carregue os artefatos salvos para prever a viabilidade e a probabilidade de novos projetos.

## Requisitos

* Python 3.7 ou superior
* pandas
* scikit-learn
* joblib

Instale todas as dependências Python via:

```bash
pip install -r requirements.txt
```

## Melhorias Futuras

* Adicionar validação cruzada e ajuste de hiperparâmetros (por exemplo, `GridSearchCV`).
* Implementar uma interface web ou CLI para facilitar a interação.
* Expandir o conjunto de características com mais atributos do projeto (por exemplo, duração, tamanho da equipe).
* Fornecer visualização de curvas ROC e métricas de desempenho.

## Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
