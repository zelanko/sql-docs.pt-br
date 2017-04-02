---
title: "Carregar dados em massa em tabelas em uma publica&#231;&#227;o de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
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
  - "carregamento em massa [replicação do SQL Server]"
  - "carregamento em massa da replicação de mesclagem [replicação do SQL Server]"
  - "sp_addtabletocontents"
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Carregar dados em massa em tabelas em uma publica&#231;&#227;o de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Quando os dados são carregados em tabelas usando o [utilitário bcp](../../tools/bcp-utility.md) ou o [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) comando, por padrão, os gatilhos de replicação de mesclagem que mantêm dados de rastreamento no [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabela do sistema não são disparados. Você pode forçar os gatilhos de replicação de mesclagem para serem acionados enquanto os dados forem carregados ou, você pode inserir os metadados de replicação gerados programaticamente após a operação de cópia em massa usando os procedimentos armazenados de replicação.  
  
### Para carregar dados em massa em tabelas publicadas por replicação de mesclagem usando o utilitário bcp  
  
1.  No Publicador ou no Assinante, execute [bcp Utility](../../tools/bcp-utility.md) ou [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) para inserir dados em uma tabela publicada usando a replicação de mesclagem.  
  
2.  Use um dos métodos abaixo para assegurar que são gerados os metadados de replicação para os dados inseridos.  
  
    -   Execute a cópia em massa usando a opção FIRE_TRIGGERS.  
  
    -   No banco de dados no qual os dados foram inseridos, execute [sp_addtabletocontents & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md). Especifique o nome da tabela na qual os dados foram inseridos para **@table_name**.  
  
  