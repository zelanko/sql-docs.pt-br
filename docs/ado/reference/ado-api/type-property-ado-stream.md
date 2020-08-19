---
description: Propriedade Type (Fluxo ADO)
title: Propriedade Type (fluxo ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd1519092d72f8a562bb266d2aa6d547d8e37df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441728"
---
# <a name="type-property-ado-stream"></a>Propriedade Type (Fluxo ADO)
Indica o tipo de dados contidos no [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) (binário ou texto).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) que especifica o tipo de dados contidos no objeto de **fluxo** . O valor padrão é **adTypeText**. No entanto, se os dados binários forem gravados inicialmente em um **fluxo**novo e vazio, o **tipo** será alterado para **adTypeBinary**.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **Type** é somente leitura/gravação quando a posição atual está no início do **fluxo** (a[posição](../../../ado/reference/ado-api/position-property-ado.md) é 0) e somente leitura em qualquer outra posição.  
  
 A propriedade**Type** determina quais métodos devem ser usados para ler e gravar o **fluxo**. Para **fluxos**de texto, use [READTEXT](../../../ado/reference/ado-api/readtext-method.md) e [WriteText](../../../ado/reference/ado-api/writetext-method.md). Para **fluxos**binários, use [leitura](../../../ado/reference/ado-api/read-method.md) e [gravação](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
