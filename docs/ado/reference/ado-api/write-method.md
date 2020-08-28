---
description: Método Write
title: Método Write | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 90f67c0804424e15d51cc8538413f3c4464ff775
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987747"
---
# <a name="write-method"></a>Método Write
Grava dados binários em um objeto de [fluxo](./stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Buffer*  
 Uma **variante** que contém uma matriz de bytes a ser gravado.  
  
## <a name="remarks"></a>Comentários  
 Os bytes especificados são gravados no objeto de **fluxo** sem nenhum espaço intermediário entre cada byte.  
  
 A [posição](./position-property-ado.md) atual é definida como o byte após os dados gravados. O método **Write** não trunca o restante dos dados em um fluxo. Se você quiser truncar esses bytes, chame [SetEOS](./seteos-method.md).  
  
 Se você gravar após a posição de [EOS](./eos-property.md) atual, o [tamanho](./size-property-ado-stream.md) do **fluxo** será aumentado para conter os novos bytes e o **EOS** será movido para o novo último byte no **fluxo**.  
  
> [!NOTE]
>  O método **Write** é usado com fluxos binários (o[tipo](./type-property-ado-stream.md) é **adTypeBinary**). Para fluxos de texto (o**tipo** é **adTypeText**), use [WriteText](./writetext-method.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método WriteText](./writetext-method.md)