---
description: Propriedade CommandStream (ADO)
title: Propriedade CommandStream (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: rothja
ms.author: jroth
ms.openlocfilehash: 20b52a91429e2db6478aab36f2db5928bc2d30f5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776145"
---
# <a name="commandstream-property-ado"></a>Propriedade CommandStream (ADO)
Indica o fluxo usado como entrada para um objeto de [comando](./command-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna o fluxo usado como entrada para um objeto de **comando** . O formato deste fluxo é específico do provedor; consulte a documentação do provedor para obter detalhes. Essa propriedade é semelhante à propriedade [CommandText](./commandtext-property-ado.md) , que é usada para especificar uma cadeia de caracteres para a entrada de um **comando**.  
  
## <a name="remarks"></a>Comentários  
 **CommandStream** e **CommandText** são mutuamente exclusivos. Quando o usuário define a propriedade **CommandStream** , a propriedade **CommandText** será definida como a cadeia de caracteres vazia (""). Se o usuário definir a propriedade **CommandText** , a propriedade **CommandStream** será definida como **Nothing**.  
  
 Os comportamentos dos métodos **Command. Parameters. Refresh** e **Command. Prepare** são definidos pelo provedor. Os valores dos parâmetros em um fluxo não podem ser atualizados.  
  
 O fluxo de entrada não está disponível para outros objetos ADO que retornam a origem de um **comando**. Por exemplo, se a [origem](./source-property-ado-recordset.md) de um [conjunto de registros](./recordset-object-ado.md) for definida como um objeto de **comando** que tem um fluxo como sua entrada, **Recordset. Source** continuará retornando a propriedade **CommandText** , que contém uma cadeia de caracteres vazia (""), em vez do conteúdo do fluxo da propriedade **CommandStream** .  
  
 Ao usar um fluxo de comando (conforme especificado por **CommandStream**), os únicos valores de [CommandTypeEnum](./commandtypeenum.md) válidos para a propriedade [CommandType](./commandtype-property-ado.md) são **adCmdText** e **adCmdUnknown**. Qualquer outro valor causará erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandText (ADO)](./commandtext-property-ado.md)   
 [Propriedade dialeto](./dialect-property.md)   
 [CommandTypeEnum](./commandtypeenum.md)