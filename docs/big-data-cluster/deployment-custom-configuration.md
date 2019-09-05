---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster de Big Data com arquivos de configuração.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a0da84d60a9513b0ca81a0256218928372882e72
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304824"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>Definir configurações de implantação para recursos e serviços de cluster

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partir de um conjunto predefinido de perfis de configuração que são criados na ferramenta de gerenciamento do azdata, você pode facilmente modificar as configurações padrão para atender melhor aos seus requisitos de carga de trabalho do BDC. A partir da versão Release Candidate, a estrutura dos arquivos de configuração foi atualizada para permitir que você atualize de maneira granular as configurações por cada serviço do recurso. 

Você também pode definir configurações de nível de recurso ou atualizar as configurações de todos os serviços em um recurso. Aqui está um resumo da estrutura para o **BDC. JSON**:

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

Para atualizar configurações de nível de recurso, como instâncias em um pool, você atualizará a especificação de recurso. Por exemplo, para atualizar o número de instâncias no pool de computação, você modificará esta seção no arquivo de configuração do **BDC. JSON** :
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

Da mesma forma, para alterar as configurações de um único serviço em um recurso específico. Por exemplo, se você quiser alterar as configurações de memória do Spark apenas para o componente do Spark no pool de armazenamento, atualizará o recurso de **armazenamento-0** com uma seção de **configurações** para o serviço do **Spark** no arquivo de configuração do **BDC. JSON** .
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
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

Se desejar aplicar as mesmas configurações para um serviço associado a vários recursos, você atualizará as **configurações** correspondentes na seção **Serviços** . Por exemplo, se você quiser definir as mesmas configurações para o Spark no pool de armazenamento e nos pools do Spark, você atualizará a seção de **configurações** na seção serviço do **Spark** no arquivo de configuração do **BDC. JSON** .

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


