---
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f66aebdd140d1ce3fe505dfd40fd5f412de7cd9
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280565"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Especifica se o [parâmetro](../../../ado/reference/ado-api/parameter-object.md) representa um parâmetro de entrada, um parâmetro de saída, uma entrada e um parâmetro de saída, ou o valor de retorno de um procedimento armazenado.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Padrão. Indica que o parâmetro representa um parâmetro de entrada.|  
|**adParamInputOutput**|3|Indica que o parâmetro representa um parâmetro de entrada e saído.|  
|**adParamOutput**|2|Indica que o parâmetro representa um parâmetro de saída.|  
|**adParamReturnValue**|4|Indica que o parâmetro representa um valor de retorno.|  
|**adParamUnknown**|0|Indica que a direção do parâmetro é desconhecida.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Propriedade Direction](../../../ado/reference/ado-api/direction-property.md)|
