# 🛡️ Pipeline ELT de Conformidade OFAC: Consolidação de Listas de Sanções (SDN, ADD, ALT)

## 📖 Descrição do Projeto

Este projeto implementa um Pipeline **ELT (Extract, Load, Transform)** de nível profissional, desenvolvido em Python e Pandas, para consumir e consolidar as principais listas de sanções do **Office of Foreign Assets Control (OFAC)**.

O objetivo é transformar os dados brutos, distribuídos em múltiplos arquivos CSV (formato legado via API), em um **Dataset de Conformidade** único e limpo. Isso é essencial para sistemas de *screening* e diligência devida (Due Diligence).

### 🎯 Funcionalidades e Foco em Qualidade de Dados

O pipeline garante a fidelidade dos dados e a aderência às regras específicas da OFAC:

* **Extração e Mesclagem Relacional:** Consome `SDN.CSV`, `ADD.CSV` (Endereços) e `ALT.CSV` (Aliases Fortes) e os une usando a chave primária `ent_num`.
* **Tratamento de Nulos Legados:** Corrige o valor nulo específico da OFAC (`"-0-"`) e o trata como `NaN` durante a ingestão.
* **Tratamento de Aliases Críticos:** Implementa a lógica de RegEx para extrair e padronizar os **"Weak Aliases"** (Aliases Fracos) da coluna `Remarks`, consolidando-os com os Aliases Fortes do `ALT.CSV`.
* **Limpeza e Outliers:** Garante a tipagem correta das colunas (Numérico/Categórico) e utiliza o método **IQR (Interquartile Range)** para detecção e remoção de *outliers* em colunas de medição (e.g., `Tonnage`, `GRT`).
* **Relatório de Qualidade (DQR):** Gera um relatório final que quantifica o impacto da limpeza e o *ratio* de consolidação dos dados.

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python
* **ELT/Processamento:** Pandas, NumPy
* **Conexão Externa:** `requests` (para API da OFAC)
* **Qualidade/Logística:** `logging`, `re` (Regex)

### Requisitos

Certifique-se de que as bibliotecas necessárias estejam instaladas:

```bash
pip install pandas numpy requests
```
📂 Estrutura do Projeto
A execução do pipeline no formato de notebook gerará os seguintes arquivos no diretório configurado:
```bash
/seu_diretorio_de_trabalho
├── pipeline_ofac.ipynb  # Notebook principal (código-fonte)
├── dados_conformidade_ofac_consolidado.csv  # ⬅️ OUTPUT: Base de Dados Consolidada e Limpa
└── /caminho/do/seu/log/
    └── pipeline_ofac.log  # Logs detalhados de cada etapa do processamento
```
🚀 Guia de Execução
1. Configuração do Ambiente e Log:O projeto utiliza um caminho absoluto para o arquivo de log. Antes de executar, localize e ajuste a variável LOG_FILE na primeira célula do seu notebook para um caminho acessível no seu sistema.

```bash
PythonLOG_FILE = '/content/drive/MyDrive/Pipelines/CSNU/log/pipeline_ofac.log' 
# ^^^ ALTE ESTE CAMINHO PARA UM LOCAL VÁLIDO ^^^
```

2. Execução do Pipeline:Execute todas as células sequencialmente no pipeline_ofac.ipynb. O pipeline fará o download dos três arquivos, executará as etapas de limpeza e mesclagem, e gerará o relatório.
3. Verificação dos Resultados:O console exibirá o Relatório de Qualidade e Consolidação detalhando as estatísticas do ent_num, a média de endereços/aliases por entidade e as linhas descartadas.O arquivo dados_conformidade_ofac_consolidado.csv será salvo, contendo todas as 23.888+ linhas consolidadas e limpas.

🔑 Chaves de Conformidade no OutputAs colunas mais importantes para o screening no arquivo final são:
Coluna Fonte OriginalDescriçãoent_numSDN, ADD, ALTID Único de Ligação.SDN_Name_CleanSDNNome Principal, padronizado (minúsculas).ProgramSDNSanctions Program (Ex: CUBA, IRAN, NPWMD).CountryADDPaís do Endereço (permite busca por jurisdição).Weak_Aliases_CleanSDN (Remarks)Aliases Fracos (nicknames, abreviações comuns), extraídos via RegEx.Strong_Aliases_CleanALTAliases Fortes (AKA, FKA) agregados em uma lista.

Autor: Fernando Torres Ferreira da Silva | fernando-torres@live.com
