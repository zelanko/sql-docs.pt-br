---
title: Objeto Field | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a50d9f3354f9d5eb5a7615c244d8a8990ffc0c9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758762"
---
# <a name="field-object"></a>Objeto Campo
Representa uma coluna de dados com um tipo de dados comum.  
  
## <a name="remarks"></a>Comentários  
 Cada objeto de **campo** corresponde a uma coluna no [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). Use a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) dos objetos **Field** para definir ou retornar dados para o registro atual. Dependendo da funcionalidade que o provedor expõe, algumas coleções, métodos ou propriedades de um objeto de **campo** podem não estar disponíveis.  
  
 Com as coleções, os métodos e as propriedades de um objeto **Field** , você pode fazer o seguinte:  
  
-   Retornar o nome de um campo com a propriedade [Name](../../../ado/reference/ado-api/name-property-ado.md) .  
  
-   Exiba ou altere os dados no campo com a propriedade **valor** . **Value** é a propriedade padrão do objeto **Field** .  
  
-   Retornar as características básicas de um campo com as propriedades [Type](../../../ado/reference/ado-api/type-property-ado.md), [Precision](../../../ado/reference/ado-api/precision-property-ado.md)e [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) .  
  
-   Retorna o tamanho declarado de um campo com a propriedade [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) .  
  
-   Retornar o tamanho real dos dados em um determinado campo com a propriedade [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) .  
  
-   Determine quais tipos de funcionalidade têm suporte para um determinado campo com a propriedade [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) e a coleção [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
-   Manipule os valores de campos que contêm dados binários longos ou de caractere longo com os métodos [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) .  
  
-   Se o provedor oferecer suporte a atualizações em lotes, resolva as discrepâncias em valores de campo durante a atualização do lote com as propriedades [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) e [subdependvalue](../../../ado/reference/ado-api/underlyingvalue-property.md) .  
  
 Todas as propriedades de metadados (**Name**, **Type**, **DefinedSize**, **Precision**e **NumericScale**) estão disponíveis antes de abrir o **conjunto de registros**do objeto **Field** . Configurá-los nesse momento é útil para construir formulários dinamicamente.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Field](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
