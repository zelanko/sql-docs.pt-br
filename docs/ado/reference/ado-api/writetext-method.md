---
title: Método WriteText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2b12293935df6f9afaf6a1691e2decce3f6c6f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="writetext-method"></a>Método WriteText
Grava uma cadeia de caracteres de texto especificado para um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Dados*  
 Um **cadeia de caracteres** valor que contém o texto em caracteres a serem gravados.  
  
 *Opções*  
 Opcional. Um [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) valor que especifica se um caractere de separador de linha deve ser gravado no final da cadeia de caracteres especificada.  
  
## <a name="remarks"></a>Remarks  
 Cadeias de caracteres especificadas são gravadas para o **fluxo** objeto sem espaços ou caracteres entre cada cadeia de caracteres.  
  
 Atual [posição](../../../ado/reference/ado-api/position-property-ado.md) é definido como o caractere após os dados gravados. O **WriteText** método não trunca o restante dos dados em um fluxo. Se você deseja truncar esses caracteres, chamar [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se você gravar depois atual [EOS](../../../ado/reference/ado-api/eos-property.md) posição, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) do **fluxo** aumenta para conter caracteres de nova e **EOS** será movido para o último byte novo no **fluxo**.  
  
> [!NOTE]
>  O **WriteText** método é usado com fluxos de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Para fluxos binários (**tipo** é **adTypeBinary**), use [gravar](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Write](../../../ado/reference/ado-api/write-method.md)
