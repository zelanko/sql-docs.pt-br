---
title: 'Espelhamento de Banco de Dados: interoperabilidade e coexistência (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60b393377747df8da93690d5820c2e46d4a7132c
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311805"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Espelhamento de banco de dados: interoperabilidade e coexistência (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O espelhamento de banco de dados pode ser usado com os seguintes recursos ou componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instâncias de cluster de failover AlwaysOn (Clustering de Failover do SQL Server)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change data capture (e controle de alterações)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Instantâneos do banco de dados](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [Catálogos de texto completo](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Envio de logs](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replicação](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 O espelhamento de banco de dados não interopera com o seguinte:  
  
-   Transações envolvendo todos os bancos de dados/transações distribuídas  
  
     Para obter informações sobre por que não há suporte para essas transações, veja [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
