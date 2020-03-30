---
title: Implantar o HDFS ou o Spark com alta disponibilidade
titleSuffix: SQL Server Big Data Clusters
description: Saiba como implantar Clusters de Big Data do SQL Server com alta disponibilidade.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 25a6b733eed0611b43fb1f17ad0fe8a0cc1d690a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75720788"
---
# <a name="deploy-hdfs-name-node-and-shared-spark-services-in-a-highly-available-configuration"></a>Implante o nó de nome do HDFS e serviços compartilhados do Spark em uma configuração altamente disponível

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Além de implantar a instância mestre do SQL Server em uma configuração altamente disponível usando grupos de disponibilidade, você pode implantar outros serviços críticos no cluster de Big Data para garantir um nível maior de confiabilidade. Você pode configurar o `HDFS name node` e os serviços compartilhados do Spark agrupados em `sparkhead` com uma réplica adicional. Nesse caso, `Zookeeper` também é implantado no cluster de Big Data para servir como coordenador de clusters e repositório de metadados para os seguintes serviços: 

- Nó de nome do HDFS
- Livy e Yarn Resource Manager. 

O Spark History, o Histórico de Trabalhos e o serviço de metadados do Hive são serviços sem estado. O ZooKeeper não está envolvido na garantia da integridade do serviço desses componentes. 

Implantar várias réplicas nesses serviços gera melhorias de escalabilidade, confiabilidade e balanceamento de carga das cargas de trabalho entre as réplicas disponíveis.

> [!NOTE]
> Os seguintes serviços são implantados como contêineres no pod `sparkhead`: 
> - Livy
> - Yarn Resource Manager
> - Spark History
> - Histórico de Trabalhos
> - Serviço de metadados do Hive  
>

A imagem a seguir mostra uma implantação de HA do Spark em um cluster de Big Data do SQL Server:

:::image type="content" source="media/deployment-high-availability-hdfs-spark/spark-ha.png" alt-text="spark-ha-bdc":::

A imagem a seguir mostra uma implantação de HA do HDFS em um cluster de Big Data do SQL Server:

:::image type="content" source="media/deployment-high-availability-hdfs-spark/hdfs-ha.png" alt-text="hdfs-ha-bdc":::

## <a name="deploy"></a>Implantar

Se o nó de nome ou o cabeçalho do Spark estiver configurado com duas réplicas, você também precisará configurar o recurso do ZooKeeper com três réplicas. Em uma configuração altamente disponível para o nó de nome do HDFS, dois pods hospedam as duas réplicas. Os pods são `nmnode-0` e `nmnode-1`. Esta configuração é ativa-passiva. Somente um dos nós de nome fica ativo por vez. O outro fica em espera e se torna ativo como resultado de um evento de failover. 

Você pode usar o `aks-dev-test-ha` ou os perfis de configuração internos do `kubeadm-prod` para começar a personalizar a implantação do cluster de Big Data. Esses perfis incluem as configurações necessárias para os recursos que você pode definir para alta disponibilidade adicional. Por exemplo, abaixo está uma seção do arquivo de configuração `bdc.json` que é relevante para implantar o nó de nome do HDFS, o ZooKeeper e recursos compartilhados do Spark (`sparkhead`) com alta disponibilidade.  

```json
{
  ...
    "nmnode-0": {
        "spec": {
            "replicas": 2
        }
    },
    "sparkhead": {
        "spec": {
            "replicas": 2
        }
    },
    "zookeeper": {
        "spec": {
            "replicas": 3
        }
    },
  ...
}
```

Como melhor prática, em uma implantação de produção, você também deve configurar a replicação de bloco do HDFS para 3. Essa configuração já está especificada nos perfis `aks-dev-test-ha` e `kubeadm-prod`. Veja a seção abaixo do arquivo de configuração `bdc.json`:

```json
{
  ...
  "hdfs": {
      "resources": [
          "nmnode-0",
          "zookeeper",
          "storage-0",
          "sparkhead"
      ],
      "settings": {
          "hdfs-site.dfs.replication": "3"
      }
  },
  ...
}
```

## <a name="known-limitations"></a>Limitações conhecidas

Os problemas e limitações conhecidos com a configuração de alta disponibilidade para os serviços do Hadoop nos clusters de Big Data do SQL Server incluem:

- Todas as configurações devem ser especificadas no momento da implantação do cluster de Big Data. Com a versão SQL Server 2019 CU1, você não pode habilitar a configuração de alta disponibilidade após a implantação.

## <a name="next-steps"></a>Próximas etapas

- Para obter mais informações sobre o uso de arquivos de configuração em implantações de cluster de Big Data, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile).
- Para obter mais informações sobre as opções de alta disponibilidade do SQL Server mestre nos clusters de Big Data, confira o tópico [Implantar a instância mestre do SQL Server com alta disponibilidade](deployment-high-availability.md).
