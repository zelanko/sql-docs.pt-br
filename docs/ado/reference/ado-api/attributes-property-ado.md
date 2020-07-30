---
title: Propriedade Attributes (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: rothja
ms.author: jroth
ms.openlocfilehash: fe649e6636f33dfc73ee5aac949830b4175cd3ec
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242446"
---
# <a name="attributes-property-ado"></a>Propriedade Attributes (ADO)
Indica uma ou mais características de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** .  
  
 Para um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) , a propriedade **Attributes** é Read/Write e seu valor pode ser a soma de um ou mais valores [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) . O padrão é zero (0).  
  
 Para um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) , a propriedade **Attributes** é Read/Write e seu valor pode ser a soma de qualquer um ou mais valores [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) . O padrão é **adParamSigned**.  
  
 Para um objeto [Field](../../../ado/reference/ado-api/field-object.md) , a propriedade **Attributes** pode ser a soma de um ou mais valores [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) . Normalmente, ele é somente leitura. No entanto, para novos objetos de **campo** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um [registro](../../../ado/reference/ado-api/record-object-ado.md), os **atributos** são de leitura/gravação somente depois que a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do **campo** tiver sido especificada e o novo **campo** tiver sido adicionado com êxito pelo provedor de dados chamando o método [Update](../../../ado/reference/ado-api/update-method.md) da coleção **Fields** .  
  
 Para um objeto [Property](../../../ado/reference/ado-api/property-object-ado.md) , a propriedade **Attributes** é somente leitura e seu valor pode ser a soma de qualquer um ou mais valores [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Attributes** para definir ou retornar características de objetos de **conexão** , objetos de **parâmetro** , objetos de **campo** ou objetos de **Propriedade** .  
  
 Ao definir vários atributos, você pode somar as constantes apropriadas. Se você definir o valor da propriedade como uma soma, incluindo constantes incompatíveis, ocorrerá um erro.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Essa propriedade não está disponível em um objeto de **conexão** do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
        [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
        [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedades Attributes e Name (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades Attributes e Name (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
