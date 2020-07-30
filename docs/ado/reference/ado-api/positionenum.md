---
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a61dae9888628302da3326a1465f4182c49e39c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243217"
---
# <a name="positionenum"></a>PositionEnum
Especifica a posição atual do ponteiro de registro em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que o ponteiro de registro atual está em BOF (ou seja, a propriedade [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **true**).|  
|**adPosEOF**|-3|Indica que o ponteiro de registro atual está em EOF (ou seja, a propriedade [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é **true**).|  
|**adPosUnknown**|-1|Indica que o **conjunto de registros** está vazio, se a posição atual é desconhecida ou o provedor não oferece suporte à propriedade [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) ou [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) .|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::
