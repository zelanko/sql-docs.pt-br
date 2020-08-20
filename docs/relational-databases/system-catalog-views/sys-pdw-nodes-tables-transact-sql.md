---
description: sys. pdw_nodes_tables (Transact-SQL)
title: sys. pdw_nodes_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7b50d1757371a1ca379a4cf8f79410ceaef9a614
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475350"
---
# <a name="syspdw_nodes_tables-transact-sql"></a>sys. pdw_nodes_tables (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém uma linha para cada objeto de tabela que uma entidade de segurança proprietária ou para a qual a entidade de segurança recebeu alguma permissão.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<inherited columns>||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. Objects](../system-catalog-views/sys-objects-transact-sql.md).||  
|lob_data_space_id|**int**||Sempre 0.|  
|filestream_data_space_id|**int**|ID de espaço de dados para um grupo de arquivos FILESTREAM ou [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULO|  
|max_column_id_used|**int**|ID de coluna máximo usada por esta tabela.||  
|lock_on_bulk_load|**bit**|A tabela é bloqueada em carregamento em massa.|TBD|  
|uses_ansi_nulls|**bit**|A tabela foi criada com a opção de banco de dados SET ANSI_NULLS definida como ON.|1|  
|is_replicated|**bit**|1 = a tabela é publicada usando replicação.|0 Não há suporte para replicação.|  
|has_replication_filter|**bit**|1 = A tabela tem um filtro de replicação.|0|  
|is_merge_published|**bit**|1 = A tabela é publicada usando replicação de mesclagem.|0 sem suporte.|  
|is_sync_tran_subscribed|**bit**|1 = A tabela é inscrita usando uma assinatura de atualização imediata.|0 sem suporte.|  
|has_unchecked_assembly_data|**bit**|1 = A tabela contém dados persistentes que dependem de um assembly cuja definição foi alterada durante o último ALTER ASSEMBLY. Será redefinida como 0 depois do próximo DBCC CHECKDB ou DBCC CHECKTABLE bem-sucedido.|0 Não há suporte para CLR.|  
|text_in_row_limit|**int**|0 = Texto em opção de linha não é definido.|Sempre 0.|  
|large_value_types_out_of_row|**bit**|1 = Tipos de valor grande são armazenados fora de linha.|Sempre 0.|  
|is_tracked_by_cdc|**bit**|1 = a tabela está habilitada para a captura de dados de alterações|Sempre 0; Não há suporte para CDC.|  
|lock_escalation|**tinyint**|O valor da opção LOCK_ESCALATION para a tabela: 2 = AUTO|Sempre 2.|  
|lock_escalation_desc|**nvarchar(60)**|Uma descrição de texto da opção lock_escalation.|Sempre "" automático.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
