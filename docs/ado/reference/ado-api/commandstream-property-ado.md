---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1048e8d243bd19d86d60c3c4f92e4e4b9d137a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828775"
---
# <a name="commandstream-property-ado"></a>Propriedade CommandStream (ADO)
Indica o fluxo usado como entrada para um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna o fluxo usado como entrada para um **comando** objeto. O formato para esse fluxo é específica do provedor; Consulte a documentação do provedor para obter detalhes. Esta propriedade é semelhante para o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade, que é usado para especificar uma cadeia de caracteres para a entrada de uma **comando**.  
  
## <a name="remarks"></a>Comentários  
 **CommandStream** e **CommandText** são mutuamente exclusivos. Quando o usuário define o **CommandStream** propriedade, o **CommandText** propriedade será definida como a cadeia de caracteres vazia (""). Se o usuário define o **CommandText** propriedade, o **CommandStream** propriedade será definida como **nada**.  
  
 Os comportamentos do **Command.Parameters.Refresh** e **Command.Prepare** métodos são definidos pelo provedor. Os valores dos parâmetros em um fluxo não podem ser atualizados.  
  
 O fluxo de entrada não está disponível para outros objetos do ADO que retornam a fonte de um **comando**. Por exemplo, se o [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) de uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) é definido como um **comando** objeto que tem um fluxo como sua entrada **Recordset.Source** continua a retornar os **CommandText** propriedade, que contém uma cadeia de caracteres vazia (""), em vez do conteúdo de fluxo dos **CommandStream** propriedade.  
  
 Ao usar um fluxo de comando (conforme especificado por **CommandStream**), válido apenas [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) os valores para o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) são de propriedade  **adCmdText** e **adCmdUnknown**. Qualquer outro valor causará um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade Dialect](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
