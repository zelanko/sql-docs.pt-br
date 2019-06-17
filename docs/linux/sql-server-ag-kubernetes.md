---
title: Grupos de disponibilidade Always On para contêineres que executam o Linux
titleSuffix: SQL Server
description: Este artigo apresenta os grupos de disponibilidade nos contêineres do SQL Server
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb9775ad0fce022fb2bd5f8fda02f7e198d1c6fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713589"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Grupos de disponibilidade Always On para contêineres do SQL Server

2019 do SQL Server dá suporte a grupos de disponibilidade em contêineres em um cluster Kubernetes. Para grupos de disponibilidade, implante o SQL Server [Kubernetes operador](https://coreos.com/blog/introducing-operators.html) ao cluster Kubernetes. O operador ajuda o pacote, implantar e gerenciar o grupo de disponibilidade em um cluster.

![AG no contêiner do Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

Na imagem acima, um cluster de quatro nós kubernetes hospedar um grupo de disponibilidade com três réplicas. A solução inclui os seguintes componentes:

* Um Kubernetes [ *implantação*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/). A implantação inclui o operador e um mapa de configuração. Eles fornecem a imagem de contêiner, software e as instruções necessárias para implantar as instâncias do SQL Server para o grupo de disponibilidade.

* Três nós, cada uma hospedando um [ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). O StatefulSet contém um [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Cada pod contém:
  * Um contêiner do SQL Server executando uma instância do SQL Server.
  * Um agente do grupo de disponibilidade. 

* Duas [ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionadas ao grupo de disponibilidade. Os ConfigMaps fornecem informações sobre:
  * A implantação para o operador.
  * O grupo de disponibilidade.

 * [*Volumes persistentes* ](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) são partes de armazenamento. Um *declaração de volume persistente* (PVC) é uma solicitação de armazenamento por um usuário. Cada contêiner é afiliado a um PVC para o armazenamento de dados e de log. No serviço de Kubernetes do Azure (AKS), você [criar uma declaração de volume persistente](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) para provisionar automaticamente o armazenamento com base em uma classe de armazenamento.


Além disso, o cluster armazena [ *segredos* ](https://kubernetes.io/docs/concepts/configuration/secret/) para as senhas, certificados, chaves e outras informações confidenciais.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Implantar o grupo de disponibilidade no Kubernetes

Para implantar um grupo de disponibilidade no Kubernetes:

1. Criar o cluster Kubernetes

   Para um grupo de disponibilidade, crie pelo menos três nós para SQL Server além de um nó para o mestre.

1. Implantar o operador

1. Configurar o armazenamento

1. Implantar o StatefulSet

   O operador de escuta para obter instruções para implantar o StatefulSet. Automaticamente cria as instâncias do SQL Server em três nós separados e configura o grupo de disponibilidade com um Gerenciador de cluster externo.

1. Criar os bancos de dados e anexá-los ao grupo de disponibilidade

Para obter etapas detalhadas, consulte [grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operador de Kubernetes do SQL Server

Depois de implantar o operador, ele registra um recurso personalizado do SQL Server. Use o operador para implantar esse recurso.  Cada recurso corresponde a uma instância do SQL Server e inclui as propriedades específicas, como `sapassword` e `monitoring policy`. O operador analisa os recursos e implanta um Kubernetes StatefulSet.

O StatfulSet contém:

* contêiner MSSQL-server

* contêiner de MSSQL-ha-supervisor

O código para o operador, o supervisor de alta disponibilidade e o SQL Server é empacotado em uma imagem do Docker chamada `mcr.microsoft.com/mssql/ha`. Esta imagem contém os binários a seguir:

* `mssql-operator`

    Esse processo é implantado como uma implantação de Kubernetes separada. Ele registra o [recurso personalizado de Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) chamado `SqlServer` (sqlservers.mssql.microsoft.com). Em seguida, ele escuta para esses recursos que está sendo criado ou atualizado no cluster Kubernetes. Para cada caso, ele cria ou atualiza os recursos de Kubernetes para a instância correspondente (por exemplo o StatefulSet ou `mssql-server-k8s-init-sql` trabalho).

* `mssql-server-k8s-health-agent`

    Esse servidor web serve Kubernetes [testes de execução](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) para determinar a integridade de uma instância do SQL Server. Monitora a integridade da instância do SQL Server local por meio da chamada `sp_server_diagnostics` e comparar os resultados com a diretiva de monitor.

* `mssql-ha-supervisor`

   Mantém o certificado do grupo de disponibilidade e o ponto de extremidade. 

* `mssql-server-k8s-ag-agent`
  
    Esse processo monitora a integridade de uma réplica de AG em uma única instância do SQL Server e executa failovers.

    Ele também mantém a eleição de líder.

* `mssql-server-k8s-init-sql`
  
    Este Kubernetes [trabalho](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) aplica uma configuração de estado desejado para uma instância do SQL Server. O trabalho é criado pelo operador sempre que um recurso do SQL Server é criado ou atualizado. Isso garante que a instância do SQL Server de destino correspondente ao recurso personalizado tem a configuração desejada, descrita no recurso.

    Por exemplo, se qualquer uma das configurações a seguir são necessárias, ele conclui-las:
  * Atualizar a senha SA
  * Cria o logon do SQL para os agentes
  * Cria o ponto de extremidade DBM

* `mssql-server-k8s-rotate-creds`
  
    Esse trabalho Kubernetes implementa a tarefa de rotação de credenciais. Crie esse trabalho para solicitar atualizações para a senha SA, senha de logon do SQL agent, cert DBM etc. A senha SA é especificada como os parâmetros do trabalho. Os outros são gerados automaticamente.

* `mssql-server-k8s-failover`

   Um trabalho do Kubernetes que implementa o fluxo de trabalho de failover manual.

### <a name="notes"></a>Observações

Independentemente da configuração de AG, o operador sempre implantará o supervisor de alta disponibilidade. Se o recurso SqlServer não listar qualquer grupo de disponibilidade, o operador ainda implantará esse contêiner.

A versão da imagem do operador é idêntica à versão da imagem do SQL Server.

## <a name="next-steps"></a>Próximas etapas

> [Contêiner do SQL Server no Kubernetes](tutorial-sql-server-containers-kubernetes.md)
