---
title: sys.xml_schema_elements (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32c5a61fe630192b6ff62a41804db22524f481a5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por componente de esquema XML que é um tipo **symbol_space** de **E**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**|**--**|Herda colunas de [xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_default_fixed**|**bit**|1 = Valor padrão é um valor fixo. Esse valor não pode ser substituído em uma instância XML.<br /><br /> 0 = Valor padrão não é um valor fixo para o elemento. (padrão).|  
|**is_abstract**|**bit**|1 = Elemento é abstrato e não pode ser usado em um documento de instância. Um membro do grupo de substituição do elemento deve aparecer no documento de instância.<br /><br /> 0 = Elemento não é abstrato. (padrão).|  
|**is_nillable**|**bit**|1 = Elemento permite valor nulo.<br /><br /> 0 = Elemento não permite valor nulo. (padrão)|  
|**must_be_qualified**|**bit**|1 = Elemento deve ser explicitamente qualificado para namespace.<br /><br /> 0 = Elemento pode ser implicitamente qualificado para namespace. (padrão)|  
|**is_extension_blocked**|**bit**|1 = Substituição com uma instância de um tipo de extensão é bloqueada.<br /><br /> 0 = Substituição com tipo de extensão é permitida. (padrão)|  
|**is_restriction_blocked**|**bit**|1 = Substituição com uma instância de um tipo de restrição é bloqueada.<br /><br /> 0 = Substituição com tipo de restrição é permitida. (padrão)|  
|**is_substitution_blocked**|**bit**|1 = Instância de um grupo de substituição não pode ser usada.<br /><br /> 0 = Substituição com grupo de substituição é permitida. (padrão)|  
|**is_final_extension**|**bit**|1 = Substituição com uma instância de um tipo de extensão não é permitida.<br /><br /> 0 = Substituição em uma instância de um tipo de extensão é permitida. (padrão)|  
|**is_final_restriction**|**bit**|1 = Substituição com uma instância de um tipo de restrição não é permitida.<br /><br /> 0 = Substituição em uma instância de um tipo de restrição é permitida. (padrão)|  
|**default_value**|**nvarchar (4000)**|Valor padrão do elemento. NULL se um valor padrão não for fornecido.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40; Sistema de tipo XML &#41; Exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
