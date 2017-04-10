---
title: "Habilitar backups coordenados para a replica&#231;&#227;o transacional (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
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
  - "replicação transacional, backup e restauração"
  - "sp_replicationdboption"
  - "sync with backup [replicação do SQL Server]"
  - "backups coordenados [replicação do SQL Server]"
  - "backups [replicação do SQL Server], replicação transacional"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Habilitar backups coordenados para a replica&#231;&#227;o transacional (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Quando habilitar um banco de dados para a replicação transacional, é possível especificar que seja efetuado um backup de todas as transações antes que elas sejam entregues ao banco de dados de distribuição. Você pode habilitar também um backup coordenado no banco de dados de distribuição de modo que o log de transações, para o banco de dados de publicação, não fique truncado até que seja efetuado o backup das transações que foram propagadas ao Distribuidor. Para obter mais informações, consulte [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### Para habilitar backups coordenados para um banco de dados publicado com replicação transacional  
  
1.  No Editor, use o [DATABASEPROPERTYEX & #40. O Transact-SQL e 41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) função para retornar o **IsSyncWithBackup** propriedade do banco de dados de publicação. Se a função retornar **1**, coordenada backups já estão habilitados para o banco de dados publicado.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) o publicador do banco de dados de publicação. Especifique um valor de **sincronizar com backup** para **@optname**, e **true** para **@value**.  
  
    > [!NOTE]  
    >  Se você alterar o **sincronizar com backup** opção **false**, o ponto de truncamento de dados de publicação será atualizado após a execução do Log Reader Agent ou após um intervalo se o Log Reader Agent está em execução continuamente. O intervalo máximo é controlado pelo **– MessageInterval** parâmetro do agente (que tem um padrão de 30 segundos).  
  
### Para habilitar backups coordenados para um banco de dados de distribuição  
  
1.  No distribuidor, use o [DATABASEPROPERTYEX & #40. O Transact-SQL e 41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) função para retornar o **IsSyncWithBackup** propriedade do banco de dados de distribuição. Se a função retornar **1**, coordenada backups já estão habilitados para o banco de dados de distribuição.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) no distribuidor no banco de dados de distribuição. Especifique um valor de **sincronizar com backup** para **@optname** e **true** para **@value**.  
  
### Para desabilitar backups coordenados  
  
1.  No Editor do banco de dados de publicação ou no distribuidor no banco de dados de distribuição, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique um valor de **sincronizar com backup** para **@optname** e **false** para **@value**.  
  
  