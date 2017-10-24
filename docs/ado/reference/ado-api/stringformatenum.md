---
title: StringFormatEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 86a1f884f237596895dce6671d3dc42fb6461b1e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita linhas por *RowDelimiter*, colunas por *ColumnDelimiter*e valores por nulos *NullExpr*. Esses três parâmetros do [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método são válidos somente com um *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)

