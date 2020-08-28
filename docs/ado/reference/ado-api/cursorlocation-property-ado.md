---
description: Propriedade CursorLocation (ADO)
title: Propriedade CursorLocation (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 121aeef137946152a82808c8a439f2e5d03a2c94
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974457"
---
# <a name="cursorlocation-property-ado"></a>Propriedade CursorLocation (ADO)
Indica o local do serviço de cursor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que pode ser definido como um dos valores de [CursorLocationEnum](./cursorlocationenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade permite que você escolha entre várias bibliotecas de cursores acessíveis ao provedor. Normalmente, você pode escolher entre usar uma biblioteca de cursores do lado do cliente ou uma que esteja localizada no servidor.  
  
 Essa configuração de propriedade afeta as conexões estabelecidas somente após a definição da propriedade. A alteração da propriedade **CursorLocation** não tem nenhum efeito nas conexões existentes.  
  
 Os cursores retornados pelo método [Execute](./execute-method-ado-connection.md) herdam essa configuração. Os objetos **Recordset** herdarão automaticamente essa configuração de suas conexões associadas.  
  
 Essa propriedade é leitura/gravação em uma [conexão](./connection-object-ado.md) ou um [conjunto de registros](./recordset-object-ado.md)fechado e somente leitura em um **conjunto de registros**aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um **conjunto de registros** do lado do cliente ou objeto de **conexão** , a propriedade **CursorLocation** só pode ser definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Connection (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)