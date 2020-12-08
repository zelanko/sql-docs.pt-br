---
title: SQL Server, objeto Travas | Microsoft Docs
description: Saiba mais sobre o objeto SQLServer:Latches, que fornece contadores para monitorar bloqueios de recursos internos do SQL Server, chamados travas.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 01d5eaa40f6e9deac5703b35b8859165218b40c3
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505666"
---
# <a name="sql-server-latches-object"></a>SQL Server, objeto Latches
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto **SQLServer:Latches** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece contadores para monitorar bloqueios de recursos internos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , chamados travas. Monitorar as travas para determinar a atividade de usuário e o uso de recursos pode ajudar a identificar gargalos de desempenho.  
  
 Esta tabela descreve os contadores **Travas** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de travas do SQL Server|Descrição|  
|---------------------------------|-----------------|  
|**Tempo Médio de Espera de Trava (ms)**|Tempo médio de espera de trava (em milissegundos) para solicitações de trava que tiveram de esperar.|  
|**Base de Tempo de Espera Médio de Trava**|Apenas para uso interno.| 
|**Esperas de Trava/s**|Número de solicitações de trava que não puderam ser concedidas imediatamente.|  
|**Número de SuperLatches**|Número de travas que atualmente são SuperLatches.|  
|**Rebaixamentos de SuperLatches/s**|Número de SuperLatches que foram rebaixados a travas regulares no último segundo.|  
|**Promoções para SuperLatch/s**|Número de travas que foram promovidas a SuperLatches no último segundo.|  
|**Tempo de Espera Total de Trava (ms)**|Tempo de espera total de trava (em milissegundos) para solicitações de trava no último segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
