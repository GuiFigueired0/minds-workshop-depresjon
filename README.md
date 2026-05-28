# Identificação e Análise de Dias Depressivos a Partir da Classificação em Séries Temporais de Atividade Motora

Repositório de código do artigo **"Identificação e Análise de Dias Depressivos a Partir da Classificação em Séries Temporais de Atividade Motora"**, apresentado no *I Workshop MinDS (Mining Digital and Social Signals for Public Health) – SBCAS 2026*.

**Autores:** Guilherme A. Rocha de Figueiredo, Julio C. S. Reis  
**Instituição:** Departamento de Informática – Universidade Federal de Viçosa (UFV)

---

## Sobre o trabalho

A depressão é um dos maiores problemas de saúde pública global, e seu diagnóstico ainda depende fortemente de avaliações clínicas subjetivas. Este trabalho investiga o uso de diferentes classificadores de séries temporais para identificar dias depressivos a partir da análise da atividade motora diária, coletada por dados de actigrafia, de pacientes com e sem diagnóstico clínico da doença.

Para isso, foram avaliados seis classificadores representantes de famílias canônicas de séries temporais, comparados a um modelo tabular (*Linear SVC*) como linha de base. Os resultados mostram que algoritmos baseados em séries temporais superam a abordagem tabular em métricas globais, com destaque para o *Time Series Forest* (TSF), que atingiu 80,3% de acurácia. A análise qualitativa dos erros revela que as falhas são consistentes entre diferentes famílias de algoritmos e estão associadas a perfis circadianos atípicos, sugerindo que a principal barreira não é apenas computacional, mas intrínseca à complexidade biológica e ao ruído de rótulo do dado.

## Estrutura do repositório

```
.
├── data/                   # Diretório para os arquivos do dataset (ver data/README.md)
├── images/                 # Gráficos gerados e utilizados no artigo
├── JoiningDatasets.ipynb   # Pré-processamento: gera time_series.csv a partir dos CSVs brutos
├── Classification.ipynb    # Classificação e análise de erros: gera todos os resultados e figuras
├── time_series.csv         # Dataset processado (saída do JoiningDatasets.ipynb)
├── results.csv             # Predições de todos os classificadores (saída do Classification.ipynb)
└── requirements.txt        # Dependências do projeto
```

## Configuração do ambiente

```bash
python -m venv venv
source venv/bin/activate   # Linux/macOS
venv\Scripts\activate      # Windows

pip install -r requirements.txt
```

## Como reproduzir

### 1. Obtenha os dados

Baixe o conjunto de dados *Depresjon* e extraia-o dentro da pasta `data/`. Veja as instruções detalhadas em [`data/README.md`](data/README.md).

### 2. Pré-processamento

Execute o notebook [`JoiningDatasets.ipynb`](JoiningDatasets.ipynb). Ele lê os CSVs brutos de cada paciente, segmenta as séries contínuas em janelas diárias de 1.440 minutos, descarta dias incompletos e salva o resultado em `time_series.csv`.

### 3. Classificação e análise

Execute o notebook [`Classification.ipynb`](Classification.ipynb) para treinar os classificadores e gerar os resultados reportados no artigo.

> **Atenção:** o treinamento dos modelos de séries temporais é computacionalmente custoso e pode levar várias horas. Caso queira apenas explorar os resultados e as análises, carregue o `results.csv` já gerado descomentando a linha indicada no início da seção de resultados do notebook.

## Resultados

Métricas consolidadas (*Out-of-Fold*) com validação cruzada estratificada de 10 partições:

| Classificador | Família | Acurácia | MCC |
|---|---|---|---|
| Linear SVC *(baseline)* | Tabular | 67,1% | 0,321 |
| Time Series Forest | Baseado em Intervalos | **80,3%** | **0,551** |
| Arsenal | Baseado em Convolução | 77,3% | 0,482 |
| Shapelet Transform | Baseado em Subsequência | 78,7% | 0,507 |
| CBOSS | Baseado em Dicionário | 75,9% | 0,429 |
| Catch22 | Baseado em Características | 74,3% | 0,398 |
| KNN com DTW | Baseado em Distância | 68,7% | 0,344 |

## Referências

- Garcia-Ceja, E. et al. (2018). *Depresjon: A Motor Activity Database of Depression Episodes in Unipolar and Bipolar Patients*. ACM Multimedia Systems Conference. — [Paper](https://dl.acm.org/doi/pdf/10.1145/3204949.3208125) · [Dataset (Zenodo)](https://zenodo.org/records/1219550) · [Dataset (Kaggle)](https://www.kaggle.com/datasets/arashnic/the-depression-dataset)
- Bagnall, A. et al. (2017). *The great time series classification bake off*. Data Mining and Knowledge Discovery, 31(3):606–660.
- Middlehurst, M. et al. (2024). *Bake off redux: a review and experimental evaluation of recent time series classification algorithms*. Data Mining and Knowledge Discovery, 38(4):1958–2031.
