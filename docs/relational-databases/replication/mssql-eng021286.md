---
title: "MSSQL_ENG021286 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG021286"
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021286
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21286|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A tabela de conflitos '%s' não existe.|  
  
## Explicação  
 Esse erro é gerado se a tabela de conflitos para um artigo listado em [sysmergearticles & #40. O Transact-SQL e 41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) Na verdade, não existe. O erro pode ocorrer ao tentar adicionar uma coluna ou descartar uma coluna de uma tabela publicada para replicação de mesclagem.  
  
## Ação do usuário  
 Executar [DBCC CHECKDB & #40. O Transact-SQL e 41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados com a tabela de conflitos ausente para verificar se não há nenhum problema de consistência de dados.  
  
 Se a tabela de conflitos estiver ausente em um Assinante, descarte a assinatura e recrie-a. Se a tabela de conflitos estiver ausente em um Publicador, descarte todas as assinaturas, descarte a publicação e, depois, recrie a publicação e todas as assinaturas. Para obter mais informações, consulte [publica dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md) e [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  