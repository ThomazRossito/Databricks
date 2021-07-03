<img src="https://files.training.databricks.com/images/Apache-Spark-Logo_TM_200px.png" style="float: left: margin: 20px"/>


# Pipelines


###  **Source para Bronze:**
>  * **01-Ativos**
>  * **02-Investors**
>  * **03-Solicitações de Empréstimo**
>  * **04-Transações de estoque**
>  * **05-Dados macro**


<h2 style="color:red">Informações: Projeto e Dataset</h2>


### Datasets:

> - **`produtos.csv`**
> - **`investments.parquet`**
> - **`assets.csv`**
> - **`stock_orders.json`**
> - **`subscriptions.csv`**
> - **`taxas.csv`**
> - **`loan_requests.xml`**
> - **`macro.csv`**


### Sobre o Projeto:                      

Este é um ambiente Fintech online que fornece um sistema de negociação de ações. A empresa oferece um portal onde os investidores podem comprar e vender ações e solicitar empréstimos para voltar a investir. Os dois principais tipos de transação são Solicitações de Empréstimos e Transações de Estoque.

Isso leva a dois tipos de produtos (**`produtos.csv`**) a serem oferecidos aos nossos investidores: Ações (para comprar e vender) e Empréstimos (para solicitar e esperar aprovação). Eles têm taxas diferentes com base nos tipos de assinatura.

Todos os investidores (**`investments.parquet`**) são pessoas físicas ativas em nosso website. Eles têm suas informações pessoais, demográficas e algumas informações comerciais relacionadas aqui, como pontuação de crédito, pontuação de risco e ações favoritas.

Assets (**`assets.csv`**) é uma lista de cotações de ações de empresas do S&P 500 (APPL, MSFT, etc) que nossos investidores compram e vendem. Nesta tabela, também estamos acompanhando os riscos dos ativos, marcando a pontuação de risco do ativo com base em dados históricos.

Nossos primeiros dados transacionais são pedidos de estoque ou transações de estoque (**`stock_orders.json`**). Temos um site através do qual nossos investidores colocam suas ordens de compra e venda. Os dados de pedidos de estoque são gerados com base nas atividades de compra, venda e cliques de nossos clientes no site. Rastreamos o tempo gasto em um ticker quando o investidor faz uma análise usando a ferramenta de análise (como verificar sua série temporal para ver como o preço estava mudando ao longo do tempo). Isso nos dá informações valiosas, pois podemos supor que eles vão comprar.

Os investidores têm assinaturas de bronze, prata e ouro (**`subscriptions.csv`**). Taxas diferentes são aplicadas com base nessas informações. Taxas (**`taxas.csv`**) é uma tabela de consulta onde as informações das taxas são registradas.

Pedidos de empréstimo (**`loan_requests.xml`**) são os segundos dados transacionais gerados por investidores que precisam de crédito de nosso sistema. Se aprovados, eles podem usar esses créditos (ou fundos) para fins de investimento apenas em nosso portal. A aprovação depende muito da pontuação de crédito do investidor.

Como empresa, também processamos alguns dados externos para ajudar na nossa tomada de decisão. Uma de nossas fontes são os Dados Macroeconômicos (**`macro.csv`**) que não tem conexão com nossos conjuntos de dados internos: recebemos mensalmente do banco central e contém alguns indicadores macroeconômicos como desemprego e PIB. Isso nos ajuda a construir uma única métrica decimal e a usamos para atualizar a pontuação de crédito dos investidores, que serve como base para aprovar ou desaprovar suas solicitações de empréstimo.


## Processamento dos dados: fluxo em três etapas:

1. Crie tabelas ** bronze **: a primeira camada com pouca intervenção, apenas lendo da fonte e salvando-as como ** Tabelas Delta **.
2. Crie tabelas ** silver **: a segunda camada com cálculos intensos envolvendo limpeza, joining, feature engineering, e windowing.
3. Crie tabelas ** gold **: a camada final com agregação e aplicação de regras de negócios.

<p>
[Databrciks Partner](https://academy.databricks.com/?_gl=1*1mslkmb*_gcl_aw*R0NMLjE2MjUzMDEyOTMuQ2p3S0NBandsWUNIQmhBUUVpd0E0SzIxbTZYakJDSzM0aE9JVktDaV9hWVE2T09HZ1N1TWFoQllhVWFJZ3BHUVpXOTlUY0FyWmpnNHVCb0NsblVRQXZEX0J3RQ..&_ga=2.65417710.1512010725.1624893208-1426243253.1622298680)  
