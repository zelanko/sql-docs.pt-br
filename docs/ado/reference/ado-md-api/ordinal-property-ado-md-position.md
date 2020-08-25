---
description: Propriedade Ordinal (Posição do ADO MD)
title: Propriedade ordinal (posição de ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: c2f145cf96222eb08ab154dc9d683c0973cad861
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777915"
---
# <a name="ordinal-property-ado-md-position"></a>Propriedade Ordinal (Posição do ADO MD)
Identifica exclusivamente uma [posição](./position-object-ado-md.md) ao longo de um eixo.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um inteiro **longo** e é somente leitura.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ordinal** de um objeto [Position](./position-object-ado-md.md) corresponde ao índice da **posição** dentro da coleção [Positions](./positions-collection-ado-md.md) .  
  
 Uma célula pode ser recuperada rapidamente usando o **ordinal** da **posição** ao longo de cada eixo com a propriedade [Item](./item-property-ado-md-cellset.md) do objeto [células](./cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Position (ADO MD)](./position-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto células (ADO MD)](./cellset-object-ado-md.md)   
 [Propriedade Item (ADO MD células)](./item-property-ado-md-cellset.md)   
 [Propriedade Ordinal (Célula do ADO MD)](./ordinal-property-ado-md-cell.md)