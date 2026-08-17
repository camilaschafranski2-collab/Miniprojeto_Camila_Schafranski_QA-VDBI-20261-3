# Mini-Projeto Avaliativo - Visualização de Dados e BI (T3)

## Identificação
- Nome do aluno: Camila Schafranski
- Turma: QA VDBI 2026/1 3
- Projeto: Miniprojeto_Camila_Schafranski_Turma

## Objetivo
Realizar uma Análise Exploratória de Dados (AED) na base de varejo, aplicando etapas de importação, validação, limpeza, estatística descritiva e agrupamentos para geração de insights operacionais.

## Estrutura de arquivos
- `Miniprojeto_AnaliseVarejo.py`: script principal da solução.
- `data/raw/`: pasta da base original (o script detecta automaticamente o CSV bruto, mesmo com nome diferente).
- `data/processed/df_limpo.csv`: base tratada gerada pelo script.

## Como executar
1. Abra o projeto no VS Code.
2. Instale a dependência:
   ```bash
   python -m pip install pandas
   ```
3. Execute o script:
   ```bash
   python Miniprojeto_AnaliseVarejo.py
   ```
4. O relatório será exibido no terminal e o arquivo `data/processed/df_limpo.csv` será gerado automaticamente.
5. Se o nome do CSV original for diferente, não é necessário alterar o código: basta manter o arquivo dentro de `data/raw/`.

## Etapas implementadas (alinhadas ao desafio)
1. Leitura estruturada com `csv.DictReader` e leitura analítica com `pandas.read_csv()`.
2. Verificação de problemas: nulos por coluna, duplicatas completas, datas inválidas e categorias vazias.
3. Limpeza mínima:
   - Remoção de colunas totalmente nulas (colunas extras `Unnamed`).
   - Preenchimento condicional de categorias vazias com `Sem Categoria`.
   - Conversão de tipos (`DATA` para datetime e `CL_FHL` para numérico).
   - Tratamento condicional de dimensões físicas quando disponíveis.
   - Remoção de duplicatas completas.
4. Estatísticas descritivas da coluna `CL_FHL`:
   - média, mediana, desvio padrão, moda, máximo, mínimo e contagem.
5. Agrupamentos com `groupby()`:
   - Vendas/compras por gênero.
   - Top categorias por volume de itens.
   - Evolução mensal (extra).
6. Validação da regra de negócio do identificador `CO_ID`:
   - verificação de consistência de cliente e data por compra.

## Reflexão teórica (ETL e qualidade de dados)
- Em ETL, a extração não garante qualidade dos dados; por isso, a etapa de transformação deve incluir validações explícitas (tipos, nulos, duplicatas e inconsistências de negócio).
- A presença de colunas totalmente nulas mostrou a importância do saneamento estrutural antes das análises.
- A deduplicação teve impacto direto no resultado analítico, reduzindo risco de superestimar volume de vendas.
- Conversão correta de datas é essencial para análises temporais e para evitar agregações incorretas por período.
- Regras de negócio (como consistência do `CO_ID`) complementam checagens técnicas, aumentando confiabilidade dos indicadores.

## Principais insights (3-6 tópicos)
- A base inicial possuía **830.000 registros** e **4 colunas totalmente nulas**, removidas na limpeza.
- Foram removidas **96.553 duplicatas**, resultando em **733.447 registros válidos**.
- A coluna de filhos (`CL_FHL`) mostrou **moda = 0** e **média = 1,146**, indicando predominância de clientes sem filhos.
- O gênero **F** apresentou maior volume de itens e maior quantidade de compras únicas que o gênero **M**.
- **ALIMENTOS** foi a categoria com maior volume de itens vendidos, seguida por **HIGIENE** e **LIMPEZA**.
- Limitação remanescente: a base não contém valor monetário de venda, impedindo análises de faturamento e ticket médio.
