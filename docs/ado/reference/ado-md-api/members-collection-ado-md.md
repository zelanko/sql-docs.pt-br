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
manager: craigg
ms.openlocfilehash: 541e1098dfd18210e7c07a0718ecd3add758c8a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616944"
---
# <a name="members-collection-ado-md"></a>Coleção Members (ADO MD)
Contém o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos de um nível ou uma posição ao longo do eixo.  
  
## <a name="remarks"></a>Comentários  
 Um **membros** coleção é usada para conter os seguintes tipos de membros:  
  
-   Os membros que constituem um nível em um cubo. Estão contidos na **membros** coleção de uma [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto. Por exemplo, usando a amostra do [visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), os quatro membros do nível de países são EUA, Canadá, Reino Unido e Alemanha.  
  
-   Os membros que são filhos de um membro específico dentro de uma hierarquia. Esses membros são retornados pelo [filhos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propriedade do pai **membro** objeto. Por exemplo, novamente usando o mesmo exemplo, dois filhos do membro Canadá são Leste do Canadá e Oeste do Canadá.  
  
-   Os membros que definem uma posição específica ao longo do eixo de um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Usando o conjunto de células do [trabalhando com dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) como exemplo, os dois membros da primeira posição no eixo x são Valentine e Seattle. Esses membros são contidos pelos **membros** coleção de uma [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto.  
  
 **Membros** é uma coleção padrão de ADO. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obter o número de objetos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Retornar um objeto da coleção com o padrão [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Atualizar os objetos na coleção do provedor com o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo Members (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Objeto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
