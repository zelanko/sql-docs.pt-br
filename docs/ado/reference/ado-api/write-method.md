---
title: Método de gravação | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945902"
---
# <a name="write-method"></a>Método Write
Grava dados binários em uma [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *buffer*  
 Um **Variant** que contém uma matriz de bytes a serem gravados.  
  
## <a name="remarks"></a>Comentários  
 Bytes especificados são gravados para o **Stream** objeto sem espaços entre cada byte intermediários.  
  
 O atual [posição](../../../ado/reference/ado-api/position-property-ado.md) é definido como o byte após os dados gravados. O **gravar** método não trunca o restante dos dados em um fluxo. Se você deseja truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se você gravar depois atual [EOS](../../../ado/reference/ado-api/eos-property.md) posição, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) dos **Stream** aumenta para conter qualquer nova bytes, e **EOS** será movido para o novo último byte na **Stream**.  
  
> [!NOTE]
>  O **escrever** método é usado com fluxos binários ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) está **adTypeBinary**). Para fluxos de texto (**tipo** é **adTypeText**), use [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
