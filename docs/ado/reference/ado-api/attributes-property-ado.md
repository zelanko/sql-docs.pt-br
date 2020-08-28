---
description: Propriedade Attributes (ADO)
title: Propriedade Attributes (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: ceb141b0ecdbc278e324f19f3bd4b3d7ed1b4eb6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975937"
---
# <a name="attributes-property-ado"></a>Propriedade Attributes (ADO)
Indica uma ou mais características de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** .  
  
 Para um objeto de [conexão](./connection-object-ado.md) , a propriedade **Attributes** é Read/Write e seu valor pode ser a soma de um ou mais valores [XactAttributeEnum](./xactattributeenum.md) . O padrão é zero (0).  
  
 Para um objeto de [parâmetro](./parameter-object.md) , a propriedade **Attributes** é Read/Write e seu valor pode ser a soma de qualquer um ou mais valores [ParameterAttributesEnum](./parameterattributesenum.md) . O padrão é **adParamSigned**.  
  
 Para um objeto [Field](./field-object.md) , a propriedade **Attributes** pode ser a soma de um ou mais valores [FieldAttributeEnum](./fieldattributeenum.md) . Normalmente, ele é somente leitura. No entanto, para novos objetos de **campo** que foram acrescentados à coleção [Fields](./fields-collection-ado.md) de um [registro](./record-object-ado.md), os **atributos** são de leitura/gravação somente depois que a propriedade [Value](./value-property-ado.md) do **campo** tiver sido especificada e o novo **campo** tiver sido adicionado com êxito pelo provedor de dados chamando o método [Update](./update-method.md) da coleção **Fields** .  
  
 Para um objeto [Property](./property-object-ado.md) , a propriedade **Attributes** é somente leitura e seu valor pode ser a soma de qualquer um ou mais valores [PropertyAttributesEnum](./propertyattributesenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Attributes** para definir ou retornar características de objetos de **conexão** , objetos de **parâmetro** , objetos de **campo** ou objetos de **Propriedade** .  
  
 Ao definir vários atributos, você pode somar as constantes apropriadas. Se você definir o valor da propriedade como uma soma, incluindo constantes incompatíveis, ocorrerá um erro.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Essa propriedade não está disponível em um objeto de **conexão** do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Connection (ADO)](./connection-object-ado.md)  
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
 [Método AppendChunk (ADO)](./appendchunk-method-ado.md)   
 [Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](./getchunk-method-ado.md)