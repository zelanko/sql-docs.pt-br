---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster Big Data com arquivos de configuração.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419441"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Definir configurações de implantação para clusters de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar os arquivos de configuração de implantação de cluster, você pode usar qualquer editor de formato JSON, como VSCode. Para gerar scripts dessas edições para fins de automação, use o comando **azdata BDC config** . Este artigo explica como configurar Big Data implantações de cluster modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, consulte a [diretriz de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Pré-requisitos

- [Instale o azdata](deploy-install-azdata.md).

- Cada um dos exemplos nesta seção pressupõe que você criou uma cópia de uma das configurações padrão. Para obter mais informações, consulte [criar uma configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria um diretório `custom` chamado que contém dois arquivos de configuração de implantação JSON, **cluster. JSON** e **Control. JSON**, com base na configuração padrão de **AKs-dev-Test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>Alterar nome do cluster

O nome do cluster é o nome do cluster Big Data e o namespace kubernetes que será criado na implantação. Ele é especificado na seguinte parte do arquivo de configuração de implantação **cluster. JSON** :

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

O comando a seguir envia um par chave-valor para o parâmetro **--JSON-** Values para alterar o nome do cluster Big data para **Test-cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do cluster de Big Data deve ter apenas caracteres alfanuméricos minúsculos, sem espaços. Todos os artefatos kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o nome do cluster especificado.

## <a id="ports"></a>Atualizar portas de ponto de extremidade

Os pontos de extremidade são definidos para o controlador no **Control. JSON** e para o gateway e SQL Server instância mestra nas seções correspondentes em **cluster. JSON**. A seguinte parte do arquivo de configuração **Control. JSON** mostra as definições de ponto de extremidade para o controlador:

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

O exemplo a seguir usa JSON embutido para alterar a porta para o ponto de extremidade do **controlador** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>Configurar réplicas do pool

As características de cada pool, como o pool de armazenamento, são definidas no arquivo de configuração **cluster. JSON** . Por exemplo, a seguinte parte do **cluster. JSON** mostra uma definição de pool de armazenamento:

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

Você pode configurar o número de instâncias em um pool modificando o  valor de réplicas para cada pool. O exemplo a seguir usa JSON embutido para alterar esses valores para o armazenamento e os `10` pools de dados para e, `4` respectivamente:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizada ao pool de armazenamento e atualiza o tamanho da declaração de volume persistente para armazenar dados em 100 GB. Primeiro, crie um arquivo patch. JSON como mostrado abaixo, que inclui a nova seção de *armazenamento* , além de *tipos* e *réplicas*

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

Em seguida, você pode usar o comando **azdata BDC config patch** para atualizar o arquivo de configuração **cluster. JSON** .
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Um arquivo de configuração baseado em **kubeadm-dev-Test** não tem uma definição de armazenamento para cada pool, mas você pode usar o processo acima para adicionar, se necessário.

Para obter mais informações sobre a configuração de armazenamento, consulte [persistência de dados com o cluster SQL Server Big data em kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a>Configurar o pool de armazenamento sem Spark

Você também pode configurar os pools de armazenamento para serem executados sem o Spark e criar um pool do Spark separado. Isso permite que você dimensione o poder de computação do Spark independentemente do armazenamento. Para ver como configurar o pool do Spark, consulte o [exemplo de arquivo de patch JSON](#jsonpatch) no final deste artigo.



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

## <a id="podplacement"></a>Configurar o posicionamento do pod usando rótulos de kubernetes

Você pode controlar o posicionamento do pod em nós kubernetes que têm recursos específicos para acomodar vários tipos de requisitos de carga de trabalho. Por exemplo, talvez você queira garantir que os pods do pool de armazenamento sejam colocados em nós com mais armazenamento, ou SQL Server instâncias mestre sejam colocadas em nós que tenham recursos de CPU e memória maiores. Nesse caso, primeiro você criará um cluster kubernetes heterogêneo com diferentes tipos de hardware e, em seguida, atribuirá os [Rótulos de nó](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) de acordo. No momento da implantação do cluster de Big Data, você pode especificar os mesmos rótulos no nível de pool no arquivo de configuração de implantação de cluster. Kubernetes, em seguida, cuidará do ajustando do pods em nós que correspondem aos rótulos especificados.

O exemplo a seguir mostra como editar um arquivo de configuração personalizado para incluir uma configuração de rótulo de nó para a instância mestra de SQL Server. Observe que não há nenhuma chave *nodeLabel* nas configurações internas, portanto, será necessário editar um arquivo de configuração personalizado manualmente ou criar um arquivo de patch e aplicá-lo ao arquivo de configuração personalizado.

Crie um arquivo chamado **patch. JSON** em seu diretório atual com o seguinte conteúdo:

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
         "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a>Arquivos de patch JSON

Os arquivos de patch JSON definem várias configurações ao mesmo tempo. Para obter mais informações sobre patches JSON, consulte [patches JSON em Python](https://github.com/stefankoegl/python-json-patch) e o avaliador do [JSONPath online](https://jsonpath.com/).

O arquivo **patch. JSON** a seguir executa as seguintes alterações:

- Atualiza a porta de um ponto de extremidade único em **Control. JSON**.
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

- Atualiza todos os pontos de extremidade (**porta** e **ServiceType**) em **Control. JSON**.
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

- Atualiza as configurações de armazenamento do controlador em **Control. JSON**. Essas configurações são aplicáveis a todos os componentes do cluster, a menos que sejam substituídas no nível do pool.
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

- Atualiza o nome da classe de armazenamento em **Control. JSON**.
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

- Atualiza as configurações de armazenamento de pool para o pool de armazenamento em **cluster. JSON**.
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

- Atualiza as configurações do Spark para o pool de armazenamento em **cluster. JSON**.
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

- Cria um pool do Spark com 2 instâncias em **cluster. JSON**.
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
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, consulte [referência de arquivo de configuração de implantação para clusters de Big data](reference-deployment-config.md).

Use os comandos de **configuração do BDC azdata** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo **patch. JSON** a um arquivo de configuração de implantação de destino **Custom/cluster. JSON**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar arquivos de configuração no Big Data implantações de cluster, consulte [como implantar SQL Server Big data clusters no kubernetes](deployment-guidance.md#configfile).
