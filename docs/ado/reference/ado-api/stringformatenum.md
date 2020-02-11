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
ms.openlocfilehash: 85bef64902f014e7b5269d6df328128bc8fe8d6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937889"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita as linhas por @ *Delimiter*, colunas por *ColumnDelimiter*e valores nulos por *NullExpr*. Esses três parâmetros do método [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) são válidos somente com um *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
