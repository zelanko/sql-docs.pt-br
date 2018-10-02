---
title: A réplica de disponibilidade não está ingressada | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70ff0d229e6e49e401c25a343912b6db9a6da70b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803074"
---
# <a name="availability-replica-is-not-joined"></a>A réplica de disponibilidade não está unida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da junção da réplica de disponibilidade|  
|**Problema**|A réplica de disponibilidade não está unida.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado da junção da réplica de disponibilidade. A política estará em um estado não íntegro quando a réplica de disponibilidade for adicionada ao grupo de disponibilidade, mas não for unida corretamente. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [A réplica de disponibilidade não está unida](http://go.microsoft.com/fwlink/p/?LinkId=220859) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 A réplica secundária não está unida ao grupo de disponibilidade. Para que uma réplica de disponibilidade seja unida com êxito ao grupo de disponibilidade, o estado da junção deve ser Instância Autônoma Unida (1) ou Cluster de Failover Unido (2).  
  
## <a name="possible-solution"></a>Solução possível  
 Use o Transact-SQL, o PowerShell ou o SQL Server Management Studio para unir a réplica secundária ao grupo de disponibilidade. Para obter mais informações sobre como unir réplicas secundárias a grupos de disponibilidade, consulte [Unir uma réplica secundária a um grupo de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
