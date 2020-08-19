---
description: Propriedade Value (ADO)
title: Propriedade Value (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: 719a647f42c66e73b9bd55ed0a7476dfb95934e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441588"
---
# <a name="value-property-ado"></a>Propriedade Value (ADO)

Indica o valor atribuído a um [campo](../../../ado/reference/ado-api/field-object.md), [parâmetro](../../../ado/reference/ado-api/parameter-object.md)ou objeto de [Propriedade](../../../ado/reference/ado-api/property-object-ado.md) .
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno

Define ou retorna um valor **Variant** que indica o valor do objeto. O valor padrão depende da propriedade [Type](../../../ado/reference/ado-api/type-property-ado.md) .
  
## <a name="remarks"></a>Comentários

Use a propriedade **Value** para definir ou retornar dados de objetos de **campo** , para definir ou retornar valores de parâmetro com objetos de **parâmetro** ou para definir ou retornar configurações de propriedade com objetos de **Propriedade** . Se a propriedade **Value** é de leitura/gravação ou somente leitura depende de vários fatores. Consulte os tópicos do respectivo objeto para obter mais informações.

O ADO permite configurar e retornar dados binários longos com a propriedade **Value** .
  
> [!NOTE]
> Para objetos de **parâmetro** , o ADO lê a propriedade **Value** somente uma vez a partir do provedor. Se um comando contiver um **parâmetro** cuja propriedade **Value** esteja vazia e você criar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) a partir do comando, certifique-se de fechar primeiro o **conjunto de registros** antes de recuperar a propriedade **Value** . Caso contrário, para alguns provedores, a propriedade **Value** pode estar vazia e não conterá o valor correto.
> 
> Para novos objetos de **campo** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) , a propriedade **Value** deve ser definida antes que qualquer outra propriedade **Field** possa ser especificada. Primeiro, um valor específico para a propriedade **Value** deve ter sido atribuído e [atualizado](../../../ado/reference/ado-api/update-method.md) na coleção **Fields** chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) , podem ser acessadas.
  
## <a name="applies-to"></a>Aplica-se A

:::row:::
    :::column:::
        [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também

[Exemplo da propriedade Value (VB)](../../../ado/reference/ado-api/value-property-example-vb.md) 
 [Exemplo da propriedade Value (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
