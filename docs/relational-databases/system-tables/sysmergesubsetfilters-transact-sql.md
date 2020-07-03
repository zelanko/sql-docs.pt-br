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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a106c5e60570d553c00d6ec077caacf43a716eee
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881334"
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações de filtro de junção para artigos particionados. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|O nome do filtro usado para criar o artigo.|  
|**join_filterid**|**int**|A ID do objeto que representa o filtro de junção.|  
|**pubid**|**uniqueidentifier**|A ID da publicação.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**art_nickname**|**int**|O apelido do artigo.|  
|**join_articlename**|**sysname**|O nome da tabela a adicionar para determinar se a linha pertence.|  
|**join_nickname**|**int**|O apelido da tabela a adicionar para determinar se a linha pertence.|  
|**join_unique_key**|**int**|Indica uma junção em uma chave exclusiva de **join_tablename**:<br /><br /> 0 = Não uma chave exclusiva.<br /><br /> 1 = Uma chave exclusiva.|  
|**expand_proc**|**sysname**|O nome do procedimento armazenado usado pelo Merge Agent para identificar as linhas que precisam ser enviadas ou removidas de um Assinante.|  
|**join_filterclause**|**nvarchar(1000)**|A cláusula de filtro usada para a junção.|  
|**filter_type**|**tinyint**|Especifica o tipo de filtro, que pode ser um dos seguintes:<br /><br /> 1 = Filtro de junção.<br /><br /> 2 = Vínculo de registro lógico.<br /><br /> 3 = Vínculo de um filtro de junção e um registro lógico.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
