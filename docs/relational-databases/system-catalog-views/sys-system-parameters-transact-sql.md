---
description: sys.system_parameters (Transact-SQL)
title: sys.system_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9d1fb8b032c107d77cb014ca143cebd5aa227ed
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464647"
---
# <a name="syssystem_parameters-transact-sql"></a>sys.system_parameters (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada objeto de sistema com parâmetros.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**name**|**sysname**|Nome do parâmetro. É exclusiva no objeto.<br /><br /> Se o objeto for uma função escalar, o nome de parâmetro será uma cadeia de caracteres vazia na linha que representa o valor de retorno.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, **parameter_id** = 0 representa o valor de retorno.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro.|  
|**user_type_id**|**int**|ID do tipo do parâmetro como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro, em bytes. O valor será-1 para quando o tipo de dados da coluna for **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.|  
|**precisão**|**tinyint**|Precisão do parâmetro se for baseado em numeric; caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; do contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída (ou retorno); do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = o parâmetro é um parâmetro de referência de cursor.|  
|**has_default_value**|**bit**|1 = Parâmetro tem valor padrão.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém valores padrão apenas para objetos CLR nesta exibição do catálogo; portanto, esta coluna terá sempre um valor de 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para exibir o valor padrão de um parâmetro em um [!INCLUDE[tsql](../../includes/tsql-md.md)] objeto, consulte a coluna **definição** da exibição de catálogo [Sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ou use a função de sistema [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) .|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **XML**.|  
|**default_value**|**sql_variant**|Se **has_default_value** for 1, o valor dessa coluna será o valor do padrão para o parâmetro; caso contrário, NULL.|  
|**xml_collection_id**|**int**|Diferente de zero se o tipo de dados do parâmetro for **XML** e o XML for digitado. O valor é o ID da coleção que contém o namespace do esquema XML de validação para o parâmetro.<br /><br /> 0 = Não há nenhuma coleção de esquemas XML.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys. Parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.all_parameters ](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
