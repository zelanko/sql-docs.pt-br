---
title: Nome de propriedade (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
helpviewer_keywords: Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e471f2ea21a72b6034fa522ced7681965b733d91
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="name-property-ado-md"></a>Propriedade Name (ADO MD)
Indica o nome de um objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Remarks  
 Você pode recuperar o **nome** propriedade de um objeto por uma referência ordinal, após o qual você pode fazer referência ao objeto diretamente por nome. Por exemplo, se `cdf.CubeDefs(0).Name` produz "Bobs vídeo Store", você pode fazer referência a este [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")`.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Propriedade de legenda (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Propriedade Description (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [Propriedade UniqueName (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
