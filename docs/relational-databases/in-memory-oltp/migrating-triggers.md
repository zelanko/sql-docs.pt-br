---
title: Migrando gatilhos | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2f151fa00c2e92ef1509ea2c6d7d93e8c8d2c69
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="migrating-triggers"></a>Migrando gatilhos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este tópico discute gatilhos DDL e tabelas com otimização de memória.  
  
 Gatilhos DML têm suporte em tabelas com otimização de memória, mas apenas com o evento de gatilho FOR | AFTER. Para obter um exemplo, veja [Implementando UPDATE com FROM ou Subconsultas](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md). 
  
 Os gatilhos LOGON são gatilhos definidos para serem disparados em eventos LOGON. Os gatilhos LOGON não afetam tabelas com otimização de memória.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Os gatilhos DDL são gatilhos definidos para disparar quando uma instrução CREATE, ALTER, DROP, GRANT, DENY, REVOKE ou UPDATE STATISTICS é executada no banco de dados ou no servidor no qual está definida.  
  
 Você não pode criar tabelas com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em CREATE_TABLE ou em qualquer grupo de eventos que o inclua. Você não pode descartar uma tabela com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em DROP_TABLE ou em qualquer grupo de eventos que o inclua.  
  
 Você não pode criar procedimentos armazenados compilados de modo nativo quando há um ou mais gatilhos DDL em CREATE_PROCEDURE, em DROP_PROCEDURE ou em qualquer grupo de eventos que inclua esses eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
