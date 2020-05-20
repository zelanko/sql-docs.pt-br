---
title: sys. xml_schema_wildcards (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_wildcards
- sys.xml_schema_wildcards_TSQL
- xml_schema_wildcards
- xml_schema_wildcards_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcards catalog view
ms.assetid: 7cedfe9a-e99e-4777-8a28-98674b6e5cff
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d7687acb160e872fbe85dc7789115a14e14e875f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833846"
---
# <a name="sysxml_schema_wildcards-transact-sql"></a>sys.xml_schema_wildcards (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por componente de esquema XML que é um curinga de atributo (**tipo** de **V**) ou curinga de elemento (**tipo** **W**), ambos com **symbol_space** de **N**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<colunas herdadas>**||Herda colunas de [Sys. xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**process_content**|**Char (1)**|Indica como os conteúdos são processados.<br /><br /> S = Validação Rígida (deve validar)<br /><br /> L = Validação incerta (valide se possível)<br /><br /> P = Ignorar validação|  
|**process_content_desc**|**nvarchar(60)**|Descrição de como os conteúdos são processados:<br /><br /> **STRICT_VALIDATION**<br /><br /> **LAX_VALIDATION**<br /><br /> **SKIP_VALIDATION**|  
|**disallow_namespaces**|**bit**|0 = namespaces enumerados em [Sys. xml_schema_wildcard_namespaces](../../relational-databases/system-catalog-views/sys-xml-schema-wildcard-namespaces-transact-sql.md) são os únicos permitidos.<br /><br /> 1 = Namespaces são os únicos não permitidos.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;o sistema de tipo XML&#41; exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
