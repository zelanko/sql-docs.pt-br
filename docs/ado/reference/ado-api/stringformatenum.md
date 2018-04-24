---
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332a19096035fc271062c8138351197316f46377
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="stringformatenum"></a>StringFormatEnum
Especifica o formato ao recuperar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita linhas por *RowDelimiter*, colunas por *ColumnDelimiter*e valores por nulos *NullExpr*. Esses três parâmetros do [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) método são válidos somente com um *StringFormat* de **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
