---
title: Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9079be52d50da3a400496dc602166c857f2b1691
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117521"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS
  Descreve os parâmetros para os algoritmos no servidor.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_SERVICE_PARAMETERS` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||O nome do algoritmo.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||O nome do parâmetro.|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||O tipo do parâmetro.|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||Um Booliano que retornará `TRUE` caso o parâmetro seja necessário.|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||Uma máscara de bits que descreve as características do parâmetro:<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) indica que o parâmetro é usado para treinamento<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) indica que o parâmetro é usado para previsão<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) indica que o parâmetro é usado para a restrição de conteúdo|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável do parâmetro.|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||O valor padrão do parâmetro. Retornará `NULL` se o valor padrão não for um tipo de dados simples.|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||Um enumerador de valores possíveis para o parâmetro.|  
|`HELP_FILE`|`DBTYPE_WSTR`||O nome do arquivo que contém a documentação deste parâmetro.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||A ID de contexto da Ajuda para esta função.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DMSCHEMA_MINING_SERVICE_PARAMETERS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  