---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster de Big Data com arquivos de configuração.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7d04df5bf881f285ab28508443fbf0ce1056fada
ms.sourcegitcommit: 316c25fe7465b35884f72928e91c11eea69984d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68969498"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Definir configurações de implantação para clusters de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar os arquivos de configuração de implantação de cluster, você pode usar qualquer editor de formato JSON, como o VS Code. Para gerar scripts dessas edições para fins de automação, use o comando **azdata bdc config**. Este artigo explica como configurar implantações de cluster de Big Data modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, confira a [diretriz de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Pré-requisitos

- [Instale o azdata](deploy-install-azdata.md).

- Cada um dos exemplos nesta seção pressupõe que você criou uma cópia de uma das configurações padrão. Para obter mais informações, confira [Criar uma configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria um diretório chamado `custom` que contém dois arquivos de configuração de implantação JSON, **cluster.json** e **control.json**, com base na configuração **aks-dev-test** padrão:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Alterar o nome do cluster

O nome do cluster é o nome do cluster de Big Data e o namespace do Kubernetes que será criado na implantação. Ele é especificado na seguinte parte do arquivo de configuração de implantação **cluster.json**:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

O comando a seguir envia um par chave-valor para o parâmetro **--json-values** para alterar o nome do cluster de Big Data para **test-cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos, sem espaços. Todos os artefatos do Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o nome do cluster especificado.

## <a id="ports"></a> Atualizar portas de ponto de extremidade

Os pontos de extremidade são definidos para o controlador no **control.json** e para o gateway e a instância mestre do SQL Server nas seções correspondentes no **cluster.json**. A seguinte parte do arquivo de configuração **control.json** mostra as definições de ponto de extremidade para o controlador:

```json
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
```

O exemplo a seguir usa JSON embutido para alterar a porta para o ponto de extremidade do **controlador**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurar as réplicas do pool

As características de cada pool, como o pool de armazenamento, são definidas no arquivo de configuração **cluster.json**. Por exemplo, a seguinte parte do **cluster.json** mostra uma definição de pool de armazenamento:

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

Você pode configurar o número de instâncias em um pool modificando o valor das **réplicas** para cada pool. O exemplo a seguir usa JSON embutido para alterar esses valores para os pools de armazenamento e de dados para `10` e `4`, respectivamente:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizada ao pool de armazenamento e atualiza o tamanho da declaração de volume persistente para armazenar dados até 100 Gb. Primeiro, crie um arquivo patch.json, como mostrado abaixo, que inclui a nova seção de *armazenamento*, além *tipo* e *réplicas*

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "storage":{
        "data":{
                "size": "100Gi",
                "className": "myStorageClass",
                "accessMode":"ReadWriteOnce"
                },
        "logs":{
                "size":"32Gi",
                "className":"myStorageClass",
                "accessMode":"ReadWriteOnce"
                }
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

Em seguida, use o comando **azdata bdc config patch** para atualizar o arquivo de configuração **cluster.json**.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Um arquivo de configuração baseado em **kubeadm-dev-test** não tem uma definição de armazenamento para cada pool, mas você pode usar o processo acima para adicionar, se necessário.

Para obter mais informações sobre a configuração de armazenamento, confira [Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configurar o pool de armazenamento sem Spark

Você também pode configurar os pools de armazenamento para serem executados sem o Spark e criar um pool do Spark separado. Isso permite que você dimensione o poder de computação do Spark independentemente do armazenamento. Para ver como configurar o pool do Spark, confira o [exemplo de arquivo de patch JSON](#jsonpatch) no final deste artigo.



Por padrão, a configuração **includeSpark** para o pool de armazenamento é definida como true, portanto, você deve adicionar o campo **includeSpark** à configuração de armazenamento para fazer alterações. O arquivo de patch JSON a seguir mostra como adicionar isso.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
       "type":"Storage",
       "replicas":2,
       "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a> Configurar o posicionamento do pod usando rótulos do Kubernetes

Você pode controlar o posicionamento do pod em nós do Kubernetes que têm recursos específicos para acomodar vários tipos de requisitos de carga de trabalho. Por exemplo, talvez você queira garantir que os pods do pool de armazenamento sejam colocados em nós com mais armazenamento ou que as instâncias mestre do SQL Server sejam colocadas em nós que tenham recursos de CPU e memória mais elevados. Nesse caso, primeiro você criará um cluster do Kubernetes heterogêneo com diferentes tipos de hardware e, em seguida, [atribuirá os rótulos de nó](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) de acordo. No momento da implantação do cluster de Big Data, você pode especificar os mesmos rótulos no nível de pool no arquivo de configuração de implantação de cluster. Em seguida, o Kubernetes cuidará do ajuste dos pods em nós que correspondem aos rótulos especificados. A chave de rótulo específica que precisa ser adicionada aos nós no cluster kubernetes é **MSSQL-cluster-Wide**. O valor desse rótulo pode ser qualquer cadeia de caracteres que você escolher.

O exemplo a seguir mostra como editar um arquivo de configuração personalizado para incluir uma configuração de rótulo de nó para a instância mestra de SQL Server, pool de computação, pool de dados & pool de armazenamento. Observe que não há nenhuma chave *nodeLabel* nas configurações internas, portanto, será necessário editar um arquivo de configuração personalizado manualmente ou criar um arquivo de patch e aplicá-lo ao arquivo de configuração personalizado. O Pod da instância mestra de SQL Server será implantado em um nó que contém um rótulo **MSSQL-cluster-Wide** com o valor **BDC-Master**. O pool de computação e os pods do pool de dados serão implantados em nós que contêm um rótulo **MSSQL-cluster-Wide** com o valor **BDC-SQL**. O pods do pool de armazenamento será implantado em nós que contêm um rótulo **MSSQL-cluster-Wide** com valor **BDC-Storage**.

Crie um arquivo chamado **patch.json** no diretório atual com o conteúdo a seguir:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
    "type": "Master",
        "replicas": 1,
        "hadrEnabled": false,
        "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Compute')].spec",
      "value": {
    "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Data')].spec",
      "value": {
    "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
    "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage"
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
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

- Atualiza as configurações de armazenamento do pool para o pool de armazenamento em **cluster.json**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
          "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
        "data":{
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode":"ReadWriteOnce"
            },
        "logs":{
            "size":"32Gi",
            "className":"myStorageClass",
            "accessMode":"ReadWriteOnce"
            }
            }
         }
        }
      ]
    }
    ```

- Atualiza as configurações do Spark para o pool de armazenamento em **cluster.json**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
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

- Cria um pool do Spark com duas instâncias em **cluster.json**.
    ```json
    {
      "patch": [
        {
          "op": "add",
          "path": "spec.pools/-",
          "value":
          {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
          }
        } 
      ]
    }
    ```



> [!TIP]
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, confira [Referência de arquivo de configuração de implantação para clusters de Big Data](reference-deployment-config.md).

Use o comando **azdata bdc config** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo **patch.json** a um arquivo de configuração de implantação de destino **custom/cluster.json**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o uso de arquivos de configuração em implantações de cluster de Big Data, confira [Como implantar clusters de Big Data do SQL Server no Kubernetes](deployment-guidance.md#configfile).
