---
title: "Exibir comandos replicados e outras informa&#231;&#245;es no banco de dados de distribui&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
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
  - "sp_browsereplcmds"
  - "replicação transacional, monitoramento"
  - "banco de dados de distribuição [replicação do SQL Server], exibindo comandos replicados"
  - "exibindo comandos replicados"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir comandos replicados e outras informa&#231;&#245;es no banco de dados de distribui&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Ao usar replicação transacional, os comandos de transação são armazenados no banco de dados de distribuição ou até que o Agente de Distribuição os propague a todos os Assinantes ou até um Agente de Distribuição enviar as alterações ao Assinante. Esses comandos pendentes no banco de dados de distribuição podem ser exibidos programaticamente por meio de procedimentos armazenados de replicação. Para obter mais informações, consulte [procedimentos armazenados de replicação e 40; O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
### Para exibir os comandos replicados de todas as publicações transacionais no banco de dados de distribuição  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md).  
  
### Para exibir comandos replicados no banco de dados de distribuição de um artigo específico ou de um banco de dados publicado específico por meio de replicação transacional  
  
1.  (Opcional) No publicador do banco de dados de publicação, execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique **@publication** e **@article**. Observe o valor de **id de artigo** no conjunto de resultados.  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md). (Opcional) Especifique a ID do artigo da etapa 2 para **@article_id**. (Opcional) Especifique a ID do banco de dados de publicação para **@publisher_database_id**, que pode ser obtido o **database_id** coluna o [Sys. Databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
## Consulte também  
 [Programmatically Monitor Replication](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  