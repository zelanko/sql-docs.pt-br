---
title: 'Tutorial: Compilar um modelo de clustering no R'
titleSuffix: SQL machine learning
description: Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means para executar clustering no R com o aprendizado de máquina do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: a8520c1ac48b88fe0aaf66096b76cdc7b705a272
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470217"
---
# <a name="tutorial-build-a-clustering-model-in-r-with-sql-machine-learning"></a>Tutorial: Criar um modelo de clustering no R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no R para executar clustering. Na próxima parte desta série, você implantará esse modelo em um banco de dados com os Serviços de Machine Learning do SQL Server ou nos Clusters de Big Data.
::: moniker-end
::: moniker range="=sql-server-2017"
Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no R para executar clustering. Na próxima parte desta série, você implantará esse modelo em um banco de dados com os Serviços de Machine Learning do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016"
Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no R para executar clustering. Na próxima parte desta série, você implantará esse modelo em um banco de dados com o SQL Server R Services.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
Na parte três desta série de tutoriais de quatro partes, você criará um modelo K-means no R para executar clustering. Na próxima parte desta série, você implantará esse modelo em um banco de dados SQL com os Serviços do Machine Learning da Instância Gerenciada de SQL do Azure.
::: moniker-end

Neste artigo, você aprenderá a:

> [!div class="checklist"]
> * Definir o número de clusters para um algoritmo K-means
> * Executar clustering
> * Analisar os resultados

Na [parte um](r-clustering-model-introduction.md), você instalou os pré-requisitos e restaurou o banco de dados de exemplo.

Na [parte dois](r-clustering-model-prepare-data.md), você aprendeu a preparar os dados de um banco de dados para executar clustering.

Na [parte quatro](r-clustering-model-deploy.md), você aprenderá a criar um procedimento armazenado em um banco de dados que pode executar clustering no R com base em novos dados.

## <a name="prerequisites"></a>Pré-requisitos

* A parte três desta série de tutoriais pressupõe que você cumpriu os pré-requisitos da [**parte um**](r-clustering-model-introduction.md) e concluiu as etapas na [**parte dois**](r-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Definir o número de clusters

Para colocar os dados do cliente em um cluster, você usará o algoritmo de clustering **K-means**, uma das maneiras mais simples e mais conhecidas de agrupar dados.
Você pode ler mais sobre o K-means em [Um guia completo para o algoritmo de clustering K-means](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html).

O algoritmo aceita duas entradas: Os dados em si e um número predefinido "*k*" que representa o número de clusters a serem gerados.
A saída é *k* clusters com os dados de entrada particionados entre os clusters.

Para determinar o número de clusters para o algoritmo a ser usado, use um gráfico da soma dos quadrados nos grupos, por número de clusters extraídos. O número correto de clusters a ser usado está na curva ou no "cotovelo" do gráfico.

```r
# Determine number of clusters by using a plot of the within groups sum of squares,
# by number of clusters extracted. 
wss <- (nrow(customer_data) - 1) * sum(apply(customer_data, 2, var))
for (i in 2:20)
    wss[i] <- sum(kmeans(customer_data, centers = i)$withinss)
plot(1:20, wss, type = "b", xlab = "Number of Clusters", ylab = "Within groups sum of squares")
```

![Gráfico de cotovelo](./media/elbow-graph.png)

Com base no gráfico, parece que *k = 4* seria um bom valor para testar. Esse valor *k* agrupará os clientes em quatro clusters.

## <a name="perform-clustering"></a>Executar clustering

No script R a seguir, você usará a função **kmeans** para executar clustering.

```r
# Output table to hold the customer group mappings.
# Generate clusters using Kmeans and output key / cluster to a table
# called return_cluster

## create clustering model
clust <- kmeans(customer_data[,2:5],4)

## create clustering ouput for table
customer_cluster <- data.frame(cluster=clust$cluster,customer=customer_data$customer,orderRatio=customer_data$orderRatio,
        itemsRatio=customer_data$itemsRatio,monetaryRatio=customer_data$monetaryRatio,frequency=customer_data$frequency)

## write cluster output to DB table
sqlSave(ch, customer_cluster, tablename = "return_cluster")

# Read the customer returns cluster table from the database
customer_cluster_check <- sqlFetch(ch, "return_cluster")

head(customer_cluster_check)
```

## <a name="analyze-the-results"></a>Analisar os resultados

Agora que você já concluiu o clustering usando o K-means, a próxima etapa é analisar o resultado e ver se você pode encontrar todas as informações acionáveis.

```r
#Look at the clustering details to analyze results
clust[-1]
```

```results
$centers
   orderRatio itemsRatio monetaryRatio frequency
1 0.621835791  0.1701519    0.35510836  1.009025
2 0.074074074  0.0000000    0.05886575  2.363248
3 0.004807692  0.0000000    0.04618708  5.050481
4 0.000000000  0.0000000    0.00000000  0.000000

$totss
[1] 40191.83

$withinss
[1] 19867.791   215.714   660.784     0.000

$tot.withinss
[1] 20744.29

$betweenss
[1] 19447.54

$size
[1]  4543   702   416 31675

$iter
[1] 3

$ifault
[1] 0

```

As quatro médias de cluster são fornecidas usando as variáveis definidas na [parte dois](r-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = taxa de devolução de pedidos (número total de pedidos parcialmente ou totalmente retornados em relação o número total de pedidos)
* *itemsRatio* = taxa de devolução de itens (número total de itens retornados em relação ao número de itens comprados)
* *monetaryRatio* = taxa de valores devolvidos (valor monetário total dos itens retornados em relação ao valor comprado)
* *frequência* = frequência de devoluções

A mineração de dados com K-means geralmente requer análise adicional dos resultados e mais etapas para entender melhor cada cluster, mas pode fornecer bons clientes potenciais.
Veja algumas maneiras de interpretar esses resultados:

* O cluster 1 (o maior cluster) parece ser um grupo de clientes que não são ativos (todos os valores são zero).
* O cluster 3 parece ser um grupo que se destaca em termos de comportamento de devolução.

## <a name="clean-up-resources"></a>Limpar os recursos

Se você não continuar com este tutorial, exclua o banco de dados tpcxbb_1gb.

## <a name="next-steps"></a>Próximas etapas

Na parte três desta série de tutoriais, você aprendeu a:

* Definir o número de clusters para um algoritmo K-means
* Executar clustering
* Analisar os resultados

Para implantar o modelo de machine learning que você criou, siga a parte quatro desta série de tutoriais:

> [!div class="nextstepaction"]
> [Implantar um modelo de clustering no R com o aprendizado de máquina do SQL](r-clustering-model-deploy.md)
