---
title: Método Write | Microsoft Docs
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
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f05ef9a599711493c4efaa50d7f9ecbc3a078ac4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="write-method"></a>Método Write
Grava dados binários em uma [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Buffer*  
 Um **Variant** que contém uma matriz de bytes a serem gravados.  
  
## <a name="remarks"></a>Remarks  
 Bytes especificados são gravados para o **fluxo** objeto sem espaços entre cada byte intermediários.  
  
 Atual [posição](../../../ado/reference/ado-api/position-property-ado.md) é definido como os bytes após os dados gravados. O **gravar** método não trunca o restante dos dados em um fluxo. Se você deseja truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se você gravar depois atual [EOS](../../../ado/reference/ado-api/eos-property.md) posição, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) do **fluxo** aumenta para conter qualquer nova bytes, e **EOS** será movido para o último byte novo no **fluxo**.  
  
> [!NOTE]
>  O **gravar** método é usado com fluxos binários ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeBinary**). Para fluxos de texto (**tipo** é **adTypeText**), use [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
