---
title: "Solicitar a propriedade dinâmica (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 065656ea3023b1526573a48cd6d7d21eee6f6179
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="prompt-property-dynamic-ado"></a>Solicitar a propriedade dinâmica (ADO)
Especifica se o provedor OLE DB deve solicitar ao usuário informações de inicialização.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 **Prompt** é uma propriedade dinâmica, que pode ser anexada ao [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção pelo provedor OLE DB. Para solicitar informações de inicialização, provedores OLE DB geralmente exibirá uma caixa de diálogo para o usuário.  
  
 Propriedades dinâmicas de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto serão perdidas quando o **Conexão** está fechado. O **Prompt** propriedade deve ser redefinida antes de abrir novamente o **Conexão** para usar um valor diferente do padrão.  
  
> [!NOTE]
>  Não especifique que o provedor deve solicitar ao usuário em cenários em que o usuário não será capaz de responder à caixa de diálogo. Por exemplo, o usuário não será capaz de responder se o aplicativo é executado em um sistema de servidor em vez de no cliente do usuário, ou se o aplicativo é executado em um sistema com nenhum usuário fez logon. Nesses casos, o aplicativo espere indefinidamente uma resposta e parece ser bloqueado.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
