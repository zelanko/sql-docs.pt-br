---
title: StreamReadEnum | Microsoft Docs
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
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32b606d6f960dc77f8d90257b8c18d19703620d9
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="streamreadenum"></a>StreamReadEnum
Especifica se o fluxo inteiro ou a próxima linha deve ser lidos de um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Padrão. Lê todos os bytes do fluxo, a partir da posição atual em diante, para o [EOS](../../../ado/reference/ado-api/eos-property.md) marcador. Isso é somente válido **StreamReadEnum** valor com fluxos binários ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeBinary**).|  
|**adReadLine**|-2|Lê a próxima linha do fluxo (designado pelo [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) propriedade).|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Read](../../../ado/reference/ado-api/read-method.md)|[Método ReadText](../../../ado/reference/ado-api/readtext-method.md)|
