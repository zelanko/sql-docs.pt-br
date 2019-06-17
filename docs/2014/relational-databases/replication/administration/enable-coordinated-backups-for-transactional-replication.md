---
title: Habilitar Backups coordenados para replicação transacional (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5055305259715c323e1f6cb26fc3428879acfddb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186982"
---
# <a name="enable-coordinated-backups-for-transactional-replication-replication-transact-sql-programming"></a>Habilitar backups coordenados para a replicação transacional (Programação Transact-SQL de replicação)
  Quando habilitar um banco de dados para a replicação transacional, é possível especificar que seja efetuado um backup de todas as transações antes que elas sejam entregues ao banco de dados de distribuição. Você pode habilitar também um backup coordenado no banco de dados de distribuição de modo que o log de transações, para o banco de dados de publicação, não fique truncado até que seja efetuado o backup das transações que foram propagadas ao Distribuidor. Para obter mais informações, consulte [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>Para habilitar backups coordenados para um banco de dados publicado com replicação transacional  
  
1.  No Publicador, use a função [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql) para retornar a propriedade **IsSyncWithBackup** do banco de dados de publicação. Se a função retornar **1**, os backups coordenados já estarão habilitados para o banco de dados publicado.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **sync with backup** para **@optname** e **verdadeiro** para **@value** .  
  
    > [!NOTE]  
    >  Se alterar a opção **sync with backup** para **falso**, o ponto de truncamento do banco de dados de publicação será atualizado após a execução do Agente de Leitor de Log ou após um intervalo, caso o Agente de Leitor de Log esteja executando continuamente. O intervalo máximo é controlado pelo parâmetro do agente **-MessageInterval** (que tem um padrão de 30 segundos).  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>Para habilitar backups coordenados para um banco de dados de distribuição  
  
1.  No Editor, use a função [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql) para retornar a propriedade **IsSyncWithBackup** do banco de dados de distribuição. Se a função retornar **1**, os backups coordenados já estarão habilitados para o banco de dados de distribuição.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) no Distribuidor do banco de dados de distribuição. Especifique um valor de **sync with backup** para **@optname** e **verdadeiro** para **@value** .  
  
### <a name="to-disable-coordinated-backups"></a>Para desabilitar backups coordenados  
  
1.  No Publicador do banco de dados de publicação ou no Distribuidor no banco de dados de distribuição, execute [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql). Especifique um valor de **sync with backup** para **@optname** e **falso** para **@value** .  
  
  
