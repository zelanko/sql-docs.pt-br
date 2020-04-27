---
title: Algumas réplicas síncronas não são sincronizadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2423a011e75d346d196ebe5ebac2597ac30914a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62788252"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Algumas réplicas síncronas não são sincronizadas
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de sincronização de dados de réplicas síncronas|  
|**Problema**|Algumas réplicas síncronas não são sincronizadas.|  
|**Categoria**|**Alerta**|  
|**Particular**|grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Essa política acumula o estado de sincronização de dados de todas as réplicas de disponibilidade e verifica se há réplicas de disponibilidade que não estão no estado de sincronização esperado. A política está em um estado não íntegro quando o estado de qualquer réplica assíncrona não é SYNCHRONIZING e o estado de qualquer réplica síncrona não é SYNCHRONIZED. Caso contrário, o estado da política é íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas síncronas não estão sincronizadas](https://go.microsoft.com/fwlink/p/?LinkId=220853) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Neste grupo de disponibilidade, pelo menos uma réplica síncrona não está sincronizada no momento. O estado de sincronização de réplica pode ser SYNCHONIZING ou NOT SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade com o estado de sincronização incorreto e, depois, resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
