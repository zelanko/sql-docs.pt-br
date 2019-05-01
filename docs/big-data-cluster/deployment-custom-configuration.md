---
title: Configurar implantações
titleSuffix: SQL Server big data clusters
description: Saiba como personalizar uma implantação de cluster de big data com arquivos de configuração.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7dd774d390587d0c2c0248ab9b419ad40f8f212b
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759163"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Definir as configurações de implantação para clusters de big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar seu arquivo de configuração de implantação de cluster, você pode usar qualquer editor de formato json, como o VSCode. Para essas edições para fins de automação de scripts, fornecemos uma **seção de configuração de cluster mssqlctl** comando. Este artigo explica como configurar implantações de cluster de big data, modificando arquivos de configuração de implantação. Ele fornece exemplos de como alterar a configuração para cenários diferentes. Para obter mais informações sobre como os arquivos de configuração são usados em implantações, consulte o [diretrizes de implantação](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisites

- [Instalar mssqlctl](deploy-install-mssqlctl.md).

- Cada um dos exemplos nesta seção pressupõem que você tenha criado uma cópia de um dos arquivos de configuração padrão. Para obter mais informações, consulte [criar um arquivo de configuração personalizada](deployment-guidance.md#customconfig). Por exemplo, o comando a seguir cria uma **custom.json** arquivo com base no padrão **aks-dev-test.json** configuração:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
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
mssqlctl cluster config section set -f custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> O nome do cluster deve ser caracteres alfa-numéricos do apenas letras minúsculas, sem espaços. Todos os artefatos de Kubernetes (contêineres, pods, conjuntos com estado, serviços) para o cluster serão criados em um namespace com o mesmo nome que o cluster do nome especificado.

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
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

O exemplo a seguir usa embutido JSON para alterar a porta para o **controlador** ponto de extremidade:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
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
                "usePersistentVolume": true,
                "className": "managed-premium",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        }
    }
]
```

Você pode configurar o número de instâncias em um pool, modificando o **réplicas** valor para cada pool. O exemplo a seguir usa embutido JSON para alterar esses valores para os pools de armazenamento e dados `10` e `4` , respectivamente:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

> [!IMPORTANT]
> Nesta versão, você não pode alterar o número de instâncias no pool de computação.

## <a id="storage"></a> Configurar o armazenamento

Você também pode alterar a classe de armazenamento e as características que são usadas para cada pool. O exemplo a seguir atribui uma classe de armazenamento personalizado para o pool de armazenamento:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec={""replicas"": 2,""storage"": {""className"": ""newStorageClass"",""size"": ""20Gi"",""accessMode"": ""ReadWriteOnce"",""usePersistentVolume"": true},""type"": ""Storage""}"
```

O exemplo a seguir atualiza apenas o tamanho do pool de armazenamento para `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.size=32Gi"
```

O exemplo a seguir atualiza o tamanho de todos os pools de `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type[*])].spec.storage.size=32Gi"
```

> [!NOTE]
> Um arquivo de configuração com base em **kubeadm-dev-test.json** não tem uma definição de armazenamento para cada pool, mas isso pode ser adicionado manualmente se necessário.

Para obter mais informações sobre a configuração de armazenamento, consulte [persistência de dados com o SQL Server, o cluster de big data no Kubernetes](concept-data-persistence.md).

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
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> Arquivos de patch JSON

Arquivos de patch JSON configuram várias configurações de uma só vez. Para obter mais informações sobre os patches JSON, consulte [Patches JSON em Python](https://github.com/stefankoegl/python-json-patch) e o [avaliador on-line de JSONPath](https://jsonpath.com/).

O seguinte **patch.json** arquivo executa as seguintes alterações:

- Atualiza a porta do ponto de extremidade única.
- Atualiza todos os pontos de extremidade (**porta** e **serviceType**).
- Atualiza o armazenamento de plano de controle.
- Atualiza o nome de classe de armazenamento no armazenamento de plano de controle.
- Atualizações de pool de armazenamento, incluindo réplicas (pool de armazenamento).
- Atualiza as configurações do Spark para um pool específico (pool de armazenamento).

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
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage",
      "value": {
        "usePersistentVolume":true,
        "accessMode":"ReadWriteMany",
        "className":"managed-premium",
        "size":"10Gi"
      }
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.className",
      "value": "default"
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "replicas": 2,
        "type": "Storage",
        "storage": {
          "usePersistentVolume": true,
          "accessMode": "ReadWriteOnce",
          "className": "managed-premium",
          "size": "10Gi"
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
    }
  ]
}
```

> [!TIP]
> Para obter mais informações sobre a estrutura e as opções para alterar um arquivo de configuração de implantação, consulte [referência de arquivo de configuração de implantação para clusters de big data](reference-deployment-config.md).

Use **conjunto de seção de configuração de cluster mssqlctl** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica-se a **patch.json** arquivo para um arquivo de configuração de implantação de destino **custom.json**.

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar arquivos de configuração em implantações de cluster de big data, consulte [clusters de como implantar grandes de dados do SQL Server em Kubernetes](deployment-guidance.md#configfile).
