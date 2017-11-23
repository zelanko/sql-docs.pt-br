---
title: Armazenamento XTP do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9cb620530972d0b8f1999f70d2a5a3996794cd8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-storage"></a>Armazenamento XTP do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho do Armazenamento XTP do SQL Server contém contadores relacionados ao armazenamento em disco para OLTP in-memory do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores do **Armazenamento XTP do SQL Server** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Pontos de verificação fechados**|Contagem de pontos de verificação fechados feita pelo agente online.|  
|**Pontos de verificação concluídos**|Contagem de pontos de verificação processados pelo thread de ponto de verificação offline.|  
|**Mesclagens de núcleo concluídas**|O número de mesclagens de núcleo concluídas pelo thread de trabalho de mesclagem. Essas mesclagens ainda precisam ser instaladas.|  
|**Avaliações de política de mesclagem**|O número de avaliações de política de mesclagem desde que o servidor foi iniciado.|  
|**Solicitações de mesclagem pendentes**|O número de solicitações de mesclagem pendentes desde que o servidor foi iniciado.|  
|**Mesclagens abandonadas**|O número de mesclagens abandonadas devido à falha.|  
|**Mesclagens instaladas**|O número de mesclagens instaladas com êxito.|  
|**Total de arquivos mesclados**|O número total de arquivos de origem mesclados. Esta contagem pode ser usada para localizar o número médio de arquivos de origem na mesclagem.|  
  
## <a name="see-also"></a>Consulte também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
