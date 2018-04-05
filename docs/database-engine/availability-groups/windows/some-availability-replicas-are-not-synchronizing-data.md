---
title: Algumas réplicas de disponibilidade não estão sincronizando dados | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 69eff6b35cb5be4081c52ae4a8c29afd62ebb238
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>Algumas réplicas de disponibilidade não estão sincronizando dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização de Dados de Réplicas de Disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade não estão sincronizando dados.|  
|**Categoria**|**Aviso**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>Description  
 Essa política acumula o estado de sincronização de dados de todas as réplicas de disponibilidade no grupo de disponibilidade e verifica se a sincronização de alguma réplica de disponibilidade não está funcionando. A política ficará em estado não íntegro se algum estado de sincronização de dados da réplica de disponibilidade for NOT SYNCRONIZING.  
  
 Essa política ficará em estado íntegro se nenhum estado de sincronização de dados da réplica de disponibilidade for NOT SYNCHRONIZING.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade não estão sincronizando os dados](http://go.microsoft.com/fwlink/p/?LinkId=220852) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas possíveis  
 Nesse grupo de disponibilidade, pelo menos uma réplica secundária tem um estado de sincronização NOT SYNCHRONIZING e não está recebendo dados da réplica primária.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade em estado NOT SYNCHROINIZING e depois resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
