---
description: Propriedade IsolationLevel
title: Propriedade IsolationLevel | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: rothja
ms.author: jroth
ms.openlocfilehash: f46199512521e6fe6fda6dc40fe894ba113c0229
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774715"
---
# <a name="isolationlevel-property"></a>Propriedade IsolationLevel
Indica o nível de isolamento para um objeto de [conexão](./connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [IsolationLevelEnum](./isolationlevelenum.md) . O padrão é **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **IsolationLevel** para definir o nível de isolamento de um objeto de **conexão** . A configuração não entrará em vigor até a próxima vez que você chamar o método [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) . Se o nível de isolamento solicitado não estiver disponível, o provedor poderá retornar o próximo nível maior de isolamento sem Atualizar a propriedade **IsolationLevel** .  
  
 A propriedade **IsolationLevel** é leitura/gravação.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto de **conexão** do lado do cliente, a propriedade **IsolationLevel** só pode ser definida como **adXactUnspecified**. Como os usuários estão trabalhando com objetos **Recordset** desconectados em um cache do lado do cliente, pode haver problemas de multiusuário. Por exemplo, quando dois usuários diferentes tentam atualizar o mesmo registro, o serviço de dados remoto simplesmente permite que o usuário que atualiza o registro primeiro seja "win". A solicitação de atualização do segundo usuário falhará com um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades IsolationLevel e Mode (VB)](./isolationlevel-and-mode-properties-example-vb.md)   
 [Exemplo das propriedades IsolationLevel e Mode (VC + +)](./isolationlevel-and-mode-properties-example-vc.md)