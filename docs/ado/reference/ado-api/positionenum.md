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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d5f7ca47177a953313ff983bb25f9178b73b4930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917600"
---
# <a name="positionenum"></a>PositionEnum
Especifica a posição atual do ponteiro do registro dentro de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica que o ponteiro de registro atual é de BOF (ou seja, o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é de propriedade **verdadeiro**).|  
|**adPosEOF**|-3|Indica que o ponteiro de registro atual é de EOF (ou seja, o [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) é de propriedade **verdadeiro**).|  
|**adPosUnknown**|-1|Indica que o **conjunto de registros** está vazio, a posição atual é desconhecida ou o provedor não dá suporte a [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) ou [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propriedade.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
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
