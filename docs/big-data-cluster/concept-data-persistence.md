---
title: Persistência de dados no Kubernetes
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre o funcionamento da persistência de dados em um cluster de big data do SQL Server de 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 701be4a352066ab0c80e0269b16114e8e279998a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729138"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistência de dados com o cluster de big data do SQL Server no Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Volumes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para o armazenamento no Kubernetes. Como o armazenamento é fornecido é abstraído do como eles são consumidos. Você pode, portanto, traga seu próprio armazenamento altamente disponível e conectá-lo ao cluster de big data do SQL Server. Isso lhe dá controle total sobre o tipo de armazenamento, disponibilidade e desempenho que você precisa. Kubernetes dá suporte a vários tipos de soluções de armazenamento, incluindo discos/arquivos do Azure, NFS, armazenamento local e muito mais.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

A maneira de um cluster de big data do SQL Server consome esses volumes persistentes é por meio [Classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento diferentes para diferentes tipos de armazenamento e especificá-los no momento da implantação de cluster de big data. Você pode configurar qual classe de armazenamento e o tamanho de declaração de volume persistente para usar para qual finalidade no nível do pool. Cria um cluster de big data do SQL Server [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) com o nome de classe de armazenamento especificada para cada componente que requer volumes persistentes. Ele, em seguida, monta os volumes persistentes correspondentes no pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Definir configurações de armazenamento de cluster de big data

Assim como outras personalizações, você pode especificar as configurações de armazenamento nos arquivos de configuração de cluster no momento da implantação para cada pool e o plano de controle. Se não houver nenhuma definição de configuração de armazenamento nas especificações de pool, então as configurações de armazenamento do plano de controle serão usadas. Este é um exemplo da seção de configuração de armazenamento que você pode incluir nas especificações de:

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

Implantação de cluster de big data usará o armazenamento persistente para armazenar dados, metadados e logs de vários componentes. Você pode personalizar o tamanho das declarações de volume persistente criado como parte da implantação. Como prática recomendada, é recomendável usar as classes de armazenamento com um *Retain* [recuperar política](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> No CTP 3.1, você não pode modificar o armazenamento configuração configuração após a implantação. Além disso, apenas `ReadWriteOnce` é suporte para o modo de acesso para o cluster inteiro.

> [!WARNING]
> A execução sem armazenamento persistente pode trabalhar em um ambiente de teste, mas isso poderá resultar em um cluster não funcional. Após a reinicialização de pod, dados de metadados e/ou usuário do cluster serão perdidos permanentemente. Não recomendamos executar nessa configuração. 

[Configurar o armazenamento](#config-samples) seção fornece mais exemplos sobre como definir as configurações de armazenamento para sua implantação de cluster de big data do SQL Server.

## <a name="aks-storage-classes"></a>Classes de armazenamento do AKS

Acompanha o AKS [duas classes de armazenamento interno](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **padrão** e **premium gerenciados** juntamente com provisionador dinâmico para eles. Você pode especificar qualquer uma dessas ou criar sua própria classe de armazenamento para a implantação de cluster de big data com o armazenamento persistente habilitado. Por padrão, a interna no arquivo de configuração de cluster do aks *aks-dev-test* vem com configurações de armazenamento persistente para usar **padrão** classe de armazenamento.

> [!WARNING]
> Volumes persistentes criados com as classes de armazenamento interno **padrão** e **premium gerenciados** têm uma política de recuperar de *excluir*. Portanto, no momento você excluir o cluster de big data do SQL Server, declarações de volume persistente obtém também os volumes excluídos e, em seguida, persistentes. Você pode criar classes de armazenamento personalizado usando **disco do azure** privioner com um *reter* recuperar política, conforme mostrado na [isso](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) artigo.


## <a name="minikube-storage-class"></a>Classe de armazenamento do Minikube

Minikube vem com uma classe de armazenamento interna chamada **standard** junto com um provedor dinâmico para ele. A configuração interna no arquivo para minikube *minikube-dev-test* tem as definições de configuração de armazenamento nas especificações do plano de controle. As mesmas configurações serão aplicadas a todas as especificações de pools. Você também pode personalizar uma cópia desse arquivo e usá-lo para sua implantação de cluster de big data no minikube. Manualmente, você pode editar o arquivo personalizado e alterar o tamanho das declarações de volumes persistentes para grupos específicos acomodar as cargas de trabalho que deseja executar. Ou, consulte [configurar o armazenamento](#config-samples) seção para obter exemplos sobre como fazer edições usando *mssqlctl* comandos.

## <a name="kubeadm-storage-classes"></a>Classes de armazenamento Kubeadm

Kubeadm não vem com uma classe de armazenamento interno. Você deve criar suas próprias classes de armazenamento e os volumes persistentes usando o armazenamento local ou o provisionador preferido, como [torre](https://github.com/rook/rook). Nesse caso, você definiria o **className** para a classe de armazenamento que você configurou. 

> [!NOTE]
>  No internos no arquivo de configuração de implantação do *kubeadm kubeadm-dev-test* há nenhum nome de classe de armazenamento especificado para o armazenamento de dados e de log. Antes da implantação, você deve personalizar o arquivo de configuração e defina o valor para className caso contrário, que as validações de pré-implantação falhará. Implantação também tem uma etapa de validação que verifica a existência da classe de armazenamento, mas não para os volumes persistentes necessários. Você deve garantir que você criar suficiente volumes dependendo da escala do seu cluster. No CTP 3.1, para o tamanho padrão do cluster, você deve criar pelo menos 23 volumes. [Aqui](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) é um exemplo sobre como criar volumes persistentes usando provisionador local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar as configurações para cada pool de armazenamento

Para todas as personalizações, você deve primeiro criar uma cópia da compilação no arquivo de configuração que você deseja usar. Por exemplo, o comando a seguir cria uma cópia do *aks-dev-test* arquivo de configuração de implantação em um subdiretório chamado `custom`:

```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```

Em seguida, você pode personalizar seu arquivo de configuração ao editá-lo manualmente, ou você pode usar **conjunto de seção de configuração de bdc mssqlctl** comando. Esse comando set usa uma combinação de bibliotecas jsonpath e jsonpatch para fornecer maneiras para editar seu arquivo de configuração.

### <a name="configure-size"></a>Configurar o tamanho

Por padrão, o tamanho das declarações de volume persistente provisionados para cada um dos pods provisionados no cluster é de 10 GB. Você pode atualizar esse valor para acomodar as cargas de trabalho que você estiver executando em um arquivo de configuração personalizadas antes da implantação de cluster.

O exemplo a seguir atualiza apenas o tamanho de declarações de volume persistente para dados armazenados no pool de armazenamento para Gi 100. Observe que a seção de armazenamento deve existir no arquivo de configuração para o pool de armazenamento antes de executar este comando:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=100Gi"
```

O exemplo a seguir atualiza o tamanho do volume persistente declarações para todos os pools para 32Gi:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.storage.data.size=32Gi"
```

### <a id="config-samples"></a> Configurar classe de armazenamento

Exemplo a seguir mostra como modificar a classe de armazenamento para o plano de controle:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.storage.data.className=<yourStorageClassName>"
```

Outra opção é editar manualmente o arquivo de configuração personalizada ou usar jsonpatch, como no exemplo a seguir que altera a classe de armazenamento para o pool de armazenamento. Criar uma *patch.json* arquivo com este conteúdo:

```json
{
  "patch": [
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
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

Aplica o arquivo de patch. Use **conjunto de seção de configuração de bdc mssqlctl** comando para aplicar as alterações no arquivo de patch JSON. O exemplo a seguir aplica o arquivo de patch.json para um custom.json de arquivo de configuração de implantação de destino.

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter a documentação completa sobre os volumes no Kubernetes, consulte o [documentação do Kubernetes em Volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obter mais informações sobre como implantar um cluster de big data do SQL Server, consulte [como implantar o SQL Server, o cluster de big data no Kubernetes](deployment-guidance.md).

