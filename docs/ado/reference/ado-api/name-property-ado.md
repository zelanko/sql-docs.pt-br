---
title: Nome de propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c2bf66589dc841e7f543b166b432f39a0869b3f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="name-property-ado"></a>Propriedade Name (ADO)
Indica o nome de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que indica o nome de um objeto.  
  
## <a name="remarks"></a>Comentários  
 Use o **nome** propriedade para atribuir um nome ou recuperar o nome de um **comando**, **propriedade**, **campo**, ou **parâmetro ** objeto.  
  
 O valor é leitura/gravação em um **comando** objeto e somente leitura em uma **propriedade** objeto.  
  
 Para uma **campo** objeto, **nome** é normalmente somente leitura. No entanto, para o novo **campo** objetos que foram acrescentados ao [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **nome** é leitura/gravação somente após o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o provedor de dados foi adicionado com êxito o novo **campo** chamando o [ Atualização](../../../ado/reference/ado-api/update-method.md) método o **campos** coleção.  
  
 Para **parâmetro** objetos ainda não acrescentado para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção, o **nome** propriedade é leitura/gravação. Para anexados **parâmetro** objetos e todos os outros objetos, o **nome** propriedade é somente leitura. Nomes não precisam ser exclusivos dentro de uma coleção.  
  
 Você pode recuperar o **nome** propriedade de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `rstMain.Properties(20).Name` produz `Updatability`, posteriormente, você pode fazer referência a esta propriedade como `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de nome (VB) e de atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades de nome (VC + +) e de atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   

