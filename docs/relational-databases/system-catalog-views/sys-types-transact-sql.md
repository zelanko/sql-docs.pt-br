---
title: Types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs: TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0fab5cee5706b0d8a00638f35c3b91d639efb3b6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="systypes-transact-sql"></a>sys.types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada tipo definido pelo usuário e sistema.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do tipo. É exclusivo no esquema.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema interno do tipo.|  
|**user_type_id**|**int**|A ID do tipo É exclusiva no banco de dados. Para tipos de dados do sistema, **user_type_id** = **system_type_id**.|  
|**schema_id**|**int**|ID do esquema ao qual o tipo pertence.|  
|**principal_id**|**int**|ID do proprietário individual se diferente do proprietário do esquema. Por padrão, os objetos contidos no esquema pertencem ao proprietário do esquema. No entanto, um proprietário alternativo pode ser especificado usando a instrução ALTER AUTHORIZATION para alterar a propriedade.<br /><br /> NULL se não houver nenhum proprietário individual alternativo.|  
|**max_length**|**smallint**|Comprimento de máximo (em bytes) do tipo.<br /><br /> -1 = a coluna de tipo de dados é **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.<br /><br /> Para **texto** colunas, o **max_length** valor será 16.|  
|**precisão**|**tinyint**|Precisão máxima do tipo se for numérico; caso contrário, 0.|  
|**escala**|**tinyint**|Escala máxima do tipo se for numérico; caso contrário, 0.|  
|**collation_name**|**sysname**|Nome do agrupamento do tipo se baseado em caractere; caso contrário, NULL.|  
|**is_nullable**|**bit**|O tipo permite valor nulo.|  
|**is_user_defined**|**bit**|1 = Tipo definido pelo usuário.<br /><br /> 0 = tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_assembly_type**|**bit**|1 = A implementação do tipo foi definida em um assembly CLR.<br /><br /> 0 = O tipo tem como base um tipo de dados de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**default_object_id**|**int**|ID do padrão autônomo associado ao tipo usando [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md).<br /><br /> 0 = Não existe padrão.|  
|**rule_object_id**|**int**|ID da regra autônoma associada ao tipo usando [sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md).<br /><br /> 0 = Não existe regra.|  
|**is_table_type**|**bit**|Indica que o tipo é uma tabela.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Escalar tipos de exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
