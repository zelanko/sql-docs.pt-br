---
description: Propriedade Precision (ADO)
title: Propriedade Precision (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: rothja
ms.author: jroth
ms.openlocfilehash: 59a42a7f577ae8f4712e679853d53939fd6f6ed1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773135"
---
# <a name="precision-property-ado"></a>Propriedade Precision (ADO)
Indica o grau de precisão para valores numéricos em um objeto de [parâmetro](./parameter-object.md) ou para objetos de [campo](./field-object.md) numérico.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **byte** que indica o número máximo de dígitos usados para representar valores.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **precisão** para determinar o número máximo de dígitos usados para representar valores para um **parâmetro** numérico ou objeto de **campo** .  
  
 O valor é leitura/gravação em um objeto de **parâmetro** .  
  
 Para um objeto **Field**, **Precision** normalmente é somente leitura. No entanto, para novos objetos **Field** que foram acrescentados à coleção [Fields](./fields-collection-ado.md) de um [registro](./record-object-ado.md), **Precision** é Read/Write only após a propriedade [Value](./value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](./update-method.md) da coleção **Fields** .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Campo](./field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](./parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades NumericScale e Precision (VB)](./numericscale-and-precision-properties-example-vb.md)   
 [Exemplo das propriedades NumericScale e Precision (VC + +)](./numericscale-and-precision-properties-example-vc.md)   
 [Propriedade NumericScale (ADO)](./numericscale-property-ado.md)