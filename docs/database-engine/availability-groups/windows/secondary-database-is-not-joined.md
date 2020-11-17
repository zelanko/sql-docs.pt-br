---
title: O banco de dados secundário não está ingressado | Microsoft Docs
description: O Estado de Junção no Banco de Dados de Disponibilidade verifica o estado de junção do banco de dados secundário como parte do gerenciamento baseado em políticas para grupos de disponibilidade Always On.
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1c66fa7c407469ec8f52b11c8393bf7e03ddc734
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583932"
---
# <a name="secondary-database-is-not-joined"></a>O banco de dados secundário não está unido
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de junção do banco de dados de disponibilidade|  
|**Problema**|O banco de dados secundário não está unido.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado de junção do banco de dados secundário (também conhecido como "réplica de banco de dados secundário"). A política ficará em estado não íntegro quando a réplica do conjunto de dados não estiver unida. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [Secondary database is not joined](https://go.microsoft.com/fwlink/p/?LinkId=220862) (O banco de dados secundário não está unido) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Este banco de dados secundário não está unido ao grupo de disponibilidade. A configuração deste banco de dados secundário está incompleta.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o Transact-SQL, o PowerShell ou o SQL Server Management Studio para unir a réplica secundária ao grupo de disponibilidade. Para obter mais informações sobre como unir réplicas secundárias a grupos de disponibilidade, consulte [Unir uma réplica secundária a um grupo de disponibilidade (SQL Server)](https://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
