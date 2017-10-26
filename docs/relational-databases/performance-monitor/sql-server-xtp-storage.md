---
title: Armazenamento XTP do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca13381f6cc2d2b9af6286f28d25791522118a72
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-storage"></a>Armazenamento XTP do SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

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
  
  

