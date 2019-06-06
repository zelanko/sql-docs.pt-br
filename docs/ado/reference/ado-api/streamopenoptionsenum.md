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
manager: jroth
ms.openlocfilehash: 091c640ab09cf70cff5e6f7ce3d7bf1dc9dd34ab
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710721"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opções para abrir um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser combinados com uma operação OR.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o **Stream** objeto no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo do *fonte* parâmetro já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. O comportamento padrão é tratar *origem* como uma URL que aponte diretamente para um nó em uma estrutura de árvore. O fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura de **Stream** objeto com as opções padrão.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
