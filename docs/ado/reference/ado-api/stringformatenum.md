---
description: StringFormatEnum
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
ms.openlocfilehash: d7831d7be2df28d31c88216e67e16efbf611b858
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441778"
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
