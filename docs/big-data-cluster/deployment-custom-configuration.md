---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster de big data com arquivos de configuração.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ba2587c2effdc3242e6032a0137bbf43ac153f1c
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388799"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Definir as configurações de implantação para clusters de big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar seu arquivo de configuração de implantação de cluster, você pode usar qualquer editor de formato JSON, como o VSCode. Para essas edições para fins de automação de script, use o **seção de configuração do bdc mssqlctl** comando. Este artigo explica como configurar implantações de cluster de big data, modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, consulte o [diretrizes de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisites

- [Instalar mssqlctl](deploy-install-mssqlctl.md).

- Cada um dos exemplos nesta seção pressupõem que você tenha criado uma cópia de um dos arquivos de configuração padrão. Para obter mais informações, consulte [criar um arquivo de configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria um diretório chamado `custom` que contém um arquivo de configuração de implantação de JSON com base no padrão **aks-dev-test** configuração:

   ```bash
   mssqlctl bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Alterar o nome do cluster

O nome do cluster é o nome do cluster de big data e o namespace do Kubernetes que será criado na implantação. Ele é especificado na seguinte parte do arquivo de configuração de implantação:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

O comando a seguir envia um par chave-valor para o **-- json-values** parâmetro para alterar o nome do cluster de big data para **test-cluster**:

```bash
mssqlctl bdc config section set --config-profile custom -j "metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do seu cluster de big data deve ser caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o cluster do nome especificado.

## <a id="ports"></a> Portas de ponto de extremidade de atualização

Pontos de extremidade são definidos para o plano de controle, bem como para pools individuais. A seguinte parte do arquivo de configuração mostra as definições de ponto de extremidade para o plano de controle:

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

O exemplo a seguir usa embutido JSON para alterar a porta para o **controlador** ponto de extremidade:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurar réplicas de pool

As características de cada pool, como o pool de armazenamento, é definido no arquivo de configuração. Por exemplo, a parte a seguir mostra uma definição de pool de armazenamento:

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
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
        }
    }
]
```

Você pode configurar o número de instâncias em um pool, modificando o **réplicas** valor para cada pool. O exemplo a seguir usa embutido JSON para alterar esses valores para os pools de armazenamento e dados `10` e `4` , respectivamente:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizado para o pool de armazenamento e atualiza o tamanho da declaração de volume persistente para armazenar dados de 100 GB. Você deve ter esta seção no arquivo de configuração para atualizar as configurações usando o *mssqlctl bdc config set* de comando, consulte abaixo mostra como usar um arquivo de patch para adicionar esta seção:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.className=storage-pool-class"
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=32Gi"
```

> [!NOTE]
> Um arquivo de configuração com base em **kubeadm-dev-test** não tem uma definição de armazenamento para cada pool, mas isso pode ser adicionado manualmente se necessário.

Para obter mais informações sobre a configuração de armazenamento, consulte [persistência de dados com o SQL Server, o cluster de big data no Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configurar o armazenamento sem spark

Você também pode configurar os pools de armazenamento para ser executado sem spark e criar um pool separado do spark. Isso permite que você escala spark computação energia independente de armazenamento. Para ver como configurar o pool de spark, consulte o [exemplo de arquivo de patch JSON](#jsonpatch) no final deste artigo.

Você deve ter esta seção no arquivo de configuração para atualizar as configurações usando o `mssqlctl cluster config set command`. O arquivo de patch JSON a seguir mostra como adicionar isso.

Por padrão, o **includeSpark** configuração para o pool de armazenamento é definido como true, você deve adicionar o **includeSpark** campo para a configuração de armazenamento para fazer alterações:

```bash
mssqlctl cluster config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].includeSpark=false"
```

## <a id="podplacement"></a> Configurar o posicionamento de pod usando rótulos de Kubernetes

Você pode controlar o posicionamento de pod em nós de Kubernetes com recursos específicos para acomodar vários tipos de requisitos de carga de trabalho. Por exemplo, você talvez queira garantir que os pods de pool de armazenamento são colocados em nós com mais armazenamento ou instâncias de mestre do SQL Server são colocadas em nós que têm recursos de memória e CPU maior. Nesse caso, primeiro você criará um cluster Kubernetes heterogêneo com diferentes tipos de hardware e, em seguida [atribuir rótulos do nó](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) adequadamente. No momento da implantação de cluster de big data, você pode especificar rótulos mesmos no nível do pool no arquivo de configuração de implantação do cluster. Kubernetes, em seguida, se encarregará de ajustar as os pods em nós que corresponderem aos rótulos especificados.

O exemplo a seguir mostra como editar um arquivo de configuração personalizada para incluir uma configuração de rótulo do nó para a instância mestre do SQL Server. Observe que não há nenhuma *nodeLabel* chave nas configurações internas para que você precisará editar um arquivo de configuração personalizado manualmente ou criar um arquivo de patch e aplicá-lo para o arquivo de configuração personalizada.

Crie um arquivo chamado **patch.json** no seu diretório atual com o seguinte conteúdo:

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a id="jsonpatch"></a> Arquivos de patch JSON

Arquivos de patch JSON configuram várias configurações de uma só vez. Para obter mais informações sobre os patches JSON, consulte [Patches JSON em Python](https://github.com/stefankoegl/python-json-patch) e o [avaliador on-line de JSONPath](https://jsonpath.com/).

O seguinte **patch.json** arquivo executa as seguintes alterações:

- Atualiza a porta do ponto de extremidade única.
- Atualiza todos os pontos de extremidade (**porta** e **serviceType**).
- Atualiza o armazenamento de plano de controle. Essas configurações são aplicáveis a todos os componentes de cluster, a menos que substituída no nível do pool.
- Atualiza o nome de classe de armazenamento no armazenamento de plano de controle.
- Atualiza as configurações do pool de armazenamento para o pool de armazenamento.
- Atualiza as configurações do Spark para o pool de armazenamento.
- Cria um pool do spark com 2 réplicas para o cluster

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
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
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.controlPlane",
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
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.data.className",
      "value": "managed-premium"
    },
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
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
    },
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
    },
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
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, consulte [referência de arquivo de configuração de implantação para clusters de big data](reference-deployment-config.md).

Use **conjunto de seção de configuração de bdc mssqlctl** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica-se a **patch.json** arquivo para um arquivo de configuração de implantação de destino **custom.json**.

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar arquivos de configuração em implantações de cluster de big data, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md#configfile).
