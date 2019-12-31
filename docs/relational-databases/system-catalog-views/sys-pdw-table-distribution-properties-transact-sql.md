---
title: sys. pdw_table_distribution_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 43974e2ae8becb5ad24daf0c52246a71c890bce2
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822166"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>sys. pdw_table_distribution_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém informações de distribuição para tabelas.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**inteiro**|ID da tabela para a qual as propriedades três foram especificadas.||  
|**distribution_policy**|**tinyint**|0 = INDEFINIDO<br /><br /> 1 = NENHUM<br /><br /> 2 = HASH<br /><br /> 3 = REPLICAR<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**nvarchar (60)**|INDEFINIDO, NENHUM, HASH, REPLICAR ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]Retorna o HASH, ROUND_ROBIN ou REPLICAte.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de data warehouse SQL Data Warehouse e paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
