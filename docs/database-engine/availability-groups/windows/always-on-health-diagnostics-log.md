---
title: Log de diagnóstico de integridade de Grupos de Disponibilidade Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
caps.latest.revision: 5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 743a80feaa322624ec9fb04111a3b57230d8bbe6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="always-on-availability-groups-health-diagnostics-log"></a>Log de diagnóstico de integridade de Grupos de Disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para monitorar a integridade da réplica de disponibilidade primária, a DLL de recurso do SQL Server executada pelo WSFC (Cluster de Failover do Windows Server) usa um procedimento armazenado na instância do SQL Server chamada [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).  
  
 A DLL de recurso do SQL Server mantém uma conexão aberta dedicada com a instância do SQL Server, por meio da qual a instância do SQL Server envia periodicamente um diagnóstico de integridade detalhado para a DLL de recurso do SQL Server. O diagnóstico de integridade, juntamente com a política de failover configurada no recurso do grupo de disponibilidade no cluster (a propriedade FailoverConditionLevel), é usado pelo cluster para determinar a necessidade de reinicializar ou de fazer failover do recurso do grupo de disponibilidade. Esse procedimento armazenado é "pulsação" da instância do SQL Server 2012 e posterior para o cluster WSFC, a qual é mais granular e confiável que no SQL Server 2008 R2 ou inferior, em que uma conexão periódica com a instância é feita com a consulta `SELECT @@SERVERNAME`. Assim, você pode controlar as condições que disparam failovers, definindo a propriedade FailureConditonLevel do grupo de disponibilidade.  
  
 **Usar os logs de diagnóstico do cluster de failover do SQL Server**
 
 Todos os diagnósticos de integridade que as DLLs de recurso do SQL Server recebem de sp_server_diagnostics são salvas automaticamente no diretório de Log padrão da instância do SQL Server (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Log). Esses logs são conhecidos como logs SQLDIAG e são salvos no formato de arquivo XEL (eventos estendidos). Esses arquivos do diretório de log do SQL Server têm o seguinte formato: \<HOSTNAME>_\<INSTANCENAME>_SQLDIAG_X_XXXXXXXXX.xel. Ao examinar os logs SQLDIAG, você poderá determinar a causa raiz dos eventos de falha ou failover de recurso do grupo de disponibilidade.  
  
 Para exibir um log SQLDIAG, arraste o arquivo .xel até o SQL Server Management Studio.  
  
  