# Insurance All

![hi](health-insurance.jpg)

# Problema de Negócio:

Uma companhia de seguros vende planos de saúde para seus clientes. Eles pretendem começar a vender seguros de veículos aos seus clientes, a fim de diversificar seus produtos. A empresa irá entrar em contato com esses clientes e oferecer esse novo tipo de seguro. Além disso, ela fez uma pesquisa com sua base de clientes para obter alguns dados e saber quais deles estariam interessados no seguro de veículos à fim de efetuar uma venda cruzada(cross-selling). A empresa tem disponibilidade para fazer somente duas mil ligações. Eles acreditam que uma das formas de atingir o maior número possível de clientes com a menor quantidade de chamadas é fazer um modelo de aprendizado de máquina que classifique a lista de clientes para maximizar a quantidade de serviços contratados.

## I. Atributos

<table style="width:100%">
<tr><th>Atributos</th><th>Descrição</th></tr>
<tr><td>id</td><td>ID exclusivo para cada cliente</td></tr>
<tr><td>gender</td><td>Gênero do cliente</td></tr>
<tr><td>age</td><td>idade do cliente</td></tr>
<tr><td>driving_license</td><td>indica se o cliente tem carteira de motorista ou não, 0 = não tem, 1 = tem</td></tr>
<tr><td>region_code</td><td>indica o código da região do cliente</td></tr>
<tr><td>previously_insured</td><td>indica se o cliente tem um seguro de veículo ou não, 0 = não tem, 1 = tem</td></tr>
<tr><td>vehicle_age</td><td>idade do veículo</td></tr>
<tr><td>vehicle_damage</td><td>indica se o veículo do cliente sofreu algum tipo de dano no passado, 0 = não sofreu, 1 = sofreu</td></tr>
<tr><td>annual_premium</td><td>quantidade de clientes que optam pagar premium no ano</td></tr>
<tr><td>policy_sales_channel</td><td>código anônimo para o canal de divulgação do cliente, ou seja, agentes diferentes, por correio, por telefone, pessoalmente, etc.</td></tr>
<tr><td>vintage</td><td>número em dias que o cliente está associado à companhia</td></tr>
<tr><td>response</td><td>se o cliente está interessado ou não, 0 = não está, 1 = está</td></tr>
</table>

# Premissas de Negócio:

* Cross-selling é uma técnica de vendas que envolve a venda de um produto ou serviço adicional a um cliente existente.
* Learning To Ranking é um tipo de problema de classificação em que o objetivo é ordenar uma tabela de dados com base na probabilidade de alguns dados serem de uma classe específica.

# Estratégia de Negócio:

Etapa 01 - Entedimento do problema de négocio.

Etapa 02 - Download do dataset diretamente do <a href="https://www.kaggle.com/datasets/anmolkumar/health-insurance-cross-sell-prediction" target="_blank">Kaggle</a>.

Etapa 03 - Limpeza do conjunto de dados removendo valores discrepantes, valores NA e recursos desnecessários.

Etapa 04 - Exploração os dados (EDA) para criar hipóteses, gerar insights e validá-los.

Etapa 05 - Preparação dos dados a serem utilizados pelos algoritmos de modelagem, codificando variáveis, dividindo o conjunto de dados em treino e teste.

Etapa 06 - Criando modelos utilizando algoritmos de Machine Learning.

Etapa 07 - Avaliando os modelos criados para encontrar aquele que melhor se configura ao problema.

Etapa 08 - Ajustar o modelo para obter uma melhor performance.

<!-- Etapa 09 - Implantar o modelo em produção para que fique disponível ao usuário. -->

<!-- # Insights: -->

# Resultados:

## I) Modelos de Machine Learning
O resultado final deste projeto é um modelo de classificação para ranquear a tabela. Portanto, foram criados cinco modelos: KNN (K-Nearest Neighbors), Logistic Regression, Random Forest, XGBoost e LightGBM.

<table style="width:100%">
<tr><th>Model Name</th><th>Precision at K</th><th>Recall at K</th></tr>
<tr><td>Random Forest</td><td>0.3663</td><td>0.0778</td></tr>
<tr><td>KNN</td><td>0.3193</td><td>0.0678</td></tr>
<tr><td>Logistic Regression</td><td>0.3028</td><td>0.0643</td></tr>
<tr><td>XGBoost</td><td>0.1414</td><td>0.0300</td></tr>
<tr><td>LightGBM</td><td>0.1334</td><td>0.0283</td></tr>
</table>

## II) Final Model
Para decidir qual seria o modelo final, foi feito um cross-validation para avaliar o desempenho dos algoritmos de forma mais robusta. Essas métricas estão representadas na tabela abaixo.

<table style="width:100%">
<tr><th>Model Name</th><th>Precision at K</th><th>Recall at K</th></tr>
<tr><td>LightGBM CV</td><td>0.4182 +/- 0.0109</td><td>0.112 +/- 0.0029</td><tr>
<tr><td>XGBoost CV</td><td>0.4062 +/- 0.0162</td><td>0.109 +/- 0.0044</td><tr>
<tr><td>Random Forest CV</td><td>0.3538 +/- 0.0091</td><td>0.095 +/- 0.0026</td><tr>
<tr><td>KNN CV</td><td>0.3104 +/- 0.0122</td><td>0.0832 +/- 0.0031</td><tr>
<tr><td>Logistic Regression CV</td><td>0.2934 +/- 0.0129</td><td>0.0788 +/- 0.0033</td><tr>
</table>

O modelo LightGBM foi o melhor entre todos os modelos criados, portanto foi o escolhido para ser implantado. Após a escolha de qual seria o modelo final, uma otimização de hiperparâmetros de busca aleatória foi utilizada para melhorar o desempenho do modelo. As métricas de avaliação do modelo final estão na tabela abaixo.

<table style="width:100%">
<tr><th>Model Name</th><th>Precision at K</th><th>Recall at K</th></tr>
<tr><td>LightGBM CV</td><td>0.41 +/- 0.01</td><td>0.1102 +/- 0.0025</td><tr>
</table>

# Conclusões:

O modelo quando aplicado ao conjunto de dados inicial com 381.109 clientes, incluiria 891 clientes a mais que desejam um seguro de veículo, do que 2.000 clientes selecionados aleatoriamente no banco de dados. Isso representaria um aumento de 338,78% no número de ligações bem sucedidas.

# Melhorias Futuras:

- Fazer o Deploy do modelo.
- Adicionar novas features.
- Explorar o dataset para encontrar mais insights.
- Testar outros algoritmos de Machine Learning.
