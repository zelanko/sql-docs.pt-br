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
author: rothja
ms.author: jroth
ms.openlocfilehash: c109ea1c44fc44a4cdbb585e2c612ebf8c9b2909
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242602"
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

:::row:::
    :::column:::
        [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Propriedade Direction](../../../ado/reference/ado-api/direction-property.md)  
    :::column-end:::
:::row-end:::
