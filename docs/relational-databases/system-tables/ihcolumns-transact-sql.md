---
title: IHcolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9985b0587316641955219eb5179ffd6ed07916d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990391"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHcolumns** tabela do sistema contém uma linha para cada coluna publicada. Esta tabela é usada para definir como os tipos de dados de coluna do publicador não SQL Server serão representados quando publicado, a qual essencialmente mapeia tipos de dados entre um sistemas de gerenciamento de banco de dados do SQL Server (DBMS) e o SQL Server. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica uma coluna publicada.|  
|**publishercolumn_id**|**int**|Associa uma coluna publicada com metadados de coluna armazenados em do [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabela do sistema.|  
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
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
