---
title: Propriedade Name (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: rothja
ms.author: jroth
ms.openlocfilehash: 38846bcb832df7cc535d35d8f07fb636f2db37f7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762417"
---
# <a name="name-property-ado"></a>Propriedade Name (ADO)
Indica o nome de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que indica o nome de um objeto.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Name** para atribuir um nome ou recuperar o nome de um **comando**, **Propriedade**, **campo**ou objeto de **parâmetro** .  
  
 O valor é leitura/gravação em um objeto de **comando** e somente leitura em um objeto de **Propriedade** .  
  
 Para um objeto **Field** , **Name** normalmente é somente leitura. No entanto, para novos objetos **Field** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **Name** é Read/Write only após a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](../../../ado/reference/ado-api/update-method.md) da coleção **Fields** .  
  
 Para objetos de **parâmetro** ainda não acrescentados à coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) , a propriedade **Name** é de leitura/gravação. Para objetos de **parâmetro** acrescentados e todos os outros objetos, a propriedade **Name** é somente leitura. Os nomes não precisam ser exclusivos em uma coleção.  
  
 Você pode recuperar a propriedade **Name** de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `rstMain.Properties(20).Name` o produz `Updatability` , você pode posteriormente fazer referência a essa propriedade como `rstMain.Properties("Updatability")` .  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Campo](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades Attributes e Name (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades Attributes e Name (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
