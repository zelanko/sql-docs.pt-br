---
title: Algumas réplicas de disponibilidade não têm uma função íntegra | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9dcb24572774bf3d2e1fc084c6157c1b1a817b86
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936435"
---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>Algumas réplicas de disponibilidade não têm uma função íntegra
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado da Função das Réplica de Disponibilidade|  
|**Problema**|Algumas réplicas de disponibilidade não têm uma função íntegra.|  
|**Categoria**|**Aviso**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>DESCRIÇÃO  
 Essa política acumula o estado de conexão de todas as réplicas de disponibilidade no grupo de disponibilidade e verifica se há alguma réplica de disponibilidade que não está em estado íntegro. A política fica em um estado não íntegro quando alguma réplica de disponibilidade não é primária nem secundária. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre as possíveis causas e soluções estão localizadas em [Algumas réplicas de disponibilidade não têm uma função íntegra](https://go.microsoft.com/fwlink/p/?LinkId=220854) no Wiki do TechNet.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Nesse grupo de disponibilidade, pelo menos uma réplica de disponibilidade não tem a função primária ou secundária atualmente.  
  
## <a name="possible-solution"></a>Solução possível  
 Use o estado da política de réplica de disponibilidade para localizar a réplica de disponibilidade cuja função não é primária ou secundária e depois resolva o problema na réplica de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
