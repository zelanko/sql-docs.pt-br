---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afee71d4f37e2b3a27247fbeacf51dab66cc1e23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933283"
---
# <a name="cursorlocation-property-ado"></a>Propriedade CursorLocation (ADO)
Indica o local do serviço de cursor.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor que pode ser definido como um dos [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade permite que você escolha entre várias bibliotecas de cursor acessíveis para o provedor. Normalmente, você pode escolher entre usar uma biblioteca de cursores do lado do cliente ou um que está localizado no servidor.  
  
 Essa configuração de propriedade afeta conexões estabelecidas somente depois que a propriedade foi definida. Alterando a **CursorLocation** propriedade não tem nenhum efeito sobre conexões existentes.  
  
 Cursores retornados pela [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método herdarão essa configuração. **Conjunto de registros** objetos herdará automaticamente essa configuração de suas conexões associadas.  
  
 Essa propriedade é leitura/gravação em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou um fechado [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e somente leitura em um aberto **conjunto de registros**.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **conjunto de registros** ou **Conexão** objeto, o **CursorLocation** propriedade só pode ser definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
