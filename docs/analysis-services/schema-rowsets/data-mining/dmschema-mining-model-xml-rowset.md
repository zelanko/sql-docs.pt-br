---
title: Conjunto de linhas DMSCHEMA_MINING_MODEL_XML | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aa57b1bed12f11bca349630e539510b162700cc1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingmodelxml-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODEL_XML
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**SIZE**|**DBTYPE_UI4**||O número de bytes na cadeia de caracteres XML.|  
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
  
  
