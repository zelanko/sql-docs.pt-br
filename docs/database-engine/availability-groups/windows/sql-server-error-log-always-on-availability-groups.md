---
title: Log de erros do SQL Server (grupos de disponibilidade)
description: Saiba mais sobre os eventos de log de erros do SQL Server que afetam um grupo de disponibilidade Always On e quais sintomas devem levar à revisão do log de erros.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: b33827f37d02edf783c4688c9ad08cd4673706e7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670879"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>Log de erros do SQL Server (Grupos de Disponibilidade Always On)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O log de erros do SQL Server relata eventos que afetam Grupos de Disponibilidade Always On, tais como:  
  
-   Comunicação com o cluster do WSFC (Cluster de Failover do Windows Server)    
-   Transições de estado de réplicas de disponibilidade    
-   Transições de estado de bancos de dados de disponibilidade    
-   Estado de conectividade de bancos de dados de disponibilidade entre réplicas primárias e secundárias    
-   Status dos pontos de extremidade de grupo de disponibilidade    
-   Status de ouvintes de grupo de disponibilidade    
-   Status da concessão entre a DLL de recurso do SQL Server (em execução no cluster WSFC) e a instância do SQL Server (para obter mais informações, veja [Como funciona tempo limite de concessão do Always On do SQL Server](/archive/blogs/psssql/how-it-works-sql-server-alwayson-lease-timeout))    
-   Eventos de erro no grupo de disponibilidade  

Os seguintes sintomas devem levar à revisão do log de erros do SQL Server:  

-   Não é possível acessar bancos de dados de disponibilidade    
-   Failover inesperado do grupo de disponibilidade    
-   Grupo de disponibilidade no estado Resolving inesperadamente    
-   Grupo de disponibilidade em um estado indeterminado  
  
Para obter mais informações, veja [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md).  
  
