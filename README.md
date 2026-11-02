# SalesInsight PY — Análise e Visualização de Dados de Vendas

## Sobre o Projeto
O **SalesInsight PY** é um mini-projeto avaliativo de análise de dados de vendas desenvolvido como parte do curso de **Desenvolvimento de IA para Análise Preditiva T5 (Módulo 1 - Semana 07)**. 

O objetivo é organizar um fluxo de análise de dados que carregue, transforme, agregue e visualize um dataset de vendas, gerando insights relevantes e exportando os resultados.

---

## Perguntas de Negócio Analisadas
A necessidade é de um relatório analítico para a reunião trimestral da diretoria de uma empresa de varejo, com base em um histórico de vendas. A análise foi projetada para responder às 5 questões fundamentais exigidas no projeto (que é o que o time de negócios quer entender):
1. **Comportamento Temporal:** Como as vendas se comportam ao longo do tempo (por mês e por trimestre)?
2. **Produtos e Categorias Líderes:** Quais produtos e categorias geram maior receita?
3. **Desempenho Regional:** Quais regiões têm melhor desempenho?
4. **Segmentação de Clientes:** Quais clientes são mais valiosos (segmentação simples por faixa de gasto)?
5. **Relação Quantidade vs. Receita:** Existe relação entre a quantidade vendida e a receita gerada por transação?

---

## Conceitos e Tecnologias Aplicados (Requisitos Obrigatórios)

### Lógica e Estrutura de Código (RF01 a RF10)
- **Ingestão e Inspeção (RF01, RF02):** Carregamento de dataset de vendas em CSV e inspeção de tipos, dimensões e nulos.
- **Limpeza e Datetime (RF03):** Tratamento de strings (`.strip()`), conversão de datas com `pd.to_datetime(..., errors='coerce')` e remoção de registros inválidos.
- **Colunas Derivadas (RF04):** Extração de variáveis temporais (`mes`, `mes_nome`, `trimestre`, `ano`) e calculadas (`receita_total`).
- **Agregações com Groupby (RF05):** Mapeamento e consolidação de métricas por mês, produto, categoria e região.
- **Segmentação com Lambda (RF06):** Classificação dos clientes em faixas de valor (Bronze, Prata, Ouro).
- **Gráficos & Subplots (RF07):** Construção de visualizações no Matplotlib/Seaborn (Linha, Barras, Dispersão) e Painel Resumo 2x2 salvo em 300 DPI com `plt.tight_layout()`.
- **Função de Ordem Superior (RF08):** Implementação da função `processar_coluna()`, que recebe outras funções como argumento e aplica transformações dinâmicas via `.apply()`.
- **Exportação CSV/JSON (RF09):** Leitura e escrita em CSV (`.to_csv()`) e JSON (`json.dump()`), incluindo etapa de validação com releitura via `json.load()`.
- **Estrutura Principal (RF10):** Organização das funções e controle de execução com o bloco `if __name__ == "__main__":` na função `main()`.

---

## Como Executar o Projeto

### Opção 1: Google Colab (Recomendado)
1. Abra o Google Colab.
2. Faça o upload do arquivo `salesinsight.ipynb`.
3. Execute todas as células em ordem (**Ambiente de execução -> Executar tudo**).
4. Os relatórios (`.csv`, `.json`) e os gráficos (`.png`) serão gerados automaticamente na barra lateral de arquivos.

### Opção 2: Localmente (VS Code / Terminal)
1. Certifique-se de ter o **Python 3.10+** instalado.
2. Instale as dependências necessárias:
   `pip install pandas numpy matplotlib seaborn`
3. Execute no terminal:
   `python salesinsight.py`

---

## Estrutura do Repositório

```text
salesinsight-py/
│-- salesinsight.py         # Código-fonte principal com todo o fluxo de análise (main)
│-- salesinsight.ipynb      # Notebook interativo executado no Google Colab
│-- vendas.csv              # Dataset sintético de vendas bruto
│-- README.md               # Documentação completa do projeto
│
├── outputs/                # Relatórios e estatísticas exportados
│   ├── metricas_por_mes.csv
│   ├── segmentacao_clientes.csv
│   └── estatisticas_gerais.json
│
└── graficos/            
    ├── receita_por_mes.png
    ├── top_produtos.png
    ├── quantidade_vs_receita.png
    └── painel_resumo.png
```

---

## Decisões Técnicas de Implementação

1. **Tratamento de Datas Inválidas (`errors='coerce'`):** Na etapa de limpeza, optou-se por converter datas corrompidas (como `"DATA INVALIDA"`) em `NaT` e descartá-las imediatamente com `.dropna()`. Por que foi decidido: Para garantir que todos os gráficos e relatórios mensais/trimestrais trabalhem apenas com datas válidas.
2. **Criação Prévia da Coluna receita_total:** Foi calculada a receita_total (quantidade * preco_unitario) na etapa inicial de transformação. Por que foi decidido: Evitou ter que ficar recalculando esse valor em cada tabela ou gráfico, deixando o código limpo e padronizado.
3. **Segmentação acumulada por cliente:** Foi agrupado o valor total gasto por cliente (groupby('cliente')) antes de classificar nas faixas Bronze, Prata e Ouro. Por que foi decidido: Para que a classificação reflita o valor real total que o cliente gastou no período, e não apenas o valor de uma única compra isolada.

---

## Git, Branches e Versionamento

O projeto seguiu um modelo de versionamento baseado em *branches* por funcionalidade:

- `main`: Código estável e pronto para entrega.
- `develop`: Branch de integração das funcionalidades.
- `feat/leitura-limpeza`: Implementação dos requisitos RF01 a RF03.
- `feat/analise-metricas`: Implementação das transformações, groupby e segmentação (RF04 a RF06).
- `feat/visualizacoes`: Criação e exportação dos gráficos Matplotlib/Seaborn (RF07).
- `feat/pipeline-main`: Organização das funções reutilizáveis, função de ordem superior e fluxo `main()` (RF08 a RF10).
- `docs/readme-video`: Elaboração da documentação README e roteiro do vídeo.

---

## Vídeo de Demonstração

Segue um vídeo com a explicação do código e execução do projeto:
- **Link do Vídeo:** [o link será colocado em seguida]