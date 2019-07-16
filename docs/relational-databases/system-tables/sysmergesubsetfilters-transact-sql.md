---
title: sysmergesubsetfilters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 84f9e2ce3026792b768d353e05b9e2299cf7ca5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029748"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações de filtro de junção para artigos particionados. Essa tabela é armazenada nos bancos de dados da publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**FilterName**|**sysname**|O nome do filtro usado para criar o artigo.|  
|**join_filterid**|**int**|A ID do objeto que representa o filtro de junção.|  
|**pubid**|**uniqueidentifier**|A ID da publicação.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**art_nickname**|**int**|O apelido do artigo.|  
|**join_articlename**|**sysname**|O nome da tabela a adicionar para determinar se a linha pertence.|  
|**join_nickname**|**int**|O apelido da tabela a adicionar para determinar se a linha pertence.|  
|**join_unique_key**|**int**|Indica uma junção em uma chave exclusiva **join_tablename**:<br /><br /> 0 = Não uma chave exclusiva.<br /><br /> 1 = Uma chave exclusiva.|  
|**expand_proc**|**sysname**|O nome do procedimento armazenado usado pelo Merge Agent para identificar as linhas que precisam ser enviadas ou removidas de um Assinante.|  
|**join_filterclause**|**nvarchar(1000)**|A cláusula de filtro usada para a junção.|  
|**filter_type**|**tinyint**|Especifica o tipo de filtro, que pode ser um dos seguintes:<br /><br /> 1 = Filtro de junção.<br /><br /> 2 = Vínculo de registro lógico.<br /><br /> 3 = Vínculo de um filtro de junção e um registro lógico.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
