---
title: 'Tutorial do Python: criar um modelo de cluster'
description: Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means para executar o clustering em Python com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669686d0163b9ce1c362e7cdf2814c7a95bfaa8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727107"
---
# <a name="tutorial-build-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>Tutorial: Criar um modelo em Python para categorizar os clientes com os Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no Python para executar o clustering. Na próxima parte desta série, você implantará esse modelo em um Banco de Dados SQL com os Serviços de Machine Learning do SQL Server.

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Definir o número de clusters para um algoritmo K-means
> * Executar clustering
> * Analisar os resultados

Na [parte um](python-clustering-model.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](python-clustering-model-prepare-data.md), você aprendeu a preparar os dados de um Banco de Dados SQL para executar o clustering.

Na [parte quatro](python-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um Banco de Dados SQL que pode executar clusters em Python com base em novos dados.

## <a name="prerequisites"></a>Prerequisites

* A parte três deste tutorial pressupõe que você cumpriu os pré-requisitos da [**parte um**](python-clustering-model.md) e concluiu as etapas na [**parte dois**](python-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Definir o número de clusters

Para colocar os dados do cliente em um cluster, você usará o algoritmo de clustering **K-means**, uma das maneiras mais simples e mais conhecidas de agrupar dados.
Você pode ler mais sobre o K-means em [Um guia completo para o algoritmo de clustering K-means](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html).

O algoritmo aceita duas entradas: Os dados em si e um número predefinido "*k*" que representa o número de clusters a serem gerados.
A saída é *k* clusters com os dados de entrada particionados entre os clusters.

O objetivo do K-means é agrupar os itens em clusters k, de modo que todos os itens no mesmo cluster sejam semelhantes uns aos outros e o mais diferente possível dos itens em outros clusters.

Para determinar o número de clusters para o algoritmo a ser usado, use um gráfico da soma dos quadrados nos grupos, por número de clusters extraídos. O número correto de clusters a ser usado está na curva ou no "cotovelo" do gráfico.

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

Com base no gráfico, parece que *k = 4* seria um bom valor para testar. Esse valor *k* agrupará os clientes em quatro clusters.

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

Agora que você executou o clustering usando K-means, a próxima etapa é analisar o resultado e ver se é possível encontrar qualquer informação acionável.

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

As quatro médias de cluster são fornecidas usando as variáveis definidas na [parte um](python-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = taxa de devolução de pedidos (número total de pedidos parcialmente ou totalmente retornados em relação o número total de pedidos)
* *itemsRatio* = taxa de devolução de itens (número total de itens retornados em relação ao número de itens comprados)
* *monetaryRatio* = taxa de valores devolvidos (valor monetário total dos itens retornados em relação ao valor comprado)
* *frequência* = frequência de devoluções

A mineração de dados com K-means geralmente requer análise adicional dos resultados e mais etapas para entender melhor cada cluster, mas pode fornecer bons clientes potenciais.
Veja algumas maneiras de interpretar esses resultados:

* O cluster 0 parece ser um grupo de clientes que não estão ativos (todos os valores são zero).
* O cluster 3 parece ser um grupo que se destaca em termos de comportamento de devolução.

O cluster 0 é um conjunto de clientes que estão claramente inativos. Talvez você possa direcionar os esforços de marketing para esse grupo para disparar um interesse por compras. Na próxima etapa, você consultará o banco de dados dos endereços de email dos clientes no cluster 0 para enviar um email de marketing para eles.

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Na parte três desta série de tutoriais, você concluiu estas etapas:

* Definir o número de clusters para um algoritmo K-means
* Executar clustering
* Analisar os resultados

Para implantar o modelo de machine learning que você criou, siga a parte quatro desta série de tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Implantar um modelo de clustering em Python com os Serviços de Machine Learning do SQL Server](python-clustering-model-deploy.md)