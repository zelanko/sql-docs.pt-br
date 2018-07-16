---
title: Exibir comandos replicados e outras informações no banco de dados de distribuição (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eec9cebdf7dc76d65642e73a5a0dc809391cc3c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227176"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>Exibir comandos replicados e outras informações no banco de dados de distribuição (Programação Transact-SQL de replicação)
  Ao usar replicação transacional, os comandos de transação são armazenados no banco de dados de distribuição ou até que o Agente de Distribuição os propague a todos os Assinantes ou até um Agente de Distribuição enviar as alterações ao Assinante. Esses comandos pendentes no banco de dados de distribuição podem ser exibidos programaticamente por meio de procedimentos armazenados de replicação. Para obter mais informações, consulte [procedimentos armazenados de replicação &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql).  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>Para exibir os comandos replicados de todas as publicações transacionais no banco de dados de distribuição  
  
1.  No Distribuidor, no banco de dados de distribuição, execute [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql).  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>Para exibir comandos replicados no banco de dados de distribuição de um artigo específico ou de um banco de dados publicado específico por meio de replicação transacional  
  
1.  (Opcional) No Publicador, no banco de dados de publicação, execute [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql). Especifique **@publication** e **@article**. Observe o valor de **id de artigo** no conjunto de resultados.  
  
2.  No Distribuidor, no banco de dados de distribuição, execute [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql). (Opcional) Especifique a ID do artigo da etapa 2 como **@article_id**. (Opcional) Especifique a id do banco de dados de publicação como **@publisher_database_id**, que pode ser obtida da coluna **database_id** na exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar programaticamente a replicação](monitoring-replication-overview.md)  
  
  
