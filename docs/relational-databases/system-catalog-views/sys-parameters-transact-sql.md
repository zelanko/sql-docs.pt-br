---
title: sys. Parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33c87d4b784e46defac98823a5cf9d4dc9420aaa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752304"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada parâmetro de um objeto que aceita parâmetros. Se o objeto for uma função escalar, também haverá uma única linha descrevendo o valor de retorno. Essa linha terá um **parameter_id** valor de 0.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**name**|**sysname**|Nome do parâmetro. É exclusiva no objeto.<br /><br /> Se o objeto for uma função escalar, o nome de parâmetro será uma cadeia de caracteres vazia na linha que representa o valor de retorno.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva no objeto.<br /><br /> Se o objeto for uma função escalar, **parameter_id** = 0 representa o valor de retorno.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro.|  
|**user_type_id**|**int**|ID do tipo do parâmetro como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, Junte-se para o [Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) essa coluna de exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro, em bytes.<br /><br /> Valor = -1 quando o tipo de dados de coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.|  
|**Precisão**|**tinyint**|Precisão do parâmetro se tiver base numérica; Caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é OUTPUT ou RETURN; caso contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = parâmetro é um parâmetro de referência de cursor.|  
|**has_default_value**|**bit**|1 = Parâmetro tem valor padrão.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém valores padrão apenas para objetos CLR nesta exibição do catálogo; portanto, essa coluna tem um valor de 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para exibir o valor padrão de um parâmetro em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] do objeto, consulte o **definição** coluna do [sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) exibição do catálogo ou usar o [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)função do sistema.|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **xml**.|  
|**default_value**|**sql_variant**|Se **has_default_value** é 1, o valor desta coluna é o valor do padrão para o parâmetro; caso contrário, nulo.|  
|**xml_collection_id**|**int**|Diferente de zero se o tipo de dados do parâmetro é **xml** e o XML for digitado. O valor é a ID da coleção que contém o namespace do esquema XML de validação do parâmetro.<br /><br /> 0 = Nenhuma coleção de esquemas XML.|  
|**is_readonly**|**bit**|1 = O parâmetro é READONLY; caso contrário, 0.|  
|**is_nullable**|**bit**|1 = O parâmetro permite valor nulo. (o padrão).<br /><br /> 0 = O parâmetro não é anulável, para uma execução mais eficiente de procedimentos armazenados compilados nativamente.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys. system_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
