---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1e7e685e9d3f23d4d1c3317e24f63d7bdac23db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730274"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opções para abrir um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser combinados com uma operação OR.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o **Stream** objeto no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo do *fonte* parâmetro já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. O comportamento padrão é tratar *origem* como uma URL que aponte diretamente para um nó em uma estrutura de árvore. O fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura de **Stream** objeto com as opções padrão.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
