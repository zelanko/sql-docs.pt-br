---
title: Valor de propriedade (ADO) | Microsoft Docs
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
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17e3c9f28e42dbd70118bb29a330514a9c29e013
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="value-property-ado"></a>Propriedade de valor (ADO)
Indica o valor atribuído a um [campo](../../../ado/reference/ado-api/field-object.md), [parâmetro](../../../ado/reference/ado-api/parameter-object.md), ou [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **Variant** valor que indica o valor do objeto. Valor padrão depende do [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade.  
  
## <a name="remarks"></a>Comentários  
 Use o **valor** propriedade para definir ou retornar dados de **campo** objetos, para definir ou retornar valores de parâmetro com **parâmetro** objetos, ou para definir ou retornar as configurações de propriedade com **Propriedade** objetos. Se o **valor** propriedade é leitura/gravação ou somente leitura depende de vários fatores??? Consulte os tópicos do respectivo objeto para obter mais informações.  
  
 ADO permite definir e retornar dados binários longos com o **valor** propriedade.  
  
> [!NOTE]
>  Para **parâmetro** objetos, leituras ADO a **valor** propriedade apenas uma vez do provedor. Se um comando contém um **parâmetro** cujo **valor** propriedade está vazia e você criar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) do comando, certifique-se de que você feche o ** Conjunto de registros** antes de recuperar o **valor** propriedade. Caso contrário, para alguns provedores, o **valor** propriedade pode estar vazia e não contêm o valor correto.  
>   
>  Para o novo **campo** objetos que foram acrescentados ao [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, o **valor** propriedade deve ser definida antes de qualquer outro **campo** propriedades podem ser especificadas. Primeiro, um valor específico para o **valor** propriedade deve ser atribuída e [atualização](../../../ado/reference/ado-api/update-method.md) no **campos** coleção chamada. Em seguida, outras propriedades, como [tipo](../../../ado/reference/ado-api/type-property-ado.md) ou [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) pode ser acessado.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade de valor (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)   
 [Exemplo da propriedade Value (VC++)](../../../ado/reference/ado-api/value-property-example-vc.md)   

