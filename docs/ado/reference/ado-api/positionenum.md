---
title: PositionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: PositionEnum
helpviewer_keywords: PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36461d4d522a6bed7b09de6580232ec4cbd9306d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="positionenum"></a>PositionEnum
Especifica a posição atual do ponteiro do registro dentro de uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que o ponteiro do registro atual está no BOF (ou seja, o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é de propriedade **True**).|  
|**adPosEOF**|-3|Indica que o ponteiro do registro atual está no EOF (ou seja, o [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é de propriedade **True**).|  
|**adPosUnknown**|-1|Indica que o **registros** está vazia, a posição atual é desconhecida ou o provedor não oferece suporte a [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) ou [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propriedade.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Propriedade AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[Propriedade AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
