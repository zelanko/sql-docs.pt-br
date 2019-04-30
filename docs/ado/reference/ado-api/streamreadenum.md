---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26ccabf3e73a67c14e7201f26e4ebf739a6352cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311863"
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica se o fluxo inteiro ou a próxima linha deve ser lidos de um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Padrão. Lê todos os bytes do fluxo, da posição atual em diante, o [EOS](../../../ado/reference/ado-api/eos-property.md) marcador. Isso é somente válido **StreamReadEnum** valor com fluxos binários ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) está **adTypeBinary**).|  
|**adReadLine**|-2|Lê a próxima linha do fluxo (designado pela [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
