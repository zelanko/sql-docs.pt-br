---
title: O banco de dados de disponibilidade está suspenso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21d788db62fe39b86eb801c028450c16cf845845
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815761"
---
# <a name="availability-database-is-suspended"></a>O banco de dados de disponibilidade está suspenso
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Suspensão do Banco de Dados de Disponibilidade|  
|**Problema**|O banco de dados de disponibilidade está suspenso.|  
|**Categoria**|**Alerta**|  
|**Particular**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica o estado de movimento de dados do banco de dados secundário (também conhecido como "réplica de banco de dados secundário"). A política ficará em estado não íntegro quando a movimentação de dados for suspensa. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>   Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [Banco de dados de disponibilidade é suspenso](https://go.microsoft.com/fwlink/p/?LinkId=220860) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 A sincronização de dados nesse banco de dados de disponibilidade pode ter sido suspensa pelo seguinte:  
  
-   Devido a um erro, o sistema pode ter suspendido a sincronização de dados.  
  
-   O administrador de banco de dados pode ter suspendido a sincronização de dados para fins de manutenção.  
  
## <a name="possible-solution"></a>Solução possível  
 Retome a sincronização de dados. Se o problema persistir, verifique o grupo de disponibilidade no log de eventos e diagnostique por que o sistema suspendeu a movimentação de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
