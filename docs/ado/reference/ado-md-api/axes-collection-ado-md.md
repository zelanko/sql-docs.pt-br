---
title: Eixos de coleção (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04ffa05b5912b00a59389b7f2d5e6665541662eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="axes-collection-ado-md"></a>Coleção de eixos (ADO MD)
Contém o [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definem um conjunto de células.  
  
## <a name="remarks"></a>Remarks  
 Um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto contém um **eixos** coleção. Uma vez o **conjunto de células** é aberto, essa coleção contém pelo menos um **eixo**. Consulte o [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objeto para obter uma explicação mais detalhada de como usar **eixo** objetos.  
  
> [!NOTE]
>  Eixo do filtro de uma **conjunto de células** não está contida no **eixos** coleção. Consulte o [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propriedade para obter mais informações.  
  
 **Eixos** é uma coleção padrão do ADO. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obter o número de objetos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Retorna um objeto da coleção com o padrão [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Atualizar os objetos na coleção do provedor com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de conjunto de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
