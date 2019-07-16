---
title: sys.all_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_parameters_TSQL
- sys.all_parameters
- all_parameters
- sys.all_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_parameters catalog view
ms.assetid: eecbb68e-9b4c-4243-94e2-8096a9cc7892
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63231301109f83243b431244028fddffb8cc6fe7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001327"
---
# <a name="sysallparameters-transact-sql"></a>sys.all_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Mostra a união de todos os parâmetros que pertencem a objetos de sistema ou definidos pelo usuário.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**name**|**sysname**|Nome do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, o nome de parâmetro será uma cadeia de caracteres vazia na linha que representa o valor de retorno.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, **parameter_id** = 0 representa o valor de retorno.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro.|  
|**user_type_id**|**int**|ID do tipo do parâmetro como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, Junte-se para o [Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) essa coluna de exibição do catálogo.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro, em bytes.<br /><br /> -1 = a coluna é do tipo de dados **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , ou **xml**.|  
|**precisão**|**tinyint**|Precisão do parâmetro, se numérico; caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; caso contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída (ou retorno); do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = Parâmetro é um parâmetro de referência do cursor.|  
|**has_default_value**|**bit**|1 = O parâmetro tem valor padrão de 1.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém valores padrão apenas para objetos CLR nesta exibição do catálogo; portanto, esta coluna terá sempre um valor de 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para exibir o valor padrão de um parâmetro em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] do objeto, consulte o **definição** coluna do [sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) exibição do catálogo ou usar o [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)função do sistema.|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **xml**.|  
|**default_value**|**sql_variant**|Se **has_default_value** é 1, o valor desta coluna é o valor do padrão para o parâmetro; caso contrário, nulo.|  
|**xml_collection_id**|**int**|É a ID da coleção de esquema XML utilizada para validar o parâmetro.<br /><br /> Diferente de zero se o tipo de dados do parâmetro é **xml** e o XML for digitado.<br /><br /> 0 = Não há nenhuma coleção de esquemas XML ou o parâmetro não é XML.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys. system_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
