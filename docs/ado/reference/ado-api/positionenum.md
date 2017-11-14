---
title: PositionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3f317b92d138f020a43f26d71cbadd0f0cd412e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

