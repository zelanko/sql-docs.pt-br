---
title: Propriedade Size (parâmetro ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3796f772dedb961ec34eb0639034350989f99142
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931051"
---
# <a name="size-property-ado-parameter"></a>Propriedade Size (Parâmetro ADO)
Indica o tamanho máximo, em bytes ou caracteres, de um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica o tamanho máximo em bytes ou caracteres de um valor em um objeto de **parâmetro** .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **tamanho** para determinar o tamanho máximo dos valores gravados ou lidos na propriedade [valor](../../../ado/reference/ado-api/value-property-ado.md) de um objeto de **parâmetro** .  
  
 Se você especificar um tipo de dados de comprimento variável para um objeto de **parâmetro** (por exemplo, qualquer tipo de **cadeia de caracteres** , como **adVarChar**), deverá definir a propriedade **size** do objeto antes de anexá-la à coleção [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) ; caso contrário, ocorrerá um erro.  
  
 Se você já tiver anexado o objeto de **parâmetro** à coleção **de parâmetros** de um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) e alterar seu tipo para um tipo de dados de comprimento variável, deverá definir a propriedade **size** do objeto de **parâmetro** antes de executar o objeto **Command** ; caso contrário, ocorrerá um erro.  
  
 Se você usar o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) para obter informações de parâmetro do provedor e ele retornar um ou mais objetos de **parâmetro** de tipo de dados de comprimento variável, o ADO poderá alocar memória para os parâmetros com base em seu tamanho máximo potencial, o que pode causar um erro durante a execução. Para evitar um erro, você deve definir explicitamente a propriedade **size** para esses parâmetros antes de executar o comando.  
  
 A propriedade **size** é leitura/gravação.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade Size (Fluxo do ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
