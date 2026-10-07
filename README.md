# Analise_de_risco_de_credito
No mercado financeiro e de fintechs, um dos maiores desafios diários é equilibrar a concessão de crédito com a mitigação de riscos de inadimplência (calotes). Ser rigoroso demais significa perder receita e clientes em potencial; ser permissivo demais eleva drasticamente os prejuízos operacionais.


Neste projeto , construímos um pipeline analítico de ponta a ponta utilizando dados reais do setor de crédito para estruturar um banco relacional, tratar inconsistências corporativas, realizar engenharia de atributos e aplicar um modelo de Machine Learning não supervisionado para segmentar perfis de risco e comportamento de clientes.

Stack Tecnológica e Arquitetura
Linguagem: Python (Pandas para manipulação, Scikit-Learn para modelagem preditiva).
Banco de Dados: SQLite (criação e persistência de um ambiente relacional local).
Linguagem de Consulta: SQL Avançado (agregações, tratamento de cardinalidade e agrupamentos por chave única de cliente).
Machine Learning: Algoritmo K-Means Clustering com padronização de variáveis (StandardScaler).
Ambiente: Kaggle Notebooks.
Etapas de Desenvolvimento do Projeto
Ingestão e Modelagem Relacional (ETL)
A partir da base transacional de cartões e histórico financeiro, criamos um script automatizado de ETL que varre a fonte de dados, extrai as informações brutas e as consolida em uma tabela estruturada dentro de um banco de dados SQLite local (banco_risco_credito.db).

O Desafio e Tratamento de Nulos Corporativos
Em bases de dados de crédito reais, a presença massiva de valores nulos (NaN) é comum. Identificamos que colunas de saldos e faturamento histórico ausentes representam, na verdade, a inatividade do cliente ou a ausência daquele produto financeiro específico.

Aplicamos tratamentos inteligentes via Pandas e SQL, convertendo os nulos financeiros em zero (indicando ausência de movimentação no período) e estruturando datas de relacionamento padrão.
Engenharia de Atributos e Agregação por Cliente (case_id)
Como o histórico transacional continha múltiplos registros por indivíduo, utilizamos consultas SQL avançadas com agregações (COUNT, MAX, SUM) e agrupamentos por case_id para construir uma Feature Store limpa. Cada linha passou a representar unicamente um cliente, destacando métricas cruciais como:

Saldo máximo em 180 dias.
Movimentações acumuladas (turnover) de 180 e 30 dias.
Volume total de transações registradas.
Machine Learning: Clusterização e Perfis de Risco (K-Means)
Para classificar inteligentemente a base sem depender de rótulos prévios, utilizamos o algoritmo K-Means. Após normalizar os dados com StandardScaler para garantir a mesma escala de importância entre as variáveis financeiras, dividimos a base em 3 clusters estratégicos para o negócio:

Baixo Risco / Padrão: Representa a grande massa de clientes com comportamento estável ou menor volume transacional (106.900 clientes).
Médio Risco / Ativo: Consumidores com engajamento financeiro intermediário e maior monitoramento (4.407 clientes).
Alto Volume / VIP: O grupo seleto de alto valor transacional e movimentação robusta (465 clientes).
Principais Insights e Aplicações Práticas
Mitigação Preventiva de Risco: A identificação precisa de grupos de médio e alto risco permite que a mesa de crédito ajuste limites dinamicamente, evitando perdas futuras com inadimplência.
Estratégias de Relacionamento (VIP): O isolamento do cluster de Alto Volume / VIP fundamenta ações comerciais direcionadas, como oferta de taxas diferenciadas e produtos de crédito exclusivos, maximizando a rentabilidade da instituição.
