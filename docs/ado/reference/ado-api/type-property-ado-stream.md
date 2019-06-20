---
title: Tipo de propriedade (ADO Stream) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c8cad8d669452fb5d3bdff154cd7c07239f25044
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710882"
---
# <a name="type-property-ado-stream"></a>Propriedade Type (Fluxo ADO)
Indica o tipo de dados contidos na [Stream](../../../ado/reference/ado-api/stream-object-ado.md) (binários ou texto).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) que especifica o tipo de dados contido no valor de **Stream** objeto. O valor padrão é **adTypeText**. No entanto, se inicialmente, os dados binários são gravados em um novo, vazio **Stream**, o **tipo** será alterado para **adTypeBinary**.  
  
## <a name="remarks"></a>Comentários  
 O **tipo** propriedade é leitura/gravação somente quando a posição atual está no início do **Stream** ([posição](../../../ado/reference/ado-api/position-property-ado.md) é 0) e somente leitura em nenhuma outra posição.  
  
 O**tipo** propriedade determina quais métodos devem ser usados para ler e gravar o **Stream**. Para texto **Streams**, use [ReadText](../../../ado/reference/ado-api/readtext-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md). Para binário **Streams**, use [leitura](../../../ado/reference/ado-api/read-method.md) e [gravar](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
