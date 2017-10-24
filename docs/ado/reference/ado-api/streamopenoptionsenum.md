---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 268d495d2163d03244a6bec57762b93a26ab32ea
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opções para abrir um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser combinados com uma operação OR.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o **fluxo** objeto no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo a *fonte* parâmetro seja já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. O comportamento padrão é tratar *fonte* como uma URL que aponta diretamente para um nó em uma estrutura de árvore. Fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura de **fluxo** objeto com as opções padrão.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)

