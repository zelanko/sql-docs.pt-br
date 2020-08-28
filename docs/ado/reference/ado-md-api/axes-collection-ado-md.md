---
description: Coleção Axes (ADO MD)
title: Coleção Axes (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: rothja
ms.author: jroth
ms.openlocfilehash: 78113cb7854ec3f56ffe6f7322a6bb732939f27f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987407"
---
# <a name="axes-collection-ado-md"></a>Coleção Axes (ADO MD)
Contém os objetos [Axis](./axis-object-ado-md.md) que definem um células.  
  
## <a name="remarks"></a>Comentários  
 Um objeto [células](./cellset-object-ado-md.md) contém uma coleção de **eixos** . Depois que o **células** for aberto, essa coleção conterá pelo menos um **eixo**. Consulte o objeto [Axis](./axis-object-ado-md.md) para obter uma explicação mais detalhada de como usar objetos **Axis** .  
  
> [!NOTE]
>  O eixo de filtro de um **células** não está contido na coleção de **eixos** . Consulte a propriedade [FilterAxis](./filteraxis-property-ado-md.md) para obter mais informações.  
  
 **Eixos** é uma coleção ADO padrão. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obtenha o número de objetos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Retornar um objeto da coleção com a propriedade de [Item](../ado-api/item-property-ado.md) padrão.  
  
-   Atualize os objetos na coleção do provedor com o método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](./cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](./axis-object-ado-md.md)