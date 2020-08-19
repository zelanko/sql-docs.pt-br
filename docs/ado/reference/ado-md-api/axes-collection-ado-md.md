---
description: Coleção Axes (ADO MD)
title: Coleção Axes (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: cc93e9ea8568a535067addbd51258074945200db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441308"
---
# <a name="axes-collection-ado-md"></a>Coleção Axes (ADO MD)
Contém os objetos [Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md) que definem um células.  
  
## <a name="remarks"></a>Comentários  
 Um objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) contém uma coleção de **eixos** . Depois que o **células** for aberto, essa coleção conterá pelo menos um **eixo**. Consulte o objeto [Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md) para obter uma explicação mais detalhada de como usar objetos **Axis** .  
  
> [!NOTE]
>  O eixo de filtro de um **células** não está contido na coleção de **eixos** . Consulte a propriedade [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) para obter mais informações.  
  
 **Eixos** é uma coleção ADO padrão. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obtenha o número de objetos na coleção com a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Retornar um objeto da coleção com a propriedade de [Item](../../../ado/reference/ado-api/item-property-ado.md) padrão.  
  
-   Atualize os objetos na coleção do provedor com o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
