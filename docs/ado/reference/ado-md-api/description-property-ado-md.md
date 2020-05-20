---
title: Propriedade Description (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: rothja
ms.author: jroth
ms.openlocfilehash: 05efe4c1e31f1ee9c7b7abd130a9d9c810ab12f4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764307"
---
# <a name="description-property-ado-md"></a>Propriedade Description (ADO MD)
Retorna uma explicação de texto do objeto atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Para objetos de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) , a **Descrição** aplica-se somente aos membros de fórmula e de medida. **Descrição** retorna uma cadeia de caracteres vazia ("") para todos os outros tipos de membros. Para obter mais informações sobre os vários tipos de membros, consulte a propriedade [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) .  
  
 Essa propriedade só tem suporte em objetos **Membros** que pertencem a um objeto de [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
  
||||  
|-|-|-|  
|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
