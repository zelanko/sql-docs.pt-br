---
title: Controlar o comportamento de gatilhos e restrições durante sincronização (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26d9a2431b91c1dc081345a06e7fe5a7533cbaa2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782028"
---
# <a name="control-the-behavior-of-triggers-and-constraints-during-synchronization-replication-transact-sql-programming"></a>Controlar o comportamento de gatilhos e restrições durante sincronização (Programação Transact-SQL de replicação)
  Durante a sincronização, os agentes de replicação executam instruções [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) e [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) em tabelas replicadas, o que pode fazer com que os gatilhos de DML (linguagem de manipulação de dados) nessas tabelas sejam executados. Há casos em que é possível que você precise impedir o acionamento desses gatilhos ou a imposição de restrições durante a sincronização. Esse comportamento depende de como o gatilho ou a restrição foram criados.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>Para evitar a execução de gatilhos durante a sincronização  
  
1.  Ao criar um novo gatilho, especifique a opção NOT FOR REPLICATION de [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
2.  Para um gatilho existente, especifique a opção NOT FOR REPLICATION de [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql).  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>Para impedir a imposição de restrições durante a sincronização  
  
1.  Ao criar uma nova restrição CHECK ou FOREIGN KEY, especifique a opção de CHECK NOT FOR REPLICATION na definição da restrição de [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
## <a name="see-also"></a>Consulte também  
 [Criar tabelas &#40;Mecanismo de Banco de Dados&#41;](../tables/create-tables-database-engine.md)  
  
  
