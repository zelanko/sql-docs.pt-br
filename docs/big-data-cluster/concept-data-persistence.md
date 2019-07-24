---
title: Persistência de dados no kubernetes
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre como a persistência de dados funciona em um cluster SQL Server 2019 Big Data.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419465"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistência de dados com o cluster SQL Server Big Data no kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Os [volumes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para armazenamento no kubernetes. Como o armazenamento é fornecido é dissociado de como ele é consumido. Portanto, você pode colocar seu próprio armazenamento altamente disponível e conectá-lo ao cluster SQL Server Big Data. Isso lhe dá controle total sobre o tipo de armazenamento, disponibilidade e desempenho que você precisa. O kubernetes dá suporte a vários tipos de soluções de armazenamento, incluindo discos/arquivos do Azure, NFS, armazenamento local e muito mais.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

A maneira como um cluster SQL Server Big Data consome esses volumes persistentes é usando [classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento diferentes para um tipo diferente de armazenamento e especificá-las no momento da implantação do cluster Big Data. Você pode configurar qual classe de armazenamento e o tamanho de declaração de volume persistente usar para qual finalidade no nível do pool. Um cluster SQL Server Big Data cria [declarações de volume persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) com o nome de classe de armazenamento especificado para cada componente que requer volumes persistentes. Em seguida, ele monta os volumes persistentes correspondentes no pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Definir Big Data configurações de armazenamento de cluster

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

A implantação do cluster de Big Data usará o armazenamento persistente para armazenar dados, metadados e logs para vários componentes. Você pode personalizar o tamanho das declarações de volume persistentes criadas como parte da implantação. Como prática recomendada, recomendamos o uso de classes de armazenamento com uma [política](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)de redeclaração de *retenção* .

> [!NOTE]
> No CTP 3,2, você não pode modificar a configuração de armazenamento após a implantação. Além disso, `ReadWriteOnce` há suporte apenas para o modo de acesso para o cluster inteiro.

> [!WARNING]
> A execução sem armazenamento persistente pode funcionar em um ambiente de teste, mas pode resultar em um cluster não funcional. Após a reinicialização do pod, os metadados do cluster e/ou os dados do usuário serão perdidos permanentemente. Não recomendamos a execução nessa configuração. 

A seção [Configurar armazenamento](#config-samples) fornece mais exemplos de como definir as configurações de armazenamento para seu SQL Server Big data implantação de cluster.

## <a name="aks-storage-classes"></a>Classes de armazenamento AKS

O AKS vem com [duas classes de armazenamento internas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **padrão** e **gerenciada Premium,** juntamente com o provisionamento dinâmico para elas. Você pode especificar qualquer um deles ou criar sua própria classe de armazenamento para implantar Big Data cluster com o armazenamento persistente habilitado. Por padrão, o arquivo de configuração de cluster interno para AKs *AKs-dev-Test* vem com configurações de armazenamento persistentes para usar a classe de armazenamento **padrão** .

> [!WARNING]
> Os volumes persistentes criados com as classes de armazenamento internas **Default** e **Managed-Premium** têm uma política de recuperação de *exclusão*. Portanto, no momento em que você exclui o SQL Server Big Data cluster, as declarações de volume persistentes são excluídas e, em seguida, os volumes persistentes também. Você pode criar classes de armazenamento personalizadas usando [o](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) **Azure-Disk** Privioner com uma política *reter* recuperação, conforme mostrado neste artigo.


## <a name="minikube-storage-class"></a>Classe de armazenamento Minikube

O Minikube vem com uma classe de armazenamento interna chamada **Standard** , juntamente com um provisionamento dinâmico para ela. O arquivo de configuração interno para minikube *minikube-dev-Test* tem as definições de configuração de armazenamento na especificação do plano de controle. As mesmas configurações serão aplicadas a todas as especificações de pools. Você também pode personalizar uma cópia desse arquivo e usá-lo para a implantação de cluster Big Data no minikube. Você pode editar manualmente o arquivo personalizado e alterar o tamanho das declarações de volumes persistentes para pools específicos para acomodar as cargas de trabalho que você deseja executar. Ou então, consulte a seção [Configurar armazenamento](#config-samples) para obter exemplos de como fazer edições usando comandos *azdata* .

## <a name="kubeadm-storage-classes"></a>Classes de armazenamento Kubeadm

Kubeadm não vem com uma classe de armazenamento interna. Você deve criar suas próprias classes de armazenamento e volumes persistentes usando o armazenamento local ou seu provisionamento preferido, como [torre](https://github.com/rook/rook). Nesse caso, você definirá o **ClassName** para a classe de armazenamento configurada. 

> [!NOTE]
>  No arquivo de configuração de implantação interno para *kubeadm kubeadm-dev-Test,* não há nenhum nome de classe de armazenamento especificado para o armazenamento de dados e de log. Antes da implantação, você deve personalizar o arquivo de configuração e definir o valor de className, caso contrário, as validações de pré-implantação falharão. A implantação também tem uma etapa de validação que verifica a existência da classe de armazenamento, mas não os volumes persistentes necessários. Você deve garantir que você crie volumes suficientes dependendo da escala do cluster. No CTP 3,1, para o tamanho de cluster padrão, você deve criar pelo menos 23 volumes. [Aqui](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) está um exemplo de como criar volumes persistentes usando o provisionamento local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar as configurações de armazenamento para cada pool

Para todas as personalizações, você deve primeiro criar uma cópia do arquivo de configuração interno que deseja usar. Por exemplo, o comando a seguir cria uma cópia dos arquivos de configuração de implantação *AKs-dev-Test* em um subdiretório `custom`chamado:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Isso cria dois arquivos, **cluster. JSON** e **Control. JSON** que podem ser personalizados editando-os manualmente ou você pode usar o comando **azdata BDC config** . Você pode usar uma combinação de bibliotecas jsonpath e jsonpatch para fornecer maneiras de editar os arquivos de configuração.


### <a id="config-samples"></a>Configurar o nome da classe de armazenamento e/ou o tamanho das declarações

Por padrão, o tamanho das declarações de volume persistentes provisionadas para cada um dos pods provisionadas no cluster é de 10 GB. Você pode atualizar esse valor para acomodar as cargas de trabalho que está executando em um arquivo de configuração personalizado antes da implantação do cluster.

O exemplo a seguir atualiza o tamanho do tamanho de declarações de volume persistente para 32Gi no **Control. jsaon**. Se não for substituído no nível do pool, essa configuração será aplicada a todos os pools:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

O exemplo a seguir mostra como modificar a classe de armazenamento para o arquivo **Control. JSON** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Outra opção é editar manualmente o arquivo de configuração personalizado ou usar o patch JSON, como no exemplo a seguir, que altera a classe de armazenamento para o pool de armazenamento. Crie um arquivo *patch. JSON* com este conteúdo:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

Aplique o arquivo de patch. Use o comando **azdata BDC config patch** para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo patch. JSON a um arquivo de configuração de implantação de destino Custom. JSON.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter a documentação completa sobre volumes no kubernetes, consulte a [documentação do kubernetes sobre volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obter mais informações sobre como implantar um cluster de Big Data SQL Server, consulte [como implantar SQL Server Cluster de Big data no kubernetes](deployment-guidance.md).

