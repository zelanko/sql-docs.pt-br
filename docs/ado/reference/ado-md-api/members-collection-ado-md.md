---
title: Coleção Members (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79394abee5b12bb10f34a34e882d2ac0562722fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949437"
---
# <a name="members-collection-ado-md"></a>Coleção Members (ADO MD)
Contém os objetos de [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) de um nível ou uma posição ao longo de um eixo.  
  
## <a name="remarks"></a>Comentários  
 Uma coleção de **Membros** é usada para conter os seguintes tipos de membros:  
  
-   Os membros que compõem um nível em um cubo. Eles estão contidos na coleção **Members** de um objeto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Por exemplo, usando o exemplo de [visão geral de esquemas e dados multidimensionais](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), os quatro membros do nível de países são Canadá, EUA, Reino Unido e Alemanha.  
  
-   Os membros que são os filhos de um membro específico dentro de uma hierarquia. Esses membros são retornados pela propriedade [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) do objeto **membro** pai. Por exemplo, novamente usando o mesmo exemplo, os dois filhos do membro do Canadá são Canadá-Leste e Canadá-oeste.  
  
-   Os membros que definem uma posição específica ao longo de um eixo de um [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Usando o células do [trabalho com dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como um exemplo, os dois membros da primeira posição no eixo x são namorados e Seattle. Esses membros são contidos na coleção **Members** de um objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
 **Membros** é uma coleção padrão do ADO. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obtenha o número de objetos na coleção com a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Retornar um objeto da coleção com a propriedade de [Item](../../../ado/reference/ado-api/item-property-ado.md) padrão.  
  
-   Atualize os objetos na coleção do provedor com o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de Membros (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
