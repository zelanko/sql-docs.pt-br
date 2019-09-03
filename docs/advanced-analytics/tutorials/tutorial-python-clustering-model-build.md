---
title: 'Tutorial: Criar um modelo de clustering no Python'
description: Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means para executar o clustering em Python com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ce7f6cbd580afbdbf71065803af8d394323e5dc3
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211970"
---
# <a name="tutorial-build-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Crie um modelo de clustering em Python com SQL Server Serviços de Machine Learning

Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no Python para executar o clustering. Na próxima parte desta série, você implantará esse modelo em um banco de dados SQL com SQL Server Serviços de Machine Learning.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Definir o número de clusters para um algoritmo K-means
> * Executar clustering
> * Analisar os resultados

Na [parte um](tutorial-python-clustering-model.md), você instalou os pré-requisitos e importou o banco de dados de exemplo.

Na [parte dois](tutorial-python-clustering-model-prepare-data.md), você aprendeu como preparar os dados de um banco de dado SQL para executar o clustering.

Na [parte quatro](tutorial-python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados SQL que pode executar o clustering em Python com base em novas informações.

## <a name="prerequisites"></a>Pré-requisitos

* A parte três deste tutorial pressupõe que você atendeu aos pré-requisitos da [**parte 1**](tutorial-python-clustering-model.md)e concluiu as etapas na [**parte dois**](tutorial-python-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Definir o número de clusters

Para clusterizar os dados do cliente, você usará o algoritmo de clustering **K-** Means, uma das maneiras mais simples e mais conhecidas de agrupar dados.
Você pode ler mais sobre K-means em [um guia completo para o algoritmo de clustering k-](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)means.

O algoritmo aceita duas entradas: Os dados em si e um número predefinido "*k*" que representa o número de clusters a serem gerados.
A saída é *k* clusters com os dados de entrada particionados entre os clusters.

O objetivo do K-means é agrupar os itens em clusters K, de modo que todos os itens no mesmo cluster sejam semelhantes uns aos outros, e tão diferente dos itens em outros clusters, o mais possível.

Para determinar o número de clusters para o algoritmo a ser usado, use uma plotagem da soma dos quadrados nos grupos, por número de clusters extraídos. O número apropriado de clusters a ser usado está na curva ou "cotovelo" do gráfico.

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![Gráfico de cotovelo](./media/python-tutorial-elbow-graph.png)

Com base no grafo, parece que *k = 4* seria um bom valor para tentar. Esse valor *k* agrupará os clientes em quatro clusters.

## <a name="perform-clustering"></a>Executar clustering

No script Python a seguir, você usará a função KMeans do pacote sklearn.

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>Analisar os resultados

Agora que você executou o Clustering usando K-means, a próxima etapa é analisar o resultado e ver se você pode encontrar qualquer informação acionável.

Examine os valores médios de cluster e os tamanhos de cluster impressos do script anterior.

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

Os quatro meios de cluster são fornecidos usando as variáveis definidas na [parte um](tutorial-python-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = taxa de ordem de retorno (número total de pedidos parcialmente ou totalmente retornados versus o número total de pedidos)
* *itemsRatio* = taxa de itens de retorno (número total de itens retornados versus o número de itens comprados)
* *monetaryRatio* = taxa de valor de retorno (valor monetário total de itens retornados versus o valor comprado)
* *frequência* = frequência de retorno

A mineração de dados usando K-means geralmente requer análise adicional dos resultados e etapas adicionais para entender melhor cada cluster, mas pode fornecer bons clientes potenciais.
Aqui estão algumas maneiras de interpretar esses resultados:

* O cluster 0 parece ser um grupo de clientes que não estão ativos (todos os valores são zero).
* O cluster 3 parece ser um grupo que se destaca em termos de comportamento de retorno.

O cluster 0 é um conjunto de clientes que estão claramente inativos. Talvez você possa direcionar os esforços de marketing para esse grupo para disparar um interesse por compras. Na próxima etapa, você consultará o banco de dados para os endereços de email dos clientes no cluster 0, para que possa enviar um email de marketing para eles.

## <a name="clean-up-resources"></a>Limpar recursos

Se você não for continuar com este tutorial, exclua o banco de dados tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte três desta série de tutoriais, você concluiu estas etapas:

* Definir o número de clusters para um algoritmo K-means
* Executar clustering
* Analisar os resultados

Para implantar o modelo de aprendizado de máquina que você criou, siga a parte quatro desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Implantar um modelo de clustering em Python com SQL Server Serviços de Machine Learning](tutorial-python-clustering-model-deploy.md)