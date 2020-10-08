---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster de Big Data com arquivos de configuração que são integrados à ferramenta de gerenciamento azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48a2c99a029517ebbab24b017bbaeba906b1c6cb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725857"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>Definir configurações de implantação para recursos e serviços de cluster

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Começando com um conjunto predefinido de perfis de configuração internos da ferramenta de gerenciamento `azdata`, você pode facilmente modificar as configurações padrão a fim de melhor atender aos seus requisitos de carga de trabalho do BDC. A estrutura dos arquivos de configuração permite que você atualize de forma granular as configurações de cada serviço do recurso.

Assista a este vídeo de 13 minutos para obter uma visão geral da configuração do cluster de Big Data:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Cluster-Configuration/player?WT.mc_id=dataexposed-c9-niner]

> [!TIP]
> Confira os artigos sobre como configurar **alta disponibilidade** para componentes críticos, como o [SQL Server mestre](deployment-high-availability.md) ou o [nó do nome do HDFS](deployment-high-availability-hdfs-spark.md), para obter detalhes sobre como implantar serviços altamente disponíveis.

Você também pode definir configurações no nível do recurso ou atualizar as configurações de todos os serviços em um recurso. Este é um resumo da estrutura de `bdc.json`:

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

Para atualizar configurações no nível do recurso, como instâncias em um pool, você atualizará a especificação do recurso. Por exemplo, para atualizar o número de instâncias no pool de computação, você modificará esta seção no arquivo de configuração `bdc.json`:

```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

Funciona de forma semelhante para alterar as configurações de um único serviço em um recurso específico. Por exemplo, se quiser alterar as configurações de memória do Spark somente para o componente do Spark no pool de armazenamento, você atualizará o recurso `storage-0` com uma seção `settings` para o serviço `spark` no arquivo de configuração `bdc.json`.

```json
"resources":{
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
                    "spark-defaults-conf.spark.driver.memory": "2g",
                    "spark-defaults-conf.spark.driver.cores": "1",
                    "spark-defaults-conf.spark.executor.instances": "3",
                    "spark-defaults-conf.spark.executor.memory": "1536m",
                    "spark-defaults-conf.spark.executor.cores": "1",
                    "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                    "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                    "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                    "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                    "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
                }
            }
        }
    }
    ...
}
```

Se quiser aplicar as mesmas configurações para um serviço associado a vários recursos, você atualizará o `settings` correspondente na seção `services`. Por exemplo, se quiser definir as mesmas configurações para o Spark no pool de armazenamento e nos pools do Spark, você atualizará a seção `settings` na seção do serviço `spark` no arquivo de configuração `bdc.json`.

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
        }
    }
    ...
}
```

