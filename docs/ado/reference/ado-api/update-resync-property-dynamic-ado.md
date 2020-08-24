---
description: Atualizar propriedade dinâmica de ressincronização (ADO)
title: Atualizar propriedade de ressincronização-dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 52884baca793ae9f5cb7b849c9f50d2399f0cf5e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777005"
---
# <a name="update-resync-property-dynamic-ado"></a>Atualizar propriedade dinâmica de ressincronização (ADO)
Especifica se o método [UpdateBatch](./updatebatch-method.md) é seguido por uma operação de método de [ressincronização](./resync-method.md) implícita e, nesse caso, o escopo dessa operação.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um ou mais dos valores de [ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md) .  
  
## <a name="remarks"></a>Comentários  
 Os valores de ADCPROP_UPDATERESYNC_ENUM podem ser combinados, exceto para adResyncAll que já representa a combinação do restante dos valores.  
  
 A constante **adResyncConflicts** armazena os valores de ressincronização como valores subjacentes, mas não substitui as alterações pendentes.  
  
 **Atualizar ressincronização** é uma propriedade dinâmica acrescentada à coleção de [Propriedades](./properties-collection-ado.md) do objeto [Recordset](./recordset-object-ado.md) quando a propriedade [CursorLocation](./cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)