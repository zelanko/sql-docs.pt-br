---
title: SQL Server, objeto Travas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b840a05c741b91064f435663a9a423eb9b035283
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821074"
---
# <a name="sql-server-latches-object"></a>SQL Server, objeto Latches
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto **SQLServer:Latches** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece contadores para monitorar bloqueios de recursos internos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , chamados travas. Monitorar as travas para determinar a atividade de usuário e o uso de recursos pode ajudar a identificar gargalos de desempenho.  
  
 Esta tabela descreve os contadores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** .  
  
|Contadores de travas do SQL Server|Descrição|  
|---------------------------------|-----------------|  
|**Tempo Médio de Espera de Trava (ms)**|Tempo médio de espera de trava (em milissegundos) para solicitações de trava que tiveram de esperar.|  
|**Base de Tempo de Espera Médio de Trava**|Somente para uso interno.| 
|**Esperas de Trava/s**|Número de solicitações de trava que não puderam ser concedidas imediatamente.|  
|**Número de SuperLatches**|Número de travas que atualmente são SuperLatches.|  
|**Rebaixamentos de SuperLatches/s**|Número de SuperLatches que foram rebaixados a travas regulares no último segundo.|  
|**Promoções para SuperLatch/s**|Número de travas que foram promovidas a SuperLatches no último segundo.|  
|**Tempo de Espera Total de Trava (ms)**|Tempo de espera total de trava (em milissegundos) para solicitações de trava no último segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
