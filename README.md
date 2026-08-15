# Projeto Final – Análise de Dados de Viagens a Serviço

## Índice

* [Sobre o Projeto](#sobre-o-projeto)
* [Objetivos](#objetivos)
* [Fonte dos Dados](#fonte-dos-dados)
* [Tecnologias Utilizadas](#tecnologias-utilizadas)
* [Arquitetura da Solução](#arquitetura-da-solução)
* [Pipeline ETL](#pipeline-etl)
* [Estrutura do Projeto](#estrutura-do-projeto)
* [Perguntas de Negócio](#perguntas-de-negócio)
* [Principais Resultados](#principais-resultados)
* [Visualizações](#visualizações)
* [Como Executar o Projeto](#como-executar-o-projeto)
* [Melhorias Futuras](#melhorias-futuras)
* [Licença](#licença)
* [Autora](#autora)

---

# Sobre o Projeto

Este projeto foi desenvolvido como requisito de avaliação da disciplina de **Análise de Dados**.

O objetivo foi construir um pipeline de ETL para extração, tratamento, modelagem e análise de dados de viagens a serviço da Administração Pública Federal, aplicando boas práticas de organização dos dados, modelagem relacional e geração de informações para apoio à tomada de decisão.

Os dados foram armazenados em um banco de dados PostgreSQL seguindo a **Arquitetura Medalhão (Raw, Silver e Gold)**, permitindo a realização de análises exploratórias e a construção de visualizações baseadas em perguntas de negócio.

---

# Objetivos

* Automatizar a extração dos dados disponibilizados em arquivo compactado (.zip);
* Realizar o tratamento e a padronização dos dados;
* Modelar o banco de dados utilizando boas práticas de integridade referencial;
* Construir um pipeline ETL organizado e reutilizável;
* Desenvolver consultas analíticas para responder perguntas de negócio;
* Produzir visualizações que auxiliem na interpretação dos resultados.

---

# Fonte dos Dados

Os dados utilizados neste projeto foram obtidos a partir do **Portal da Transparência do Governo Federal**, contendo informações sobre viagens a serviço da Administração Pública Federal.

Os dados são públicos e foram utilizados exclusivamente para fins educacionais e acadêmicos.

---

# Tecnologias Utilizadas

* Python
* PostgreSQL
* SQLAlchemy
* Pandas
* Matplotlib
* Seaborn
* Jupyter Notebook
* python-dotenv
* Git
* GitHub

---

# Arquitetura da Solução

O projeto foi estruturado seguindo a **Arquitetura Medalhão**, composta por três camadas.

---

## Camada Raw

Responsável pelo armazenamento dos dados exatamente como foram extraídos da fonte original.

Nesta etapa foram realizadas:

* extração automatizada dos arquivos;
* leitura do arquivo compactado (.zip);
* carga dos dados originais no banco de dados.

---

## Camada Silver

Responsável pela limpeza, padronização e modelagem dos dados.

Foram aplicadas as seguintes transformações:

* tratamento de valores nulos;
* conversão de tipos de dados;
* padronização de datas;
* tratamento de valores monetários;
* criação das tabelas relacionais;
* definição de chaves primárias (PK);
* definição de chaves estrangeiras (FK);
* aplicação de constraints para garantir a integridade dos dados.

---

## Camada Gold

Responsável pela consolidação das informações utilizadas nas análises.

As consultas analíticas utilizam operações como:

* JOIN;
* GROUP BY;
* SUM;
* AVG;
* COUNT;
* ORDER BY.

Essa camada fornece a base para responder às perguntas de negócio propostas.

---
# Pipeline ETL

O processamento dos dados segue as etapas abaixo:

1. Criação da estrutura do banco de dados;
2. Extração automatizada dos arquivos;
3. Carga da camada Raw;
4. Limpeza e transformação dos dados;
5. Carga da camada Silver;
6. Construção da camada Gold;
7. Análise dos dados e geração de visualizações.

---

# Estrutura do Projeto

```text
projeto-final-analise-dados/

├── README.md
├── requirements.txt
├── .gitignore
│
├── sql/
│   └── 0_criar_banco.sql
│
├── scripts/
│   ├── 1_extrair.py
│   └── 2_transformar.py
│
├── notebooks/
│   └── 3_analise.ipynb
│
├── data/
│   ├── Viagem.csv
│   ├── Trecho.csv
│   ├── Pagamento.csv
│   └── Passagem.csv
│
└── images/
```

---

# Perguntas de Negócio

Durante a etapa analítica, foram respondidas sete perguntas de negócio relacionadas aos gastos, deslocamentos e comportamento financeiro das viagens a serviço da Administração Pública Federal.

---

## 1. Quais os 5 órgãos com maior custo total em viagens?

### Insight

Foi realizado o mapeamento das unidades orçamentárias com maior desembolso acumulado em viagens durante o período analisado.

A análise permitiu identificar os órgãos que concentram a maior parcela dos custos operacionais relacionados aos deslocamentos.

### Recomendação de Negócio

Realizar auditorias internas de viabilidade nas agendas de deslocamento dos cinco principais órgãos, avaliando se os custos elevados são consequência do volume de viagens realizadas ou de valores unitários acima da média.

---

## 2. Quais os 3 destinos com maior custo médio por viagem?

### Insight

Foram identificados os destinos operacionais que apresentam as maiores médias de gasto por deslocamento realizado.

A análise demonstra quais localidades exercem maior impacto financeiro médio sobre o orçamento destinado às viagens.

### Recomendação de Negócio

Para destinos com custos médios elevados, recomenda-se implementar políticas de compra antecipada de passagens e negociação de tarifas corporativas, buscando maior eficiência na utilização dos recursos públicos.

---

## 3. Qual foi a viagem de maior duração e qual o seu custo total?

### Insight

Foi identificado o registro de deslocamento com maior quantidade contínua de dias em trânsito, considerando informações como servidor, órgão solicitante e valor total consumido.

A análise permitiu compreender o impacto financeiro de viagens prolongadas.

### Recomendação de Negócio

Avaliar alternativas para deslocamentos de longa duração, como modelos de atuação híbridos ou divisão das atividades em períodos menores, reduzindo custos relacionados a diárias.

---

## 4. Qual o tipo de pagamento com maior valor médio?

### Insight

Foi analisada a modalidade financeira responsável pelo maior valor médio por transação, considerando categorias como diárias, passagens e restituições.

A análise permitiu identificar quais tipos de pagamento apresentam maior impacto individual.

### Recomendação de Negócio

Modalidades com alto valor médio por lançamento devem possuir fluxos de aprovação com validações automáticas e auditoria contínua antes da liquidação, reduzindo riscos de inconsistências.

---

## 5. Qual o meio de transporte mais utilizado nos trechos?

### Insight

Foi identificado o modal de transporte predominante nos deslocamentos analisados, permitindo compreender o comportamento da malha de viagens.

A análise evidencia a dependência dos principais meios de transporte utilizados pela Administração Pública.

### Recomendação de Negócio

A partir da identificação dos modais mais utilizados, recomenda-se avaliar contratos corporativos e estratégias de negociação com fornecedores para aumentar a previsibilidade dos custos e buscar redução de despesas.

---
## 6. Qual UF de destino aparece em mais trechos?

### Insight

Foi realizado o levantamento das unidades federativas de destino com maior frequência de trechos registrados.

A análise permitiu identificar concentrações geográficas dos deslocamentos realizados pela Administração Pública Federal.

### Recomendação de Negócio

A concentração de viagens em determinados polos político-econômicos possibilita estratégias de negociação em escala, como contratos corporativos e planejamento antecipado de deslocamentos recorrentes, buscando maior eficiência orçamentária.

---

## 7. Qual órgão pagou mais no total de liquidações efetuadas?

### Insight

Foi identificado o órgão responsável pelo maior volume financeiro liquidado, considerando os valores registrados nos pagamentos efetuados.

A análise possibilitou compreender a distribuição dos desembolsos financeiros entre as unidades responsáveis pelos pagamentos.

### Recomendação de Negócio

O acompanhamento das unidades responsáveis pelas liquidações é fundamental para fortalecer a governança financeira, auxiliar no planejamento orçamentário e aprimorar a gestão dos recursos destinados às viagens a serviço.

---

# Principais Resultados

A análise dos dados permitiu identificar padrões relacionados aos gastos com viagens, meios de transporte utilizados, distribuição geográfica dos deslocamentos e comportamento dos pagamentos.

Os resultados demonstram como a aplicação de técnicas de ETL, modelagem relacional e análise exploratória de dados possibilita transformar dados brutos em informações úteis para apoio à tomada de decisão.

A construção das camadas Raw, Silver e Gold permitiu organizar o fluxo de dados desde a extração até a geração de informações analíticas, garantindo maior estrutura e rastreabilidade no processo.

---

# Visualizações

O projeto apresenta visualizações desenvolvidas com **Matplotlib** e **Seaborn** a partir dos dados consolidados na camada Gold.

Os gráficos foram construídos com foco em facilitar a interpretação dos resultados, utilizando:

* títulos descritivos;
* identificação dos eixos;
* legendas explicativas;
* rótulos de dados ajustados para melhorar a leitura.

As visualizações auxiliam na identificação de padrões, tendências e pontos de atenção relacionados aos custos e deslocamentos analisados.

---

# Como Executar o Projeto

## 1. Clone o repositório

```bash
git clone https://github.com/EveraldoFS/projeto-final-analise-dados.git
```

Acesse o diretório do projeto:

```bash
cd projeto-final-analise-dados
```

---

## 2. Crie um ambiente virtual

```bash
python -m venv venv
```

Ative o ambiente virtual conforme o sistema operacional utilizado.

---

## 3. Instale as dependências

```bash
pip install -r requirements.txt
```

---

## 4. Configure o arquivo `.env`

Informe os parâmetros de conexão com o banco de dados PostgreSQL.

---

## 5. Execute o projeto

Execute os arquivos na seguinte ordem:

```text
1. sql/0_criar_banco.sql

2. scripts/1_extrair.py

3. scripts/2_transformar.py

4. notebooks/3_analise.ipynb
```
---

# Controle de Versão e Organização do GitHub

O desenvolvimento do projeto foi realizado utilizando Git e GitHub como ferramentas de controle de versão.

A organização do repositório foi estruturada utilizando branches para separar as etapas de desenvolvimento, permitindo maior organização, rastreabilidade das alterações e aplicação de boas práticas de versionamento.

## Estratégia de Branches

As principais branches utilizadas no desenvolvimento foram:

- `main`: versão final e estável do projeto;
- `feature/modelagem`: desenvolvimento da estrutura do banco de dados e modelagem relacional;
- `feature/extracao`: implementação do processo de extração dos dados;
- `feature/transformacao`: desenvolvimento das etapas de limpeza e transformação;
- `feature/analise`: construção das análises exploratórias e visualizações;
- `feature/documentacao`: elaboração e atualização da documentação do projeto.

## Histórico de Desenvolvimento

Os commits foram organizados de acordo com as etapas de evolução do projeto, permitindo acompanhar a implementação das funcionalidades desde a criação da estrutura inicial até a documentação final.

Essa organização demonstra a aplicação de práticas de desenvolvimento colaborativo e gerenciamento de código utilizando Git.

---

# Melhorias Futuras

Possíveis evoluções para o projeto:

* Automatizar o pipeline ETL completo;
* Implementar testes automatizados;
* Containerizar a aplicação utilizando Docker;
* Desenvolver dashboards interativos utilizando Power BI ou Streamlit;
* Automatizar a atualização periódica dos dados.

---

# Licença

Este projeto foi desenvolvido para fins acadêmicos e educacionais.

---

# Autor

**Everaldo F S**

Projeto desenvolvido como requisito da disciplina de **Análise de Dados**, aplicando conceitos de:

* ETL;
* modelagem relacional;
* SQL;
* Python;
* análise exploratória de dados.

O projeto demonstra a aplicação de técnicas de engenharia e análise de dados para transformar dados operacionais em informações úteis para apoio à tomada de decisão.




