---
title: Propriedade IsolationLevel | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Connection15::IsolationLevel
helpviewer_keywords: IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 116364552e8cbbb7ec1b9fce712c2eaf68f5c64e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="isolationlevel-property"></a>Propriedade IsolationLevel
Indica o nível de isolamento para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) valor. O padrão é **adXactReadCommitted**.  
  
## <a name="remarks"></a>Comentários  
 Use o **IsolationLevel** propriedade para definir o isolamento de nível de um **Conexão** objeto. A configuração não terá efeito até a próxima vez que você chamar o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se o nível de isolamento solicitar estiver disponível, o provedor pode retornar o próximo maior nível de isolamento sem atualizar o **IsolationLevel** propriedade.  
  
 O **IsolationLevel** propriedade é leitura/gravação.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **Conexão** objeto, o **IsolationLevel** propriedade pode ser definida somente como **adXactUnspecified**. Como os usuários estão trabalhando com desconectada **registros** objetos em um cache do lado do cliente, pode haver problemas de multiusuários. Por exemplo, quando dois usuários diferentes tentam atualizar o mesmo registro, serviço de dados remoto simplesmente permite que o usuário que atualiza o registro pela primeira vez "win". Solicitação de atualização do segundo usuário falhará com um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de modo (VB) e IsolationLevel](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Exemplo de propriedades de modo (VC + +) e IsolationLevel](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
