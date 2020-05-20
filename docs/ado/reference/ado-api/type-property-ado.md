---
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
ms.openlocfilehash: 46718126ede409caa749b3a49dfaaffe118afc77
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761824"
---
# <a name="type-property-ado"></a>Propriedade Type (ADO)
Indica o tipo operacional ou o tipo de dados de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md), [campo](../../../ado/reference/ado-api/field-object.md)ou objeto de [Propriedade](../../../ado/reference/ado-api/property-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Para objetos de **parâmetro** , a propriedade **Type** é leitura/gravação. Para novos objetos **Field** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **Type** é Read/Write only após a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](../../../ado/reference/ado-api/update-method.md) da coleção **Fields** .  
  
 Para todos os outros objetos, a propriedade **Type** é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se A  
  
||||  
|-|-|-|  
|[Objeto Campo](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Type (campo) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Exemplo da propriedade Type (Propriedade) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (Fluxo ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
