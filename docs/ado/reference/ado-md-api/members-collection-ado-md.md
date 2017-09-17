---
title: "A coleção de membros (ADO MD) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d72b7b87507e13ae4aa103a6333e7e2caaf581ae
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="members-collection-ado-md"></a>Coleção de membros (ADO MD)
Contém o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos de um nível ou uma posição em um eixo.  
  
## <a name="remarks"></a>Comentários  
 Um **membros** coleção é usada para conter os seguintes tipos de membros:  
  
-   Os membros que constituem um nível em um cubo. Estão contidos no **membros** coleção de um [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Por exemplo, usando o exemplo do [visão geral de esquemas multidimensionais e dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), os quatro membros do nível de países são Canadá, Estados Unidos, Reino Unido e Alemanha.  
  
-   Os membros que são filhos de um membro específico dentro de uma hierarquia. Esses membros são retornados pelo [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade do pai **membro** objeto. Por exemplo, usando o mesmo exemplo, dois filhos do membro Canadá são Canadá-Leste e Oeste Canadá.  
  
-   Os membros que definem uma posição específica em um eixo de um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Usando o conjunto de células de [trabalhando com dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como exemplo, os dois membros da primeira posição no eixo x são dos Namorados e Seattle. Esses membros contidos pelo **membros** coleção de um [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
 **Membros** é uma coleção padrão do ADO. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obter o número de objetos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Retorna um objeto da coleção com o padrão [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Atualizar os objetos na coleção do provedor com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de membros (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
