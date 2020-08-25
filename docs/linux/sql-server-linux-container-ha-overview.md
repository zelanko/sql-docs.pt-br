---
title: Alta disponibilidade para contêineres do SQL Server
description: Saiba mais sobre a alta disponibilidade para contêineres do SQL Server. Saiba mais também sobre a implantação de um contêiner com o SQL Server no Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 00665a8306dbf586b92cfec14a8fe21f631f96c9
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088891"
---
# <a name="high-availability-for-sql-server-containers"></a>Alta disponibilidade para contêineres do SQL Server

Crie e gerencie instâncias do SQL Server nativamente no Kubernetes.

Implante o SQL Server em contêineres do Docker gerenciados pelo [Kubernetes](https://kubernetes.io/). No Kubernetes, um contêiner com uma instância do SQL Server pode se recuperar automaticamente caso um nó de cluster falhe.

O SQL Server 2017 introduz uma imagem do Docker que pode ser implantada no Kubernetes. Você pode configurar a imagem com um PVC (declaração de volume persistente) do Kubernetes. O Kubernetes monitora o processo do SQL Server no contêiner. Se o processo, Pod, contêiner ou nó falhar, o Kubernetes inicializará outra instância automaticamente e se reconectará ao armazenamento.

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contêiner com instância do SQL Server no Kubernetes

O Kubernetes 1.6 e posterior tem suporte para [*classes de armazenamento*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [*declarações de volume persistentes*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) e o [*tipo de volume de disco do Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

Nessa configuração, o Kubernetes desempenha a função do orquestrador de contêineres. 

![Diagrama do cluster do SQL Server Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

No diagrama anterior, `mssql-server` é uma instância do SQL Server (contêiner) em um [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Um [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) verifica se o pod está recuperado automaticamente após uma falha de nó. Os aplicativos conectam-se ao serviço. Nesse caso, o serviço representa um balanceador de carga que hospeda um endereço IP que permanece o mesmo após a falha do `mssql-server`.

O Kubernetes orquestra os recursos no cluster. Quando um nó que hospeda um contêiner de instância do SQL Server falha, ele inicializa um novo contêiner com uma instância do SQL Server e o anexa ao mesmo armazenamento persistente.

O SQL Server 2017 e versões posteriores dão suporte a contêineres no Kubernetes.

Para criar um contêiner no Kubernetes, confira [Implantar um contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="next-steps"></a>Próximas etapas

Para implantar contêineres do SQL Server no AKS (Serviço de Kubernetes do Azure), confira estes exemplos:
* [Implantar o SQL Server no contêiner do Docker](sql-server-linux-configure-docker.md)
* [Implantar um contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)
