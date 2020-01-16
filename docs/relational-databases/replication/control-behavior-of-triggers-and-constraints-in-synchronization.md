---
title: Controlar o comportamento de gatilhos e restrições na sincronização
description: Saiba como impedir a execução de gatilhos ou a imposição de restrições durante a sincronização de uma replicação de publicação do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 816bda09c547345f5d05cd511d51c72135f15029
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321794"
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>Controlar o comportamento de gatilhos e restrições na sincronização
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Durante a sincronização, os agentes de replicação executam instruções [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) e [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) em tabelas replicadas, o que pode fazer com que os gatilhos de DML (linguagem de manipulação de dados) nessas tabelas sejam executados. Há casos em que é possível que você precise impedir o acionamento desses gatilhos ou a imposição de restrições durante a sincronização. Esse comportamento depende de como o gatilho ou a restrição foram criados.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>Para evitar a execução de gatilhos durante a sincronização  
  
1.  Ao criar um novo gatilho, especifique a opção NOT FOR REPLICATION de [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
2.  Para um gatilho existente, especifique a opção NOT FOR REPLICATION de [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md).  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>Para impedir a imposição de restrições durante a sincronização  
  
1.  Ao criar uma nova restrição CHECK ou FOREIGN KEY, especifique a opção de CHECK NOT FOR REPLICATION na definição da restrição de [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
