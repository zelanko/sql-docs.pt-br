---
title: Item de propriedade (conjunto de células do ADO MD) | Microsoft Docs
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
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f22f8195a082ffe1333efe46a270fb1e18057ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="item-property-ado-md-cellset"></a>Propriedade item (conjunto de células do ADO MD)
Recupera uma célula de uma [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) usando suas coordenadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Posições*  
 Um **VariantArray** de valores que especificam exclusivamente uma célula. *Posições* pode ser um dos seguintes:  
  
-   Uma matriz de números de posição  
  
-   Uma matriz de nomes de membro  
  
-   A posição ordinal  
  
## <a name="remarks"></a>Remarks  
 Use o **Item** propriedade para retornar um [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto dentro de um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto. Se o **Item** propriedade não é possível localizar a célula correspondente a *posições* argumento, um erro ocorre.  
  
 O **Item** é a propriedade padrão para o **conjunto de células** objeto. Formas de sintaxe a seguir são intercambiáveis:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Remarks  
 O *posições* argumento especifica qual célula para retornar. Você pode especificar a célula pela posição ordinal ou pela posição de cada eixo. Ao especificar a célula por posição em cada eixo, você pode especificar o valor numérico da posição ou os nomes dos membros para cada posição.  
  
 A posição ordinal é um número que identifica exclusivamente uma célula dentro de **conjunto de células**. Conceitualmente, as células são numeradas em um **conjunto de células** como se o **conjunto de células** foram um *p*-matriz dimensional, onde *p* é o número de eixos. As células são tratadas em ordem linha-principal. Abaixo está a fórmula para calcular o número ordinal de uma célula:  
  
 Se os nomes de membro são passados como cadeias de caracteres para **Item**, os membros devem ser listados em ordem crescente de identificadores de eixo numérico. Dentro de um eixo, os membros devem ser listados em ordem crescente de aninhamento de dimensão — ou seja, membros da dimensão mais externa vier primeiro, seguido por membros das dimensões internas. Cada dimensão deve ser representado por uma cadeia de caracteres separada, e a lista de cadeias de caracteres de membro deve ser separada por vírgulas.  
  
> [!NOTE]
>  Recuperando células por nome de membro não pode ter suporte por seu provedor de dados. Consulte a documentação do provedor para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de célula (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
