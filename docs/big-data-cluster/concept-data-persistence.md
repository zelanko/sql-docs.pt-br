---
title: Persistência de dados no Kubernetes
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre como a persistência de dados funciona em um cluster de Big Data do SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dcc30e8d86a1a767291b410df7cfd3aa42edf27f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470999"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Os [Volumes Persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para armazenamento no Kubernetes. O modo como o armazenamento é fornecido é dissociado de como ele é consumido. Portanto, você pode colocar seu próprio armazenamento altamente disponível e conectá-lo ao cluster de Big Data do SQL Server. Isso dá a você controle total sobre o tipo de armazenamento, disponibilidade e desempenho de que você precisa. O Kubernetes dá suporte a vários tipos de soluções de armazenamento, incluindo discos/arquivos do Azure, NFS, armazenamento local e muito mais.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

A forma como um cluster de Big Data do SQL Server consume esses volumes persistentes é usando [Classes de Armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento diferentes para um tipo diferente de armazenamento e especificá-las no momento da implantação do cluster de Big Data. Você pode configurar a classe de armazenamento e o tamanho da declaração de volume persistente a serem usados para qual finalidade no nível do pool. Um cluster de Big Data do SQL Server cria [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) com o nome de classe de armazenamento especificado para cada componente que requer volumes persistentes. Em seguida, ele monta os volumes persistentes correspondentes no pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Definir configurações de armazenamento de cluster de Big Data

Semelhante a outras personalizações, você pode especificar as configurações de armazenamento nos arquivos de configuração de cluster no momento da implantação para cada pool e o plano de controle. Se não houver definições de configuração de armazenamento nas especificações do pool, as configurações de armazenamento do plano de controle serão usadas. Este é um exemplo da seção de configuração de armazenamento que você pode incluir na especificação:

```json
    "storage": 
    {
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
```

A implantação do cluster de Big Data usará o armazenamento persistente para armazenar dados, metadados e logs para vários componentes. Você pode personalizar o tamanho das declarações de volume persistente criadas como parte da implantação. Como melhor prática, recomendamos o uso de classes de armazenamento com uma [política de recuperação](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) de *Retenção*.

> [!NOTE]
> No CTP 3.2, você não pode modificar a configuração de armazenamento após a implantação. Além disso, há suporte apenas para o modo de acesso `ReadWriteOnce` para o cluster inteiro.

> [!WARNING]
> A execução sem armazenamento persistente pode funcionar em um ambiente de teste, mas pode resultar em um cluster não funcional. Após a reinicialização do pod, os metadados do cluster e/ou os dados do usuário serão perdidos permanentemente. Não recomendamos a execução nessa configuração. 

A seção [Configurar armazenamento](#config-samples) fornece mais exemplos de como definir as configurações de armazenamento para sua implantação de cluster de Big Data do SQL Server.

## <a name="aks-storage-classes"></a>Classes de armazenamento do AKS

O AKS é fornecido com [duas classes de armazenamento internas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **padrão** e **gerenciadas Premium**, juntamente com o provisionador dinâmico para elas. Você pode especificar qualquer uma delas ou criar sua própria classe de armazenamento para implantar o cluster de Big Data com o armazenamento persistente habilitado. Por padrão, o arquivo de configuração de cluster interno para o AKS *aks-dev-test* é fornecido com configurações de armazenamento persistentes para usar a classe de armazenamento **padrão**.

> [!WARNING]
> Os volumes persistentes criados com as classes de armazenamento internas **padrão** e **gerenciada Premium** têm uma política de recuperação de *Exclusão*. Portanto, no momento em que você exclui o cluster de Big Data do SQL Server, as declarações de volume persistente são excluídas e, em seguida, os volumes persistentes também. Você pode criar classes de armazenamento personalizadas usando o provisionador **azure-disk** com uma política de recuperação de *Retenção* conforme mostrado [neste](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) artigo.


## <a name="minikube-storage-class"></a>Classe de armazenamento do Minikube

O Minikube vem com uma classe de armazenamento interna chamada **padrão**, juntamente com um provisionador dinâmico para ela. O arquivo de configuração interno para minikube *minikube-dev-test* tem as configurações de armazenamento na especificação do plano de controle. As mesmas configurações serão aplicadas a todas as especificações de pools. Você também pode personalizar uma cópia desse arquivo e usá-lo para a implantação do cluster de Big Data no minikube. Você pode editar manualmente o arquivo personalizado e alterar o tamanho das declarações de volumes persistentes para pools específicos a fim de acomodar as cargas de trabalho que você deseja executar. Ou então, confira a seção [Configurar armazenamento](#config-samples) para obter exemplos de como fazer edições usando os comandos *azdata*.

## <a name="kubeadm-storage-classes"></a>Classes de armazenamento do Kubeadm

Kubeadm não vem com uma classe de armazenamento interna. Você precisa criar suas próprias classes de armazenamento e volumes persistentes usando o armazenamento local ou seu provisionador preferido, como [Torre](https://github.com/rook/rook). Nesse caso, você definirá **className** para a classe de armazenamento configurada. 

> [!NOTE]
>  No arquivo de configuração de implantação interno para *kubeadm kubeadm-dev-test*, não há nenhum nome de classe de armazenamento especificado para o armazenamento de dados e de log. Antes da implantação, você precisa personalizar o arquivo de configuração e definir o valor de className; caso contrário, as validações de pré-implantação falharão. A implantação também tem uma etapa de validação que verifica a existência da classe de armazenamento, mas não os volumes persistentes necessários. Você precisa criar volumes suficientes dependendo da escala do cluster. No CTP 3.1, para o tamanho de cluster padrão, você deve criar pelo menos 23 volumes. [Aqui](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) está um exemplo de como criar volumes persistentes usando o provisionador local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar as configurações de armazenamento para cada pool

Para todas as personalizações, você deve primeiro criar uma cópia do arquivo de configuração interno que deseja usar. Por exemplo, o comando a seguir cria uma cópia dos arquivos de configuração de implantação *aks-dev-test* em um subdiretório chamado `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Isso cria dois arquivos, **cluster.json** e **control.json** que podem ser personalizados editando-os manualmente ou você pode usar o comando **azdata bdc config**. Você pode usar uma combinação de bibliotecas jsonpath e jsonpatch para fornecer maneiras de editar os arquivos de configuração.


### <a id="config-samples"></a> Configurar o nome da classe de armazenamento e/ou o tamanho das declarações

Por padrão, o tamanho das declarações de volume persistente provisionadas para cada um dos pods provisionados no cluster é de 10 GB. Você pode atualizar esse valor para acomodar as cargas de trabalho que está executando em um arquivo de configuração personalizado antes da implantação do cluster.

O exemplo a seguir atualiza o tamanho das declarações de volume persistente para 32Gi no **control.jsaon**. Se não for substituída no nível do pool, essa configuração será aplicada a todos os pools:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

O exemplo a seguir mostra como modificar a classe de armazenamento para o arquivo **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Outra opção é editar manualmente o arquivo de configuração personalizado ou usar json patch como no exemplo a seguir, que altera a classe de armazenamento para o pool de armazenamento. Crie um arquivo *patch.json* com este conteúdo:

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

Aplique o arquivo de patch. Use o comando **azdata bdc config patch** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo patch.json a um arquivo de configuração de implantação de destino custom.json.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter a documentação completa sobre volumes no Kubernetes, confira a [documentação do Kubernetes sobre volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obter mais informações sobre a implantação de um cluster de Big Data do SQL Server, confira [Como implantar um cluster de Big Data do SQL Server no Kubernetes](deployment-guidance.md).

