#MVP Engenharia de Dados
##Expansão dos veículos Eletrificados e Consumo dos Combustíveis no Brasil

# 1. Contexto de Negócios e Perguntas
O crescimento de vendas de veículos eletrificados vem transformando gradualmente o setor automotivo brasileiro. Entretanto ainda existe a necessidade de avaliar se essa expansão já apresenta sinais perceptíveis sobre o mercado nacional de combustíveis.

Este Trabalho tem como objetivo analisar a evolução das vendas de veículos eletrificados e o comportamento de vendas de Gasolina C e Etanol Hidratado no Brasil entre 2020 e 2024, buscando identificar possíveis relações entre essas tendências.

As perguntas de negócio que orientam o desenvolvimento de pipeline foram:

1. Como evoluíram as vendas de veículos eletrificados no Brasil entre 2020 e 2024?
2. Como se comportaram as vendas de Gasolina C se Etanol Hidratado no mesmo período?
3. Existe alguma relação entre o crescimento das vendas de veículos eletrificados e o comportamento das vendas de combustíveis.
4. Mantidas as tendências observadas, quais os cenários observados nos próximos anos

Foram utilizadas duas fontes de dados:

- **ABVE - Associação Brasileira de Veículo Eletrico:** dados históricos mensais sobre a venda de veículos eletrificados, contendo ano, número, mês e total de eletrificados.
 - **ANP - Assoociação de Petróleo, Gás Natural e Biocombustíveis:** dados anuais de vendas de Gasolina C e Etano Hidratado por município contendo ano, região, unidade federativa, produto, código IBGE, município e volume de vendas em litros.

 As bases abrangem o período de 2020 a 2024 e foram obtidas a partir de fontes públicas. As evidências de acesso, origem e condições de disponibilidade estão registradas na pasta 'evidencias' deste repositório.
# 2. Carga de dados

Os dados da ANP foram obtidos em formato tabular e exportados para arquivos CSV para a utilização no pipeline.

Já os dados históricos da ABVE foram disponibilizados em formato de tabela pública. Para possibilitar a leitura automatizada no Databricks, a estrutura foi consolidada e convertida para um arquivo CSV, preservando os dados originais disponibilizados pela fonte.

Após essa etapa, os arquivos foram armazenados na área de dados do projeto e carregado para o ambiente Databricks para processamento nas camadas Bronze, Silver e Gold.

# 3. Modelagem e Catálogo de dados

O projeto foi estruturado seguindo a arquitetura medalhão (Bronze, Silver e Gold), amplamente utilizadas em ambientes Lakehouse.

Na camada Bronze foram armazenados os dados brutos provenientes das fontes ABVE e ANP, preservando a rastreabilidade dos arquivos originais.

Na camada Silver, foram realizados os processos de preparação de dados, incluindo a seleção dos atributos relevantes e consolidação das informações em nível anual.

Na camada Gold, foi contruída uma base analítica consolidada contendo indicadores de vendas de veículos eletrificados, vendas de Gasolina C e Etanol Hidratado, além de métricas derivadas utilizadas nas análises, correlações e projeções.

O catálogo de dados foi elaborado a partir do levantamento das tabelas e colunas utitilzados no pipeline, documentando a estrutura, tipo de dados e finalidade dos atributos empregados no estudo.

**Evidências**
 - Inserir screenshot do invetário de tabelas.
 - Inserir screenshot do invetário de colunas.
 - Inserir screenshot da estrutura das camadas Bronze, Silver e Gold. 
# 4. Pipeline de dados

O pipeline foi organizado seguindo a arquitetura medalhão, separando as atividades de ingestão, preparação e análise em notebooks distintos.

### Camada Bronze - Ingestão de Dados

Responsável pela leitura de arquivos provenientes da ABVE e ANP, realizando as validações iniciais da carga e preservando os dados em seu formato original.

Notebook:
- notebooks/bronze/ingestao_dados

### Camada Silver - Preparação dos Dados

