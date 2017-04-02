---
title: "Controlar o comportamento de gatilhos e restri&#231;&#245;es durante sincroniza&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "identidades [replicação do SQL Server]"
  - "restrições [SQL Server], replicação"
  - "gatilhos [SQL Server], replicação"
  - "gatilhos [replicação do SQL Server]"
  - "restrições [replicação do SQL Server]"
  - "opção NOT FOR REPLICATION "
  - "opção NFR"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Controlar o comportamento de gatilhos e restri&#231;&#245;es durante sincroniza&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Durante a sincronização, os agentes de replicação executam [Inserir & #40. O Transact-SQL e 41;](../../t-sql/statements/insert-transact-sql.md), [a & TUALIZAR 40; O Transact-SQL e 41;](../../t-sql/queries/update-transact-sql.md), e [Excluir & #40. O Transact-SQL e 41;](../../t-sql/statements/delete-transact-sql.md) instruções em tabelas replicadas, o que podem causar a manipulação de dados gatilhos DML (linguagem) nessas tabelas a ser executado. Há casos em que é possível que você precise impedir o acionamento desses gatilhos ou a imposição de restrições durante a sincronização. Esse comportamento depende de como o gatilho ou a restrição foram criados.  
  
### Para evitar a execução de gatilhos durante a sincronização  
  
1.  Ao criar um novo disparador, especifique a opção NOT FOR REPLICATION de [CREATE TRIGGER & #40. O Transact-SQL e 41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
2.  Para um gatilho existente, especifique a opção NOT FOR REPLICATION de [ALTER TRIGGER & #40. O Transact-SQL e 41;](../../t-sql/statements/alter-trigger-transact-sql.md).  
  
### Para impedir a imposição de restrições durante a sincronização  
  
1.  Ao criar uma nova restrição CHECK ou FOREIGN KEY, especifique a opção de verificação NOT FOR REPLICATION na definição da restrição de [CREATE TABLE & #40. O Transact-SQL e 41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## Consulte também  
 [Criar tabelas & 40; o mecanismo de banco de dados & 41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  