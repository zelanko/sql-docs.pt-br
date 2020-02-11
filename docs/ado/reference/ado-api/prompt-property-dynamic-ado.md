---
title: Propriedade do prompt – dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931574"
---
# <a name="prompt-property-dynamic-ado"></a>Solicitar a propriedade dinâmica (ADO)
Especifica se o provedor de OLE DB deve solicitar informações de inicialização ao usuário.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um valor de [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) .  
  
## <a name="remarks"></a>Comentários  
 **Prompt** é uma propriedade dinâmica, que pode ser anexada à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) pelo provedor de OLE DB. Para solicitar informações de inicialização, os provedores de OLE DB normalmente exibirão uma caixa de diálogo para o usuário.  
  
 As propriedades dinâmicas de um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) são perdidas quando a **conexão** é fechada. A propriedade **prompt** deve ser redefinida antes de reabrir a **conexão** para usar um valor diferente do padrão.  
  
> [!NOTE]
>  Não especifique que o provedor deve solicitar ao usuário cenários em que o usuário não poderá responder à caixa de diálogo. Por exemplo, o usuário não poderá responder se o aplicativo estiver em execução em um sistema de servidor em vez de no cliente do usuário, ou se o aplicativo estiver sendo executado em um sistema sem usuário conectado. Nesses casos, o aplicativo aguardará indefinidamente uma resposta e parecerá bloquear.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
