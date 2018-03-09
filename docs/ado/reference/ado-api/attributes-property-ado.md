---
title: Atributos de propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2b63ff111ddf295784a6e8d3d574f0c36267f19
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="attributes-property-ado"></a>Propriedade Attributes (ADO)
Indica uma ou mais características de um objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor.  
  
 Para uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, o **atributos** propriedade é leitura/gravação e seu valor pode ser a soma de uma ou mais [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) valores. O padrão é zero (0).  
  
 Para uma [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto, o **atributos** propriedade é leitura/gravação e seu valor pode ser a soma de uma ou mais [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) valores. O padrão é **adParamSigned**.  
  
 Para uma [campo](../../../ado/reference/ado-api/field-object.md) objeto, o **atributos** propriedade pode ser a soma de uma ou mais [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valores. Ele é normalmente somente leitura. No entanto, para o novo **campo** objetos que foram acrescentados ao [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **atributos** é leitura/gravação somente Depois que o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o novo **campo** foi adicionado com êxito pelo provedor de dados chamando o [ Atualização](../../../ado/reference/ado-api/update-method.md) método o **campos** coleção.  
  
 Para uma [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto, o **atributos** propriedade é somente leitura e seu valor pode ser a soma de uma ou mais [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) valores.  
  
## <a name="remarks"></a>Remarks  
 Use o **atributos** propriedade para definir ou retornar as características de **Conexão** objetos, **parâmetro** objetos, **campo** objetos, ou **Propriedade** objetos.  
  
 Quando você definir vários atributos, você pode somar as constantes apropriadas. Se você definir o valor da propriedade como uma soma incluindo constantes incompatíveis, ocorrerá um erro.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** essa propriedade não está disponível em um cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de nome (VB) e de atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Exemplo de propriedades de nome (VC + +) e de atributos](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans e métodos RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
