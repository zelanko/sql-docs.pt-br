---
title: sys.xml_schema_facets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84008ec923ef5203ede7e4bd8827e21eb475720e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945897"
---
# <a name="sysxmlschemafacets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada faceta (restrição) de uma definição de tipo de xml (corresponde ao **xml_types**).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID do componente XML (tipo) ao qual esta faceta pertence.|  
|**facet_id**|**int**|ID (ordinal de base 1) da faceta, exclusiva na id de componente.|  
|**kind**|**char(2)**|Tipo de faceta:<br /><br /> LG = Comprimento<br /><br /> LN = Comprimento mínimo<br /><br /> LX = Comprimento máximo<br /><br /> PT = Padrão (expressão regular)<br /><br /> EU = Enumeração<br /><br /> IN = Valor inclusivo mínimo<br /><br /> IX = Valor inclusivo máximo<br /><br /> EN = Valor exclusivo mínimo<br /><br /> EX = Valor exclusivo máximo<br /><br /> DT = Total de dígitos<br /><br /> DF = Dígitos fracionários<br /><br /> WS = Normalização de espaço em branco|  
|**kind_desc**|**nvarchar (60)**|Descrição do tipo de faceta:<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = A faceta tem um valor fixo previamente especificado.<br /><br /> 0 = Nenhum valor fixo. (padrão)|  
|**value**|**nvarchar (4000)**|Valor fixo previamente especificado da faceta.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;sistema de tipo XML&#41; exibições do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
