---
title: sys. pdw_column_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5b71df1a25a9cd8480f23dc104792ad8f3e70f35
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401690"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>sys. pdw_column_distribution_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações de distribuição para colunas.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**inteiro**|ID do objeto ao qual a coluna pertence.||  
|**column_id**|**inteiro**|ID da coluna.||  
|**distribution_ordinal**|**tinyint**|Ordinal (baseado em 1) dentro do conjunto de distribuição.|0 = não é uma coluna de distribuição. 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] está usando esta coluna para distribuir a tabela pai.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de data warehouse SQL Data Warehouse e paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
