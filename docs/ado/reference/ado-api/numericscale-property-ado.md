---
description: Propriedade NumericScale (ADO)
title: Propriedade NumericScale (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: rothja
ms.author: jroth
ms.openlocfilehash: 120d88e82f77af622de962ac306442625487ff08
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990407"
---
# <a name="numericscale-property-ado"></a>Propriedade NumericScale (ADO)
Indica a escala de valores numéricos em um objeto de [campo](./field-object.md) ou [parâmetro](./parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **byte** que indica o número de casas decimais para as quais os valores numéricos serão resolvidos.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **NumericScale** para determinar quantos dígitos à direita do ponto decimal serão usados para representar valores para um **parâmetro** numérico ou objeto de **campo** .  
  
 Para objetos de **parâmetro** , a propriedade **NumericScale** é leitura/gravação.  
  
 Para um objeto **Field**, **NumericScale** normalmente é somente leitura. No entanto, para novos objetos de **campo** que foram acrescentados à coleção [Fields](./fields-collection-ado.md) de um [registro](./record-object-ado.md), **NumericScale** é leitura/gravação somente depois que a propriedade [Value](./value-property-ado.md) do **campo** tiver sido especificada e o provedor de dados tiver adicionado com êxito o novo **campo** chamando o método [Update](./update-method.md) da coleção [Fields](./fields-collection-ado.md) .  
  
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
 [Propriedade Precision (ADO)](./precision-property-ado.md)