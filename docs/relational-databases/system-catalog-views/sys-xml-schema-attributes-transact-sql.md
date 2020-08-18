---
description: sys.xml_schema_attributes (Transact-SQL)
title: sys.xml_schema_attributes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: dd0c98aa-5e72-4df6-96d9-482786c8dbb1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c5f1eab66cd09f1d52c5e675761c691801baf67e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400412"
---
# <a name="sysxml_schema_attributes-transact-sql"></a>sys.xml_schema_attributes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha por componente de esquema XML que é um atributo, **symbol_space** de **um**.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|Herda de [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_default_fixed**|**bit**|1 = O valor padrão é um valor fixo. Esse valor não pode ser substituído em uma instância XML.<br /><br /> 0 = O valor padrão não é um valor fixo para o atributo. (padrão)|  
|**must_be_qualified**|**bit**|1 = O atributo deve ser qualificado explicitamente pelo namespace.<br /><br /> 0 = O atributo pode ser qualificado implicitamente pelo namespace. (padrão)|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|Valor padrão do atributo. É NULL se um valor padrão não for fornecido.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Esquemas XML &#40;o sistema de tipo XML&#41; exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
