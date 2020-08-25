---
description: PositionEnum
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
ms.openlocfilehash: 2d7b443e94f3bea5977aeaf953e84c66c826daeb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773165"
---
# <a name="positionenum"></a>PositionEnum
Especifica a posição atual do ponteiro de registro em um [conjunto de registros](./recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que o ponteiro de registro atual está em BOF (ou seja, a propriedade [BOF](./bof-eof-properties-ado.md) é **true**).|  
|**adPosEOF**|-3|Indica que o ponteiro de registro atual está em EOF (ou seja, a propriedade [EOF](./bof-eof-properties-ado.md) é **true**).|  
|**adPosUnknown**|-1|Indica que o **conjunto de registros** está vazio, se a posição atual é desconhecida ou o provedor não oferece suporte à propriedade [AbsolutePage](./absolutepage-property-ado.md) ou [AbsolutePosition](./absoluteposition-property-ado.md) .|  
  
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
        [Propriedade AbsolutePage (ADO)](./absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [Propriedade AbsolutePosition (ADO)](./absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::