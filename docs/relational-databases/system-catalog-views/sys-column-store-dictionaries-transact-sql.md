---
title: sys. column_store_dictionaries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2348633a2c357868e4688d7b37c5cf28aed6441a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304759"
---
# <a name="syscolumn_store_dictionaries-transact-sql"></a>sys.column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada dicionário usado em índices columnstore otimizados para memória xVelocity. Dicionários são usados para codificar alguns, mas não todos os tipos de dados; portanto, nem todas as colunas em um índice columnstore têm dicionários. Um dicionário pode existir como um dicionário primário (para todos os segmentos) e, possivelmente, para outros dicionários secundários usados para um subconjunto de segmentos da coluna.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|ID do índice de heap ou árvore B (HoBT) para a tabela que tem este índice columnstore.|  
|**column_id**|**int**|ID da coluna columnstore começando com 1. A primeira coluna tem ID = 1, a segunda coluna tem ID = 2, etc.|  
|**dictionary_id**|**int**|Pode haver dois tipos de dicionários, globais e locais, associados a um segmento de coluna. Um dictionary_id de 0 representa o dicionário global que é compartilhado entre todos os segmentos de coluna (um para cada grupo de linhas) para essa coluna.|  
|**version**|**int**|Versão de formato do dicionário.|  
|**type**|**int**|Tipo de dicionário:<br /><br /> 1-dicionário de hash contendo valores **int**<br /><br /> 2-não usado<br /><br /> 3-dicionário de hash contendo valores de cadeia de caracteres<br /><br /> 4-dicionário de hash que contém valores **float**<br /><br /> Para obter mais informações sobre dicionários, consulte [Guia de índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md).|  
|**last_id**|**int**|A última ID de dados no dicionário.|  
|**entry_count**|**bigint**|Número de entradas no dicionário.|  
|**on_disc_size**|**bigint**|Tamanho do dicionário em bytes.|  
|**partition_id**|**bigint**|Indica a ID da partição. É exclusivo em um banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Requer a permissão `VIEW DEFINITION` na tabela. As colunas a seguir retornam NULL, a menos que o usuário também tenha a permissão `SELECT`: last_id, ENTRY_COUNT, data_ptr.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Guia de Índices Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

