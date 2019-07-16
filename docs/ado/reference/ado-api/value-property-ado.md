---
title: Valor de propriedade (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e35dd93e6d90a81934d8f272ea79c5eb7c8a97c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913918"
---
# <a name="value-property-ado"></a>Propriedade Value (ADO)

Indica o valor atribuído a um [campo](../../../ado/reference/ado-api/field-object.md), [parâmetro](../../../ado/reference/ado-api/parameter-object.md), ou [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto.
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno

Define ou retorna um **Variant** valor que indica o valor do objeto. Valor padrão depende do [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade.
  
## <a name="remarks"></a>Comentários

Use o **valor** propriedade para definir ou retornar dados de **campo** objetos para definir ou retornar valores de parâmetro com **parâmetro** objetos, ou para definir ou retornar as configurações de propriedade com **Propriedade** objetos. Se o **valor** propriedade é leitura/gravação ou somente leitura depende de vários fatores. Consulte os tópicos do respectivo objeto para obter mais informações.

ADO permite definir e retornar dados binários longos com o **valor** propriedade.
  
> [!NOTE]
> Para **parâmetro** objetos, leituras de ADO a **valor** propriedade apenas uma vez do provedor. Se um comando contiver um **parâmetro** cujo **valor** propriedade estiver vazia, e você criar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do comando, certifique-se de que você primeiro feche o  **Conjunto de registros** antes de recuperar o **valor** propriedade. Caso contrário, para alguns provedores, o **valor** propriedade pode estar vazia e não conterá o valor correto.
> 
> Para o novo **campo** objetos que foram acrescentados para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, o **valor** propriedade deve ser definida antes de qualquer outro **campo** propriedades podem ser especificadas. Primeiro, um valor específico para o **valor** propriedade deverá ser atribuída e [atualização](../../../ado/reference/ado-api/update-method.md) sobre o **campos** coleção chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) pode ser acessado.
  
## <a name="applies-to"></a>Aplica-se a
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Consulte também

[Exemplo da propriedade (VB) de valor](../../../ado/reference/ado-api/value-property-example-vb.md)
[valor de exemplo da propriedade (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
