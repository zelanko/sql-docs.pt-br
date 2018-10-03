---
title: sys.Periods (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58ee2ac11e86481c57da79d84bc75507c273b829
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702514"
---
# <a name="sysperiods-transact-sql"></a>sys.periods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada tabela para a qual período foi definido.  
  
|Cabeçalho de coluna|Tipo de dados|Description|  
|-------------------|---------------|-----------------|  
|period_type|**sysname**|Nome do período|  
|period_type_desc|**tinyint**|O valor numérico que representa o tipo de período:<br /><br /> 1 = período de tempo do sistema|  
|object_id|**nvarchar(60)**|A descrição de texto do tipo de coluna:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|A id da tabela que contém a coluna period_type|  
|start_column_id|**int**|A id da coluna que define o período limite inferior|  
|end_column_id|**int**|A id da coluna que define o limite superior de período|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)  
  
  
