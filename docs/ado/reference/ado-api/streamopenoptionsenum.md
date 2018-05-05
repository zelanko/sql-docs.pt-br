---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2594a0a2095d49a0819b21967ee7e2a45c8337c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opções para abrir um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser combinados com uma operação OR.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o **fluxo** objeto no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo a *fonte* parâmetro seja já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. O comportamento padrão é tratar *fonte* como uma URL que aponta diretamente para um nó em uma estrutura de árvore. Fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura de **fluxo** objeto com as opções padrão.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
