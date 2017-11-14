---
title: Propriedade CursorLocation (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6679a7a8a83f954039587776e5e668bd5ed05365
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="cursorlocation-property-ado"></a>Propriedade CursorLocation (ADO)
Indica o local do serviço de cursor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que pode ser definido como uma da [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade permite que você escolha entre várias bibliotecas de cursor acessíveis para o provedor. Normalmente, você pode escolher entre usar uma biblioteca de cursores do lado do cliente ou que está localizado no servidor.  
  
 Essa configuração de propriedade afeta conexões estabelecidas somente depois que a propriedade foi definida. Alterando o **CursorLocation** propriedade não tem efeito sobre conexões existentes.  
  
 Cursores retornados pelo [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método herdam essa configuração. **Conjunto de registros** objetos herdarão automaticamente essa configuração de suas conexões associadas.  
  
 Esta propriedade é leitura/gravação em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou um [registros](../../../ado/reference/ado-api/recordset-object-ado.md)e somente leitura em um aberto **registros**.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **registros** ou **Conexão** objeto, o **CursorLocation** propriedade só pode ser definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)

