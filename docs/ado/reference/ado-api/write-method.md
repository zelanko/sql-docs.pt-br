---
title: Método Write | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84e10e8edb6cca3c4e56ac1dd0106b3c641af872
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67945902"
---
# <a name="write-method"></a>Método Write
Grava dados binários em um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Buffer*  
 Uma **variante** que contém uma matriz de bytes a ser gravado.  
  
## <a name="remarks"></a>Comentários  
 Os bytes especificados são gravados no objeto de **fluxo** sem nenhum espaço intermediário entre cada byte.  
  
 A [posição](../../../ado/reference/ado-api/position-property-ado.md) atual é definida como o byte após os dados gravados. O método **Write** não trunca o restante dos dados em um fluxo. Se você quiser truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se você gravar após a posição de [EOS](../../../ado/reference/ado-api/eos-property.md) atual, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) do **fluxo** será aumentado para conter os novos bytes e o **EOS** será movido para o novo último byte no **fluxo**.  
  
> [!NOTE]
>  O método **Write** é usado com fluxos binários (o[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeBinary**). Para fluxos de texto (o**tipo** é **adTypeText**), use [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