Para personalizar os arquivos de configuração de implantação de cluster, você pode usar qualquer editor de formato JSON, como o VS Code. Para gerar scripts dessas edições para fins de automação, use o comando **azdata bdc config**. Este artigo explica como configurar implantações de cluster de Big Data modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, confira a [diretriz de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Pré-requisitos

- [Instale o azdata](deploy-install-azdata.md).

- Cada um dos exemplos nesta seção pressupõe que você criou uma cópia de uma das configurações padrão. Para obter mais informações, confira [Criar uma configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria um diretório `custom` chamado que contém dois arquivos de configuração de implantação JSON, **BDC. JSON** e **Control. JSON**, com base na configuração padrão de **AKs-dev-Test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Alterar o nome do cluster

O nome do cluster é o nome do cluster de Big Data e o namespace do Kubernetes que será criado na implantação. Ele é especificado na seguinte parte do arquivo de configuração de implantação do **BDC. JSON** :

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

O comando a seguir envia um par chave-valor para o parâmetro **--json-values** para alterar o nome do cluster de Big Data para **test-cluster**:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos, sem espaços. Todos os artefatos do Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o nome do cluster especificado.

## <a id="ports"></a> Atualizar portas de ponto de extremidade

Os pontos de extremidade são definidos para o controlador no **Control. JSON** e para o gateway e SQL Server instância mestra nas seções correspondentes no **BDC. JSON**. A seguinte parte do arquivo de configuração **control.json** mostra as definições de ponto de extremidade para o controlador:

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

O exemplo a seguir usa JSON embutido para alterar a porta para o ponto de extremidade do **controlador**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurar as réplicas do pool

As configurações de cada recurso, como o pool de armazenamento, são definidas no arquivo de configuração do **BDC. JSON** . Por exemplo, a seguinte parte do **BDC. JSON** mostra uma definição de recurso **de armazenamento-0** :

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
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

Você pode configurar o número de instâncias em um pool modificando o valor das **réplicas** para cada pool. O exemplo a seguir usa JSON embutido para alterar esses valores para os pools de armazenamento e de dados para `10` e `4`, respectivamente:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizada ao armazenamento e aos pools de dados e atualiza o tamanho da declaração de volume persistente para armazenar dados em 500 GB para HDFS (pool de armazenamento) e 100 GB para o pool de dados. Primeiro, crie um arquivo patch.json, como mostrado abaixo, que inclui a nova seção de *armazenamento*, além *tipo* e *réplicas*

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
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

Em seguida, você pode usar o comando **azdata BDC config patch** para atualizar o arquivo de configuração do **BDC. JSON** .
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> Um arquivo de configuração baseado em **kubeadm-dev-test** não tem uma definição de armazenamento para cada pool, mas você pode usar o processo acima para adicionar, se necessário.

Para obter mais informações sobre a configuração de armazenamento, confira [Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configurar o pool de armazenamento sem Spark

Você também pode configurar os pools de armazenamento para serem executados sem o Spark e criar um pool do Spark separado. Isso permite que você dimensione o poder de computação do Spark independentemente do armazenamento. Para ver como configurar o pool do Spark, confira o [exemplo de arquivo de patch JSON](#jsonpatch) no final deste artigo.


Por padrão, a configuração **includeSpark** do recurso de pool de armazenamento é definida como true, portanto, você deve editar o campo **includeSpark** na configuração de armazenamento para fazer alterações. O comando a seguir mostra como editar esse valor usando JSON embutido.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> Configurar o posicionamento do pod usando rótulos do Kubernetes

Você pode controlar o posicionamento do pod em nós do Kubernetes que têm recursos específicos para acomodar vários tipos de requisitos de carga de trabalho. Por exemplo, talvez você queira garantir que os pods de recursos do pool de armazenamento sejam colocados em nós com mais armazenamento, ou SQL Server instâncias mestre sejam colocadas em nós que tenham recursos de CPU e memória maiores. Nesse caso, primeiro você criará um cluster do Kubernetes heterogêneo com diferentes tipos de hardware e, em seguida, [atribuirá os rótulos de nó](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) de acordo. No momento da implantação do cluster de Big Data, você pode especificar os mesmos rótulos no nível de pool no arquivo de configuração de implantação de cluster. Em seguida, o Kubernetes cuidará do ajuste dos pods em nós que correspondem aos rótulos especificados. A chave de rótulo específica que precisa ser adicionada aos nós no cluster kubernetes é **MSSQL-cluster-Wide**. O valor desse rótulo pode ser qualquer cadeia de caracteres que você escolher.

O exemplo a seguir mostra como editar um arquivo de configuração personalizado para incluir uma configuração de rótulo de nó para a instância mestra de SQL Server, pool de computação, pool de dados & pool de armazenamento. Não há nenhuma chave *nodeLabel* nas configurações internas, portanto, será necessário editar um arquivo de configuração personalizado manualmente ou criar um arquivo de patch e aplicá-lo ao arquivo de configuração personalizado. O Pod da instância mestra de SQL Server será implantado em um nó que contém um rótulo **MSSQL-cluster-Wide** com o valor **BDC-Master**. O pool de computação e os pods do pool de dados serão implantados em nós que contêm um rótulo **MSSQL-cluster-Wide** com o valor **BDC-SQL**. O pods do pool de armazenamento será implantado em nós que contêm um rótulo **MSSQL-cluster-Wide** com valor **BDC-Storage**.

Crie um arquivo chamado **patch.json** no diretório atual com o conteúdo a seguir:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a> Arquivos de patch JSON

Os arquivos de patch JSON definem várias configurações ao mesmo tempo. Para obter mais informações sobre patches JSON, confira [Patches JSON em Python](https://github.com/stefankoegl/python-json-patch) e o [JSONPath Online Evaluator](https://jsonpath.com/).

O arquivo **patch.json** a seguir executa as seguintes alterações:

- Atualiza a porta de um ponto de extremidade único em **control.json**.
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

- Atualiza todos os pontos de extremidade (**porta** e **serviceType**) em **control.json**.
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

- Atualiza as configurações de armazenamento do controlador em **control.json**. Essas configurações são aplicáveis a todos os componentes do cluster, a menos que sejam substituídas no nível do pool.
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

- Atualiza o nome da classe de armazenamento em **control.json**.
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

- Atualiza as configurações de armazenamento do pool para o pool de armazenamento no **BDC. JSON**.
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

- Atualiza as configurações do Spark para o pool de armazenamento no **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
      "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
      }
    }
  ]
}
```

- Cria um pool do Spark com 2 instâncias no **BDC. JSON**.
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
    },
    {
      "op": "add",
      "path": "spec.services.spark.settings",
      "value": {
        "DriverMemory": "2g",
        "DriverCores": "1",
        "ExecutorInstances": "2",
        "ExecutorMemory": "2g",
        "ExecutorCores": "1"
      }
    }
  ]
}
```

> [!TIP]
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, confira [Referência de arquivo de configuração de implantação para clusters de Big Data](reference-deployment-config.md).

Use o comando **azdata bdc config** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo **patch. JSON** a um arquivo de configuração de implantação de destino **Custom/BDC. JSON**.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>Desabilitar ElasticSearch para execução em modo privilegiado
Por padrão, o contêiner ElasticSearch é executado no modo de privilégio no cluster Big Data. Isso é para garantir que, no tempo de inicialização do contêiner, o contêiner tenha permissões suficientes para atualizar uma configuração no host necessária quando o ElasticSearch processa uma quantidade maior de logs. Você pode encontrar mais informações sobre este tópico neste [artigo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html). 

Para desabilitar o contêiner que executa o ElasticSearch para ser executado no modo privilegiado, você deve atualizar a seção de **configurações** no **Control. JSON** e especificar o valor de **VM. Max _map_count** como **-1**. Aqui está um exemplo de como esta seção ficaria assim:
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

Você pode manualmente editar o **Control. JSON** e adicionar a seção acima à **especificação**, ou pode criar um arquivo de patch **elasticsearch-patch. JSON** como abaixo e usar a CLI do **azdata** para corrigir o arquivo **config. JSON** :

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
        "storage": {
            "data": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "15Gi"
            },
            "logs": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

Execute este comando para corrigir o arquivo de configuração:
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> Recomendamos como uma prática recomendada atualizar manualmente a configuração **max_map_count** manualmente em cada host no cluster kubernetes de acordo com as instruções neste [artigo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar arquivos de configuração no Big data implantações de cluster, consulte [como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em kubernetes](deployment-guidance.md#configfile).
