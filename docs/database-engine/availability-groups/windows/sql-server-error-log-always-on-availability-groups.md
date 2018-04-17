---
title: Log de erros do SQL Server (Grupos de Disponibilidade Always On) (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
caps.latest.revision: 4
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 535e8612c3b569a7dfcd9bbe88572e0fdc8c1f29
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>Log de erros do SQL Server (Grupos de Disponibilidade Always On)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O log de erros do SQL Server relata eventos que afetam Grupos de Disponibilidade Always On, tais como:  
  
-   Comunicação com o cluster do WSFC (Cluster de Failover do Windows Server)  
  
-   Transições de estado de réplicas de disponibilidade  
  
-   Transições de estado de bancos de dados de disponibilidade  
  
-   Estado de conectividade de bancos de dados de disponibilidade entre réplicas primárias e secundárias  
  
-   Status dos pontos de extremidade de grupo de disponibilidade  
  
-   Status de ouvintes de grupo de disponibilidade  
  
-   Status da concessão entre a DLL de recurso do SQL Server (em execução no cluster WSFC) e a instância do SQL Server (para obter mais informações, veja [Como funciona o tempo limite de concessão do Always On do SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx))  
  
-   Eventos de erro no grupo de disponibilidade  


Os seguintes sintomas devem levar à revisão do log de erros do SQL Server:  

-   Não é possível acessar bancos de dados de disponibilidade  
  
-   Failover inesperado do grupo de disponibilidade  
  
-   Grupo de disponibilidade no estado Resolving inesperadamente  
  
-   Grupo de disponibilidade em um estado indeterminado  
  
Para obter mais informações, veja [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md).  
  
  