---
title: O banco de dados de disponibilidade está suspenso | Microsoft Docs
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
- sql12.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 6ff9d79ede6794d1242a7ad743f1a29d279183ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019890"
---
# <a name="availability-database-is-suspended"></a>O banco de dados de disponibilidade está suspenso
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Suspensão do Banco de Dados de Disponibilidade|  
|**Problema**|O banco de dados de disponibilidade está suspenso.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Description  
 Esta política verifica o estado de movimento de dados do banco de dados secundário (também conhecido como "réplica de banco de dados secundário"). A política ficará em estado não íntegro quando a movimentação de dados for suspensa. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O banco de dados de disponibilidade está suspenso](http://go.microsoft.com/fwlink/p/?LinkId=220860) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 A sincronização de dados nesse banco de dados de disponibilidade pode ter sido suspensa pelo seguinte:  
  
-   Devido a um erro, o sistema pode ter suspendido a sincronização de dados.  
  
-   O administrador de banco de dados pode ter suspendido a sincronização de dados para fins de manutenção.  
  
## <a name="possible-solution"></a>Solução possível  
 Retome a sincronização de dados. Se o problema persistir, verifique o grupo de disponibilidade no log de eventos e diagnostique por que o sistema suspendeu a movimentação de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  