---
title: O banco de dados secundário não está ingressado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: c5b4c1de21187d552cd351c916a9f0341a38d2b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118178"
---
# <a name="secondary-database-is-not-joined"></a>O banco de dados secundário não está unido
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de junção do banco de dados de disponibilidade|  
|**Problema**|O banco de dados secundário não está unido.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Description  
 Esta política verifica o estado de junção do banco de dados secundário (também conhecido como "réplica de banco de dados secundário"). A política ficará em estado não íntegro quando a réplica do conjunto de dados não estiver unida. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [Secondary database is not joined](http://go.microsoft.com/fwlink/p/?LinkId=220862) (O banco de dados secundário não está unido) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas possíveis  
 Este banco de dados secundário não está unido ao grupo de disponibilidade. A configuração deste banco de dados secundário está incompleta.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o Transact-SQL, o PowerShell ou o SQL Server Management Studio para unir a réplica secundária ao grupo de disponibilidade. Para obter mais informações sobre como unir réplicas secundárias a grupos de disponibilidade, consulte [Unir uma réplica secundária a um grupo de disponibilidade (SQL Server)](http://msdn.microsoft.com/en-sg/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  