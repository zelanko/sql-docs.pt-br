---
description: Propriedade Name (ADO MD)
title: Propriedade Name (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 4dfec86bb631dda661b957e02667cd320c20fec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986237"
---
# <a name="name-property-ado-md"></a>Propriedade Name (ADO MD)
Indica o nome de um objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Você pode recuperar a propriedade **Name** de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `cdf.CubeDefs(0).Name` o gerar "bobs Video Store", você poderá fazer referência a esse [CubeDef](./cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Axis (ADO MD)](./axis-object-ado-md.md)  
        [Objeto Catalog (ADO MD)](./catalog-object-ado-md.md)  
        [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Dimension (ADO MD)](./dimension-object-ado-md.md)  
        [Objeto Hierarchy (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Level (ADO MD)](./level-object-ado-md.md)  
        [Objeto Member (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](./catalog-example-vb.md)   
 [Propriedade Caption (ADO MD)](./caption-property-ado-md.md)   
 [Propriedade Description (ADO MD)](./description-property-ado-md.md)   
 [Propriedade UniqueName (ADO MD)](./uniquename-property-ado-md.md)