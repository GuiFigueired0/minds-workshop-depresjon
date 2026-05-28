# Dados

Este diretório deve conter os arquivos do conjunto de dados *Depresjon* antes de executar os notebooks.

## Sobre o conjunto de dados

O *Depresjon* é uma base pública de registros de actigrafia coletados de 55 indivíduos — 23 com diagnóstico clínico de depressão (unipolar ou bipolar) e 32 controles saudáveis. Os dados foram obtidos ao longo de pelo menos duas semanas com um actígrafo de pulso no braço direito, registrando a atividade motora minuto a minuto.

> Garcia-Ceja, E. et al. (2018). *Depresjon: A Motor Activity Database of Depression Episodes in Unipolar and Bipolar Patients*. ACM Multimedia Systems Conference.

## Como obter os dados

Baixe os arquivos em um dos repositórios abaixo e extraia o conteúdo diretamente nesta pasta (`data/`):

- **Zenodo:** https://zenodo.org/records/1219550
- **Kaggle:** https://www.kaggle.com/datasets/arashnic/the-depression-dataset

## Estrutura esperada

Após a extração, a pasta deve conter:

```
data/
├── condition/          # Séries temporais dos pacientes diagnosticados (condition_1.csv … condition_23.csv)
├── control/            # Séries temporais dos indivíduos saudáveis (control_1.csv … control_32.csv)
└── scores.csv          # Metadados clínicos dos participantes (diagnóstico, MADRS, dados demográficos)
```
