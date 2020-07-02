---
title: IHpublisherindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fc84090e08c3c8890a4613e6f73e1914209c0ba7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750169"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHpublisherindexes** contém uma linha para cada índice replicado de Publicadores não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|Identifica um índice publicado.|  
|**table_id**|**int**|Identifica a tabela de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) à qual o índice pertence.|  
|**publisher_id**|**smallint**|Identifica o Editor não SQL Server a partir do qual o índice é publicado.|  
|**name**|**sysname**|O nome do índice publicado.|  
|**type**|**nvarchar (255)**|Um tipo de índice com suporte da tabela do sistema [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) .|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
