---
title: sys. allocation_units (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c996a258ae9f0dacec09fc58b3f433e620b6d663
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822070"
---
# <a name="sysallocation_units-transact-sql"></a>sys.allocation_units (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada unidade de alocação no banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|ID da unidade de alocação. É exclusivo em um banco de dados.|  
|tipo|**tinyint**|Tipo de unidade de alocação:<br /><br /> 0 = Descartado<br /><br /> 1 = Dados em linha (todos os tipos de dados, exceto LOB)<br /><br /> 2 = dados de objeto grande (LOB) (**Text**, **ntext**, **Image**, **XML**, tipos de valor grande e tipos CLR definidos pelo usuário)<br /><br /> 3 = Dados do estouro de linha|  
|type_desc|**nvarchar(60)**|Descrição do tipo de unidade de alocação:<br /><br /> **PASSOU**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|ID do contêiner de armazenamento associado à unidade de alocação.<br /><br /> Se type = 1 ou 3, container_id = sys.partitions.hobt_id.<br /><br /> Se type for 2, container_id = sys.partitions.partition_id.<br /><br /> 0 = Unidade de alocação marcada para descarte diferido|  
|data_space_id|**int**|ID do grupo de arquivos no qual reside a unidade de alocação.|  
|total_pages|**bigint**|Número total de páginas alocadas ou reservadas pela unidade de alocação.|  
|used_pages|**bigint**|Número total de páginas realmente em uso.|  
|data_pages|**bigint**|Número de páginas usadas que têm:<br /><br /> Dados em linha<br /><br /> Dados LOB<br /><br /> Dados do estouro de linha<br /><br /> <br /><br /> Observe que o valor retornado exclui páginas de índice interno e páginas de gerenciamento de alocação.|  
  
> [!NOTE]  
>  Quando você descarta ou reconstrói índices grandes, ou descarta ou trunca tabelas grandes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados, até depois que a transação confirme. Operações de cancelamento adiadas não libertam espaço alocado imediatamente. Portanto os valores retornados por sys.allocation_units imediatamente após o descarte ou truncamento de um objeto grande podem não refletir o espaço em disco realmente disponível.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. partitions &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
