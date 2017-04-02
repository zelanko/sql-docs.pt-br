---
title: "Executar uma atualiza&#231;&#227;o fict&#237;cia para um artigo de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "sp_mergedummyupdate"
  - "atualizações fictícias [replicação SQL Server]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Executar uma atualiza&#231;&#227;o fict&#237;cia para um artigo de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  As replicações de mesclagem usam gatilhos como parte do processo de replicação. Quando uma atualização é executada em uma tabela publicada, um gatilho de atualização é acionado. Em alguns casos, os dados podem ser atualizados sem que o gatilho seja acionado, como durante as operações WRITETEXT e UPDATETEXT. Nesses casos, você precisa adicionar uma instrução UPDATE fictícia explicitamente para replicar a alteração. Você pode adicionar uma instrução UPDATE fictícia que usa procedimentos armazenados de replicação.  
  
### Para adicionar uma instrução UPDATE fictícia  
  
1.  Execute a operação (por exemplo, UPDATETEXT) em uma linha em uma tabela de mesclagem publicada que exija uma atualização fictícia.  
  
2.  No servidor (Editor ou assinante) no banco de dados onde a alteração foi feita, execute [sp_mergedummyupdate & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Especifique a tabela na qual a alteração foi feita para **@source_object**, e o identificador exclusivo da linha alterada para **@rowguid**.  
  
3.  Sincronize a assinatura para replicar a linha alterada.  
  
  