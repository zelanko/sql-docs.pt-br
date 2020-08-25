---
description: Propriedade Name (ADO)
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
ms.openlocfilehash: da88b8e5a98e7d3ae105cc6e826804158f4bf7c8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774165"
---
# <a name="name-property-ado"></a>Propriedade Name (ADO)
Indica o nome de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que indica o nome de um objeto.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Name** para atribuir um nome ou recuperar o nome de um **comando**, **Propriedade**, **campo**ou objeto de **parâmetro** .  
  
 O valor é leitura/gravação em um objeto de **comando** e somente leitura em um objeto de **Propriedade** .  
  
 Para um objeto **Field** , **Name** normalmente é somente leitura. No entanto, para novos objetos **Field** que foram acrescentados à coleção [Fields](./fields-collection-ado.md) de um [registro](./record-object-ado.md), **Name** é Read/Write only após a propriedade [Value](./value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](./update-method.md) da coleção **Fields** .  
  
 Para objetos de **parâmetro** ainda não acrescentados à coleção de [parâmetros](./parameters-collection-ado.md) , a propriedade **Name** é de leitura/gravação. Para objetos de **parâmetro** acrescentados e todos os outros objetos, a propriedade **Name** é somente leitura. Os nomes não precisam ser exclusivos em uma coleção.  
  
 Você pode recuperar a propriedade **Name** de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `rstMain.Properties(20).Name` o produz `Updatability` , você pode posteriormente fazer referência a essa propriedade como `rstMain.Properties("Updatability")` .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Command (ADO)](./command-object-ado.md)  
        [Objeto Campo](./field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](./parameter-object.md)  
        [Objeto Property (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades Attributes e Name (VB)](./attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades Attributes e Name (VC + +)](./attributes-and-name-properties-example-vc.md)