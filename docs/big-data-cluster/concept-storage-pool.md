---
title: O que é o pool de armazenamento?
titleSuffix: SQL Server big data clusters
description: Conheça a função do pool de armazenamento do SQL Server em um cluster de Big Data do SQL Server 2019, bem como a arquitetura e a funcionalidade de um pool de armazenamento do SQL.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16a0309eda16ceab13720c83e1c36045dee2c1ff
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725047"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>O que é o pool de armazenamento ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve a função do *Pool de armazenamento do SQL Server* em um BDC ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]). As seções a seguir descrevem a arquitetura e a funcionalidade de um pool de armazenamento do SQL.

## <a name="storage-pool-architecture"></a>Arquitetura do pool de armazenamento

O pool de armazenamento é o cluster do HDFS local (Hadoop) no ecossistema BDC do SQL Server. Ele fornece armazenamento persistente para dados não estruturados e semiestruturados. Arquivos de dados, como Parquet ou texto delimitado, podem ser armazenados no pool de armazenamento. Para persistir o armazenamento, cada pod no pool tem um Volume Persistente anexado a ele. Os arquivos do pool de armazenamento podem ser acessados via o [PolyBase](../relational-databases/polybase/polybase-guide.md) por meio do SQL Server ou diretamente usando um Gateway do Apache Knox.

Uma configuração do HDFS clássico consiste em um conjunto de computadores de hardware de mercadoria com armazenamento anexado. Os dados são distribuídos em blocos em todos os nós para fins de tolerância a falhas e aproveitamento do processamento paralelo. Um dos nós no cluster funciona como o Nó de Nome e contém as informações de metadados sobre os arquivos localizados nos nós de dados.

![Configuração do HDFS clássico](media/concept-storage-pool/classic-hdfs-setup.png)

O pool de armazenamento consiste em nós de armazenamento que são membros de um cluster HDFS. Ele executa um ou mais pods do Kubernetes e cada pod hospeda os seguintes contêineres:

- Um contêiner Hadoop vinculado a um Volume Persistente (armazenamento). Todos os contêineres desse tipo juntos formam o cluster Hadoop. No contêiner Hadoop, há um processo do gerenciador de nós do YARN que pode criar processos de trabalho do Apache Spark sob demanda. O nó de cabeçalho do Spark hospeda o metastore do hive, o histórico do Spark e os contêineres do histórico de trabalhos do YARN.
- Uma instância do SQL Server para ler dados do HDFS usando a tecnologia OpenRowSet.
- `collectd` para coletar dados de métricas.
- `fluentbit` para coletar dados de log.

![arquitetura do pool de armazenamento](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>Responsabilidades

Os nós de armazenamento são responsáveis por:

- Ingestão de dados por meio do Apache Spark.
- Armazenamento de dados no HDFS (Parquet e formato de texto delimitado). O HDFS também fornece persistência de dados, pois os dados do HDFS são distribuídos em todos os nós de armazenamento no cluster no BDC do SQL.
- Acesso a dados por meio dos pontos de extremidade do HDFS e do SQL Server.

## <a name="accessing-data"></a>Accessing data

Os principais métodos para acessar os dados no pool de armazenamento são:

- Trabalhos do Spark.
- Utilização de tabelas externas do SQL Server para permitir a consulta de dados usando nós de computação do PolyBase e as instâncias de SQL Server em execução nos nós do HDFS.

Você também pode interagir com o HDFS usando:

- Azure Data Studio.
- A ferramenta de cliente azdata.
- O kubectl para emitir comandos para o contêiner Hadoop.
- Gateway de HTTP do HDFS.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
