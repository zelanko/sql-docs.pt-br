---
title: 'Espelhamento de Banco de Dados: interoperabilidade e coexistência (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba2e5af89a4a9eabb420e0d75a8a90b4ef48540
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120411"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Espelhamento de banco de dados: interoperabilidade e coexistência (SQL Server)
  O espelhamento de banco de dados pode ser usado com os seguintes recursos ou componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instâncias de Cluster de Failover do AlwaysOn (SQL Server Failover Clustering)](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change data capture (e controle de alterações)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Instantâneos do banco de dados](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [Catálogos de texto completo](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Envio de logs](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replicação](database-mirroring-and-replication-sql-server.md)  
  
 O espelhamento de banco de dados não interopera com o seguinte:  
  
-   Transações envolvendo todos os bancos de dados/transações distribuídas  
  
     Para obter informações sobre por que não há suporte para essas transações, consulte [Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  