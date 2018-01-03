---
title: Tipo de propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords: Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 635a1ad2cae9e9e698bebdbf479a3b542af4d953
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="type-property-ado"></a>Propriedade Type (ADO)
Indica o tipo de dados ou tipo operacional de um [parâmetro](../../../ado/reference/ado-api/parameter-object.md), [campo](../../../ado/reference/ado-api/field-object.md), ou [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor.  
  
## <a name="remarks"></a>Remarks  
 Para **parâmetro** objetos, o **tipo** propriedade é leitura/gravação. Para o novo **campo** objetos que foram acrescentados ao [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **tipo** é leitura/gravação somente após o [ Valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o provedor de dados foi adicionado com êxito o novo **campo** chamando o [atualizar](../../../ado/reference/ado-api/update-method.md)método o **campos** coleção.  
  
 Para todos os outros objetos, o **tipo** propriedade é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedade de tipo (campo) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Exemplo de propriedade de tipo (propriedade) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Propriedade Type (Fluxo ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
