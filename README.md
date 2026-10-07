# Analise_de_risco_de_credito
   <p>No mercado financeiro e de fintechs, um dos maiores desafios diários é equilibrar a concessão de crédito com a mitigação de riscos de inadimplência (calotes). Ser rigoroso demais significa perder receita e clientes em potencial; ser permissivo demais eleva drasticamente os prejuízos operacionais.
</p>

    <p>Neste projeto , construímos um pipeline analítico de ponta a ponta utilizando dados reais do setor de crédito para estruturar um banco relacional, tratar inconsistências corporativas, realizar engenharia de atributos e aplicar um modelo de Machine Learning não supervisionado para segmentar perfis de risco e comportamento de clientes.
</p>

    <h3>Stack Tecnológica e Arquitetura</h3>

        <ul>
      <li>Linguagem: Python (Pandas para manipulação, Scikit-Learn para modelagem preditiva).</li>
      <li>Banco de Dados: SQLite (criação e persistência de um ambiente relacional local).</li>
      <li>Linguagem de Consulta: SQL Avançado (agregações, tratamento de cardinalidade e agrupamentos por chave única de cliente).</li>
      <li>Machine Learning: Algoritmo K-Means Clustering com padronização de variáveis (StandardScaler).</li>
      <li>Ambiente: Kaggle Notebooks.</li>

  </ul>


<h3>Etapas de Desenvolvimento do Projeto</h3>
<h4>Ingestão e Modelagem Relacional (ETL)</h4>

<p>A partir da base transacional de cartões e histórico financeiro, criamos um script automatizado de ETL que varre a fonte de dados, extrai as informações brutas e as consolida em uma tabela estruturada dentro de um banco de dados SQLite local (banco_risco_credito.db).</p>

<h4>O Desafio e Tratamento de Nulos Corporativos</h4>
<p>Em bases de dados de crédito reais, a presença massiva de valores nulos (NaN) é comum. Identificamos que colunas de saldos e faturamento histórico ausentes representam, na verdade, a inatividade do cliente ou a ausência daquele produto financeiro específico.</p>

    <ul>
       <li>Aplicamos tratamentos inteligentes via Pandas e SQL, convertendo os nulos financeiros em zero (indicando ausência de movimentação no período) e estruturando datas de relacionamento padrão.</li>
    </ul>

<h4>Engenharia de Atributos e Agregação por Cliente (case_id)</h4>
<p>Como o histórico transacional continha múltiplos registros por indivíduo, utilizamos consultas SQL avançadas com agregações (COUNT, MAX, SUM) e agrupamentos por case_id para construir uma Feature Store limpa. Cada linha passou a representar unicamente um cliente, destacando métricas cruciais como:</p>
<ul>
    <li>Saldo máximo em 180 dias.</li>
    <li>Movimentações acumuladas (turnover) de 180 e 30 dias.</li>
    <li>Volume total de transações registradas.</li>
</ul>

<h4>Machine Learning: Clusterização e Perfis de Risco (K-Means)</h4>
<p>Para classificar inteligentemente a base sem depender de rótulos prévios, utilizamos o algoritmo K-Means. Após normalizar os dados com StandardScaler para garantir a mesma escala de importância entre as variáveis financeiras, dividimos a base em 3 clusters estratégicos para o negócio:</p>

<ul>
    <li>Baixo Risco / Padrão: Representa a grande massa de clientes com comportamento estável ou menor volume transacional (106.900 clientes).</li>
    <li>Médio Risco / Ativo: Consumidores com engajamento financeiro intermediário e maior monitoramento (4.407 clientes).</li>
    <li>Alto Volume / VIP: O grupo seleto de alto valor transacional e movimentação robusta (465 clientes).</li>
</ul>

<h3>Principais Insights e Aplicações Práticas</h3>
<ul>
    <li>Mitigação Preventiva de Risco: A identificação precisa de grupos de médio e alto risco permite que a mesa de crédito ajuste limites dinamicamente, evitando perdas futuras com inadimplência.</li>
    <li>Estratégias de Relacionamento (VIP): O isolamento do cluster de Alto Volume / VIP fundamenta ações comerciais direcionadas, como oferta de taxas diferenciadas e produtos de crédito exclusivos, maximizando a rentabilidade da instituição.</li>
</ul>

