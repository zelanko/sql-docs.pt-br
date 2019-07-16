---
title: Tipo de propriedade (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ee1058299becb4a7a4234debc097516cb02dd41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937863"
---
# <a name="type-property-ado"></a>Propriedade Type (ADO)
Indica o tipo de dados ou tipo operacional de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md), [campo](../../../ado/reference/ado-api/field-object.md), ou [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 Para **parâmetro** objetos, o **tipo** propriedade é leitura/gravação. Para o novo **campo** objetos que foram acrescentados para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **tipo** é leitura/gravação somente após o [ Valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o provedor de dados foi adicionado com êxito a nova **campo** chamando o [atualizar](../../../ado/reference/ado-api/update-method.md)método de **campos** coleção.  
  
 Para todos os outros objetos, o **tipo** propriedade é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Type (campo) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Exemplo da propriedade Type (propriedade) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (Fluxo ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
