---
title: sysmergesubsetfilters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66ef85eacefa716b50e3af7e125e877116185a64
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações de filtro de junção para artigos particionados. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**FilterName**|**sysname**|O nome do filtro usado para criar o artigo.|  
|**join_filterid**|**int**|A ID do objeto que representa o filtro de junção.|  
|**PubID**|**uniqueidentifier**|A ID da publicação.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**art_nickname**|**int**|O apelido do artigo.|  
|**join_articlename**|**sysname**|O nome da tabela a adicionar para determinar se a linha pertence.|  
|**join_nickname**|**int**|O apelido da tabela a adicionar para determinar se a linha pertence.|  
|**join_unique_key**|**int**|Indica uma junção em uma chave exclusiva de **join_tablename**:<br /><br /> 0 = Não uma chave exclusiva.<br /><br /> 1 = Uma chave exclusiva.|  
|**expand_proc**|**sysname**|O nome do procedimento armazenado usado pelo Merge Agent para identificar as linhas que precisam ser enviadas ou removidas de um Assinante.|  
|**join_filterclause**|**nvarchar (1000)**|A cláusula de filtro usada para a junção.|  
|**filter_type**|**tinyint**|Especifica o tipo de filtro, que pode ser um dos seguintes:<br /><br /> 1 = Filtro de junção.<br /><br /> 2 = Vínculo de registro lógico.<br /><br /> 3 = Vínculo de um filtro de junção e um registro lógico.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
