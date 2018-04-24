---
title: O objeto de propriedade (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a6dbac85e1a99ce34fc3ec94d9cd1047e74893c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="property-object-adox"></a>Objeto de propriedade (ADOX)
Representa uma característica de um objeto ADOX.  
  
## <a name="remarks"></a>Remarks  
 Objetos ADOX têm dois tipos de propriedades: interna e dinâmicos.  
  
 Propriedades internas são as propriedades disponíveis imediatamente para qualquer novo objeto, usando a sintaxe MyObject.Property. Eles não são exibidas como objetos de propriedade em um objeto [coleção Properties](../../../ado/reference/ado-api/properties-collection-ado.md), portanto, embora você possa alterar seus valores, você não pode modificar suas características.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem na coleção de propriedades para o objeto ADOX apropriado.  Propriedades dinâmicas podem ser referenciadas apenas por meio da coleção, usando a sintaxe MyObject.Properties(0) ou MyObject.Properties("Name").  
  
 Não é possível excluir o tipo de propriedade.  
  
 Um objeto de propriedade dinâmico tem quatro propriedades internas de seu próprio:  
  
 O [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
 O [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedade é um inteiro que especifica o tipo de dados da propriedade.  
  
 O [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade é um tipo variant que contém a configuração da propriedade. Valor é a propriedade padrão para um objeto de propriedade.  
  
 O [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade é um valor longo que indica as características da propriedade específica do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Property ADOX](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
