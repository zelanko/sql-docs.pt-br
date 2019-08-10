---
title: Alta disponibilidade para contêineres do SQL Server
description: Este artigo apresenta a alta disponibilidade para contêineres do SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077486"
---
# <a name="high-availability-for-sql-server-containers"></a>Alta disponibilidade para contêineres do SQL Server

Crie e gerencie instâncias do SQL Server nativamente no Kubernetes.

Implante o SQL Server em contêineres do Docker gerenciados pelo [Kubernetes](https://kubernetes.io/). No Kubernetes, um contêiner com uma instância do SQL Server pode se recuperar automaticamente caso um nó de cluster falhe. Para obter uma disponibilidade mais robusta, configure o Grupo de Disponibilidade Always On do SQL Server com instâncias do SQL Server em contêineres em um cluster do Kubernetes. Este artigo compara as duas soluções.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Comparar versões do SQL Server no Kubernetes

O SQL Server 2017 fornece uma imagem do Docker que pode ser implantada no Kubernetes. Você pode configurar a imagem com um PVC (declaração de volume persistente) do Kubernetes. O Kubernetes monitora o processo do SQL Server no contêiner. Se o processo, Pod, contêiner ou nó falhar, o Kubernetes inicializará outra instância automaticamente e se reconectará ao armazenamento.

O SQL Server 2019 (versão prévia) introduz uma arquitetura mais robusta com um StatefulSet do Kubernetes. O Kubernetes orquestra instâncias do SQL Server em imagens de contêiner que participam de um grupo de disponibilidade Always On do SQL Server. Esse padrão fornece monitoramento de integridade aprimorado, além de recuperação, expansão de leitura e backup de descarregamento mais rápidos.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contêiner com instância do SQL Server no Kubernetes

O Kubernetes 1.6 e posterior tem suporte para [*classes de armazenamento*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [*declarações de volume persistentes*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) e o [*tipo de volume de disco do Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

Nessa configuração, o Kubernetes desempenha a função do orquestrador de contêineres. 

![Diagrama do cluster do SQL Server Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é uma instância do SQL Server (contêiner) em um [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Um [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) verifica se o pod está recuperado automaticamente após uma falha de nó. Os aplicativos conectam-se ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

O Kubernetes orquestra os recursos no cluster. Quando um nó que hospeda um contêiner de instância do SQL Server falha, ele inicializa um novo contêiner com uma instância do SQL Server e o anexa ao mesmo armazenamento persistente.

O SQL Server 2017 e versões posteriores dão suporte a contêineres no Kubernetes.

Para criar um contêiner no Kubernetes, confira [Implantar um contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Um grupo de disponibilidade do SQL Server Always On em contêineres do SQL Server no Kubernetes

O SQL Server 2019 dá suporte a grupos de disponibilidade em contêineres no Kubernetes. Para grupos de disponibilidade, implante o [operador do Kubernetes do SQL Server](https://coreos.com/blog/introducing-operators.html) em seu cluster do Kubernetes. O operador ajuda a agrupar, implantar e gerenciar instâncias do SQL Server e o grupo de disponibilidade em um cluster.

![Grupo de disponibilidade no contêiner do Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Na imagem acima, um cluster do Kubernetes de quatro nós hospeda um grupo de disponibilidade com três réplicas. A solução inclui os seguintes componentes:

* Uma [*implantação*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) do Kubernetes. A implantação inclui o operador e um mapa de configuração. A implantação descreve a imagem de contêiner, o software e instruções necessários para implantar instâncias do SQL Server para o grupo de disponibilidade.

* Três nós, cada um hospedando um [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). O StatefulSet contém um pod. Cada pod contém:
  * Um contêiner do SQL Server executando uma instância do SQL Server.
  * Um `mcr.microsoft.com/mssql/ha` supervisor para gerenciar o grupo de disponibilidade.

* Dois [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionados ao grupo de disponibilidade. Os ConfigMaps fornecem informações sobre:
  * A implantação do operador.
  * O grupo de disponibilidade.

 * Volumes persistentes para cada instância do SQL Server fornecem o armazenamento para os arquivos de dados e de log.

Além disso, o cluster armazena [*segredos*](https://kubernetes.io/docs/concepts/configuration/secret/) para senhas, certificados, chaves e outras informações confidenciais.

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>Comparar a alta disponibilidade do SQL Server em contêineres com e sem o grupo de disponibilidade

A tabela a seguir compara a funcionalidade de alta disponibilidade do SQL Server em contêineres no Kubernetes com e sem um grupo de disponibilidade:

| |Com um grupo de disponibilidade | Instância de contêiner autônoma<br/> Sem grupo de disponibilidade
|:------|:------|:------
|Recuperar automaticamente de uma falha de nó | Sim | Sim
|Recuperar automaticamente de uma falha de pod | Sim | Sim
|Failover mais rápido |Sim |
|Recuperar automaticamente de uma falha de instância do SQL Server | Sim | 
|Recuperar automaticamente de uma falha de verificação de integridade do banco de dados | Sim | 
|Fornecer réplicas somente leitura | Sim |
|Backup de réplica secundária | Sim | 
|Executa como um StatefulSet | Sim | 

Uma diferença importante é que o tempo de recuperação (ou failover) é mais rápido com um grupo de disponibilidade do que com uma única instância do SQL Server em um contêiner. Essa melhoria ocorre porque o grupo de disponibilidade do SQL Server mantém as réplicas secundárias em outros nós no cluster. No failover, uma réplica secundária é selecionada e promovida para primária. Os aplicativos conectados ao serviço são redirecionados para a nova réplica primária.

Sem o grupo de disponibilidade, quando o Kubernetes detecta um failover, ele precisa criar o contêiner, conectá-lo ao armazenamento e, em seguida, os aplicativos conectados ao serviço são reconectados. O tempo de failover exato depende de onde o failover ocorreu e de como ele foi detectado. 

Geralmente, o tempo de failover para um grupo de disponibilidade é medido em segundos, enquanto o tempo de failover para uma única instância para recuperar um contêiner pode ser de até dez minutos.

## <a name="next-steps"></a>Próximas etapas

Para implantar contêineres do SQL Server no AKS (Serviço de Kubernetes do Azure), confira estes exemplos:

* [Implantar o SQL Server no contêiner do Docker](sql-server-linux-configure-docker.md)
* [Implantar um contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)
* [Grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md)

