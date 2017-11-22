---
title: sys.xml_schema_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc42e2b600a276ad7dd3512b3aa2a20925c84016
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por componente de esquema XML que é um tipo **symbol_space** de **T**.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**||Herda colunas de [xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_abstract**|**bit**|1 = O tipo é abstrato. Todas as instâncias de um elemento desse tipo devem usar **xsi: Type** para indicar um tipo derivado não é abstrato.<br /><br /> 0 = O tipo não é abstrato. (padrão)|  
|**allows_mixed_content**|**bit**|1 = É permitido conteúdo misturado<br /><br /> 0 = Não é permitido conteúdo misturado (padrão)|  
|**is_extension_blocked**|**bit**|1 = substituição com uma extensão do tipo está bloqueada nas instâncias quando o bloco de atributo no **complexType** definição ou o **blockDefault** atributo do ancestral \<esquema > item de informação do elemento é definido como "extension" ou "#all".<br /><br /> 0 = A substituição pela extensão não está bloqueada.|  
|**is_restriction_blocked**|**bit**|1 = substituição com uma restrição de tipo está bloqueada nas instâncias quando o bloco de atributo no **complexType** definição ou o **blockDefault** atributo do ancestral \<esquema > item de informação do elemento é definido como "restriction" ou "#all".<br /><br /> 0 = A substituição pela restrição não está bloqueada. (padrão)|  
|**is_final_extension**|**bit**|1 = a derivação pela extensão do tipo é bloqueada quando o atributo final no **complexType** definição ou o **finalDefault** atributo do ancestral \<esquema > informações do elemento item é definido como "extension" ou "#all".<br /><br /> 0 = A extensão é permitida. (padrão)|  
|**is_final_restriction**|**bit**|1 = a derivação por restrição do tipo é bloqueada quando o atributo final em simples ou **complexType** definição ou o **finalDefault** atributo do ancestral \<esquema > elemento item de informação é definido como "restriction" ou "#all".<br /><br /> 0 = A restrição é permitida. (padrão)|  
|**is_final_list_member**|**bit**|1 = Esse tipo simples não pode ser usado como o tipo de item em uma lista.<br /><br /> 0 = Esse é um tipo complexo ou pode ser usado como tipo de item de lista. (padrão)|  
|**is_final_union_member**|**bit**|1 = Esse tipo simples não pode ser usado como o tipo de membro de um tipo de união.<br /><br /> 0 = É um tipo complexo ou pode ser usado como tipo de membro de união. (padrão)|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40; Sistema de tipo XML &#41; Exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
