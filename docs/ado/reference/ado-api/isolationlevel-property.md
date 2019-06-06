---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e027e325ec27bf5a80cf4df85afcfe59656ce3c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697589"
---
# <a name="isolationlevel-property"></a>Propriedade IsolationLevel
Indica o nível de isolamento para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) valor. O padrão é **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentários  
 Use o **IsolationLevel** propriedade para definir o isolamento de nível de uma **Conexão** objeto. A configuração não terá efeito até a próxima vez que você chamar o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se o nível de isolamento é solicitar estiver indisponível, o provedor pode retornar o próximo nível maior de isolamento sem atualizar o **IsolationLevel** propriedade.  
  
 O **IsolationLevel** propriedade é leitura/gravação.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **Conexão** objeto, o **IsolationLevel** propriedade pode ser definida somente como **adXactUnspecified**. Como os usuários estão trabalhando com desconectada **Recordset** objetos em um cache do lado do cliente, pode haver problemas de multiusuários. Por exemplo, quando dois usuários diferentes tentam atualizar o mesmo registro, serviço de dados remotos simplesmente permite que o usuário que atualiza o registro primeiro "win". Solicitação de atualização do segundo usuário falhará com um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [IsolationLevel e exemplo de propriedades de modo (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel e modo propriedades (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
