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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dbe2846674d760163fa9eb3ab78e07e68b80d0e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759892"
---
# <a name="seteos-method"></a>Método SetEOS
Define a posição que é o final do fluxo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Comentários  
 **SetEOS** atualiza o valor da propriedade [EOS](../../../ado/reference/ado-api/eos-property.md) , tornando a [posição](../../../ado/reference/ado-api/position-property-ado.md) atual o final do fluxo. Todos os bytes ou caracteres após a posição atual são truncados.  
  
 Como [Write](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md)e [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) não truncam nenhum valor extra em objetos de **fluxo** existentes, você pode truncar esses bytes ou caracteres definindo a nova posição de fim de fluxo com **SetEOS**.  
  
> [!CAUTION]
>  Se você definir **EOS** como uma posição anterior à extremidade real do fluxo, perderá todos os dados após a nova posição de **EOS** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
