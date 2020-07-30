---
title: Propriedade Mode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: rothja
ms.author: jroth
ms.openlocfilehash: 3487463bf4a13cc97cbc7cd031e18cef5dccb2a7
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242636"
---
# <a name="mode-property-ado"></a>Propriedade Mode (ADO)
Indica as permissões disponíveis para modificar dados em um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md)ou [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) . O valor padrão para uma **conexão** é **adModeUnknown**. O valor padrão para um objeto de **registro** é **adModeRead**. O valor padrão para um **fluxo** associado a uma fonte subjacente (aberta com uma URL como a origem ou como o **fluxo** padrão de um **registro**) é **adModeRead**. O valor padrão para um **fluxo** não associado a uma fonte subjacente (instanciada na memória) é **adModeUnknown**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Mode** para definir ou retornar as permissões de acesso em uso pelo provedor na conexão atual. Você pode definir a propriedade **modo** somente quando o objeto de **conexão** é fechado.  
  
 Para um objeto de **fluxo** , se o modo de acesso não for especificado, ele será herdado da fonte usada para abrir o objeto de **fluxo** . Por exemplo, se um **fluxo** for aberto a partir de um objeto de **registro** , por padrão ele será aberto no mesmo modo que o **registro**.  
  
 Essa propriedade é de leitura/gravação enquanto o objeto é fechado e é somente leitura enquanto o objeto está aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto de **conexão** do lado do cliente, a propriedade **Mode** só pode ser definida como **adModeUnknown**.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades IsolationLevel e Mode (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Exemplo das propriedades IsolationLevel e Mode (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
