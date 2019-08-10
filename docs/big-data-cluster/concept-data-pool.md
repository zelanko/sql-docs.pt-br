---
title: O que são pools de dados?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o pool de dados em um cluster de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f9355508e4d32dd9a6152781fba325ded2fa7425
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958732"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>O que são pools de dados em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função dos *Pools de dados do SQL Server* em um cluster de Big Data do SQL Server 2019 (versão prévia). As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de dados do SQL.

## <a name="data-pool-architecture"></a>Arquitetura do pool de dados

Um pool de dados é composto por uma ou mais instâncias de pool de dados do SQL Server. As instâncias de pool de dados do SQL fornecem armazenamento persistente no SQL Server para o cluster. Um pool de dados é usado para ingerir dados de consultas SQL ou de trabalhos do Spark. Para fornecer um melhor desempenho em grandes conjuntos de dados, os dados em um pool de dados são distribuídos em fragmentos entre as instâncias membro do pool de dados do SQL.

## <a name="scale-out-data-marts"></a>Data marts de expansão

Os pools de dados permitem a criação de data marts de expansão, em que dados externos de várias fontes são incluídos no pool de dados. Como os dados são distribuídos entre instâncias do pool de dados, consultas paralelas em relação aos dados organizados são mais eficientes.

![Data mart de expansão](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de Big Data do SQL Server, confira os seguintes recursos:

- [O que são os clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de Big Data do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
