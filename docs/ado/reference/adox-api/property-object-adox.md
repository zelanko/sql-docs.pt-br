---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2f07d14d30f3fd87be8fc61552716a931ed86d68
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705958"
---
# <a name="property-object-adox"></a>Objeto Property (ADOX)
Representa uma característica de um objeto do ADOX.  
  
## <a name="remarks"></a>Comentários  
 Objetos ADOX têm dois tipos de propriedades: interna e dinâmicos.  
  
 Propriedades internas são as propriedades disponíveis imediatamente para qualquer novo objeto, usando a sintaxe MyObject.Property. Eles não aparecem como objetos de propriedade em um objeto [coleção de propriedades](../../../ado/reference/ado-api/properties-collection-ado.md), portanto, embora você possa alterar seus valores, você não pode modificar suas características.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na coleção de propriedades para o objeto ADOX apropriado.  Propriedades dinâmicas podem ser referenciadas apenas por meio da coleção, usando a sintaxe MyObject.Properties(0) ou MyObject.Properties("Name").  
  
 Você não pode excluir um desses tipos de propriedade.  
  
 Um objeto dinâmico de propriedade tem quatro propriedades internas de seu próprio:  
  
 O [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
 O [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade é um inteiro que especifica o tipo de dados de propriedade.  
  
 O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade é uma variante que contém a configuração da propriedade. Valor é a propriedade padrão para um objeto de propriedade.  
  
 O [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade é um valor longo que indica as características da propriedade específica do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Property ADOX](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
