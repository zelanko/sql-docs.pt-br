---
title: sys. all_parameters (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc5c7fff4b0226012e82d103dc9f52d84036c218
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822136"
---
# <a name="sysall_parameters-transact-sql"></a>sys.all_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Mostra a união de todos os parâmetros que pertencem a objetos de sistema ou definidos pelo usuário.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto ao qual pertence o parâmetro.|  
|**name**|**sysname**|Nome do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, o nome de parâmetro será uma cadeia de caracteres vazia na linha que representa o valor de retorno.|  
|**parameter_id**|**int**|ID do parâmetro. É exclusiva no objeto. Se o objeto for uma função escalar, **parameter_id** = 0 representa o valor de retorno.|  
|**system_type_id**|**tinyint**|ID do tipo de sistema do parâmetro.|  
|**user_type_id**|**int**|ID do tipo do parâmetro como definido pelo usuário.<br /><br /> Para retornar o nome do tipo, ingresse na exibição do catálogo [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) nesta coluna.|  
|**max_length**|**smallint**|Comprimento máximo do parâmetro, em bytes.<br /><br /> -1 = o tipo de dados da coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.|  
|**precisão**|**tinyint**|Precisão do parâmetro, se numérico; caso contrário, 0.|  
|**scale**|**tinyint**|Escala do parâmetro, se numérico; caso contrário, 0.|  
|**is_output**|**bit**|1 = Parâmetro é saída (ou retorno); do contrário, 0.|  
|**is_cursor_ref**|**bit**|1 = Parâmetro é um parâmetro de referência do cursor.|  
|**has_default_value**|**bit**|1 = O parâmetro tem valor padrão de 1.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém valores padrão apenas para objetos CLR nesta exibição do catálogo; portanto, esta coluna terá sempre um valor de 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para exibir o valor padrão de um parâmetro em um [!INCLUDE[tsql](../../includes/tsql-md.md)] objeto, consulte a coluna **definição** da exibição de catálogo [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ou use a função de sistema [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) .|  
|**is_xml_document**|**bit**|1 = O conteúdo é um documento XML completo.<br /><br /> 0 = o conteúdo é um fragmento de documento ou o tipo de dados da coluna não é **XML**.|  
|**default_value**|**sql_variant**|Se **has_default_value** for 1, o valor dessa coluna será o valor do padrão para o parâmetro; caso contrário, NULL.|  
|**xml_collection_id**|**int**|É a ID da coleção de esquema XML utilizada para validar o parâmetro.<br /><br /> Diferente de zero se o tipo de dados do parâmetro for **XML** e o XML for digitado.<br /><br /> 0 = Não há nenhuma coleção de esquemas XML ou o parâmetro não é XML.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes sobre o catálogo do sistema SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys. Parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys. system_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