Para personalizar os arquivos de configuração de implantação de cluster, você pode usar qualquer editor de formato JSON, como o VS Code. Para gerar scripts dessas edições para fins de automação, use o comando `azdata bdc config`. Este artigo explica como configurar implantações de cluster de Big Data modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, confira a [diretriz de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Pré-requisitos

- [Instale o azdata](../azdata/install/deploy-install-azdata.md).

- Cada um dos exemplos nesta seção pressupõe que você criou uma cópia de uma das configurações padrão. Para obter mais informações, confira [Criar uma configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria um diretório chamado `custom-bdc` que contém dois arquivos de configuração de implantação JSON, `bdc.json` e `control.json`, com base na configuração `aks-dev-test` padrão:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom-bdc
   ```

## <a name="change-default-docker-registry-repository-and-images-tag"></a><a id="docker"></a> Alterar o Registro, o repositório e a tag de imagens padrão do Docker

Os arquivos de configuração internos, especificamente control.json, incluem uma seção `docker` em que o registro de contêiner, o repositório e a tag de imagens são preenchidos previamente. Por padrão, as imagens necessárias para clusters de Big Data estão no Registro de Contêiner da Microsoft (`mcr.microsoft.com`), no repositório `mssql/bdc`:

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "Cluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-GDR1-ubuntu-16.04",
            "imagePullPolicy": "Always"
        },
        ...
    }
}
```

Antes da implantação, você pode personalizar as configurações de `docker` editando diretamente o arquivo de configuração `control.json` ou usando comandos `azdata bdc config`. Por exemplo, os comandos a seguir estão atualizando um arquivo de configuração control.json `custom-bdc` com um `<registry>`, um `<repository>` e um `<image_tag>` diferentes:

```bash
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.registry=<registry>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.repository=<repository>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.imageTag=<image_tag>"
```

> [!TIP]
> Como melhor prática, você deve usar uma tag de imagem específica da versão e evitar usar a tag de imagem `latest`, pois isso pode causar incompatibilidade de versões, o que causará problemas de integridade do cluster.

> [!TIP]
> As implantações de clusters de Big Data precisam ter acesso ao registro de contêiner e ao repositório do qual será efetuado pull das imagens de contêiner. Se o ambiente não tiver acesso ao Registro de Contêiner da Microsoft padrão, você poderá executar uma instalação offline na qual as imagens necessárias são colocadas primeiro em um repositório privado do Docker. Para obter mais informações sobre instalações offline, confira [Executar uma implantação offline de um cluster de Big Data do SQL Server](deploy-offline.md). Observe que você deve definir as [variáveis de ambiente](deployment-guidance.md#env) `DOCKER_USERNAME` e `DOCKER_PASSWORD` antes de emitir a implantação para garantir que o fluxo de trabalho de implantação tenha acessado seu repositório privado para extrair as imagens.

## <a name="change-cluster-name"></a><a id="clustername"></a> Alterar o nome do cluster

O nome do cluster é o nome do cluster de Big Data e o namespace do Kubernetes que será criado na implantação. Ele é especificado na seguinte parte do arquivo de configuração de implantação `bdc.json`:

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

O comando a seguir envia um par chave-valor para o parâmetro `--json-values` para alterar o nome do cluster de Big Data para `test-cluster`:

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos, sem espaços. Todos os artefatos do Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o nome do cluster especificado.

## <a name="update-endpoint-ports"></a><a id="ports"></a> Atualizar portas de ponto de extremidade

Os pontos de extremidade são definidos para o controlador no `control.json` e para o gateway e a instância mestre do SQL Server nas seções correspondentes no `bdc.json`. A seguinte parte do arquivo de configuração `control.json` mostra as definições de ponto de extremidade para o controlador:

```json
{
  "endpoints": [
    {
      "name": "Controller",
      "serviceType": "LoadBalancer",
      "port": 30080
    },
    {
      "name": "ServiceProxy",
      "serviceType": "LoadBalancer",
      "port": 30777
    }
  ]
}
```

O exemplo a seguir usa JSON embutido para alterar a porta para o ponto de extremidade do `controller`:

```bash
azdata bdc config replace --config-file custom-bdc/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a name="configure-scale"></a><a id="replicas"></a> Configurar a escala

As configurações de cada recurso, como o pool de armazenamento, são definidas no arquivo de configuração `bdc.json`. Por exemplo, a seguinte parte de `bdc.json` mostra uma definição do recurso `storage-0`:

```json
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
                "spark-defaults-conf.spark.driver.memory": "2g",
                "spark-defaults-conf.spark.driver.cores": "1",
                "spark-defaults-conf.spark.executor.instances": "3",
                "spark-defaults-conf.spark.executor.memory": "1536m",
                "spark-defaults-conf.spark.executor.cores": "1",
                "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
            }
        }
    }
}
```

Você pode configurar o número de instâncias em um pool de armazenamento, computação e/ou dados modificando o valor `replicas` de cada pool. O exemplo a seguir usa JSON embutido para alterar esses valores para os pools de armazenamento, computação e dados para `10`, `4` e `4`, respectivamente:

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.compute-0.spec.replicas=4"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

> [!NOTE]
> O número máximo de instâncias validadas para pools de computação e de dados é `8` para cada um. Não há nenhuma imposição desse limite no momento da implantação, mas não recomendamos a configuração de uma escala maior em implantações de produção.

## <a name="configure-storage"></a><a id="storage"></a> Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizada aos pools de armazenamento e dados e atualiza o tamanho da declaração de volume persistente para armazenar dados até 500 GB para o HDFS (pool de armazenamento) e 100 GB para o pool de dados e mestre. 

> [!TIP]
> Para obter mais informações sobre a configuração de armazenamento, confira [Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes](concept-data-persistence.md).

Primeiro, crie um arquivo patch.json como o mostrado abaixo para ajustar as configurações de *armazenamento*

```json
{
        "patch": [
                {
                        "op": "add",
                        "path": "spec.resources.storage-0.spec.storage",
                        "value": {
                                "data": {
                                        "size": "500Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                },
        {
                        "op": "add",
                        "path": "spec.resources.master.spec.storage",
                        "value": {
                                "data": {
                                        "size": "100Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                },
                {
                        "op": "add",
                        "path": "spec.resources.data-0.spec.storage",
                        "value": {
                                "data": {
                                        "size": "100Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                }
        ]
}

```

Em seguida, você pode usar o comando `azdata bdc config patch` para atualizar o arquivo de configuração `bdc.json`.
```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch ./patch.json
```

> [!NOTE]
> Um arquivo de configuração baseado em `kubeadm-dev-test` não tem uma definição de armazenamento para cada pool, mas você pode usar o processo acima para adicionar, se necessário.

## <a name="configure-storage-pool-without-spark"></a><a id="sparkstorage"></a> Configurar o pool de armazenamento sem Spark

Você também pode configurar os pools de armazenamento para serem executados sem o Spark e criar um pool do Spark separado. Essa configuração permite que você dimensione o poder de computação do Spark independentemente do armazenamento. Para ver como configurar o Pool do Spark, confira a seção [Criar um Pool do Spark](#sparkpool) neste artigo.

> [!NOTE]
> Não há suporte para a implantação de um cluster de Big Data sem o Spark. Portanto, você precisa ter `includeSpark` definido como `true` ou precisa criar um [Pool do Spark](#sparkpool) separado com pelo menos uma instância. Você também pode ter o Spark em execução no pool de armazenamento (`includeSpark` é `true`) e ter um Pool do Spark separado.

Por padrão, a configuração `includeSpark` para o recurso do pool de armazenamento é definida como true, portanto, você precisa adicionar o campo `includeSpark` à configuração de armazenamento para fazer alterações. O comando a seguir mostra como editar esse valor usando JSON embutido.

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a name="create-a-spark-pool"></a><a id="sparkpool"></a> Criar um Pool do Spark

Você pode criar um Pool do Spark além das instâncias do Spark em execução no pool de armazenamento ou em vez delas. O exemplo a seguir mostra como criar um Pool do Spark com duas instâncias por meio da aplicação de patch no arquivo de configuração `bdc.json`. 

Primeiro, crie um arquivo `spark-pool-patch.json` como este:

```json
{
    "patch": [
        {
            "op": "add",
            "path": "spec.resources.spark-0",
            "value": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Spark",
                    "replicas": 2
                }
            }
        },
        {
            "op": "add",
            "path": "spec.services.spark.resources/-",
            "value": "spark-0"
        },
        {
            "op": "add",
            "path": "spec.services.hdfs.resources/-",
            "value": "spark-0"
        }
    ]
}
```

Em seguida, execute o comando `azdata bdc config patch`:

```bash
azdata bdc config patch -c custom-bdc/bdc.json -p spark-pool-patch.json
```

## <a name="configure-pod-placement-using-kubernetes-labels"></a><a id="podplacement"></a> Configurar o posicionamento do pod usando rótulos do Kubernetes

Você pode controlar o posicionamento do pod em nós do Kubernetes que têm recursos específicos para acomodar vários tipos de requisitos de carga de trabalho. Usando rótulos do Kubernetes, você pode personalizar quais nós em seu cluster do Kubernetes são usados para implantar recursos de cluster de Big Data, mas também pode restringir quais nós são usados para recursos específicos.
Por exemplo, talvez você queira garantir que os pods do recurso de pool de armazenamento sejam colocados em nós com mais armazenamento, enquanto as instâncias mestre do SQL Server sejam colocadas em nós que tenham recursos de CPU e memória mais elevados. Nesse caso, primeiro você criará um cluster do Kubernetes heterogêneo com diferentes tipos de hardware e, em seguida, [atribuirá os rótulos de nó](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) de acordo. No momento da implantação do cluster Big Data, você pode especificar os mesmos rótulos no nível do cluster para indicar quais nós são usados para o cluster de Big Data usando o atributo `clusterLabel` no arquivo `control.json`. Em seguida, rótulos diferentes serão usados para o posicionamento do nível do pool. Esses rótulos podem ser especificados nos arquivos de configuração da implantação do cluster de Big Data usando o atributo `nodeLabel`. O Kubernetes atribui o pods em nós que correspondem aos rótulos especificados. As chaves de rótulo específicas que precisam ser adicionadas aos nós no cluster do Kubernetes são `mssql-cluster` (para indicar quais nós são usados para o cluster de Big Data) e `mssql-resource` (para indicar em quais nós específicos os pods são colocados para vários recursos). Os valores desses rótulos podem ser qualquer cadeia de caracteres que você escolher.

> [!NOTE]
> Devido à natureza do pods que coletam as métricas no nível do nó, pods `metricsdc` são implantadas em todos os nós com o rótulo `mssql-cluster`, e o `mssql-resource` não se aplica a esses pods.

O exemplo a seguir mostra como editar um arquivo de configuração personalizado para incluir um rótulo de nó `bdc` para todo o cluster de Big Data, um rótulo `bdc-master` para colocar pods da instância mestre do SQL Server em um nó específico, `bdc-storage-pool` para recursos do pool de armazenamento, `bdc-compute-pool` para pods do pool de computação e do pool de dados e `bdc-shared` para o restante dos recursos. 

Primeiro, rotule os nós do Kubernetes:

```bash
kubectl label node <kubernetesNodeName1> mssql-cluster=bdc mssql-resource=bdc-shared --overwrite=true
kubectl label node <kubernetesNodeName2> mssql-cluster=bdc mssql-resource=bdc-master --overwrite=true
kubectl label node <kubernetesNodeName3> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName4> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName5> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName6> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName7> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName8> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
```

Em seguida, atualize os arquivos de configuração da implantação do cluster para incluir os valores de rótulo. Este exemplo pressupõe que você esteja personalizando arquivos de configuração em um perfil `custom-bdc`. Por padrão, não há chaves `nodeLabel` e `clusterLabel` nas configurações internas, portanto, você precisará editar um arquivo de configuração personalizado manualmente ou usar os comandos `azdata bdc config add` para fazer as edições necessárias.

```bash
azdata bdc config add -c custom-bdc/control.json -j "$.spec.clusterLabel=bdc"
azdata bdc config add -c custom-bdc/control.json -j "$.spec.nodeLabel=bdc-shared"

azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.master.spec.nodeLabel=bdc-master"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.compute-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.data-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.storage-0.spec.nodeLabel=bdc-storage-pool"

# below can be omitted in which case we will take the node label default from the control.json
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.nmnode-0.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.sparkhead.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.zookeeper.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.gateway.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.appproxy.spec.nodeLabel=bdc-shared"
```
>[!NOTE]
> A melhor prática evita fornecer ao mestre Kubernetes qualquer uma das funções do BDC acima. Se você planejar atribuir essas funções ao nó mestre do Kubernetes de qualquer maneira, precisará [remover o taint ``master:NoSchedule``.](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/) Lembre-se: isso pode sobrecarregar o nó mestre e inibir a capacidade dele de executar as funções de gerenciamento do Kubernetes em clusters grandes. É normal ver alguns pods agendados para o mestre em qualquer implantação: eles já toleram o taint ``master:NoSchedule`` e são usados principalmente para ajudar a gerenciar o cluster. 

## <a name="other-customizations-using-json-patch-files"></a><a id="jsonpatch"></a> Outras personalizações usando arquivos de patch JSON

Os arquivos de patch JSON definem várias configurações ao mesmo tempo. Para obter mais informações sobre patches JSON, confira [Patches JSON em Python](https://github.com/stefankoegl/python-json-patch) e o [JSONPath Online Evaluator](https://jsonpath.com/).

Os arquivos `patch.json` a seguir executam as seguintes alterações:

- Atualizar a porta de um ponto de extremidade único em `control.json`.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    }
  ]
}
```

- Atualizar todos os pontos de extremidade (`port` e `serviceType`) em `control.json`.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
          "serviceType": "LoadBalancer",
          "port": 30778,
          "name": "ServiceProxy"
        }
      ]
    }
  ]
}
```

- Atualizar as configurações de armazenamento do controlador em `control.json`. Essas configurações são aplicáveis a todos os componentes do cluster, a menos que sejam substituídas no nível do pool.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage",
      "value": {
        "data": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "100Gi"
        },
        "logs": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "32Gi"
        }
      }
    }
  ]
}
```

- Atualizar o nome da classe de armazenamento em `control.json`.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage.data.className",
      "value": "managed-premium"
    }
  ]
}
```

- Atualizar as configurações de armazenamento do pool de armazenamento em `bdc.json`.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- Atualizar as configurações do Spark para o pool de armazenamento em `bdc.json`.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
      "value": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
      }
    }
  ]
}
```

