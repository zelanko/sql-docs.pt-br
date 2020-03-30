---
title: Exibir comandos replicados e informações no banco de dados de distribuição
description: Saiba como exibir comandos replicados e outras informações relacionadas à replicação no banco de dados de distribuição do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3794d249002fb6038be6a6d27d88e5f70e042104
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286326"
---
# <a name="view-replicated-commands-and-information-in-distribution-database"></a>Exibir comandos replicados e informação no banco de dados de distribuição
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Ao usar replicação transacional, os comandos de transação são armazenados no banco de dados de distribuição ou até que o Agente de Distribuição os propague a todos os Assinantes ou até um Agente de Distribuição enviar as alterações ao Assinante. Esses comandos pendentes no banco de dados de distribuição podem ser exibidos programaticamente por meio de procedimentos armazenados de replicação. Para obter mais informações, consulte [procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>Para exibir os comandos replicados de todas as publicações transacionais no banco de dados de distribuição  
  
1.  No Distribuidor, no banco de dados de distribuição, execute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md).  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>Para exibir comandos replicados no banco de dados de distribuição de um artigo específico ou de um banco de dados publicado específico por meio de replicação transacional  
  
1.  (Opcional) No Publicador, no banco de dados de publicação, execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique `@publication` e `@article`. Observe o valor de **id de artigo** no conjunto de resultados.  
  
2.  No Distribuidor, no banco de dados de distribuição, execute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md). (Opcional) Especifique a ID do artigo da etapa 2 para `@article_id`. (Opcional) Especifique a ID do banco de dados de publicação para `@publisher_database_id`, que pode ser obtida da coluna **database_id** na exibição de catálogo [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar programaticamente a replicação](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
