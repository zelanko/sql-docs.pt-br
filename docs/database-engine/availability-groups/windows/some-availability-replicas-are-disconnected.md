---
title: "Algumas réplicas de disponibilidade estão desconectadas | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords: Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1dae927419403deb993127620c3ff7a012241b7b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="some-availability-replicas-are-disconnected"></a>Algumas réplicas de disponibilidade são desconectadas
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da conexão em réplicas de disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade estão desconectadas.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Essa política acumula o estado de conexão de todas as réplicas de disponibilidade e verifica se há alguma réplica DISCONNECTED. O estado da política é não íntegro quando qualquer réplica de disponibilidade é DISCONNECTED. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Nesta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade são desconectadas](http://go.microsoft.com/fwlink/p/?LinkId=220855) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 Nesse grupo de disponibilidade, pelo menos uma réplica secundária não está conectada à réplica primária. O estado de conexão é DISCONNECTED.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade que é DISCONNECTED; depois, resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
