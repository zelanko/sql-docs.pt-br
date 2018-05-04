---
title: SearchDirectionEnum | Microsoft Docs
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
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f354c2069a1862a1b4d6b69b4db78516a292405
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica a direção de uma pesquisa de registro em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Description|  
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
