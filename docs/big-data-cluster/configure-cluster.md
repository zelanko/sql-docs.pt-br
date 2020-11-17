---
title: Configurar cluster
titleSuffix: Configure a SQL Server big data cluster
description: Visão geral de como configurar um cluster de Big Data do SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549979"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>Configurar um cluster de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Você pode configurar propriedades para a instância mestra do SQL Server, o Apache Spark e o Apache Hadoop no Cluster de Big Data do SQL Server 2019 no momento da implantação.

Após a implantação, os Clusters de Big Data não dão suporte à modificação das propriedades de configuração.

## <a name="configuration-scopes"></a>Escopos de configuração
A configuração de Clusters de Big Data tem dois níveis de escopo: `service` e `resource`. A hierarquia das configurações segue nessa ordem também, da mais alta para a mais baixa. Os componentes do BDC utilizarão o valor da configuração definida no escopo mais baixo. Se a configuração não estiver definida em determinado escopo, ela herdará o valor de seu escopo pai mais alto.

Por exemplo, talvez você queira definir o número padrão de núcleos que o driver do Spark usará nos `resources` Pool de Armazenamento e Sparkhead. É possível fazer isso de duas formas: 
- Especifique um valor de núcleos padrão no escopo de serviço `Spark`  
- Especifique um valor de núcleos padrão no escopo de recurso `storage-0` e `sparkhead`

No primeiro cenário, todos os recursos de escopo inferior do serviço Spark (Pool de Armazenamento e Sparkhead) *herdarão* o número padrão de núcleos do valor padrão do serviço Spark.

No segundo cenário, cada recurso usará o valor definido em seu respectivo escopo.

Se o número padrão de núcleos estiver configurado no escopo de serviço e de recurso, o valor do escopo de recurso substituirá o valor do escopo de serviço, pois esse é o escopo mais baixo **definido pelo usuário** para a configuração especificada.

Confira informações específicas sobre a configuração nos artigos apropriados:

Como fazer: 
- [Configurar a instância mestra do [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)
- [Configurar Apache Spark e Apache Hadoop em Clusters de Big Data](configure-spark-hdfs.md)

Referência: 
- [Propriedades de configuração da instância mestra do SQL Server](reference-config-master-instance.md)
- [Propriedades de configuração do Apache Spark e Apache Hadoop (HDFS)](reference-config-spark-hadoop.md)
