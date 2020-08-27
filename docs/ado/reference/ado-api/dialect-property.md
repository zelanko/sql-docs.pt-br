---
description: Propriedade Dialect
title: Propriedade do dialeto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: rothja
ms.author: jroth
ms.openlocfilehash: be93ceb76aa0aadba5b28673c16704b0881186f9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973897"
---
# <a name="dialect-property"></a>Propriedade Dialect
Indica o dialeto das propriedades [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) ou [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) . O dialeto define a sintaxe e as regras gerais que o provedor usa para analisar a cadeia de caracteres ou o fluxo.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 A propriedade **Dialect** contém um GUID válido que representa o dialeto do texto do comando ou do fluxo. O valor padrão para essa propriedade é {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}, que indica que o provedor deve escolher como interpretar o texto do comando ou o fluxo.  
  
## <a name="remarks"></a>Comentários  
 O ADO não consulta o provedor quando o usuário lê o valor dessa propriedade; Ele retorna uma representação de cadeia de caracteres do valor atualmente armazenado no objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) .  
  
 Quando o usuário definir a propriedade **Dialect** , o ADO validará o GUID e gerará um erro se o valor fornecido não for um GUID válido. Consulte a documentação do seu provedor para determinar os valores de GUID com suporte pela propriedade **Dialect** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)
