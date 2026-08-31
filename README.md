# Mineração de Dados — Regras de Associação no dataset *Supermarket*

Projeto acadêmico da disciplina **Mineração e Visualização de Dados**, do curso de **Ciências de Dados & IA** da **PUC-Campinas**.

O trabalho aplica o algoritmo **Apriori** sobre o dataset *Supermarket* para extrair regras de associação fortes entre categorias de produtos e, a partir delas, propor intervenções comerciais para um supermercado.

---

## Objetivo

Identificar padrões de compra conjunta em transações reais de supermercado e transformar esses padrões em recomendações acionáveis de layout e sortimento de loja.

O trabalho se divide em duas frentes:

- **Preparação dos dados (Python / Google Colab)** → conversão do formato `.arff`, inspeção de valores ausentes e remoção de colunas sem informação útil.
- **Mineração e análise (WEKA)** → execução do Apriori com diferentes configurações de parâmetros, seleção das regras estatisticamente relevantes e interpretação de negócio de cada uma.

---

## Dataset

- **Nome:** Supermarket
- **Formato original:** `.arff` (formato nativo do WEKA)
- **Natureza:** dados transacionais binários — cada linha é uma compra, cada coluna indica se determinada categoria de produto esteve presente (`t`) ou ausente (`?`)

---

## Ferramentas

- **Google Colab** → ambiente de execução do notebook, sem necessidade de configuração local
- **Python 3** → linguagem da etapa de preparação
- **pandas** → manipulação do DataFrame, tratamento de ausentes e exportação para CSV
- **NumPy** → operações auxiliares de array e verificação de valores nulos
- **SciPy (`scipy.io.arff`)** → leitura do arquivo `.arff` original
- **WEKA** → execução do algoritmo Apriori e cálculo das métricas de associação

---

## Pipeline do projeto

1. **Carregamento** → o arquivo `supermarket.arff` é lido com `loadarff` e convertido em um DataFrame pandas.
2. **Exportação intermediária** → o DataFrame é salvo como `supermarket.csv`.
3. **Tratamento de ausentes** → o CSV é relido com `na_values=['?']`, de modo que as ausências passem a ser reconhecidas como `NaN`.
4. **Remoção de colunas vazias** → colunas em que *todos* os registros são nulos são identificadas e descartadas, pois não contribuem para nenhuma regra.
5. **Remoção das colunas `department`** → colunas agregadoras iniciadas por `depart` são removidas para que a análise se concentre em categorias de produto específicas.
6. **Exportação final** → o resultado é salvo como `supermarket_filtrado.csv`, base usada na etapa seguinte.
7. **Mineração no WEKA** → o dataset tratado é submetido ao Apriori sob diferentes combinações de parâmetros até a obtenção de regras fortes.

---

## Metodologia no WEKA

O Apriori foi executado em múltiplas tentativas, variando os parâmetros de suporte mínimo, métrica de avaliação e número de regras retornadas. Configurações muito restritivas não retornaram nenhuma regra; configurações muito permissivas retornaram regras triviais. As tentativas e seus resultados estão documentados no relatório.

Parâmetros ajustados a cada execução:

- `lowerBoundMinSupport` → suporte mínimo aceito
- `upperBoundMinSupport` → suporte máximo aceito
- `metricType` → métrica de ordenação (Leverage ou Lift)
- `minMetric` → valor mínimo da métrica escolhida
- `numRules` → quantidade de regras retornadas

Observação metodológica: em parte das análises a coluna `total` foi temporariamente excluída, por dominar as associações sem agregar interpretação de negócio.

---

## Métricas de avaliação

- **Suporte** → frequência com que o conjunto de itens aparece no total de transações
- **Confiança** → probabilidade de o consequente ocorrer dado que o antecedente ocorreu
- **Lift** → quanto a associação supera a frequência esperada sob independência; acima de 1 indica relação positiva
- **Leverage** → diferença entre a co-ocorrência observada e a esperada pelo acaso
- **Convicção** → grau de dependência do consequente em relação ao antecedente

---

## Regras selecionadas

Três regras foram escolhidas como fortes, cada uma acompanhada de um cenário de consumo e de uma proposta de intervenção comercial:

- **Biscoitos + Vegetais → Frutas** → confiança 0,80 | lift 1,24 | leverage 0,06
- **Pão e bolo + Biscoitos → Comidas congeladas** → confiança 0,72 | lift 1,23 | leverage 0,06
- **Sucos + Biscoitos → Lanches de festa** → confiança 0,69 | lift 1,38 | leverage 0,06

A análise completa de cada regra, com a hipótese de comportamento do consumidor e a intervenção sugerida ao supermercado, está no relatório em `docs/`.

---

## Estrutura

- `notebooks/` → notebook do Google Colab com toda a etapa de preparação dos dados
- `data/raw/` → dataset original em `.arff`
- `data/processed/` → dataset tratado, pronto para o WEKA
- `docs/` → relatório final em PDF com as regras, cenários e intervenções
- `weka/` → configurações do Apriori utilizadas e capturas das execuções

---

## Como reproduzir

1. Abrir `notebooks/MD_Supermarket_Trabalho.ipynb` no Google Colab.
2. Fazer upload de `data/raw/supermarket.arff` para o diretório `/content` do ambiente.
3. Executar as células na ordem — o notebook gera `supermarket_filtrado.csv`.
4. Abrir o arquivo gerado no WEKA Explorer.
5. Na aba *Associate*, selecionar o algoritmo **Apriori** e aplicar os parâmetros descritos em `weka/configs.md`.

---

## Autores

Trabalho desenvolvido em grupo:

- Caio de Moraes — [LinkedIn](https://linkedin.com/in/moraes-caio)
- Diego Pavan
- Fernando Mattar Modenese
- Lucas Queiroz da Silva

Orientação: Prof. Fernando — PUC-Campinas
