---
title: Persistência de dados no Kubernetes
titleSuffix: SQL Server big data clusters
description: Saiba como os volumes persistentes fornecem um modelo de plug-in para armazenamento no Kubernetes. Saiba também como funciona a persistência de dados em um cluster de Big Data do SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 970b049ec7933af9fab1d213d7441f101e01f7c1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765685"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-in-kubernetes"></a>Persistência de dados com o cluster de Big Data do SQL Server em Kubernetes

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Os [volumes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) fornecem um modelo de plug-in para armazenamento no Kubernetes. Nesse modelo, o modo como o armazenamento é fornecido é dissociado de como ele é consumido. Portanto, você pode colocar seu próprio armazenamento altamente disponível e conectá-lo ao cluster de Big Data do SQL Server. Isso dá a você controle total sobre o tipo de armazenamento, disponibilidade e desempenho de que você precisa. O Kubernetes dá suporte a [vários tipos de soluções de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner), incluindo discos/arquivos do Azure, NFS (Network File System) e armazenamento local.

## <a name="configure-persistent-volumes"></a>Configurar volumes persistentes

Um cluster de Big Data do SQL Server consume esses volumes persistentes usando [classes de armazenamento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Você pode criar classes de armazenamento distintas para um tipo diferente de armazenamento e especificá-las no momento da implantação do cluster de Big Data. Você pode configurar a classe de armazenamento e o tamanho da declaração de volume persistente a serem usados para uma finalidade específica no nível do pool. Um cluster de Big Data do SQL Server cria [declarações de volume persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) usando o nome de classe de armazenamento especificado para cada componente que requer volumes persistentes. Em seguida, ele monta o(s) volume(s) persistente(s) correspondente(s) no pod. 

Estes são alguns aspectos importantes a serem considerados quando você estiver planejando a configuração de armazenamento para seu cluster de Big Data:

- Para uma implantação de cluster de Big Data bem-sucedida, verifique se você tem o número necessário de volumes persistentes disponíveis. Se você estiver realizando a implantação em um cluster do AKS (Azure Kubernetes Service) e estiver usando uma classe de armazenamento interna (`default` ou `managed-premium`), ela dará suporte ao provisionamento dinâmico para os volumes persistentes. Portanto, você não precisa pré-criar os volumes persistentes, mas deve garantir que os nós de trabalho disponíveis no cluster do AKS possam anexar tantos discos quanto o número de volumes persistentes que são necessários para a implantação. Dependendo do [tamanho da VM](/azure/virtual-machines/linux/sizes) especificado para os nós de trabalho, cada nó pode anexar determinado número de discos. Para um cluster de tamanho padrão (sem alta disponibilidade), são necessários, no mínimo, 24 discos. Se você estiver habilitando a alta disponibilidade ou expandindo qualquer pool, verifique se você tem, no mínimo, dois volumes persistentes por cada réplica adicional, independentemente do recurso que você está expandindo.

- Se o provisionador de armazenamento para a classe de armazenamento que você está fornecendo na configuração não der suporte ao provisionamento dinâmico, você precisará pré-criar os volumes persistentes. Por exemplo, o provisionador `local-storage` não habilita o provisionamento dinâmico. Confira este [script de exemplo](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) para obter diretrizes sobre como proceder em um cluster do Kubernetes implantado com `kubeadm`.

- Ao implantar um cluster de Big Data, você pode configurar a mesma classe de armazenamento para ser usada por todos os componentes no cluster. Mas, como uma melhor prática para uma implantação de produção, vários componentes exigirão configurações de armazenamento diferentes para acomodar várias cargas de trabalho em termos de tamanho ou taxa de transferência. Substitua a configuração de armazenamento padrão especificada no controlador para cada um dos pools de armazenamento, conjuntos de dados e instâncias mestres do SQL Server. Este artigo fornece exemplos de como fazer isso.

- Ao calcular os requisitos de dimensionamento do pool de armazenamento, considere o fator de replicação com o qual o HDFS está configurado.  O fator de replicação é configurável no momento da implantação no arquivo de configuração da implantação do cluster. O valor padrão para os perfis de DevTest (ou seja, `aks-dev-test` ou `kubeadm-dev-test`) é 2 e, para os perfis que recomendamos para implantações de produção (ou seja, `kubeadm-prod`), é 3. Como melhor prática, recomendamos que você configure sua implantação de produção do cluster de Big Data com um fator de replicação para o HDFS de pelo menos 3. O valor do fator de replicação afetará o número de instâncias no pool de armazenamento: no mínimo, você precisa implantar um número de instâncias do pool de armazenamento equivalente ao valor do fator de replicação. Além disso, você precisa dimensionar o armazenamento adequadamente e levar em conta os dados sendo replicados no HDFS tantas vezes quanto for o valor do fator de replicação. Encontre mais informações sobre a replicação de dados no HDFS [aqui](https://hadoop.apache.org/docs/r3.2.1/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Data_Replication). 

- Da versão SQL Server 2019 CU1 em diante, não é possível modificar uma definição de configuração de armazenamento após a implantação. Esta restrição impede você não apenas de modificar o tamanho da declaração de volume persistente para cada instância, mas também de expandir operações de dimensionamento após a implantação. Portanto, é muito importante planejar o layout de armazenamento antes de implantar um cluster de Big Data.

- Ao implantar no Kubernetes como aplicativos em contêineres e usar recursos como conjuntos com estado e armazenamento persistente, o Kubernetes garante que os pods sejam reiniciados em caso de problemas de integridade e anexados ao mesmo armazenamento persistente. Mas caso haja uma falha de nó e um pod precise ser reiniciado em outro nó, haverá um risco maior de não disponibilidade se o armazenamento for local para o nó com falha. Para reduzir esse risco, é necessário configurar a redundância adicional e habilitar [recursos de alta disponibilidade](deployment-high-availability.md) ou usar o armazenamento com redundância remota. Veja abaixo uma visão geral das opções de armazenamento para vários componentes nos Clusters de Big Data:

| Recursos | Tipo de armazenamento para dados | Tipo de armazenamento para log |  Observações |
|---|---|---|--|
| Instância mestra do SQL Server | Armazenamento local (réplicas>=3) ou com redundância remota (réplica=1) | Armazenamento local | Implementação baseada em conjunto com estado em que os pods que ficam com os nós garantirão que as reinicializações e as falhas transitórias não causem perda de dados. |
| Pool de computação | Armazenamento local | Armazenamento local | Nenhum dado de usuário armazenado. |
| Pool de dados | Armazenamento local/com redundância remota | Armazenamento local | Use o armazenamento com redundância remota se o pool de dados não puder ser recriado com base em outras fontes de dados.  |
| Pool de armazenamento (HDFS) | Armazenamento local/com redundância remota | Armazenamento local | A replicação HDFS está habilitada. |
| Pool do Spark | Armazenamento local | Armazenamento local | Nenhum dado de usuário armazenado. |
| Controle (controldb, metricsdb, logsdb)| Armazenamento com redundância remota | Armazenamento local | É crítico o uso da redundância no nível de armazenamento para metadados do cluster de Big Data. |

> [!IMPORTANT]
> Garanta que os componentes relacionados ao controle estejam em um dispositivo de armazenamento com redundância remota. Um pod `controldb-0` hospeda uma instância do SQL Server com bancos de dados que armazenam todos os metadados relacionados aos estados do serviço de cluster, várias configurações e outras informações relevantes. Se essa instância ficar não disponível, ela causará problemas de integridade com outros serviços dependentes no cluster.

## <a name="configure-big-data-cluster-storage-settings"></a>Definir configurações de armazenamento de cluster de Big Data

Como em outras personalizações, você pode especificar configurações de armazenamento nos arquivos de configuração do cluster no momento da implantação para cada pool no arquivo de configuração `bdc.json` e para os serviços de controle no arquivo `control.json`. Se não houver definições de configuração de armazenamento nas especificações do pool, as configurações de armazenamento do controle serão usadas para todos os outros componentes, incluindo mestre do SQL Server (recurso `master`), HDFS (recurso `storage-0`) e componentes de pool de dados. O seguinte exemplo de código representa a seção de configuração de armazenamento que você pode incluir na especificação:

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

A implantação do cluster de Big Data usa o armazenamento persistente para armazenar dados, metadados e logs para vários componentes. Você pode personalizar o tamanho das declarações de volume persistente criadas como parte da implantação. Como melhor prática, recomendamos usar classes de armazenamento com uma [política de recuperação](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy) de *Retenção*.

> [!WARNING]
> A execução sem armazenamento persistente pode funcionar em um ambiente de teste, mas pode resultar em um cluster não funcional. Quando um pod é reinicializado, os metadados do cluster e/ou os dados do usuário são perdidos permanentemente. Não recomendamos a execução nessa configuração.

A seção [Configurar armazenamento](#config-samples) fornece mais exemplos de como definir configurações de armazenamento para sua implantação de cluster de Big Data do SQL Server.

## <a name="aks-storage-classes"></a>Classes de armazenamento do AKS

O AKS é fornecido com [duas classes de armazenamento internas](/azure/aks/azure-disks-dynamic-pv/), `default` e `managed-premium`, juntamente com um provisionador dinâmico para elas. Você pode especificar qualquer uma delas ou criar uma classe de armazenamento própria para implantar o cluster de Big Data com o armazenamento persistente habilitado. Por padrão, o arquivo de configuração do cluster interno para o AKS, `aks-dev-test`, é fornecido com as configurações de armazenamento persistente para usar a classe de armazenamento `default`.

> [!WARNING]
> Os volumes persistentes criados com as classes de armazenamento internas `default` e `managed-premium` têm uma política de recuperação de *Exclusão*. Portanto, quando você exclui o cluster de Big Data do SQL Server, as declarações de volume persistente são excluídas, assim como os volumes persistentes. Você pode criar classes de armazenamento personalizadas usando o provisionador `azure-disk` com uma política de recuperação `Retain`, conforme descrito em [conceitos de armazenamento](/azure/aks/concepts-storage/#storage-classes).

## <a name="storage-classes-for-kubeadm-clusters"></a>Classes de armazenamento para clusters `kubeadm` 

Os clusters do Kubernetes que são implantados usando `kubeadm` não têm uma classe de armazenamento interna. Você precisa criar classes de armazenamento e volumes persistentes usando o armazenamento local ou seu [provisionador de armazenamento preferido](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner). Nessa situação, você define a `className` como a classe de armazenamento configurada.

> [!IMPORTANT]
>  Nos arquivos de configuração de implantação internos para kubeadm (`kubeadm-dev-test` e `kubeadm-prod`), não há nenhum nome de classe de armazenamento especificado para armazenamento de dados e de log. Antes da implantação, você precisa personalizar o arquivo de configuração e definir o valor de `className`. Caso contrário, as validações de pré-implantação falharão. A implantação também tem uma etapa de validação que verifica a existência da classe de armazenamento, mas não os volumes persistentes necessários. Certifique-se de criar volumes suficientes dependendo da escala do cluster. Para o tamanho mínimo de cluster padrão (escala padrão, sem alta disponibilidade), é necessário criar, pelo menos, 24 volumes persistentes. Para obter um exemplo de como criar volumes persistentes usando um provisionamento local, confira [Criar um cluster do Kubernetes usando o Kubeadm](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu).

## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar as configurações de armazenamento para cada pool

Para todas as personalizações, você deve primeiro criar uma cópia do arquivo de configuração interno que deseja usar. Por exemplo, o seguinte comando cria uma cópia dos arquivos de configuração de implantação `aks-dev-test` em um subdiretório chamado `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Esse processo cria dois arquivos, `bdc.json` e `control.json`, que você pode personalizar, editando-os manualmente ou usando o comando `azdata bdc config`. Você pode usar uma combinação de bibliotecas jsonpath e jsonpatch para fornecer maneiras de editar os arquivos de configuração.


### <a name="configure-storage-class-name-andor-claims-size"></a><a id="config-samples"></a> Configurar o nome da classe de armazenamento e/ou o tamanho das declarações

Por padrão, o tamanho das declarações de volume persistente provisionadas para cada um dos pods provisionados no cluster é de 10 gigabytes (GB). É possível atualizar esse valor para acomodar as cargas de trabalho que você está executando em um arquivo de configuração personalizado antes da implantação do cluster.

No exemplo a seguir, o tamanho das declarações de volume persistente está atualizado para 32 GB no `control.json`. Se não for substituída no nível do pool, essa configuração será aplicada a todos os pools.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

O seguinte exemplo mostra como modificar a classe de armazenamento para o arquivo `control.json`:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Você também tem a opção de editar manualmente o arquivo de configuração personalizado ou usar um patch .json que altera a classe de armazenamento para o pool de armazenamento, como no seguinte exemplo:

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

Aplique o arquivo de patch. Use o comando `azdata bdc config patch` para aplicar as alterações ao arquivo de patch .json. O seguinte exemplo aplica o arquivo `patch.json` a um arquivo de configuração de implantação de destino, `custom.json`:

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Próximas etapas

- Para obter a documentação completa sobre volumes no Kubernetes, confira a [documentação do Kubernetes sobre volumes](https://kubernetes.io/docs/concepts/storage/volumes/).

- Para obter mais informações sobre a implantação de um cluster de Big Data do SQL Server, confira [Como implantar um cluster de Big Data do SQL Server no Kubernetes](deployment-guidance.md).