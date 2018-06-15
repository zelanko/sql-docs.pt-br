---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f6cba75e0e4a2bf164c36f65c9e5fe58d81b1e4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281565"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica a direção de uma pesquisa de registro em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Parando no início de pesquisas com versões anteriores, o **registros**. Se uma correspondência não for encontrada, o ponteiro do registro é posicionado na [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Procura de mensagens, parando no final de **registros**. Se uma correspondência não for encontrada, o ponteiro do registro é posicionado na [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
