---
title: Apache Spark e Apache Hadoop
titleSuffix: Configure Apache Spark and Apache Hadoop in Big Data Clusters
description: Os Clusters de Big Data do SQL Server permitem as soluções Spark e HDFS. Saiba como configurá-los.
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 53d7b050fe1269f704a38ca5542c0dae6fdfd0f7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724997"
---
# <a name="configure-apache-spark-and-apache-hadoop-in-big-data-clusters"></a>Configurar Apache Spark e Apache Hadoop em Clusters de Big Data

Para configurar o Apache Spark e o Apache Hadoop em Clusters de Big Data, você precisa modificar o perfil de cluster no momento da implantação.

Um cluster de Big Data tem quatro categorias de configuração: 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`, `hdfs`, `spark`, `sql` são serviços. Cada serviço é mapeado para a mesma categoria de configuração nomeada. Todas as configurações de gateway vão para a categoria `gateway`. 

Por exemplo, todas as configurações no `hdfs` de serviço pertencem à categoria `hdfs`. Observe que todas as configurações do Hadoop (core-site), HDFS e ZooKeeper pertencem à categoria `hdfs`. Todas as configurações de metastore do Livy, Spark, Yarn, Hive pertencem à categoria `spark`. 

As [configurações com suporte](reference-config-spark-hadoop.md#supported-configurations) listam as propriedades do Apache Spark e do Hadoop que você pode definir ao implantar um Cluster de Big Data do SQL Server.

As seções a seguir listam as propriedades que você **não pode** modificar em um cluster:

- [Configurações do `spark` não compatíveis](reference-config-spark-hadoop.md#unsupported-spark-configurations)
- [Configurações do `hdfs` não compatíveis](reference-config-spark-hadoop.md#unsupported-hdfs-configurations)
- [Configurações do `gateway` não compatíveis](reference-config-spark-hadoop.md#unsupported-gateway-configurations)


## <a name="configurations-via-cluster-profile"></a>Configurações por meio do perfil do cluster

No perfil de cluster, há recursos e serviços. No momento da implantação, podemos especificar as configurações de uma das duas maneiras: 

* Em primeiro lugar, no nível de recurso: 

   Os seguintes exemplos são os arquivos de patch para o perfil: 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.zookeeper.spec.settings", 
         "value": { 
           "hdfs": { 
             "zoo-cfg.syncLimit": "6" 
           } 
         } 
   }
   ```

   Ou: 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.gateway.spec.settings", 
         "value": { 
           "gateway": { 
             "gateway-site.gateway.httpclient.socketTimeout": "95s" 
           } 
         } 
   } 
   ```

* Em segundo lugar, no nível de serviço. Atribua vários recursos a um serviço e especifique as configurações para o serviço.

Confira abaixo um exemplo do arquivo de patch do perfil para definir o tamanho do bloco do HDFS: 

   ```json
   { 
         "op": "add", 
         "path": "spec.services.hdfs.settings", 
         "value": { 
           "hdfs-site.dfs.block.size": "268435456" 
        } 
   } 
   ```

O `hdfs` de serviço é definido como:

```json
{ 
  "spec": { 
   "services": { 
     "hdfs": { 
        "resources": [ 
          "nmnode-0", 
          "zookeeper", 
          "storage-0", 
          "sparkhead" 
        ], 
        "settings":{ 
          "hdfs-site.dfs.block.size": "268435456" 
        } 
      } 
    } 
  } 
} 
```
 
> [!NOTE]
> Configurações de nível de recurso substituem configurações de nível de serviço. Um recurso pode ser atribuído a vários serviços.

## <a name="enable-spark-in-the-storage-pool"></a>Habilitar o Spark no pool de armazenamento
Além das configurações compatíveis do Apache, também oferecemos a capacidade de configurar se os trabalhos do Spark podem ser executados no pool de armazenamento. Esse valor booliano, `includeSpark`, está no arquivo de configuração `bdc.json` em `spec.resources.storage-0.spec.settings.spark`.

Um exemplo de definição de pool de armazenamento no bdc.json pode ser assim:
```json
...
"storage-0": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Storage",
                    "replicas": 2,
                    "settings": {
                        "spark": {
                            "includeSpark": "true"
                        }
                    }
                }
            }
```


## <a name="limitations"></a>Limitações

As configurações só podem ser especificadas no nível de categoria. Para especificar várias configurações com a mesma subcategoria, não podemos extrair o prefixo comum no perfil de cluster. 

```json
{ 
      "op": "add", 
      "path": "spec.services.hdfs.settings.core-site.hadoop", 
      "value": { 
        “proxyuser.xyz.users”: “*”, 
        “proxyuser.abc.users”: “*” 
     } 
} 
```

## <a name="next-steps"></a>Próximas etapas

- [Propriedades de configuração do Apache Spark e Apache Hadoop (HDFS).](reference-config-spark-hadoop.md)
- [Referência de `azdata`](../azdata/reference/reference-azdata.md)
- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)