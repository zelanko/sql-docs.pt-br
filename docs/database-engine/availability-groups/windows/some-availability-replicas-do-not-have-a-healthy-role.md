---
title: Algumas réplicas de disponibilidade não têm uma função íntegra | Microsoft Docs
description: O Estado de Conexão das Réplicas de Disponibilidade verifica se há alguma réplica de disponibilidade que não está em estado íntegro.
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
author: cawrites
ms.author: chadam
ms.openlocfilehash: 514de23cf905f7344f76a3597658f8a9d40d1013
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583851"
---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>Algumas réplicas de disponibilidade não têm uma função íntegra
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da Função das Réplica de Disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade não têm uma função íntegra.|  
|**Categoria**|**Aviso**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Essa política acumula o estado de conexão de todas as réplicas de disponibilidade no grupo de disponibilidade e verifica se há alguma réplica de disponibilidade que não está em estado íntegro. A política fica em um estado não íntegro quando alguma réplica de disponibilidade não é primária nem secundária. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade não têm uma função íntegra](https://go.microsoft.com/fwlink/p/?LinkId=220854) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Nesse grupo de disponibilidade, pelo menos uma réplica de disponibilidade não tem a função primária ou secundária atualmente.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade cuja função não é primária ou secundária e depois resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
