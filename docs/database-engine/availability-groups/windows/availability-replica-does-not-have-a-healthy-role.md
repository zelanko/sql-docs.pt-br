---
title: A réplica de disponibilidade não tem uma função íntegra em um grupo de disponibilidade
description: Identifique as possíveis causas de uma réplica não ter uma função íntegra em um Grupo de Disponibilidade AlwaysOn.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d072fc8664163e5b2a0a175a90cb0c13fe3495e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204263"
---
# <a name="availability-replica-does-not-have-a-healthy-role-for-an-always-on-availability-group"></a>A réplica de disponibilidade não tem uma função íntegra em um Grupo de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da função da réplica de disponibilidade|  
|**Problema**|A réplica de disponibilidade não tem uma função íntegra.|  
|**Categoria**|**Crítico**|  
|**Faceta**|Réplica de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado da função da réplica de disponibilidade. O estado da política é não íntegro quando a função da réplica de disponibilidade não é primária nem secundária. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [A réplica de disponibilidade não tem uma função íntegra](https://go.microsoft.com/fwlink/p/?LinkId=220856) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 A função desta réplica de disponibilidade é não íntegra. A réplica não tem a função primária ou secundária.  
  
## <a name="possible-solution-informationstilltocome"></a>Solução possível: Information_still_to_come  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
