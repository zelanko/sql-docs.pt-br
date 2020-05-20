---
title: CDC. index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2dac6ec3b2799a4489d660c9467000b27391236
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833067"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada coluna de índice associada a uma tabela de alteração. As colunas de índice são usadas pela captura de dados de alteração para identificar exclusivamente linhas na tabela de origem. Por padrão, as colunas da chave primária da tabela de origem são incluídas. Porém, se um índice exclusivo na tabela de origem for especificado quando a captura de dados de alteração for habilitada na tabela de origem, serão usadas então as colunas nesse índice. Uma chave primária ou índice exclusivo será necessário na tabela de origem se o rastreamento de alterações de rede estiver habilitado. Para obter mais informações, consulte [Sys. sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 É recomendável não consultar diretamente as tabelas do sistema. Em vez disso, execute o procedimento armazenado [Sys. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) .  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela de alteração.|  
|**column_name**|**sysname**|Nome da coluna do índice.|  
|**index_ordinal**|**tinyint**|Ordinal (base 1) da coluna no índice.|  
|**column_id**|**int**|ID da coluna na tabela de origem.|  
  
## <a name="see-also"></a>Consulte Também  
 [CDC. change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
