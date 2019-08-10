---
title: Grupos de disponibilidade Always On para contêineres que executam Linux
titleSuffix: SQL Server
description: Este artigo apresenta os grupos de disponibilidade em contêineres do SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910477"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Grupos de disponibilidade Always On para contêineres do SQL Server

O SQL Server 2019 dá suporte a grupos de disponibilidade em contêineres em um cluster do Kubernetes. Para grupos de disponibilidade, implante o [operador do Kubernetes do SQL Server](https://coreos.com/blog/introducing-operators.html) em seu cluster do Kubernetes. O operador ajuda a empacotar, implantar e gerenciar o grupo de disponibilidade em um cluster.

![AG no contêiner do Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Na imagem acima, um cluster Kubernetes de quatro nós hospeda um grupo de disponibilidade com três réplicas. A solução inclui os seguintes componentes:

* Uma [*implantação*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) do Kubernetes. A implantação inclui o operador e um mapa de configuração. Eles fornecem a imagem de contêiner, o software e instruções necessários para implantar instâncias do SQL Server para o grupo de disponibilidade.

* Três nós, cada um hospedando um [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). O StatefulSet contém um [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Cada pod contém:
  * Um contêiner do SQL Server executando uma instância do SQL Server.
  * Um agente do grupo de disponibilidade. 

* Dois [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionados ao grupo de disponibilidade. Os ConfigMaps fornecem informações sobre:
  * A implantação do operador.
  * O grupo de disponibilidade.

 * [*Volumes persistentes*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) são partes de armazenamento. Uma PVC (*declaração de volume persistente*) é uma solicitação de armazenamento por um usuário. Cada contêiner é afiliado a um PVC para o armazenamento de dados e de log. No AKS (Serviço de Kubernetes do Azure), [crie uma declaração de volume persistente](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) para provisionar automaticamente armazenamento com base em uma classe de armazenamento.


Além disso, o cluster armazena [*segredos*](https://kubernetes.io/docs/concepts/configuration/secret/) para senhas, certificados, chaves e outras informações confidenciais.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Implantar o grupo de disponibilidade no Kubernetes

Para implantar um grupo de disponibilidade no Kubernetes:

1. Crie o cluster do Kubernetes

   Para um grupo de disponibilidade, crie pelo menos três nós para o SQL Server, além de um nó para o mestre.

1. Implante o operador

1. Configure o armazenamento

1. Implante o StatefulSet

   O operador escuta instruções para implantar o StatefulSet. Ele cria automaticamente as instâncias do SQL Server nos três nós separados e configura o grupo de disponibilidade com um gerenciador de cluster externo.

1. Criar os bancos de dados e anexá-los ao grupo de disponibilidade

Para obter etapas detalhadas, confira [Grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operador do Kubernetes do SQL Server

Depois de implantar o operador, ele registra um recurso de SQL Server personalizado. Use o operador para implantar esse recurso.  Cada recurso corresponde a uma instância do SQL Server e inclui propriedades específicas como `sapassword` e `monitoring policy`. O operador analisa o recurso e implanta um StatefulSet do Kubernetes.

O StatfulSet contém:

* contêiner mssql-server

* contêiner mssql-ha-supervisor

O código do operador, o supervisor de HA e o SQL Server é empacotado em uma imagem do Docker chamada `mcr.microsoft.com/mssql/ha`. Essa imagem contém os seguintes binários:

* `mssql-operator`

    Esse processo é implantado como uma implantação do Kubernetes separada. Ele registra o [recurso personalizado do Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) chamado `SqlServer` (sqlservers.mssql.microsoft.com). Em seguida, ele escuta esses repositórios sendo criados ou atualizados no cluster do Kubernetes. Para cada evento desse tipo, ele cria ou atualiza os recursos do Kubernetes para a instância correspondente (por exemplo, o StatefulSet ou o trabalho `mssql-server-k8s-init-sql`).

* `mssql-server-k8s-health-agent`

    Esse servidor Web atende a [investigações de atividade](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) do Kubernetes para determinar a integridade de uma instância do SQL Server. Monitora a integridade da instância do SQL Server local chamando `sp_server_diagnostics` e comparando os resultados com a política de monitor.

* `mssql-ha-supervisor`

   Mantém o certificado de AG e o ponto de extremidade. 

* `mssql-server-k8s-ag-agent`
  
    Esse processo monitora a integridade de uma réplica de AG em uma instância do SQL Server única e executa failovers.

    Ele também mantém a eleição do líder.

* `mssql-server-k8s-init-sql`
  
    Esse [trabalho](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) do Kubernetes aplica uma configuração de estado desejado a uma instância do SQL Server. O trabalho é criado pelo operador sempre que um recurso do SqlServer é criado ou atualizado. Ele verifica se a instância do SQL Server de destino correspondente ao recurso personalizado tem a configuração desejada descrita no recurso.

    Por exemplo, se qualquer uma das configurações a seguir forem necessárias, ele as concluirá:
  * Atualizar a senha SA
  * Cria o logon do SQL para os agentes
  * Cria o ponto de extremidade DBM

* `mssql-server-k8s-rotate-creds`
  
    Este trabalho do Kubernetes implementa a tarefa de girar credenciais. Crie esse trabalho para solicitar atualizações para a senha SA, a senha de logon do SQL do agente, o certificado DBM, etc. A senha SA é especificada como os parâmetros de trabalho. Os outros são gerados automaticamente.

* `mssql-server-k8s-failover`

   Um trabalho do Kubernetes que implementa o fluxo de trabalho de failover manual.

### <a name="notes"></a>Observações

Independentemente da configuração do AG, o operador sempre implantará o supervisor de HA. Se o recurso SqlServer não listar nenhum AG, o operador ainda implantará esse contêiner.

A versão da imagem do operador é idêntica à versão da imagem do SQL Server.

## <a name="next-steps"></a>Próximas etapas

> [Contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)
