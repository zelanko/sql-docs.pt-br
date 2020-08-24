---
description: Coleção Members (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b302661baefaf7c4e9659e836d92b293d127e2aa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777965"
---
# <a name="members-collection-ado-md"></a>Coleção Members (ADO MD)
Contém os objetos de [membro](./member-object-ado-md.md) de um nível ou uma posição ao longo de um eixo.  
  
## <a name="remarks"></a>Comentários  
 Uma coleção de **Membros** é usada para conter os seguintes tipos de membros:  
  
-   Os membros que compõem um nível em um cubo. Eles estão contidos na coleção **Members** de um objeto [Level](./level-object-ado-md.md) . Por exemplo, usando o exemplo de [visão geral de esquemas e dados multidimensionais](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), os quatro membros do nível de países são Canadá, EUA, Reino Unido e Alemanha.  
  
-   Os membros que são os filhos de um membro específico dentro de uma hierarquia. Esses membros são retornados pela propriedade [Children](./children-property-ado-md.md) do objeto **membro** pai. Por exemplo, novamente usando o mesmo exemplo, os dois filhos do membro do Canadá são Canadá-Leste e Canadá-oeste.  
  
-   Os membros que definem uma posição específica ao longo de um eixo de um [células](./cellset-object-ado-md.md). Usando o células do [trabalho com dados multidimensionais](../../guide/multidimensional/working-with-multidimensional-data.md) como um exemplo, os dois membros da primeira posição no eixo x são namorados e Seattle. Esses membros são contidos na coleção **Members** de um objeto [Position](./position-object-ado-md.md) .  
  
 **Membros** é uma coleção padrão do ADO. Com as propriedades e métodos de uma coleção, você pode fazer o seguinte:  
  
-   Obtenha o número de objetos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Retornar um objeto da coleção com a propriedade de [Item](../ado-api/item-property-ado.md) padrão.  
  
-   Atualize os objetos na coleção do provedor com o método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de Membros (VBScript)](./members-example-vbscript.md)   
 [Objeto Member (ADO MD)](./member-object-ado-md.md)