---
title: Alta disponibilidade para contêineres do SQL Server
description: Este artigo apresenta alta disponibilidade para contêineres do SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: da4c702e8ec5e8c1d645af616df53edd287eae5a
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833921"
---
# <a name="high-availability-for-sql-server-containers"></a>Alta disponibilidade para contêineres do SQL Server

Criar e gerenciar suas instâncias do SQL Server nativamente no Kubernetes.

Implantar o SQL Server para contêineres do docker gerenciados pelo [Kubernetes](https://kubernetes.io/). No Kubernetes, um contêiner com uma instância do SQL Server pode se recuperar automaticamente em caso de falha de um nó de cluster. Para disponibilidade mais robusta, configure o grupo de disponibilidade Always On do SQL Server com instâncias do SQL Server em contêineres em um cluster Kubernetes. Este artigo compara as duas soluções.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Comparar versões do SQL Server no Kubernetes

SQL Server 2017 fornece uma imagem do Docker que pode implantar no Kubernetes. Você pode configurar a imagem com uma declaração de volume persistente Kubernetes (PVC). Kubernetes monitora o processo do SQL Server no contêiner. Se o processo, pod, contêiner ou nó falhar, o Kubernetes automaticamente inicializa a outra instância e reconecta-se ao armazenamento.

2019 do SQL Server (versão prévia) apresenta uma arquitetura mais robusta com um Kubernetes StatefulSet. O Kubernetes orquestra as instâncias do SQL Server em imagens de contêiner que participam de um SQL Server sempre no grupo de disponibilidade. Esse padrão fornece monitoramento de integridade aprimorada, uma recuperação mais rápida, backup de descarregamento e escala de leitura-out.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contêiner com a instância do SQL Server no Kubernetes

Kubernetes 1.6 ou posterior tem suporte para [ *classes de armazenamento*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [ *declarações de volume persistente*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)e o [  *Tipo de volume de disco do Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

Nessa configuração, o Kubernetes desempenha a função de orquestrador de contêiner. 

![Diagrama de cluster do Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é uma instância do SQL Server (contêiner) em um [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Um [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garante que o pod é automaticamente recuperado após uma falha de nó. Aplicativos se conectam ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

O Kubernetes orquestra os recursos do cluster. Quando um nó que hospeda um contêiner de instância do SQL Server falha, ele inicializa um novo contêiner com uma instância do SQL Server e anexa-o para o mesmo armazenamento persistente.

SQL Server 2017 e posterior com suporte a contêineres no Kubernetes.

Para criar um contêiner no Kubernetes, consulte [implantar um contêiner do SQL Server em Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Um grupo de disponibilidade Always On do SQL Server em contêineres do SQL Server no Kubernetes

2019 do SQL Server dá suporte a grupos de disponibilidade em contêineres em um Kubernetes. Para grupos de disponibilidade, implante o SQL Server [Kubernetes operador](https://coreos.com/blog/introducing-operators.html) ao cluster Kubernetes. O operador ajuda o pacote, implantar e gerenciar instâncias do SQL Server e o grupo de disponibilidade em um cluster.

![AG no contêiner do Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Na imagem acima, um cluster de quatro nós kubernetes hospeda um grupo de disponibilidade com três réplicas. A solução inclui os seguintes componentes:

* Um Kubernetes [ *implantação*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). A implantação inclui o operador e um mapa de configuração. A implantação descreve a imagem de contêiner, software e as instruções necessárias para implantar as instâncias do SQL Server para o grupo de disponibilidade.

* Três nós, cada uma hospedando um [ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). O StatefulSet contém um pod. Cada pod contém:
  * Um contêiner do SQL Server executando uma instância do SQL Server.
  * Um supervisor `mcr.microsoft.com/mssql/ha` para gerenciar o grupo de disponibilidade.

* Duas [ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionadas ao grupo de disponibilidade. Os ConfigMaps fornecem informações sobre:
  * A implantação para o operador.
  * O grupo de disponibilidade.

 * Volumes persistentes para cada instância do SQL Server fornecem o armazenamento para os arquivos de log e de dados.

Além disso, o cluster armazena [ *segredos* ](https://kubernetes.io/docs/concepts/configuration/secret/) para as senhas, certificados, chaves e outras informações confidenciais.

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>Compare a alta disponibilidade do SQL Server em contêineres com e sem o grupo de disponibilidade

A tabela a seguir compara o recurso de alta disponibilidade do SQL Server em contêineres no Kubernetes com e sem um grupo de disponibilidade:

| |Com um grupo de disponibilidade | Instância de contêiner autônoma<br/> Nenhum grupo de disponibilidade
|:------|:------|:------
|Se recuperar automaticamente de falhas do nó | Sim | Sim
|Se recuperar automaticamente de falhas de pod | Sim | Sim
|Failover mais rápido |Sim |
|Se recuperar automaticamente de falha da instância do SQL Server | Sim | 
|Se recuperar automaticamente de falha de verificação de integridade do banco de dados | Sim | 
|Fornecer réplicas somente leitura | Sim |
|Backup de réplica secundária | Sim | 
|É executado como um StatefulSet | Sim | 

Uma diferença importante é que o tempo de recuperação (ou failover) é mais rápido com um grupo de disponibilidade que com uma única instância do SQL Server em um contêiner. Essa melhoria é porque o grupo de disponibilidade do SQL Server mantém as réplicas secundárias em outros nós no cluster. Durante o failover, uma réplica secundária está selecionada e promovida a primária. Aplicativos conectados ao serviço são redirecionados para a nova réplica primária.

Sem o grupo de disponibilidade, quando Kubernetes detecta um failover, ele precisa criar o contêiner, conecte-se para o armazenamento e, em seguida, os aplicativos conectados ao serviço sejam reconectados. O tempo de failover exata depende de onde foi o failover, e como ele foi detectado. 

Em geral, o tempo de failover para um grupo de disponibilidade é medido em segundos, enquanto o tempo de failover de única instância recuperar um contêiner pode ser de até 10 minutos.

## <a name="next-steps"></a>Próximas etapas

Para implantar contêineres do SQL Server no serviço de Kubernetes do Azure (AKS), consulte estes exemplos:

* [Implantar o SQL Server no contêiner do Docker](sql-server-linux-configure-docker.md)
* [Implantar um contêiner do SQL Server em Kubernetes](tutorial-sql-server-containers-kubernetes.md)
* [Grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md)

