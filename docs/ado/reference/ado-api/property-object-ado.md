---
title: Objeto Property (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4a0c5a1217cb8143a0b275ea3d0c31e16b7d1cd1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Objetos de ADO têm dois tipos de propriedades: interna e dinâmicos.  
  
 Propriedades internas são as propriedades implementadas no ADO e imediatamente disponíveis para qualquer novo objeto, usando o `MyObject.Property` sintaxe. Eles não aparecem como **propriedade** objetos em um objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, portanto, embora você possa alterar seus valores, você não pode modificar suas características.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem no **propriedades** coleção do objeto ADO apropriado. Por exemplo, uma propriedade específica do provedor pode indicar se uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto oferece suporte a transações ou atualização. Essas propriedades adicionais serão exibidas como **propriedade** objetos em que **registros** do objeto **propriedades** coleção. Propriedades dinâmicas que podem ser referenciadas apenas por meio da coleção, usando o `MyObject.Properties(0)` ou `MyObject.Properties("Name")` sintaxe.  
  
 Não é possível excluir o tipo de propriedade.  
  
 Um dinâmico **propriedade** objeto tem quatro propriedades internas de seu próprio:  
  
-   O [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
-   O [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade é um inteiro que especifica o tipo de dados da propriedade.  
  
-   O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade é um tipo variant que contém a configuração da propriedade. **Valor** é a propriedade padrão para um **propriedade** objeto.  
  
-   O [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade é um valor longo que indica as características da propriedade específica do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Objeto de propriedades, métodos e eventos](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

