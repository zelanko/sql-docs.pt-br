---
title: A réplica de disponibilidade não está ingressada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50a2dcbb776b9f8bc3a736e8e6f06f572f76b449
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194956"
---
# <a name="availability-replica-is-not-joined"></a>A réplica de disponibilidade não está unida
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da junção da réplica de disponibilidade|  
|**Problema**|A réplica de disponibilidade não está unida.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>Description  
 Esta política verifica o estado da junção da réplica de disponibilidade. A política estará em um estado não íntegro quando a réplica de disponibilidade for adicionada ao grupo de disponibilidade, mas não for unida corretamente. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [A réplica de disponibilidade não está unida](http://go.microsoft.com/fwlink/p/?LinkId=220859) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 A réplica secundária não está unida ao grupo de disponibilidade. Para que uma réplica de disponibilidade seja unida com êxito ao grupo de disponibilidade, o estado da junção deve ser Instância Autônoma Unida (1) ou Cluster de Failover Unido (2).  
  
## <a name="possible-solution"></a>Solução possível  
 Use o Transact-SQL, o PowerShell ou o SQL Server Management Studio para unir a réplica secundária ao grupo de disponibilidade. Para obter mais informações sobre como unir réplicas secundárias a grupos de disponibilidade, consulte [Unir uma réplica secundária a um grupo de disponibilidade (SQL Server)](http://msdn.microsoft.com/en-sg/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
