---
title: Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d64b63f6aae163e6703f7f2a7074f3c1e543adb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingserviceparameters-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve os parâmetros para os algoritmos no servidor.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DMSCHEMA_MINING_SERVICE_PARAMETERS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|O nome do algoritmo.|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|O nome do parâmetro.|  
|**TIPO_DE_PARÂMETRO**|**DBTYPE_WSTR**|O tipo do parâmetro.|  
|**IS_REQUIRED**|**DBTYPE_BOOL**|Um Booliano que retornará **TRUE** caso o parâmetro seja necessário.|  
|**PARAMETER_FLAGS**|**DBTYPE_UI4**|Uma máscara de bits que descreve as características do parâmetro:<br /><br /> **DM_PARAMETER_TRAINING** (**0x0000001**) indica que o parâmetro é usado para treinamento<br /><br /> **DM_PARAMETER_PREDICTION** (**0x00000002**) indica que o parâmetro é usado para previsão<br /><br /> **DM_PARAMETER_CONTENT** (**0x00000003**) indica que o parâmetro é usado para restrição de conteúdo|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição amigável do parâmetro.|  
|**DEFAULT_VALUE**|**DBTYPE_WSTR**|O valor padrão do parâmetro. Retornará **NULL** se o valor padrão não for um tipo de dados simples.|  
|**VALUE_ENUMERATION**|**DBTYPE_WSTR**|Um enumerador de valores possíveis para o parâmetro.|  
|**HELP_FILE**|**DBTYPE_WSTR**|O nome do arquivo que contém a documentação deste parâmetro.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|A ID de contexto da Ajuda para esta função.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DMSCHEMA_MINING_SERVICE_PARAMETERS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
