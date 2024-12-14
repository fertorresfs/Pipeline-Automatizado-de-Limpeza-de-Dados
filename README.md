# Pipeline Automatizado de Limpeza de Dados

Este projeto implementa um pipeline para automatizar a limpeza de dados em conjuntos de dados brutos. O pipeline inclui as seguintes etapas:

* **Carregamento de dados:** Lê dados de um arquivo CSV.
* **Tratamento de valores ausentes:** Remove linhas com valores ausentes ou preenche com a média das colunas numéricas.
* **Formatação de dados:** Converte colunas para os tipos de dados corretos (data, categórico).
* **Detecção de outliers:** Identifica e remove outliers em colunas numéricas usando o Z-score.

## Uso

1.  **Instalação:** Certifique-se de ter as bibliotecas necessárias instaladas (`pandas`, `numpy`).
2.  **Configuração:** Substitua `'seu_arquivo.csv'` pelo caminho do seu arquivo de dados.
3.  **Execução:** Execute o notebook `pipeline_limpeza_dados.ipynb`.
4.  **Saída:** Os dados limpos serão salvos em `dados_limpos.csv`.  Um arquivo de log (`limpeza_dados.log`) registrará as ações realizadas e eventuais erros.

## Funcionalidades

* **`carregar_dados(caminho_arquivo)`:** Carrega os dados de um arquivo CSV.
* **`tratar_valores_ausentes(df, estrategia='remover_linhas')`:**  Trata valores ausentes usando a estratégia especificada.
* **`formatar_dados(df, colunas_data=None, colunas_categoricas=None)`:** Formata colunas de data e categóricas.
* **`detectar_outliers(df, colunas_numericas, metodo='zscore', limiar=3)`:** Detecta e remove outliers.

## Próximos passos

* Implementar mais métodos para tratamento de outliers (IQR).
* Adicionar mais estratégias para tratamento de valores ausentes (mediana, moda, imputação).
* Criar testes unitários para garantir a qualidade do código.
* Implementar tratamento de erros mais robusto.

## Melhorias

* **Validação de tipo de dado:** Implementar verificações para garantir que as colunas tenham o tipo de dado esperado (int, float, string, data, etc.).
* **Tratamento de dados inconsistentes:** Adicionar lógica para lidar com dados inconsistentes, como diferentes formatos de data ou separadores decimais.
* **Normalização/Padronização:** Incluir opções para normalizar ou padronizar dados numéricos.
* **Limpeza de texto:** Adicionar funções para limpar texto, como remover pontuação, converter para minúsculas, remover stop words, etc. (se aplicável).
* **Relatório de limpeza:** Gerar um relatório resumindo as ações de limpeza realizadas, como o número de valores ausentes removidos, outliers detectados, etc.

## Autor
Fernando Torres Ferreira da Silva
fernando-torres@live.com
