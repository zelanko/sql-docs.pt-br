---
title: SQL Server, objeto Travas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d0d9249a5cfb801e07a85132060bb4d1781346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63251097"
---
# <a name="sql-server-latches-object"></a>SQL Server, objeto Latches
  O objeto **SqlServer: travas** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar bloqueios de recursos internos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamados de travas. Monitorar as travas para determinar a atividade de usuário e o uso de recursos pode ajudar a identificar gargalos de desempenho.  
  
 Esta tabela descreve os contadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** .  
  
|Contadores de travas do SQL Server|DESCRIÇÃO|  
|---------------------------------|-----------------|  
|**Tempo médio de espera de trava (MS)**|Tempo médio de espera de trava (em milissegundos) para solicitações de trava que tiveram de esperar.|  
|**Esperas de trava/s**|Número de solicitações de trava que não puderam ser concedidas imediatamente.|  
|**Número de supertravas**|Número de travas que atualmente são SuperLatches.|  
|**Rebaixamentos da supertrava/s**|Número de SuperLatches que foram rebaixados a travas regulares no último segundo.|  
|**Promoções de supertravamento/s**|Número de travas que foram promovidas a SuperLatches no último segundo.|  
|**Tempo de espera total de trava (MS)**|Tempo de espera total de trava (em milissegundos) para solicitações de trava no último segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
