# Identificação de Vírus de Alto Risco

Solução de classificação binária pra identificar vírus de alto risco com potencial de impacto em saúde pública, a partir de informações biológicas e epidemiológicas.


## Estrutura do repositório

```
├── Apresentacao/
│   └── resumo_executivo.md       # Resumo executivo pra gestores
├── data/
│   ├── raw/                      # Dados originais fornecidos
│   └── processed/                # Dataset tratado e pronto pra modelagem
├── notebooks/
│   ├── EDA_Tratamento.ipynb      # Análise exploratória e tratamento dos dados
│   └── Modelagem.ipynb           # Construção e avaliação dos modelos
├── requirements.txt
└── README.md
```

## Como executar

### Pré-requisitos

- Python 3.11
- pip

### Passo a passo

1. Clone o repositório:

```bash
git clone https://github.com/kenedysilva27/virus-risk.git
cd virus-risk
```

2. Crie e ative um ambiente virtual:

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# Linux/Mac
source .venv/bin/activate
```

3. Instale as dependências:

```bash
pip install -r requirements.txt
```

4. Execute os notebooks na ordem:

   - `notebooks/EDA_Tratamento.ipynb` — faz a análise exploratória, limpeza e gera o dataset processado em `data/processed/`
   - `notebooks/Modelagem.ipynb` — usa o dataset processado pra treinar e avaliar os modelos

## Resumo da solução

- **Problema**: classificação binária de vírus em alto risco (1) ou não alto risco (0)
- **Base**: 70 vírus catalogados, com forte desbalanceamento (apenas 2 de alto risco)
- **Modelo final**: regressão logística com class_weight='balanced' e RandomOverSampler, validado com cross-validation estratificada
- **Resultado**: recall de 100% na classe positiva (identificou os 2 vírus de alto risco), com 1 falso positivo que corresponde a um registro com suspeita de erro de rotulagem

Detalhes completos e considerações pra gestão em `Apresentacao/resumo_executivo.md`.