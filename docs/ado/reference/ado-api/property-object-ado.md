---
title: Objeto Property (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: af077c1606148eacb4f93ba6cfb52c3bb5eeefce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702948"
---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Objetos do ADO têm dois tipos de propriedades: interna e dinâmicos.  
  
 Propriedades internas são as propriedades implementadas no ADO e fica imediatamente disponíveis para qualquer novo objeto, usando o `MyObject.Property` sintaxe. Eles não aparecem como **propriedade** objetos em um objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, portanto, embora você possa alterar seus valores, você não pode modificar suas características.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na **propriedades** coleção do objeto ADO apropriado. Por exemplo, uma propriedade específica do provedor pode indicar se um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto dá suporte a transações ou atualizando. Essas propriedades adicionais serão exibido como **propriedade** objetos em que **conjunto de registros** do objeto **propriedades** coleção. Propriedades dinâmicas podem ser referenciadas apenas por meio da coleção, usando o `MyObject.Properties(0)` ou `MyObject.Properties("Name")` sintaxe.  
  
 Você não pode excluir um desses tipos de propriedade.  
  
 Dinâmico **propriedade** objeto tem quatro propriedades internas de seu próprio:  
  
-   O [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
-   O [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade é um inteiro que especifica o tipo de dados de propriedade.  
  
-   O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade é uma variante que contém a configuração da propriedade. **Valor** é a propriedade padrão para um **propriedade** objeto.  
  
-   O [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade é um valor longo que indica as características da propriedade específica do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto property](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
