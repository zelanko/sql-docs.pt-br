---
description: Objeto Property (ADOX)
title: Objeto Property (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: rothja
ms.author: jroth
ms.openlocfilehash: 75a4722803e66527873f98fe469825d4af82ca33
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769535"
---
# <a name="property-object-adox"></a>Objeto Property (ADOX)
Representa uma característica de um objeto ADOX.  
  
## <a name="remarks"></a>Comentários  
 Os objetos ADOX têm dois tipos de propriedades: interno e dinâmico.  
  
 As propriedades internas são essas propriedades imediatamente disponíveis para qualquer novo objeto, usando a sintaxe MyObject. Property. Eles não aparecem como objetos de propriedade na [coleção de propriedades](../ado-api/properties-collection-ado.md)de um objeto, portanto, embora você possa alterar seus valores, não é possível modificar suas características.  
  
 As propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na coleção de propriedades do objeto ADOX apropriado.  As propriedades dinâmicas podem ser referenciadas somente por meio da coleção, usando a sintaxe MyObject. Properties (0) ou MyObject. Properties ("Name").  
  
 Não é possível excluir qualquer tipo de propriedade.  
  
 Um objeto de propriedade dinâmica tem quatro propriedades internas próprias:  
  
 A propriedade [Name](../ado-api/name-property-ado.md) é uma cadeia de caracteres que identifica a propriedade.  
  
 A propriedade [Type](../ado-api/type-property-ado.md) é um inteiro que especifica o tipo de dados Property.  
  
 A propriedade [Value](../ado-api/value-property-ado.md) é uma variante que contém a configuração de propriedade. Valor é a propriedade padrão para um objeto de propriedade.  
  
 A propriedade [Attributes](../ado-api/attributes-property-ado.md) é um valor longo que indica as características da propriedade específica para o provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Property ADOX](./adox-property-object-properties-methods-and-events.md)