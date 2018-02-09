---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e234d22e68d90819d73702542f7d3763ddd2f8c3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opções para abrir um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser combinados com uma operação OR.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o **fluxo** objeto no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo a *fonte* parâmetro seja já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. O comportamento padrão é tratar *fonte* como uma URL que aponta diretamente para um nó em uma estrutura de árvore. Fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura de **fluxo** objeto com as opções padrão.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
