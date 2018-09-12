---
title: SQL Server, objeto Travas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e56ec72b03ca7b4ea4a93ce91a5fe1ac89e50bb2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820942"
---
# <a name="sql-server-latches-object"></a>SQL Server, objeto Latches
  O objeto **SQLServer:Latches** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece contadores para monitorar bloqueios de recursos internos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , chamados travas. Monitorar as travas para determinar a atividade de usuário e o uso de recursos pode ajudar a identificar gargalos de desempenho.  
  
 Esta tabela descreve os contadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** .  
  
|Contadores de travas do SQL Server|Description|  
|---------------------------------|-----------------|  
|**Tempo Médio de Espera de Trava (ms)**|Tempo médio de espera de trava (em milissegundos) para solicitações de trava que tiveram de esperar.|  
|**Esperas de Trava/s**|Número de solicitações de trava que não puderam ser concedidas imediatamente.|  
|**Número de SuperLatches**|Número de travas que atualmente são SuperLatches.|  
|**Rebaixamentos de SuperLatches/s**|Número de SuperLatches que foram rebaixados a travas regulares no último segundo.|  
|**Promoções para SuperLatch/s**|Número de travas que foram promovidas a SuperLatches no último segundo.|  
|**Tempo de Espera Total de Trava (ms)**|Tempo de espera total de trava (em milissegundos) para solicitações de trava no último segundo.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
