---
title: sys.xml_schema_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 90fbd2b92ccfcf01da2c2742a3b5a083f30f1e03
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por componente de um esquema XML. O par (**collection_id**, **namespace_id**) é uma chave estrangeira composta para o namespace que contém. Para componentes nomeados, os valores para **symbol_space**, **nome**, **scoping_xml_component_id**, **is_qualified**,  **xml_namespace_id**, **xml_collection_id** são exclusivos.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**Int**|ID exclusiva do componente de esquema XML no banco de dados.|  
|**xml_collection_id**|**Int**|ID da coleção de esquema XML que contém o namespace desse componente.|  
|**xml_namespace_id**|**Int**|ID do namespace XML na coleção.|  
|**is_qualified**|**bit**|1 = Este componente tem um qualificador de namespace explícito.<br /><br /> 0 = É um componente com escopo local. Nesse caso, o par **namespace_id**, **collection_id**, refere-se para o "no namespace" **targetNamespace**.<br /><br /> Para componentes curinga, esse valor será igual a 1.|  
|**name**|**nvarchar**<br /><br /> **(4000)**|Nome exclusivo do componente de esquema XML. Será NULL se o componente não for nomeado.|  
|**symbol_space**|**char(1)**|Espaço no qual esse nome de símbolo é exclusivo, com base em **tipo**:<br /><br /> N = Nenhum<br /><br /> T = Tipo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelo<br /><br /> A = Atributo<br /><br /> G = Grupo de atributo|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Descrição de espaço no qual esse nome de símbolo é exclusivo, com base em **tipo**:<br /><br /> Nenhuma<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**tipo**|**char(1)**|Tipo de componente de esquema XML.<br /><br /> N = Qualquer tipo (componente intrínseco especial)<br /><br /> Z = Qualquer tipo simples (componente intrínseco especial)<br /><br /> P = Tipo primitivo (tipos intrínsecos)<br /><br /> S = Tipo simples<br /><br /> L = Tipo de lista<br /><br /> U = Tipo de união<br /><br /> C = Tipo simples complexo (derivado de Simples)<br /><br /> K = Tipo complexo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelo<br /><br /> W = Curinga de elemento<br /><br /> A = Atributo<br /><br /> G = Grupo de atributo<br /><br /> V = Curinga de atributo|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Descrição do tipo de componente de esquema XML:<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivação**|**char(1)**|Método de derivação para tipos derivados:<br /><br /> N = Nenhum (não derivado)<br /><br /> X= Extensão<br /><br /> R = Restrição<br /><br /> S = Substituição|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Descrição de método de derivação para tipos derivados:<br /><br /> Nenhuma<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**Int**|ID do componente do qual esse componente é derivado. NULL se não existir nenhuma.|  
|**scoping_xml_component_id**|**Int**|ID exclusiva do componente de escopo. NULL se não existir nenhuma (escopo global).|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;sistema tipo XML&#41; exibições do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
