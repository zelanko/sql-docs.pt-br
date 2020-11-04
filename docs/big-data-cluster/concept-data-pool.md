---
title: O que são pools de dados?
titleSuffix: SQL Server big data clusters
description: Conheça a função de pools de dados do SQL Server em um cluster de Big Data do SQL Server, bem como a arquitetura e a funcionalidade de um pool de dados de SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 73fe5c5b7be90d8c351aa08b3d5fe0247ecfceb0
ms.sourcegitcommit: ab9ddcc16fdfc245cf9a49d1e90bb1ffe3958c38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914321"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de dados em um cluster de Big Data do SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve a função dos *pools de dados do SQL Server* em um cluster de Big Data do SQL Server. As seções a seguir descrevem a arquitetura, a funcionalidade e os cenários de uso de um pool de dados.

Este vídeo de 5 minutos apresenta pools de dados e mostra como consultar dados de pools de dados:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Querying-Data-from-Big-Data-Cluster-Data-Pool/player?WT.mc_id=dataexposed-c9-niner]

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados consiste em uma ou mais instâncias do pool de dados do SQL Server que fornecem armazenamento do SQL Server persistente para o cluster. Ele permite a consulta de desempenho de dados armazenados em cache em fontes de dados externas e o descarregamento de trabalho. Os dados são incluídos no pool de dados usando consultas T-SQL ou de trabalhos do Spark. Para aprimorar o desempenho em grandes conjuntos de dados, os dados ingeridos são distribuídos em fragmentos e armazenados em todas as instâncias do SQL Server no pool. Os métodos de distribuições com suporte são round robin e replicados. Para a otimização de acesso de leitura, um índice columnstore clusterizado é criado em cada tabela em cada instância do pool de dados. Um pool de dados funciona como o data mart de expansão para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

![Data mart de expansão](media/concept-data-pool/data-virtualization-improvements.png)

O acesso às instâncias do SQL Server no pool de dados é gerenciado por meio da instância mestra do SQL Server. Uma fonte de dados externa ao pool de dados é criada, juntamente com as tabelas externas do PolyBase para armazenar o cache de dados. Em segundo plano, o controlador cria um banco de dados no pool de data com tabelas que correspondem às tabelas externas. Na instância mestra do SQL Server, o fluxo de trabalho é transparente; o controlador redireciona as solicitações de tabela externa específicas às instâncias do SQL Server no pool de dados, o que pode ocorrer por meio do pool de computação, executa consultas e retorna o conjunto de resultados. Os dados no pool de dados só podem ser ingeridos ou consultados e não podem ser modificados. Portanto, qualquer atualização de dados exigiria uma remoção da tabela, seguida da recriação dela e de um novo preenchimento de dados subsequente.

## <a name="data-pool-scenarios"></a>Cenários de pool de dados

 A finalidade dos relatórios é um cenário de pool de dados comum. Por exemplo, uma consulta complexa que une várias fontes de dados do PolyBase, usada para um relatório semanal, pode ser descarregada para o pool de dados. Os dados armazenados em cache fornecem uma computação rápida local e eliminam a necessidade de voltar para os conjuntos de dados originais. Da mesma forma, os dados do painel que exigem atualização periódica podem ser armazenados em cache no pool de dados para relatórios otimizados. A exploração de repetição do Machine Learning também poderia se beneficiar do armazenamento em cache de conjuntos de dados no pool de dados.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
