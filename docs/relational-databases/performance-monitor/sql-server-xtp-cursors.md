---
title: Cursores XTP do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2442e178c91d459356330fe7342eb1319ccb270
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-xtp-cursors"></a>Cursores de XTP do SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho Cursores de XTP do SQL Server contém os contadores relacionados aos cursores do mecanismo de XTP interno OLTP in-memory. Os cursores são os blocos de construção de baixo nível que o mecanismo OLTP In-Memory usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.  
  
 Esta tabela descreve os contadores de **Cursores de XTP do SQL Server** .  
  
|Contador|Descrição|  
|-------------|-----------------|  
|**Exclusões de cursor/s**|O número de exclusões de cursor (em média), por segundo.|  
|**Inserções de Cursor/s**|O número de inserções de cursor (em média), por segundo.|  
|**Verificações de cursor iniciadas/s**|O número de verificações de cursor iniciadas (em média), por segundo.|  
|**Violações exclusivas de cursor/s**|O número de violações de restrição exclusiva (em média), por segundo.|  
|**Atualizações de cursor/s**|O número de atualizações de cursor (em média), por segundo.|  
|**Conflitos de gravação de cursor/s**|O número de conflitos de gravação/gravação para a mesma versão de linha (em média), por segundo.|  
|**Tentativas de verificação de canto sujo/s (emitido pelo usuário)**|O número de novas tentativas de verificação devido a conflitos de gravação durante as varreduras de canto sujo emitidas pela verificação de tabela inteira de um usuário (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Linhas expiradas removidas/s**|O número de linhas expiradas removidas por cursores (em média), por segundo.|  
|**Linhas expiradas tocadas/s**|O número de linhas expiradas tocadas por cursores (em média), por segundo.|  
|**Linhas retornadas/s**|O número de linhas retornadas por cursores (em média), por segundo.|  
|**Linhas tocadas/s**|O número de linhas tocadas por cursores (em média), por segundo.|  
|**Linhas excluídas por tentativa tocadas/s**|O número de linhas expirando tocadas por cursores (em média), por segundo. Uma linha está expirando quando a transação que a excluiu ainda está ativa (ou seja, ainda não foi confirmada nem anulada).|  
  
## <a name="see-also"></a>Consulte também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
