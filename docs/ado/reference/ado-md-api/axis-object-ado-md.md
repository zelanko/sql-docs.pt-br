---
description: Objeto Axis (ADO MD)
title: Objeto Axis (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: 6206ee753e42853dc0f209cb80fb9571806f68d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987387"
---
# <a name="axis-object-ado-md"></a>Objeto Axis (ADO MD)
Representa um eixo de posição ou de filtro de um células, que contém os membros selecionados de uma ou mais dimensões.  
  
## <a name="remarks"></a>Comentários  
 Um objeto de **eixo** pode ser contido por uma coleção de [eixos](./axes-collection-ado-md.md) ou retornado pela propriedade [FilterAxis](./filteraxis-property-ado-md.md) de um [células](./cellset-object-ado-md.md).  
  
 Com as coleções e propriedades de um objeto **Axis** , você pode fazer o seguinte:  
  
-   Identifique o **eixo** com a propriedade [Name](./name-property-ado-md.md) .  
  
-   Iterar em cada posição ao longo de um **eixo** usando a coleção [Positions](./positions-collection-ado-md.md) .  
  
-   Obtenha o número de dimensões no **eixo** com a propriedade [DimensionCount](./dimensioncount-property-ado-md.md) .  
  
-   Obtenha atributos específicos do provedor do **eixo** com a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de eixo (VBScript)](./axis-example-vbscript.md)   
 [Coleção Axes (ADO MD)](./axes-collection-ado-md.md)   
 [Coleção Positions (ADO MD)](./positions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)