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
author: rothja
ms.author: jroth
ms.openlocfilehash: 67814e1236bc10e9b008d1684586796dd62950b4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759552"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita as linhas por @ *Delimiter*, colunas por *ColumnDelimiter*e valores nulos por *NullExpr*. Esses três parâmetros do método [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) são válidos somente com um *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
