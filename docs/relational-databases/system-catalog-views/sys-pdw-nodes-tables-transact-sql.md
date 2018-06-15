---
title: sys.pdw_nodes_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
caps.latest.revision: 8
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 16b8bd03970051d0295d9a89792c7f2de2011466
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180872"
---
# <a name="syspdwnodestables-transact-sql"></a>sys.pdw_nodes_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada objeto de tabela que possui uma entidade ou no qual a entidade de segurança recebeu alguma permissão.  
  
|Nome da coluna|Tipo de dados|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<herdado colunas >||Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. Objects](http://msdn.microsoft.com/en-us/c36fa71e-549a-4533-a6cd-1314d26f533f).||  
|lob_data_space_id|**Int**||Sempre 0.|  
|filestream_data_space_id|**Int**|ID do espaço de dados para um grupo de arquivos FILESTREAM ou [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**Int**|ID de coluna máximo usada por esta tabela.||  
|lock_on_bulk_load|**bit**|A tabela é bloqueada em carregamento em massa.|TBD|  
|uses_ansi_nulls|**bit**|A tabela foi criada com a opção de banco de dados SET ANSI_NULLS definida como ON.|1|  
|is_replicated|**bit**|1 = tabela for publicada utilizando replicação.|0; Não há suporte para replicação.|  
|has_replication_filter|**bit**|1 = A tabela tem um filtro de replicação.|0|  
|is_merge_published|**bit**|1 = A tabela é publicada usando replicação de mesclagem.|0; Não há suporte.|  
|is_sync_tran_subscribed|**bit**|1 = A tabela é inscrita usando uma assinatura de atualização imediata.|0; Não há suporte.|  
|has_unchecked_assembly_data|**bit**|1 = A tabela contém dados persistentes que dependem de um assembly cuja definição foi alterada durante o último ALTER ASSEMBLY. Será redefinida como 0 depois do próximo DBCC CHECKDB ou DBCC CHECKTABLE bem-sucedido.|0; Não há suporte do CLR.|  
|text_in_row_limit|**Int**|0 = Texto em opção de linha não é definido.|Sempre 0.|  
|large_value_types_out_of_row|**bit**|1 = Tipos de valor grande são armazenados fora de linha.|Sempre 0.|  
|is_tracked_by_cdc|**bit**|1 = tabela está habilitada para change data capture|Sempre 0; Não há suporte de CDC.|  
|lock_escalation|**tinyint**|O valor da opção LOCK_ESCALATION da tabela: 2 = AUTO|Sempre 2.|  
|lock_escalation_desc|**nvarchar(60)**|Uma descrição de texto da opção lock_escalation.|Sempre ꞌAUTOꞌ.|  
|pdw_node_id|**Int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
