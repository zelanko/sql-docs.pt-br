---
title: Propriedade Name (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 40a392e355e2ec8a468034b382956489f554ac78
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243127"
---
# <a name="name-property-ado-md"></a>Propriedade Name (ADO MD)
Indica o nome de um objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Você pode recuperar a propriedade **Name** de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `cdf.CubeDefs(0).Name` o gerar "bobs Video Store", você poderá fazer referência a esse [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)  
        [Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)  
        [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)  
        [Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)  
        [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Propriedade Caption (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Propriedade Description (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [Propriedade UniqueName (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
