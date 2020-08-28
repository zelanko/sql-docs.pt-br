---
description: Propriedade Size (Parâmetro ADO)
title: Propriedade Size (parâmetro ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 914f751c4bfd48755470ce3da9e994dae4a33477
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989117"
---
# <a name="size-property-ado-parameter"></a>Propriedade Size (Parâmetro ADO)
Indica o tamanho máximo, em bytes ou caracteres, de um objeto de [parâmetro](./parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que indica o tamanho máximo em bytes ou caracteres de um valor em um objeto de **parâmetro** .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **tamanho** para determinar o tamanho máximo dos valores gravados ou lidos na propriedade [valor](./value-property-ado.md) de um objeto de **parâmetro** .  
  
 Se você especificar um tipo de dados de comprimento variável para um objeto de **parâmetro** (por exemplo, qualquer tipo de **cadeia de caracteres** , como **adVarChar**), deverá definir a propriedade **size** do objeto antes de anexá-la à coleção [Parameters](./parameters-collection-ado.md) ; caso contrário, ocorrerá um erro.  
  
 Se você já tiver anexado o objeto de **parâmetro** à coleção **de parâmetros** de um objeto de [comando](./command-object-ado.md) e alterar seu tipo para um tipo de dados de comprimento variável, deverá definir a propriedade **size** do objeto de **parâmetro** antes de executar o objeto **Command** ; caso contrário, ocorrerá um erro.  
  
 Se você usar o método [Refresh](./refresh-method-ado.md) para obter informações de parâmetro do provedor e ele retornar um ou mais objetos de **parâmetro** de tipo de dados de comprimento variável, o ADO poderá alocar memória para os parâmetros com base em seu tamanho máximo potencial, o que pode causar um erro durante a execução. Para evitar um erro, você deve definir explicitamente a propriedade **size** para esses parâmetros antes de executar o comando.  
  
 A propriedade **size** é leitura/gravação.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Parameter](./parameter-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade Size (Fluxo do ADO)](./size-property-ado-stream.md)