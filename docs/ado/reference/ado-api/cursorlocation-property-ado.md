---
description: Propriedade CursorLocation (ADO)
title: Propriedade CursorLocation (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: rothja
ms.author: jroth
ms.openlocfilehash: 92567057acad1edb0a0571a0057a11a47a3c65d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444298"
---
# <a name="cursorlocation-property-ado"></a>Propriedade CursorLocation (ADO)
Indica o local do serviço de cursor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que pode ser definido como um dos valores de [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade permite que você escolha entre várias bibliotecas de cursores acessíveis ao provedor. Normalmente, você pode escolher entre usar uma biblioteca de cursores do lado do cliente ou uma que esteja localizada no servidor.  
  
 Essa configuração de propriedade afeta as conexões estabelecidas somente após a definição da propriedade. A alteração da propriedade **CursorLocation** não tem nenhum efeito nas conexões existentes.  
  
 Os cursores retornados pelo método [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) herdam essa configuração. Os objetos **Recordset** herdarão automaticamente essa configuração de suas conexões associadas.  
  
 Essa propriedade é leitura/gravação em uma [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)fechado e somente leitura em um **conjunto de registros**aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um **conjunto de registros** do lado do cliente ou objeto de **conexão** , a propriedade **CursorLocation** só pode ser definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
