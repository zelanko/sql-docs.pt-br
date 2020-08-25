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
ms.openlocfilehash: 90c6214caa0adc1c11cdc0660b65795624919e51
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777135"
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [conjunto de registros](./recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita as linhas por @ *Delimiter*, colunas por *ColumnDelimiter*e valores nulos por *NullExpr*. Esses três parâmetros do método [GetString](./getstring-method-ado.md) são válidos somente com um *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método GetString (ADO)](./getstring-method-ado.md)