---
title: Método SetEOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0db8c7972d6b647cdd021d43dbb3cdee1ba0452
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63314741"
---
# <a name="seteos-method"></a>Método SetEOS
Define a posição em que é o final do fluxo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Comentários  
 **SetEOS** atualiza o valor da [EOS](../../../ado/reference/ado-api/eos-property.md) propriedade fazendo atual [posição](../../../ado/reference/ado-api/position-property-ado.md) o final do fluxo. Qualquer bytes ou caracteres após a posição atual são truncados.  
  
 Porque [escrever](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), e [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) nenhum valor extra existente não truncar **Stream** objetos, é possível truncar esses bytes ou caracteres definindo a nova posição final do fluxo com **SetEOS**.  
  
> [!CAUTION]
>  Se você definir **EOS** para uma posição antes do final do fluxo real, você perderá todos os dados depois que o novo **EOS** posição.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
