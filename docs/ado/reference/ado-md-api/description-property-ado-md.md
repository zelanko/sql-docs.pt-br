---
description: Propriedade Description (ADO MD)
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
ms.openlocfilehash: acc3d3554e4046321b1fe76beebc9dddc942b5ac
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778215"
---
# <a name="description-property-ado-md"></a>Propriedade Description (ADO MD)
Retorna uma explicação de texto do objeto atual.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna uma **cadeia de caracteres** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 Para objetos de [membro](./member-object-ado-md.md) , a **Descrição** aplica-se somente aos membros de fórmula e de medida. **Descrição** retorna uma cadeia de caracteres vazia ("") para todos os outros tipos de membros. Para obter mais informações sobre os vários tipos de membros, consulte a propriedade [Type](./type-property-ado-md.md) .  
  
 Essa propriedade só tem suporte em objetos **Membros** que pertencem a um objeto de [nível](./level-object-ado-md.md) . Um erro ocorre quando essa propriedade é referenciada de objetos **Membros** que pertencem a um objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
        [Objeto Dimension (ADO MD)](./dimension-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Hierarchy (ADO MD)](./hierarchy-object-ado-md.md)  
        [Objeto Level (ADO MD)](./level-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Member (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::