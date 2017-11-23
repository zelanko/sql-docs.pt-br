---
title: "Tamanho de propriedade (parâmetro ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Parameter::Size
helpviewer_keywords: Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2208300a31c141c2092caae62bc11cfe83606cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="size-property-ado-parameter"></a>Propriedade Size (parâmetro ADO)
Indica o tamanho máximo, em bytes ou caracteres, de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica o tamanho máximo em bytes ou caracteres de um valor em uma **parâmetro** objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o **tamanho** propriedade para determinar o tamanho máximo de valores gravado ou lido a partir de [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade de um **parâmetro** objeto.  
  
 Se você especificar um tipo de dados de comprimento variável para um **parâmetro** objeto (por exemplo, qualquer **cadeia de caracteres** tipo, como **adVarChar**), você deve definir o objeto  **Tamanho** propriedade antes de acrescentá-lo para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção; caso contrário, ocorrerá um erro.  
  
 Se você já tiver acrescentado a **parâmetro** o objeto para o **parâmetros** coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto e alterar seu tipo para um tipo de dados de comprimento variável, você deve definir o **parâmetro** do objeto **tamanho** propriedade antes de executar o **comando** objeto; caso contrário, ocorrerá um erro.  
  
 Se você usar o [atualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método para obter informações de parâmetro de provedor e retorna o tipo de dados de comprimento variável de um ou mais **parâmetro** objetos, ADO pode alocar memória para os parâmetros com base em seu tamanho potencial máximo que pode causar um erro durante a execução. Para evitar um erro, você deve definir explicitamente o **tamanho** propriedade desses parâmetros antes de executar o comando.  
  
 O **tamanho** é de propriedade de leitura/gravação.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propriedade Size (Fluxo do ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
