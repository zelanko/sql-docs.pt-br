---
title: Persistência de dados no Kubernetes
titleSuffix: SQL Server big data clusters
description: Saiba mais sobre como a persistência de dados funciona em um cluster de Big Data do SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4671bc07dd21a769746257339ea7903e3dda4701
ms.sourcegitcommit: 385a907ed1de8fa7ada76260ea3f92583eb09238
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74063971"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistência de dados com o cluster de Big Data do SQL Server no Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Os [Volumes Persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para armazenamento no Kubernetes. O modo como o armazenamento é fornecido é dissociado de como ele é consumido. Portanto, você pode colocar seu próprio armazenamento altamente disponível e conectá-lo ao cluster de Big Data do SQL Server. Isso dá a você controle total sobre o tipo de armazenamento, disponibilidade e desempenho de que você precisa. O Kubernetes dá suporte a vários tipos de soluções de armazenamento, incluindo discos/arquivos do Azure, NFS, armazenamento local e muito mais.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

A forma como um cluster de Big Data do SQL Server consume esses volumes persistentes é usando [Classes de Armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento diferentes para um tipo diferente de armazenamento e especificá-las no momento da implantação do cluster de Big Data. Você pode configurar a classe de armazenamento e o tamanho da declaração de volume persistente a serem usados para qual finalidade no nível do pool. Um cluster de Big Data do SQL Server cria [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) com o nome de classe de armazenamento especificado para cada componente que requer volumes persistentes. Em seguida, ele monta os volumes persistentes correspondentes no pod. 

Estes são alguns aspectos importantes a serem considerados quando você estiver planejando a configuração de armazenamento para seu cluster de Big Data:

- Para uma implantação de cluster de Big Data bem-sucedida, é necessário garantir que o número necessário de volumes persistentes esteja disponível. Se você estiver realizando a implantação em um cluster do AKS e estiver usando uma das classes de armazenamento internas (`default` ou `managed-premium`), elas darão suporte ao provisionamento dinâmico para os volumes persistentes. Isso significa que você não precisa pré-criar os volumes persistentes, mas precisa garantir que os nós de trabalho disponíveis no cluster do AKS possam anexar o número de discos para os volumes persistentes que forem necessários para a implantação. Dependendo do [tamanho da VM](/azure/virtual-machines/linux/sizes/) especificado para os nós de trabalho, cada nó pode anexar determinado número de discos. Para um cluster de tamanho padrão (sem alta disponibilidade), são necessários, no mínimo, 24 discos. Se você estiver habilitando a alta disponibilidade ou expandindo qualquer pool, precisará garantir, no mínimo, dois volumes persistentes por cada réplica adicional, independentemente do recurso que está sendo expandido.

- Se o provisionador de armazenamento para a classe de armazenamento que você está fornecendo na configuração não der suporte ao provisionamento dinâmico, você precisará pré-criar os volumes persistentes. Por exemplo, o provisionador `local-storage` não habilita o provisionamento dinâmico. Confira este [script de exemplo](https://github.com/microsoft/sql-server-samples/tree/cu1-bdc/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) para saber como fazer isso em um cluster do Kubernetes implantado com `kubeadm`.

- Ao implantar um cluster de Big Data, você pode configurar a mesma classe de armazenamento a ser usada por todos os componentes no cluster. Mas, como uma melhor prática para uma implantação de produção, vários componentes exigirão configurações de armazenamento diferentes para acomodar várias cargas de trabalho em termos de tamanho ou taxa de transferência. Substitua a configuração de armazenamento padrão especificada no controlador para cada um dos pools de armazenamento e dados e instância mestra do SQL Server. Este artigo fornece exemplos de como fazer isso.

- Da versão SQL Server 2019 CU1 em diante, não é possível modificar a definição de configuração de armazenamento após a implantação. Isso inclui não só a modificação do tamanho da declaração de volume persistente para cada instância, mas também o fato de que não há suporte para operações de dimensionamento após a implantação. Portanto, o planejamento do layout de armazenamento antes do cluster de Big Data é muito importante.

- Pela natureza da implantação no Kubernetes como aplicativos em contêineres e usando recursos como conjuntos com estado e armazenamento persistente, o Kubernetes garante que os pods sejam reiniciados em caso de problemas de integridade e anexados ao mesmo armazenamento persistente. Mas caso haja uma falha de nó e o pod precise ser reiniciado em outro nó, haverá um risco maior de indisponibilidade se o armazenamento for local para o nó com falha. Para superar esse risco, é necessário configurar a redundância adicional e habilitar [recursos de alta disponibilidade](deployment-high-availability.md) ou usar o armazenamento com redundância remota. Veja a seguir uma visão geral das opções de armazenamento para vários componentes nos clusters de Big Data.

| Recursos | Tipo de armazenamento para dados | Tipo de armazenamento para log |  Observações |
|---|---|---|--|
| Instância mestra do SQL Server | Armazenamento local (réplicas>=3) ou com redundância remota (réplica=1) | Armazenamento local | A implementação baseada em conjunto com estado em que os pods se limitam aos nós garantirá que as reinicializações e as falhas transitórias não causem perda de dados. |
| Pool de computação | Armazenamento local* | Armazenamento local | Nenhum dado de usuário armazenado. |
| Pool de dados | Armazenamento local/com redundância remota | Armazenamento local | Use o armazenamento com redundância remota se o pool de dados não puder ser recriado com base em outras fontes de dados.  |
| Pool de armazenamento (HDFS) | Armazenamento local/com redundância remota | Armazenamento local | A replicação HDFS está habilitada. |
| Pool do Spark | Armazenamento local* | Armazenamento local | Nenhum dado de usuário armazenado. |
| Controle (controldb, metricsdb, logsdb)| Armazenamento com redundância remota | Armazenamento local | É crítico o uso da redundância no nível de armazenamento para metadados do cluster de Big Data. |

> [!IMPORTANT]
> É necessário garantir que os componentes relacionados ao controle estejam no armazenamento com redundância remota. O pod `controldb-0` hospeda uma instância do SQL Server com bancos de dados que armazenam todos os metadados sobre os estados do serviço de cluster, várias configurações etc. A indisponibilidade dessa instância causará problemas de integridade com outros serviços dependentes no cluster.

## <a name="configure-big-data-cluster-storage-settings"></a>Definir configurações de armazenamento de cluster de Big Data

De modo semelhante a outras personalizações, você pode especificar configurações de armazenamento nos arquivos de configuração do cluster no momento da implantação para cada pool no arquivo de configuração `bdc.json` e para os serviços de controle no arquivo `control.json`. Se não houver definições de configuração de armazenamento nas especificações do pool, as configurações de armazenamento do controle serão usadas para todos os outros componentes, incluindo mestre do SQL Server (recurso `master`), HDFS (recurso `storage-0`) ou pool de dados. Este é um exemplo da seção de configuração de armazenamento que você pode incluir na especificação:

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

> [!WARNING]
> A execução sem armazenamento persistente pode funcionar em um ambiente de teste, mas pode resultar em um cluster não funcional. Após a reinicialização do pod, os metadados do cluster e/ou os dados do usuário serão perdidos permanentemente. Não recomendamos a execução nessa configuração. 

A seção [Configurar armazenamento](#config-samples) fornece mais exemplos de como definir as configurações de armazenamento para sua implantação de cluster de Big Data do SQL Server.

## <a name="aks-storage-classes"></a>Classes de armazenamento do AKS

O AKS é fornecido com [duas classes de armazenamento internas](/azure/aks/azure-disks-dynamic-pv/) `default` e `managed-premium`, juntamente com o provisionador dinâmico para elas. Você pode especificar qualquer uma delas ou criar sua própria classe de armazenamento para implantar o cluster de Big Data com o armazenamento persistente habilitado. Por padrão, o arquivo de configuração do cluster interno para o AKS `aks-dev-test`é fornecido com as configurações de armazenamento persistente para usar a classe de armazenamento `default`.

> [!WARNING]
> Os volumes persistentes criados com as classes de armazenamento internas `default` e `managed-premium` têm uma política de recuperação de *Exclusão*. Portanto, no momento em que você exclui o cluster de Big Data do SQL Server, as declarações de volume persistente são excluídas e, em seguida, os volumes persistentes também. Você pode criar classes de armazenamento personalizadas usando o provisionador `azure-disk` com uma política de recuperação `Retain`, conforme mostrado [neste](/azure/aks/concepts-storage/#storage-classes) artigo.

## <a name="storage-classes-for-kubeadm-clusters"></a>Classes de armazenamento para clusters `kubeadm` 

Os clusters do Kubernetes implantados com o uso de `kubeadm` não têm uma classe de armazenamento interna. Você precisa criar suas próprias classes de armazenamento e volumes persistentes usando o armazenamento local ou seu provisionador preferido, como [Torre](https://github.com/rook/rook). Nesse caso, você definirá a `className` como a classe de armazenamento configurada. 

> [!IMPORTANT]
>  Nos arquivos de configuração de implantação internos para kubeadm (`kubeadm-dev-test` ou `kubeadm-prod`), não há nenhum nome de classe de armazenamento especificado para o armazenamento de dados e de log. Antes da implantação, você precisa personalizar o arquivo de configuração e definir o valor de `className`; caso contrário, as validações de pré-implantação falharão. A implantação também tem uma etapa de validação que verifica a existência da classe de armazenamento, mas não os volumes persistentes necessários. Você precisa criar volumes suficientes dependendo da escala do cluster. Para o tamanho mínimo de cluster padrão (escala padrão, sem alta disponibilidade), é necessário criar, pelo menos, 24 volumes persistentes.
>
>[Criar um cluster do Kubernetes](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) apresenta um exemplo de como você pode criar volumes persistentes usando o provisionador local. Este exemplo apresenta o armazenamento do Kubernetes.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar as configurações de armazenamento para cada pool

Para todas as personalizações, você deve primeiro criar uma cópia do arquivo de configuração interno que deseja usar. Por exemplo, o seguinte comando cria uma cópia dos arquivos de configuração de implantação `aks-dev-test` em um subdiretório chamado `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Isso cria dois arquivos, `bdc.json` e `control.json`, que podem ser personalizados pela edição manual ou você pode usar o comando `azdata bdc config`. Você pode usar uma combinação de bibliotecas jsonpath e jsonpatch para fornecer maneiras de editar os arquivos de configuração.


### <a id="config-samples"></a> Configurar o nome da classe de armazenamento e/ou o tamanho das declarações

Por padrão, o tamanho das declarações de volume persistente provisionadas para cada um dos pods provisionados no cluster é de 10 GB. Você pode atualizar esse valor para acomodar as cargas de trabalho que está executando em um arquivo de configuração personalizado antes da implantação do cluster.

O exemplo a seguir atualiza o tamanho das declarações de volume persistente para 32Gi no `control.json`. Se não for substituída no nível do pool, essa configuração será aplicada a todos os pools:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

O seguinte exemplo mostra como modificar a classe de armazenamento para o arquivo `control.json`:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Outra opção é editar manualmente o arquivo de configuração personalizado ou usar json patch como no exemplo a seguir, que altera a classe de armazenamento para o pool de armazenamento. Crie um arquivo `patch.json` com este conteúdo:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
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

Aplique o arquivo de patch. Use o comando `azdata bdc config patch` para aplicar as alterações ao arquivo de patch JSON. O exemplo a seguir aplica o arquivo `patch.json` a um arquivo de configuração de implantação de destino `custom.json`.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

Para obter a documentação completa sobre volumes no Kubernetes, confira a [documentação do Kubernetes sobre volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obter mais informações sobre a implantação de um cluster de Big Data do SQL Server, confira [Como implantar um cluster de Big Data do SQL Server no Kubernetes](deployment-guidance.md).
