---
description: Objeto Property (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f51334996eaeeaf7bdaae599dcbad16dc90824a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772975"
---
# <a name="property-object-ado"></a>Objeto Property (ADO)
Representa uma característica dinâmica de um objeto ADO que é definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Os objetos ADO têm dois tipos de propriedades: interno e dinâmico.  
  
 As propriedades internas são aquelas implementadas no ADO e imediatamente disponibilizadas para qualquer novo objeto, usando a `MyObject.Property` sintaxe. Eles não aparecem como objetos de **Propriedade** na coleção de [Propriedades](./properties-collection-ado.md) de um objeto, portanto, embora você possa alterar seus valores, não é possível modificar suas características.  
  
 As propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na coleção de **Propriedades** do objeto ADO apropriado. Por exemplo, uma propriedade específica para o provedor pode indicar se um objeto [Recordset](./recordset-object-ado.md) dá suporte a transações ou atualizações. Essas propriedades adicionais serão exibidas como objetos de **Propriedade** na coleção de **Propriedades** do objeto **Recordset** . As propriedades dinâmicas podem ser referenciadas somente por meio da coleção, usando a `MyObject.Properties(0)` `MyObject.Properties("Name")` sintaxe ou.  
  
 Não é possível excluir qualquer tipo de propriedade.  
  
 Um objeto de **Propriedade** dinâmica tem quatro propriedades internas próprias:  
  
-   A propriedade [Name](./name-property-ado.md) é uma cadeia de caracteres que identifica a propriedade.  
  
-   A propriedade [Type](./type-property-ado.md) é um inteiro que especifica o tipo de dados Property.  
  
-   A propriedade [Value](./value-property-ado.md) é uma variante que contém a configuração de propriedade. **Valor** é a propriedade padrão para um objeto de **Propriedade** .  
  
-   A propriedade [Attributes](./attributes-property-ado.md) é um valor longo que indica as características da propriedade específica para o provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Property](./property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Command (ADO)](./command-object-ado.md)   
 [Objeto de conexão (ADO)](./connection-object-ado.md)   
 [Objeto Field](./field-object.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)   
 [Objeto Recordset (ADO)](./recordset-object-ado.md)