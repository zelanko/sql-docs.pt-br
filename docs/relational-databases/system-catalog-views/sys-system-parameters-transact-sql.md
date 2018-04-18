---
title: system_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.system_parameters
- sys.system_parameters_TSQL
- system_parameters_TSQL
- system_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_parameters catalog view
ms.assetid: 0d135c5f-68b5-4009-a0da-35e6abfee0ff
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 66ef0a52aa2e02520897629903111f0d241b2531
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="syssystemparameters-transact-sql"></a>sys.system_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada objeto de sistema com parâmetros.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto ao qual pertence o parâmetro.|  
|**name**|**sysname**|Nome do parâmetro. É exclusiva no objeto.<br /><br /> Se o objeto for uma função escalar, o nome de parâmetro será uma cadeia de caracteres vazia na linha que representa o valor de retorno.|  
|**parameter_id**|**Int**|ID do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, **parameter_id** = 0, que representa o valor de retorno.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro.|  
|**user_type_id**|**Int**|ID do tipo do parâmetro como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, unir o [Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) essa coluna de exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro, em bytes. Valor será -1 para quando o tipo de dados de coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.|  
|**precisão**|**tinyint**|Precisão do parâmetro se tiver base numérica; Caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída (ou retorno); do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = parâmetro é um parâmetro de referência de cursor.|  
|**has_default_value**|**bit**|1 = Parâmetro tem valor padrão.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém valores padrão apenas para objetos CLR nesta exibição do catálogo; portanto, esta coluna terá sempre um valor de 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para exibir o valor padrão de um parâmetro em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] de objeto, consulte o **definição** coluna do [sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) exibição do catálogo ou use o [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)função do sistema.|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **xml**.|  
|**default_value**|**sql_variant**|Se **has_default_value** é 1, o valor dessa coluna é o valor padrão para o parâmetro; caso contrário será NULL.|  
|**xml_collection_id**|**Int**|Diferente de zero se o tipo de dados do parâmetro é **xml** e o XML for digitado. O valor é o ID da coleção que contém o namespace do esquema XML de validação para o parâmetro.<br /><br /> 0 = Não há nenhuma coleção de esquemas XML.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [all_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
