---
description: Propriedade Type (ADO)
title: Propriedade Type (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: rothja
ms.author: jroth
ms.openlocfilehash: cd16324e4daa3e14e47da21ad4fd528e68c1a614
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777095"
---
# <a name="type-property-ado"></a>Propriedade Type (ADO)
Indica o tipo operacional ou o tipo de dados de um [parâmetro](./parameter-object.md), [campo](./field-object.md)ou objeto de [Propriedade](./property-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [DataTypeEnum](./datatypeenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Para objetos de **parâmetro** , a propriedade **Type** é leitura/gravação. Para novos objetos **Field** que foram acrescentados à coleção [Fields](./fields-collection-ado.md) de um [registro](./record-object-ado.md), **Type** é Read/Write only após a propriedade [Value](./value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](./update-method.md) da coleção **Fields** .  
  
 Para todos os outros objetos, a propriedade **Type** é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Campo](./field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](./parameter-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Property (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Type (campo) (VB)](./type-property-example-field-vb.md)   
 [Exemplo da propriedade Type (Propriedade) (VC + +)](./type-property-example-property-vc.md)   
 [Propriedade RecordType (ADO)](./recordtype-property-ado.md)   
 [Propriedade Type (Fluxo ADO)](./type-property-ado-stream.md)