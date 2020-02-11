---
title: MSarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81598b65daf5fa7370004c890ab775e5b29b518f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132104"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **MSarticles** contém uma linha para cada artigo sendo replicado por um Publicador. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do Publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**publication_id**|**int**|A ID da publicação.|  
|**artigo**|**sysname**|O nome do artigo.|  
|**article_id**|**int**|A ID do artigo.|  
|**destination_object**|**sysname**|O nome da tabela criada no Assinante.|  
|**source_owner**|**sysname**|O nome do esquema da tabela de origem no Publicador.|  
|**source_object**|**sysname**|O nome do objeto de origem do qual adicionar o artigo.|  
|**ndescrição**|**nvarchar (255)**|A descrição do artigo.|  
|**destination_owner**|**sysname**|O nome do esquema da tabela criada no Assinante.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
