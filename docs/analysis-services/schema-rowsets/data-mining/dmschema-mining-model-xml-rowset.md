---
title: Conjunto de linhas DMSCHEMA_MINING_MODEL_XML | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_XML
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_XML rowset
ms.assetid: f58b00e9-3f72-4cff-b448-21a9fb529772
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0d508a1bc916d75ff33e5aba19c6306a547af8fb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingmodelxml-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODEL_XML
  Retorna a estrutura XML do modelo de mineração. O formato da cadeia de caracteres XML segue o padrão PMML (Predictive Model Markup Language) 2.1.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DMSCHEMA_MINING_MODEL_XML** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||O nome do catálogo. Preenchido com o nome do banco de dados do qual o modelo é membro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**||O nome do modelo. Esta coluna não pode conter **NULL**.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||O tipo de modelo. É uma cadeia de caracteres específica do provedor. Pode ser **NULL**.|  
|**MODEL_GUID**|**DBTYPE_GUID**||O GUID que identifica o modelo. Os provedores que não usam GUIDs para identificar tabelas retornam **NULL**.|  
|**MODEL_PMML**|**DBTYPE_WSTR**||Uma representação XML do conteúdo do modelo em formato de PMML.|  
|**TAMANHO**|**DBTYPE_UI4**||O número de bytes na cadeia de caracteres XML.|  
|**LOCAL**|**DBTYPE_WSTR**||O local do arquivo XML. Será **NULL** se um arquivo físico não for usado para armazenamento.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas de DMSCHEMA_MINING_MODEL_XML pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_W**STR|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

