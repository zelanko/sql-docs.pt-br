---
title: Algumas réplicas de disponibilidade estão desconectadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ebc6b8e8d06418c289726fd3ff2a1e56830f464
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155936"
---
# <a name="some-availability-replicas-are-disconnected"></a>Algumas réplicas de disponibilidade são desconectadas
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da conexão em réplicas de disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade estão desconectadas.|  
|**Categoria**|**Aviso**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>Description  
 Essa política acumula o estado de conexão de todas as réplicas de disponibilidade e verifica se há alguma réplica DISCONNECTED. O estado da política é não íntegro quando qualquer réplica de disponibilidade é DISCONNECTED. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Nesta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade são desconectadas](http://go.microsoft.com/fwlink/p/?LinkId=220855) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 Nesse grupo de disponibilidade, pelo menos uma réplica secundária não está conectada à réplica primária. O estado de conexão é DISCONNECTED.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade que é DISCONNECTED; depois, resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
