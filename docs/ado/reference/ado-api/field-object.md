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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918681"
---
# <a name="field-object"></a>Objeto Campo
Representa uma coluna de dados com um tipo de dados comum.  
  
## <a name="remarks"></a>Comentários  
 Cada **campo** objeto corresponde a uma coluna na [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). Você usa o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade de **campo** objetos para definir ou retornar dados para o registro atual. Dependendo da funcionalidade de provedor expõe, algumas coleções, métodos ou propriedades de um **campo** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **campo** do objeto, você pode fazer o seguinte:  
  
-   Retornar o nome de um campo com o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade.  
  
-   Exibir ou alterar os dados do campo com o **valor** propriedade. **Valor** é a propriedade padrão de **campo** objeto.  
  
-   Retornar as características básicas de um campo com o [tipo](../../../ado/reference/ado-api/type-property-ado.md), [Precision](../../../ado/reference/ado-api/precision-property-ado.md), e [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) propriedades.  
  
-   Retornar o tamanho declarado de um campo com o [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propriedade.  
  
-   Retornar o tamanho real dos dados em um determinado campo com o [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propriedade.  
  
-   Determinar quais tipos de funcionalidades têm suporte para um determinado campo com o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade e [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
-   Manipular os valores dos campos que contêm dados binários longos ou de caracteres longa com o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) métodos.  
  
-   Se o provedor oferece suporte a atualizações em lotes, resolver as discrepâncias nos valores de campo durante a atualização em lotes com o [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) e [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propriedades.  
  
 Todas as propriedades de metadados (**nome**, **tipo**, **DefinedSize**, **precisão**, e **NumericScale**) estão disponíveis antes de abrir o **campo** do objeto **conjunto de registros**. Defini-los no momento é útil para criar dinamicamente os formulários.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto Field](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
