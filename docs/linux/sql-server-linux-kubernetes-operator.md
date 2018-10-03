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
ms.openlocfilehash: f8667c74843ab26b251c5a23a1e93f7f26e72fef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759354"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On disponibilidade Kubernetes operador parâmetros do grupo

Um grupo de disponibilidade Always On no Kubernetes requer um operador. O operador é descrito em um arquivo. YAML.  Veja um exemplo da especificação em [este tutorial](tutorial-sql-server-ag-kubernetes.md).

Este artigo explica as variáveis de ambiente global do operador.

## <a name="example"></a>Exemplo

O exemplo a seguir descreve uma implantação para o `mssql-operator`.

## <a name="global-environment-variables"></a>Variáveis de ambiente globais

* `MSSQL_K8S_POD_NAMESPACE` 
  * Obrigatório
  * **Descrição**: o namespace de Kubernetes do operador.

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * Opcional
  * **Descrição**: A duração do sql server externo gravar concessão para manter o sql server gravável e evitar cenários de separação. Réplicas secundárias aguardar essa expiração após eleger um novo líder.

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * Opcional
  * **Descrição**: O período para monitorar se o estado do grupo de disponibilidade. Determina o quão rapidamente as réplicas são adicionadas e removidas. Deve ser menor que `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`.
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
  * **Descrição**: duração atuando [mestre](http://kubernetes.io/docs/concepts/architecture/master-node-communication/) aguardará antes de renovar a concessão de líder. Deve ser menor que `MSSQL_K8S_LEASE_DURATION_SECONDS`.
  * **Padrão**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * Opcional
  * **Descrição**: período de réplicas secundárias sondam se a concessão de líder expirou. 
  * **Padrão**: 1


  ## <a name="next-steps"></a>Próximas etapas

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
