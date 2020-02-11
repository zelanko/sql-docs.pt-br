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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04dbf3069896b9a7668d64a2f1d322f0b17ca5f3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918681"
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
