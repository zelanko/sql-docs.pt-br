---
description: IHcolumns (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a27e72b46fed5f814e91d447abf30c9c905cba4d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540955"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHcolumns** contém uma linha para cada coluna publicada. Essa tabela é usada para definir como os tipos de dados de coluna de Editor não SQL Server serão representados, quando forem publicados, a qual essencialmente mapeia tipos de dados entre DBMS (sistemas de gerenciamento de banco de dados) não SQL Server e o SQL Server. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica uma coluna publicada.|  
|**publishercolumn_id**|**int**|Associa uma coluna publicada com metadados de coluna armazenados na tabela do sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) .|  
|**name**|**sysname**|Especifica o nome de coluna.|  
|**article_id**|**int**|Identifica o artigo ao qual a coluna pertence.|  
|**column_ordinal**|**int**|Identifica a coluna por ordem.|  
|**mapped_type**|**tinyint**|O tipo de dados da coluna.de destino no Assinante.|  
|**mapped_length**|**bigint**|O comprimento da coluna no Assinante.|  
|**mapped_prec**|**int**|A precisão da coluna no Assinante.|  
|**mapped_scale**|**int**|A escala da coluna no Assinante.|  
|**mapped_nullable**|**bit**|Indica se a coluna no Assinante aceita valores nulos, em que **1** significa que valores nulos são aceitos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;exibição do sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [&#41;sysarticlecolumns &#40;Transact-SQL ](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
