---
title: IHcolumns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs: TSQL
helpviewer_keywords: IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 857380d30397d02b2fe1ba9adfd11ca9382b9eee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHcolumns** tabela do sistema contém uma linha para cada coluna publicada. Esta tabela é usada para definir como os tipos de dados de coluna do publicador não SQL Server serão representados quando publicado, qual essencialmente mapeia tipos de dados entre um sistemas de gerenciamento de banco de dados do SQL Server (DBMS) e o SQL Server. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica uma coluna publicada.|  
|**publishercolumn_id**|**int**|Associa uma coluna publicada com metadados de coluna armazenados o [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabela do sistema.|  
|**name**|**sysname**|Especifica o nome de coluna.|  
|**article_id**|**int**|Identifica o artigo ao qual a coluna pertence.|  
|**column_ordinal**|**int**|Identifica a coluna por ordem.|  
|**mapped_type**|**tinyint**|O tipo de dados da coluna.de destino no Assinante.|  
|**mapped_length**|**bigint**|O comprimento da coluna no Assinante.|  
|**mapped_prec**|**int**|A precisão da coluna no Assinante.|  
|**mapped_scale**|**int**|A escala da coluna no Assinante.|  
|**mapped_nullable**|**bit**|Indica se a coluna no assinante aceita valores NULL, onde **1** significa que valores NULL são aceitos.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40; Exibição do sistema &#41; &#40; Transact-SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
