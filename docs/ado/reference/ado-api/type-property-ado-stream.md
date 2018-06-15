---
title: Tipo de propriedade (fluxo de ADO) | Microsoft Docs
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
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b334a6f6feab4e8a9a491624a5a3a43d2bd333ff
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282765"
---
# <a name="type-property-ado-stream"></a>Propriedade Type (fluxo de ADO)
Indica o tipo de dados contidos no [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) (binários ou texto).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) valor que especifica o tipo de dados contidos no **fluxo** objeto. O valor padrão é **adTypeText**. No entanto, se os dados binários inicialmente são gravados em um novo, vazio **fluxo**, o **tipo** será alterado para **adTypeBinary**.  
  
## <a name="remarks"></a>Remarks  
 O **tipo** propriedade é leitura/gravação somente quando a posição atual está no início do **fluxo** ([posição](../../../ado/reference/ado-api/position-property-ado.md) é 0) e somente leitura em qualquer outra posição.  
  
 O**tipo** propriedade determina quais métodos devem ser usados para ler e gravar o **fluxo**. Para texto **fluxos**, use [ReadText](../../../ado/reference/ado-api/readtext-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md). Para o binário **fluxos**, use [leitura](../../../ado/reference/ado-api/read-method.md) e [gravar](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
