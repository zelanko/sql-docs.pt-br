---
title: Solicitar a propriedade dinâmica (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 4f2c778a6e922477cd8b21251a638d430ce15480
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703160"
---
# <a name="prompt-property-dynamic-ado"></a>Solicitar a propriedade dinâmica (ADO)
Especifica se o provedor OLE DB deve solicitar ao usuário para informações de inicialização.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define e retorna um [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 **Prompt** é uma propriedade dinâmica, que pode ser acrescentada ao [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção pelo provedor OLE DB. Para solicitar informações de inicialização, provedores OLE DB geralmente exibirá uma caixa de diálogo para o usuário.  
  
 Propriedades dinâmicas de uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto serão perdidos quando o **Conexão** está fechado. O **Prompt** propriedade deve ser redefinida antes de abrir novamente o **Conexão** para usar um valor diferente do padrão.  
  
> [!NOTE]
>  Não especifique que o provedor deve solicitar ao usuário em cenários em que o usuário não será capaz de responder à caixa de diálogo. Por exemplo, o usuário não será capaz de responder se o aplicativo está em execução em um sistema de servidor, em vez de no cliente do usuário, ou se o aplicativo está em execução em um sistema com nenhum usuário fez logon. Nesses casos, o aplicativo irá esperar indefinidamente por uma resposta e parece travar.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
