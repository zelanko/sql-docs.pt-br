---
title: sys. sql_dependencies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e6ec79ad00de37b7887164795752b350630193f8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833953"
---
# <a name="syssql_dependencies-transact-sql"></a>sys.sql_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada dependência em uma entidade referenciada na expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] ou instruções que definem algum outro objeto de referência.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) .  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**classes**|**tinyint**|Identifica a classe da entidade referenciada:<br /><br /> 0 = Objeto ou coluna (somente referências não associadas a esquema)<br /><br /> 1 = Objeto ou coluna (somente referências associadas a esquema)<br /><br /> 2 = Tipos (referências associadas a esquema)<br /><br /> 3 = Coleções de esquema XML (referências associadas a esquema)<br /><br /> 4 = Função de partição (referências associadas a esquema)|  
|**class_desc**|**nvarchar(60)**|Descrição da classe da entidade referenciada:<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|ID do objeto de referência.|  
|**column_id**|**int**|Se a ID de referência for uma coluna, ID da coluna de referência; caso contrário, 0.|  
|**referenced_major_id**|**int**|ID da entidade referenciada, interpretada por valor de classe, de acordo com:<br /><br /> 0, 1 = ID de objeto do objeto ou coluna.<br /><br /> 2 = ID do tipo.<br /><br /> 3 = ID da coleção de esquemas XML.|  
|**referenced_minor_id**|**int**|ID secundária da entidade referenciada, interpretada pelo valor de classe, como mostrado a seguir.<br /><br /> Quando classe =:<br /><br /> 0, **referenced_minor_id** é uma ID de coluna; ou, se não for uma coluna, será 0.<br /><br /> 1, **referenced_minor_id** é uma ID de coluna; ou, se não for uma coluna, será 0.<br /><br /> Caso contrário, **referenced_minor_id** = 0.|  
|**is_selected**|**bit**|Objeto ou coluna é selecionada.|  
|**is_updated**|**bit**|Objeto ou coluna é atualizada.|  
|**is_select_all**|**bit**|Objeto é usado na cláusula SELECT * (somente no nível do objeto).|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
