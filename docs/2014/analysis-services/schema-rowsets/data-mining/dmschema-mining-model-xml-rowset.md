---
title: Conjunto de linhas DMSCHEMA_MINING_MODEL_XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_XML
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_XML rowset
ms.assetid: f58b00e9-3f72-4cff-b448-21a9fb529772
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3be57336379c66577c245a891e047ec95f763fd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130816"
---
# <a name="dmschemaminingmodelxml-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODEL_XML
  Retorna a estrutura XML do modelo de mineração. O formato da cadeia de caracteres XML segue o padrão PMML (Predictive Model Markup Language) 2.1.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_MODEL_XML` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||O nome do catálogo. Preenchido com o nome do banco de dados do qual o modelo é membro.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||O nome do modelo. Esta coluna não pode conter `NULL`.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||O tipo de modelo. É uma cadeia de caracteres específica do provedor. Ele pode ser `NULL`.|  
|`MODEL_GUID`|`DBTYPE_GUID`||O GUID que identifica o modelo. Os provedores que não usam GUIDs para identificar tabelas retornam `NULL`.|  
|`MODEL_PMML`|`DBTYPE_WSTR`||Uma representação XML do conteúdo do modelo em formato de PMML.|  
|`SIZE`|`DBTYPE_UI4`||O número de bytes na cadeia de caracteres XML.|  
|`LOCATION`|`DBTYPE_WSTR`||O local do arquivo XML. Será `NULL` se um arquivo físico não for usado para armazenamento.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas de DMSCHEMA_MINING_MODEL_XML pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_W`STR|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
