---
title: Propriedade (parâmetro ADO) size | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 682a7aa30596af8a3727eec0daaba4e9fd412ac4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601614"
---
# <a name="size-property-ado-parameter"></a>Propriedade Size (Parâmetro ADO)
Indica o tamanho máximo, em bytes ou caracteres, de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica o tamanho máximo em bytes ou caracteres de um valor em uma **parâmetro** objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o **tamanho** propriedade para determinar o tamanho máximo para valores gravados ou lidos do [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade de um **parâmetro** objeto.  
  
 Se você especifica um tipo de dados de comprimento variável para um **parâmetro** objeto (por exemplo, qualquer **cadeia de caracteres** tipo, como **adVarChar**), você deve definir o objeto  **Tamanho** propriedade antes de acrescentá-lo para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção; caso contrário, ocorrerá um erro.  
  
 Se você já tenha sido anexado a **parâmetro** do objeto para o **parâmetros** coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto e você alterar seu tipo para um tipo de dados de comprimento variável, você deve Defina as **parâmetro** do objeto **tamanho** propriedade antes de executar o **comando** objeto; caso contrário, ocorrerá um erro.  
  
 Se você usar o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método para obter informações de parâmetro de provedor e ele retorna um ou mais tipos de dados de comprimento variável **parâmetro** objetos, o ADO pode alocar memória para os parâmetros com base em seu tamanho potencial máximo, que pode causar um erro durante a execução. Para evitar um erro, você deve definir explicitamente o **tamanho** propriedade desses parâmetros antes de executar o comando.  
  
 O **tamanho** propriedade é leitura/gravação.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade Size (Fluxo do ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
