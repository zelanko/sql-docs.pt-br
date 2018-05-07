---
title: Objeto Field | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49960f2763b402a291531a2ab010ef6a0682107f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="field-object"></a>Objeto Campo
Representa uma coluna de dados com um tipo de dados comum.  
  
## <a name="remarks"></a>Remarks  
 Cada **campo** objeto corresponde a uma coluna de [registros](../../../ado/reference/ado-api/recordset-object-ado.md). Você usa o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade **campo** objetos para definir ou retornar dados para o registro atual. Dependendo da funcionalidade de provedor expõe, algumas coleções, métodos ou propriedades de um **campo** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **campo** do objeto, você pode fazer o seguinte:  
  
-   Retornar o nome de um campo com o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade.  
  
-   Exibir ou alterar os dados no campo com o **valor** propriedade. **Valor** é a propriedade padrão do **campo** objeto.  
  
-   Retornar as características básicas de um campo com o [tipo](../../../ado/reference/ado-api/type-property-ado.md), [precisão](../../../ado/reference/ado-api/precision-property-ado.md), e [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) propriedades.  
  
-   Retornar o tamanho declarado de um campo com o [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propriedade.  
  
-   Retornar o tamanho real dos dados em um determinado campo com o [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propriedade.  
  
-   Determinar quais tipos de funcionalidade tem suporte para um determinado campo com o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade e [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
-   Manipular os valores dos campos que contêm dados binários longos ou caracteres de tempo com o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) métodos.  
  
-   Se o provedor oferece suporte a atualizações em lotes, resolver as discrepâncias em valores de campo durante a atualização em lotes com o [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) e [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propriedades.  
  
 Todas as propriedades de metadados (**nome**, **tipo**, **DefinedSize**, **precisão**, e **NumericScale**) estão disponíveis antes de abrir o **campo** do objeto **registros**. Configurá-los no momento é útil para a criação dinâmica de formulários.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de campo](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