> [!TIP]
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, confira [Referência de arquivo de configuração de implantação para clusters de Big Data](reference-deployment-config.md).

Use os comandos `azdata bdc config` para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo `patch.json` a um arquivo de configuração de implantação de destino `custom-bdc/bdc.json`.

```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>Desabilitar ElasticSearch para execução em modo privilegiado

Por padrão, o contêiner ElasticSearch é executado no modo de privilégio no cluster Big Data. Essa configuração garante que, no momento da inicialização do contêiner, ele tenha permissões suficientes para atualizar uma configuração no host necessária quando o ElasticSearch processa uma quantidade maior de logs. Você pode encontrar mais informações sobre este tópico [neste artigo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html). 

Para desabilitar o contêiner que executa o ElasticSearch para execução no modo privilegiado, você deve atualizar a seção `settings` no `control.json` e especificar o valor de `vm.max_map_count` para `-1`. Este é um exemplo de como esta seção ficaria:

```json
{
    "apiVersion": "v1",
    "metadata": {...},
    "spec": {
        "docker": {...},
        "storage": {...},
        "endpoints": [...],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
            }
        }
    }
}
```

Você pode editar manualmente o `control.json` e adicionar a seção acima ao `spec` ou pode criar um arquivo de patch `elasticsearch-patch.json` como abaixo e usar a CLI do `azdata` para corrigir o arquivo `control.json`:

```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.settings",
      "value": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
        }
      }
    }
  ]
}
```

Execute este comando para aplicar o patch no arquivo de configuração:

```bash
azdata bdc config patch --config-file custom-bdc/control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> Recomendamos, como uma melhor prática, atualizar manualmente a configuração `max_map_count` em cada host no cluster do Kubernetes de acordo com as instruções [neste artigo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).

## <a name="turn-pods-and-nodes-metrics-collection-onoff"></a>Ativar/desativar coleta de métricas de pods e nós

O SQL Server 2019 CU5 habilitou duas opções de recurso para controlar a coleta de métricas de pods e nós. Caso você esteja usando soluções diferentes para monitorar sua infraestrutura de Kubernetes, é possível desligar a coleção de métricas internas para nós de host e pods definindo *allowNodeMetricsCollection* e *allowPodMetricsCollection* como *false* no arquivo de configuração de implantação *control.json*. Para ambientes do OpenShift, essas configurações são definidas como *false* por padrão nos perfis de implantação internos, pois a coleta de métricas de pod e de nó exige capacidades privilegiadas.
Execute este comando para atualizar os valores dessas configurações em seu arquivo de configuração personalizado usando a CLI *azdata*:

```bash
 azdata bdc config replace -c custom-bdc/control.json -j "$.security.allowNodeMetricsCollection=false"
 azdata bdc config replace -c custom-bdc/control.json -j "$.security.allowPodMetricsCollection=false"
 ```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o uso de arquivos de configuração em implantações de cluster de Big Data, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile).