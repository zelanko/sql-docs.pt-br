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
manager: jroth
ms.openlocfilehash: 37d2ba0834d2a4469d97a36f39677f407a5e61be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710677"
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
