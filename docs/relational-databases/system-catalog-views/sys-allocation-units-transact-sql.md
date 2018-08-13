---
title: sys. allocation_units (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.allocation_units_TSQL
- sys.allocation_units
- allocation_units_TSQL
- allocation_units
dev_langs:
- TSQL
helpviewer_keywords:
- sys.allocation_units catalog view
ms.assetid: ec9de780-68fd-4551-b70b-2d3ab3709b3e
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1199e2cc93541af9a089eade6be4e9b5b13f0433
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565740"
---
# <a name="sysallocationunits-transact-sql"></a>sys.allocation_units (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada unidade de alocação no banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|ID da unidade de alocação. É exclusivo em um banco de dados.|  
|Tipo|**tinyint**|Tipo de unidade de alocação:<br /><br /> 0 = Descartado<br /><br /> 1 = Dados em linha (todos os tipos de dados, exceto LOB)<br /><br /> 2 = dados de objeto grande (LOB) (**texto**, **ntext**, **imagem**, **xml**, tipos de valor grande e tipos CLR definidos pelo usuário)<br /><br /> 3 = Dados do estouro de linha|  
|type_desc|**nvarchar(60)**|Descrição do tipo de unidade de alocação:<br /><br /> **DESCARTADO**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|ID do contêiner de armazenamento associado à unidade de alocação.<br /><br /> Se type = 1 ou 3, container_id = sys.partitions.hobt_id.<br /><br /> Se type for 2, container_id = sys.partitions.partition_id.<br /><br /> 0 = Unidade de alocação marcada para descarte diferido|  
|data_space_id|**int**|ID do grupo de arquivos no qual reside a unidade de alocação.|  
|total_pages|**bigint**|Número total de páginas alocadas ou reservadas pela unidade de alocação.|  
|used_pages|**bigint**|Número total de páginas realmente em uso.|  
|data_pages|**bigint**|Número de páginas usadas que têm:<br /><br /> Dados em linha<br /><br /> Dados LOB<br /><br /> Dados do estouro de linha<br /><br /> <br /><br /> Observe que o valor retornado exclui páginas de índice internas e páginas de gerenciamento de alocação.|  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Portanto os valores retornados por sys.allocation_units imediatamente após o descarte ou truncamento de um objeto grande podem não refletir o espaço em disco realmente disponível.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
