---
title: O grupo de disponibilidade não está pronto para o failover automático
description: Identifique os possíveis motivos de um Grupo de Disponibilidade AlwaysOn não estar pronto para failover.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 78f61b21ae2399a3aa5d0b5432a4047c3f4fd4b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991493"
---
# <a name="always-on-availability-group-is-not-ready-for-automatic-failover"></a>O Grupo de Disponibilidade AlwaysOn não está pronto para o failover automático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Prontidão para Failover Automático do Grupo de Disponibilidade|  
|**Problema**|O grupo de disponibilidade não está pronto para o failover automático.|  
|**Categoria**|**Crítico**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política verifica se o grupo de disponibilidade tem ao menos uma réplica secundária pronta para failover. A política estará em estado não íntegro e um alerta será emitido quando o modo de failover da réplica primária for automático, mas nenhuma das réplicas secundárias do grupo de disponibilidade está pronta para failover.  
  
 A política estará em estado íntegro quando pelo menos uma réplica secundária estiver pronta para failover automático.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [O grupo de disponibilidade não está pronto para failover automático](https://go.microsoft.com/fwlink/p/?LinkId=220851) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Causas possíveis  
 O grupo de disponibilidade não está pronto para o failover automático. A réplica primária está configurada para failover automático; porém, a réplica secundária não está pronta para failover automático. A réplica secundária que está configurada para failover automático pode estar indisponível ou seu estado de sincronização de dados não é atualmente SYNCHRONIZED.  
  
## <a name="possible-solutions"></a>Soluções possíveis  
 Estas são as possíveis soluções para este problema:  
  
-   Verifique se pelo menos uma réplica secundária está configurada como failover automático. Se não houver uma réplica secundária configurada como failover automático, atualize a configuração de uma réplica secundária para ser o destino de failover automático com confirmação síncrona.  
  
-   Use a política para verificar se os dados estão em estado de sincronização e se o destino de failover automático é SYNCHRONIZED, e depois resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
