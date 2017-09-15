---
title: A propriedade CommandStream (ADO) | Microsoft Docs
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
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28e4c73b4fdc94be1687ec011ad3a42e5b51bd78
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="commandstream-property-ado"></a>Propriedade CommandStream (ADO)
Indica o fluxo usado como entrada para uma [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna o fluxo usado como entrada para uma **comando** objeto. O formato para esse fluxo é específica do provedor; Consulte a documentação do provedor para obter detalhes. Esta propriedade é semelhante de [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade usada para especificar uma cadeia de caracteres para a entrada de um **comando**.  
  
## <a name="remarks"></a>Comentários  
 **CommandStream** e **CommandText** são mutuamente exclusivos. Quando o usuário define o **CommandStream** propriedade, o **CommandText** propriedade será definida como a cadeia de caracteres vazia (""). Se o usuário define o **CommandText** propriedade, o **CommandStream** propriedade será definida como **nada**.  
  
 Os comportamentos do **Command.Parameters.Refresh** e **Command.Prepare** métodos são definidos pelo provedor. Os valores dos parâmetros em um fluxo não podem ser atualizados.  
  
 O fluxo de entrada não está disponível para outros objetos de ADO que retornam a origem de um **comando**. Por exemplo, se o [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) é definido como um **comando** objeto que tem um fluxo como entrada, **Recordset.Source** continua a retornar o **CommandText** propriedade, que contém uma cadeia de caracteres vazia (""), em vez do conteúdo de fluxo do **CommandStream** propriedade.  
  
 Ao usar um fluxo de comando (conforme especificado por **CommandStream**), válido apenas [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores para o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) são de propriedade ** adCmdText** e **adCmdUnknown**. Qualquer outro valor causará um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade Dialect](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