Responsável pela seleção dos atributos relevantes, padronização da estrutura das bases e consolidação das informações em nível anual para suportar as análises de estudo.

Notebook:
- notebooks/silver/preparacao_dados

### Camada Gold - Análise e Consolidação

Responsável pela ingestão das bases de indicadores, geração das visualizações, análise das correlações e contrução das projeções exploratórias.

Notebook:
- notebooks/gold/analise_consolidada

### Tecnologias utilizadas:
O desenvolvimento foi realizado utilizando Python no ambiente Databricks Free Edition. As etapas de tratamento e manipulação de dados foram executadas com Pandas, as visualizações foram construídas com Matplotlib e Seaborn e as projeções exploratórias foram realizadas com Scikit-Learn. O versionamento e a disponibilização do projeto foram realizados por meio do GitHub.
# 5. Qualidade de Dados

Foram realizadas verificações iniciais de qualidade de dados com foco nos aspectos de completude, consistência e estrutura das bases utilizadas.

Durante a etapa de preparação de dados, foram analisados os atributos disponíveis nas fontes da ABVE e ANP, sendo selecionado apenas as colunas relevantes para o objetivo do estudo. Também foi realizada a consolidação anual das informações garantindo compatibilidade entre as bases utilizadas na análise.

Não foram identificados problemas críticos na qualidade que inviabilizasse o desenvolvimento do pipeline. As transformações realizadas tiveram como principal objetivo organizar e padronizar os dados para permitir a comparação entre venda de veículos eletrificados e o consumo de combustíveis ao longo do período analisado.
# 6. Análise de Dados

As análises realizadas buscaram responder às perguntas de negócio definidas no início do projeto.

Os resultados mostraram o crescimento acelerado de vendas de veículos eletrificados entre 2020 e 2024, enquanto o consumo de Gasolina C e Etanol Hidratado permaneceu em níveis elevados ao longo do mesmo período.

A análise de correlação indicou associação positiva entre as variáveis analisadas, sugerindo que o aumento das vendas de veículos eletrificados ainda não resultou em uma redução perceptível no consumo de combustíveis estudados.

Também foram realizadas projeções exploratórias por meio de regreção linear, permitindo observar continuidade das tendências identificadas na série histórica. Entretanto, devido à quantidade limitada de observações e à influência de fatores externos não contemplados no modelo, esses dados devem ser interpretados com cautela.

De forma geral, os resultados não forneceram evidências suficientes para afirmar que o crescimento de vendas de veículos eletrificados já esteja impactando significativamente o consumo de combustíveis no Brasil.

As evidências gráficas, tabelas de apoio, análises de correlação e projeções encontram-se documentadas no notebook da camada Gold.

# 7. Autoavaliação

A escolha do tema foi motivada pela minha atuação em uma distribuidora de combustíveis, contexto que despertou o interesse em entender como a expansão desse segmento pode influenciar o mercado de combustíveis nos próximos anos. Essa proximidade com o tema contribuiu para aumentar o engajamento e a motivação durante o desenvolvimento do projeto e para direcionar a escolha das perguntas de negócio analisadas.

Acredito que, mesmo sendo um projeto não tão extenso, os objetivos propostos para o MVP foram atigindos de forma satisfatória. Foi possível construir um pipeline de dados completo em ambiente de nuvem, contemplando as etapas de ingestão, preparação, modelagem e aanálise de dados.

Durante o desenvolvimento do projeto, os principais desafios foram obter, organizar e integrar diferentes fontes de dados seguindo a estrutura medalhão do Databricks. Que se mostrou desafiador e assustador, mas que fez muito sentido quando implementado.

Esse projeto contribuiu para o meu aprendizado técnico com a integração Github + Databricks, boas práticas de desenvolvimento com a arquitetura medalhão, documentação de dados, não só para guiar o projeto, mas para compatilhar o conteúdo de forma precisa, além de conhecimento prático sobre o negócio que conversou diretamente com a minha área de atuação.