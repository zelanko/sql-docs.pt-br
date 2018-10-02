---
title: Processador Fantasma de XTP do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e4ce18946f7ec5346ea67c3599736f493949fbd1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806654"
---
# <a name="sql-server-xtp-phantom-processor"></a>Processador Fantasma de XTP do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho Processador Fantasma de XTP do SQL Server contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo OLTP in-memory. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE, bem como na validação de restrição em cenários de simultaneidade.  
  
 Esta tabela descreve os contadores do **Processador Fantasma de XTP do SQL Server** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Tentativas de verificação de canto sujo/s (emitido pelo fantasma)**|O número de tentativas de digitalização devido a conflitos de gravação durante as varreduras de canto sujo emitidas pelo processador fantasma (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Linhas fantasma expiradas removidas/s**|O número de linhas expiradas removidas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma expiradas tocadas/s**|O número de linhas expiradas tocadas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma expirando tocadas/s**|O número de linhas expirando tocadas por verificações fantasma (em média), por segundo.|  
|**Linhas fantasma tocadas/s**|O número de linhas tocadas por verificações fantasma (em média), por segundo.|  
|**Verificações fantasma iniciadas/s**|O número de verificações fantasma iniciadas (em média), por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
