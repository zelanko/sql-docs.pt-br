---
title: sys.xml_schema_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c7c3dc90f505f406583f36980ac758033aeb1519
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899965"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha por componente de esquema XML que é um tipo, **symbol_space** de **T**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**||Herda colunas de [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_abstract**|**bit**|1 = O tipo é abstrato. Todas as instâncias de um elemento desse tipo devem usar **xsi: Type** para indicar um tipo derivado que não é abstract.<br /><br /> 0 = O tipo não é abstrato. (padrão)|  
|**allows_mixed_content**|**bit**|1 = É permitido conteúdo misturado<br /><br /> 0 = Não é permitido conteúdo misturado (padrão)|  
|**is_extension_blocked**|**bit**|1 = a substituição com uma extensão do tipo é bloqueada em instâncias quando o atributo block na definição **complexType** ou o atributo **blockDefault** do item de \<schema> informações do elemento ancestral é definido como "Extension" ou "#all".<br /><br /> 0 = A substituição pela extensão não está bloqueada.|  
|**is_restriction_blocked**|**bit**|1 = a substituição com uma restrição do tipo é bloqueada em instâncias quando o atributo block na definição **complexType** ou o atributo **blockDefault** do item de \<schema> informações do elemento ancestral está definido como "restriction" ou "#all".<br /><br /> 0 = A substituição pela restrição não está bloqueada. (padrão)|  
|**is_final_extension**|**bit**|1 = derivação por extensão do tipo é bloqueada quando o atributo final na definição **complexType** ou o atributo **finalDefault** do item de \<schema> informações do elemento ancestral é definido como "Extension" ou "#all".<br /><br /> 0 = A extensão é permitida. (padrão)|  
|**is_final_restriction**|**bit**|1 = a derivação por restrição do tipo é bloqueada quando o atributo final na definição simples ou **complexa** ou o atributo **finalDefault** do item de \<schema> informações do elemento ancestral é definido como "restriction" ou "#all".<br /><br /> 0 = A restrição é permitida. (padrão)|  
|**is_final_list_member**|**bit**|1 = Esse tipo simples não pode ser usado como o tipo de item em uma lista.<br /><br /> 0 = Esse é um tipo complexo ou pode ser usado como tipo de item de lista. (padrão)|  
|**is_final_union_member**|**bit**|1 = Esse tipo simples não pode ser usado como o tipo de membro de um tipo de união.<br /><br /> 0 = É um tipo complexo ou pode ser usado como tipo de membro de união. (padrão)|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;o sistema de tipo XML&#41; exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
