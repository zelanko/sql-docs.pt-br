---
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68aaa0bfb8aa72c9e94a8b5db65768fe85895f0e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917747"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
Especifica se o [parâmetro](../../../ado/reference/ado-api/parameter-object.md) representa um parâmetro de entrada, um parâmetro de saída, um parâmetro de entrada e de saída ou o valor de retorno de um procedimento armazenado.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|Padrão. Indica que o parâmetro representa um parâmetro de entrada.|  
|**adParamInputOutput**|3|Indica que o parâmetro representa um parâmetro de entrada e saída.|  
|**adParamOutput**|2|Indica que o parâmetro representa um parâmetro de saída.|  
|**adParamReturnValue**|4|Indica que o parâmetro representa um valor de retorno.|  
|**adParamUnknown**|0|Indica que a direção do parâmetro é desconhecida.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Propriedade Direction](../../../ado/reference/ado-api/direction-property.md)|
