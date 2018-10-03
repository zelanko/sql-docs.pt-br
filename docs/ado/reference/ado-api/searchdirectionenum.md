---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05af48f2edcdcf2c6adc6e3617860fdad38bde7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776151"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica a direção de uma pesquisa de registro dentro de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Parando no início de pesquisas com versões anteriores, o **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro está posicionado em [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Encaminham pesquisas, parando no final de **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro está posicionado em [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
