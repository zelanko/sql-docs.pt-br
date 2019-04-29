---
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2740c7fb25b71e3588bebb924ea9d5f907e3560
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910880"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita linhas por *RowDelimiter*, colunas por *ColumnDelimiter*e os valores por nulos *NullExpr*. Esses três parâmetros do [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método são válidas somente com um *StringFormat* dos **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
