---
title: O banco de dados secundário não está ingressado | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ca86d30647ea0dd2841248a512725aabb5617b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788421"
---
# <a name="secondary-database-is-not-joined"></a>O banco de dados secundário não está unido
    
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
  
## <a name="possible-causes"></a>Causas possíveis  
 Este banco de dados secundário não está unido ao grupo de disponibilidade. A configuração deste banco de dados secundário está incompleta.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o Transact-SQL, o PowerShell ou o SQL Server Management Studio para unir a réplica secundária ao grupo de disponibilidade. Para obter mais informações sobre como unir réplicas secundárias a grupos de disponibilidade, consulte [Unir uma réplica secundária a um grupo de disponibilidade (SQL Server)](https://msdn.microsoft.com/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
