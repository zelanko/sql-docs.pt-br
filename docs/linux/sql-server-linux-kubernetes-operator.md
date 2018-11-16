---
title: SQL Server Always On grupo Kubernetes operador globais requisitos de disponibilidade
description: Este artigo explica os parâmetros para os Kubernetes Always On do SQL Server grupo operador globais requisitos de disponibilidade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd3cf1cd36866010843347d5c7a05a8cd39c20ef
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660591"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On disponibilidade Kubernetes operador parâmetros do grupo

Um grupo de disponibilidade Always On no Kubernetes requer um operador. Um manifesto descreve o operador. O manifesto é um `.yaml` arquivo. Veja um exemplo da especificação em [grupos de disponibilidade Always On para contêineres do SQL Server](sql-server-ag-kubernetes.md).

Este artigo explica as variáveis de ambiente global do operador.

## <a name="example"></a>Exemplo

O exemplo a seguir descreve uma implantação para o `mssql-operator`.

## <a name="global-environment-variables"></a>Variáveis de ambiente globais

* `MSSQL_K8S_POD_NAMESPACE` 
  * Obrigatório
  * **Descrição**: Kubernetes o namespace do operador.

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * Opcional
  * **Descrição**: A duração da concessão de gravação do servidor sql. Usado para manter o sql server gravável e evitar cenários de separação. Réplicas secundárias Aguarde esse número de segundos depois de selecionar um novo líder.

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * Opcional
  * **Descrição**: O período para monitorar o estado do grupo de disponibilidade. Determina o quão rapidamente as réplicas são adicionadas e removidas. Deve ser menor que `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`.
  * **Padrão**: 1

* `MSSQL_K8S_LEASE_DURATION_SECONDS`
  * Opcional
  * **Descrição**: duração da concessão de líder do grupo de disponibilidade. Determina quanto tempo as réplicas secundárias aguardar antes de eleger novamente se a réplica primária travado. Isso é diferente de concessão de gravação do SQL Server. 
  * **Padrão**: 10
  
  >[!NOTE]
  >Outras configurações calculados automaticamente com base em `MSSQL_K8S_LEASE_DURATION_SECONDS`.

* `MSSQL_K8S_RENEW_DEADLINE_SECONDS`
  * Opcional
  * **Descrição**: duração que a réplica primária de agir repete a liderança de atualização antes de desistir. Deve ser menor que `MSSQL_K8S_LEASE_DURATION_SECONDS`.
  * **Padrão**:  `MSSQL_K8S_LEASE_DURATION_SECONDS` /2

* `MSSQL_K8S_RETRY_PERIOD_SECONDS`
  * Opcional
  * **Descrição**: duração atuando [mestre](https://kubernetes.io/docs/concepts/architecture/master-node-communication/) aguardará antes de renovar a concessão de líder. Deve ser menor que `MSSQL_K8S_LEASE_DURATION_SECONDS`.
  * **Padrão**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * Opcional
  * **Descrição**: período de réplicas secundárias sondam se a concessão de líder expirou. 
  * **Padrão**: 1


  ## <a name="next-steps"></a>Próximas etapas

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
