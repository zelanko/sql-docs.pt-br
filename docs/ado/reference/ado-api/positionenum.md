---
description: PositionEnum
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a871f6d2f7b73e7430761318a5acee31f05df3c1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990067"
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