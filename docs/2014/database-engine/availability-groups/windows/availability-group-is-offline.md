---
title: O grupo de disponibilidade está offline | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35d8f9cdda7c3b85c77d290f9c793640705438e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62815419"
---
# <a name="availability-group-is-offline"></a>O grupo de disponibilidade está offline
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado Online do Grupo de Disponibilidade|  
|**Problema**|O grupo de disponibilidade está offline.|  
|**Categoria**|**Crítico**|  
|**Faceta**|grupo de disponibilidade|  
  
## <a name="description"></a>DESCRIÇÃO  
 Esta política verifica o estado online ou offline do grupo de disponibilidade. A política estará em estado não íntegro e um alerta será emitido quando o recurso de cluster do grupo de disponibilidade estiver offline ou o grupo de disponibilidade não tiver uma réplica primária.  
  
 O estado da política será íntegro quando o recurso de cluster do grupo de disponibilidade estiver online e o grupo de disponibilidade tiver uma réplica primária.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [O grupo de disponibilidade está offline](https://go.microsoft.com/fwlink/p/?LinkId=220850) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Possíveis causas  
 Esse problema pode ser causado por uma falha na instância de servidor que hospeda a réplica primária ou pelo recurso de grupo de disponibilidade WSFC (Windows Server Failover Cluster) que entra offline. Estas são as possíveis causas do grupo de disponibilidade estar offline:  
  
-   O grupo de disponibilidade não está configurado com o modo de failover automático. A réplica primária torna-se indisponível e a função de todas as réplicas do grupo de disponibilidade torna-se RESOLVING.  
  
    -   O serviço de instância de réplica primária está inativo ou não respondendo.  
  
    -   O grupo de disponibilidade tem um problema de conectividade com o cluster.  
  
-   O grupo de disponibilidade está configurado com o modo de failover automático e não é concluído com êxito.  
  
    -   Durante o failover automático, a verificação de prontidão primária na réplica de destino falha e não há réplica disponível para se tornar a nova primária.  
  
-   O recurso de grupo de disponibilidade no cluster fica offline.  
  
    -   Qualquer recurso de cluster dependente encontra um problema crítico e se torna offline. O recurso de grupo de disponibilidade também permanece offline até que o recurso dependente ficar online.  
  
    -   Um problema crítico no cluster desativa o recurso de grupo de disponibilidade.  
  
-   Há um failover automático, manual ou forçado em andamento para o grupo de disponibilidade.  
  
## <a name="possible-solutions"></a>Soluções possíveis  
 Estas são as possíveis soluções para este problema:  
  
-   Se a instância do SQL Server da réplica primária estiver inativa, reinicie o servidor e verifique se o grupo de disponibilidade recupera o estado íntegro.  
  
-   Se o failover automático parece ter falhado, verifique se os bancos de dados da réplica estão sincronizados com a réplica primária previamente conhecida, e execute o failover da réplica primária. Se os bancos de dados não estiverem sincronizados, selecione uma réplica com perda mínima de dados e recupere no modo de failover.  
  
-   Se o recurso no cluster estiver offline enquanto as instâncias do SQL Server parecerem íntegras, use o Gerenciador de Cluster de Failover para verificar a integridade do cluster ou outros problemas no cluster do servidor. Você também pode usar o Gerenciador de Cluster de Failover para tentar colocar o recurso de grupo de disponibilidade online.  
  
-   Se houver um failover em andamento, aguarde a conclusão do failover.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Use o painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
