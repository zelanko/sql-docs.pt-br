---
description: cdc.captured_columns (Transact-SQL)
title: cdc.captured_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3337ab3e4b4c2221c018c326762251ff954b329d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081485"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada coluna rastreada em uma instância de captura. Por padrão, todas as colunas na tabela de origem são capturadas. Porém, colunas podem ser incluídas ou excluídas quando a tabela de origem é habilitada para Change Data Capture especificando uma lista de colunas. Para obter mais informações, consulte [sys.sp_cdc_enable_table &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Recomendamos que você **não consulte as tabelas do sistema diretamente**. Em vez disso, execute o procedimento armazenado [Sys.sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) .  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela de alteração à qual a coluna capturada pertence.|  
|**column_name**|**sysname**|Nome da coluna capturada.|  
|**column_id**|**int**|A identificação da coluna capturada dentro da tabela de origem.|  
|**column_type**|**sysname**|O tipo de coluna capturada.|  
|**column_ordinal**|**int**|O ordinal da coluna (com base em 1) na tabela de alteração. As colunas de metadados na tabela de alteração são excluídas. O ordinal 1 é atribuído à primeira coluna capturada.|  
|**is_computed**|**bit**|Indica que a coluna capturada é uma coluna computada na tabela de origem.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de cdc.change_tables ](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
