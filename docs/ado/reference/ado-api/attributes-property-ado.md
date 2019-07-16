---
title: Atributos de propriedade (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b40b71dee32608756721d84a2e13f5f54f7bcbfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920542"
---
# <a name="attributes-property-ado"></a>Propriedade Attributes (ADO)
Indica uma ou mais características de um objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor.  
  
 Para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, o **atributos** propriedade é leitura/gravação e seu valor pode ser a soma de uma ou mais [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) valores. O padrão é zero (0).  
  
 Para um [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto, o **atributos** propriedade é leitura/gravação e seu valor pode ser a soma de uma ou mais [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) valores. O padrão é **adParamSigned**.  
  
 Para um [campo](../../../ado/reference/ado-api/field-object.md) objeto, o **atributos** propriedade pode ser a soma de uma ou mais [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valores. Ele é normalmente somente leitura. No entanto, para o novo **campo** objetos que foram acrescentados para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **atributos** é leitura/gravação somente Depois que o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o novo **campo** tiver sido adicionado com êxito pelo provedor de dados chamando o [ Atualização](../../../ado/reference/ado-api/update-method.md) método da **campos** coleção.  
  
 Para um [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto, o **atributos** propriedade é somente leitura e seu valor pode ser a soma de uma ou mais [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **atributos** propriedade para definir ou retornar as características de **Conexão** objetos **parâmetro** objetos, **campo** objetos, ou **Propriedade** objetos.  
  
 Quando você define vários atributos, você pode somar as constantes apropriadas. Se você definir o valor da propriedade como uma soma, incluindo constantes incompatíveis, ocorrerá um erro.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** essa propriedade não está disponível em um lado do cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e exemplo de propriedades de nome (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades de nome (VC + +) e atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans e RollbackTrans métodos (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
