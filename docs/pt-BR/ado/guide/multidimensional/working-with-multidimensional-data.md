---
title: Trabalhando com dados multidimensionais | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8368710b3377520771a2cfa3bc936bb3fbd1653
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-multidimensional-data"></a>Trabalhando com dados multidimensionais
Um *conjunto de células* é o resultado de uma consulta em dados multidimensionais. Ele consiste em uma coleção de eixos, geralmente não mais do que quatro eixos e geralmente apenas dois ou três. Um *eixo* é uma coleção de membros de uma ou mais dimensões, que é usada para localizar ou filtrar valores específicos em um cubo.  
  
 Um *posição* é um ponto em um eixo. Para um eixo consiste em uma única dimensão, essas posições são um subconjunto dos membros de dimensão. Se um eixo consiste em mais de uma dimensão, cada posição é uma entidade composta, que tem *n* partes onde *n* é o número de dimensões orientados ao longo do eixo. Cada parte da posição é um membro de uma dimensão constituinte.  
  
 Por exemplo, se as dimensões de Geografia e de produto de um cubo que contém dados de vendas são orientadas ao longo do eixo x de um conjunto de células, uma posição ao longo desse eixo pode conter os membros "EUA" e "Computadores". Neste exemplo, determinar uma posição no eixo requer que os membros de cada dimensão são orientados ao longo do eixo.  
  
 Um *célula* é um objeto posicionado na interseção de coordenadas do eixo. Cada célula tem várias partes de informações associadas, incluindo os dados em si, uma cadeia de caracteres formatada (o formulário de exibição de dados de célula) e o valor ordinal da célula. (Cada célula é um valor ordinal exclusivo no conjunto de células. O valor ordinal da primeira célula no conjunto de células é zero, enquanto a célula mais à esquerda na segunda linha de um conjunto de células com oito colunas teria um valor ordinal de oito.)  
  
 Por exemplo, um cubo tem as seguintes dimensões de seis (Observe que esse esquema de cubo é ligeiramente diferente do exemplo fornecido em [visão geral de esquemas multidimensionais e dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Vendedor  
  
-   Geografia (hierarquia natural) — continentes, países, Estados e assim por diante  
  
-   Trimestres — Dias de trimestres, meses,  
  
-   Years  
  
-   Medidas — Vendas, PercentChange, BudgetedSales  
  
-   Products  
  
 O conjunto de células a seguir representa as vendas para 1991 para todos os produtos:  
  
> [!NOTE]
>  Os valores de célula no exemplo podem ser exibidos como pares ordenadas de ordinais de posição do eixo onde o primeiro dígito representa a posição do eixo x e o segundo dígito a posição do eixo y.  
  
 As características desse conjunto de células são as seguintes:  
  
-   Dimensões de eixo: trimestres, vendedor, geografia  
  
-   Dimensões de filtro: medidas, anos, produtos  
  
-   Dois eixos: (x, ou eixo 0) de coluna e linha (y, ou eixo 1)  
  
-   eixo x: dois aninhados dimensões, o vendedor e Geografia  
  
-   eixo y: dimensão trimestres  
  
 O eixo x possui duas dimensões aninhadas: vendedor e Geografia. De geografia, quatro membros estão selecionados: Seattle, Boston, Sul dos EUA e Japão. Dois membros forem selecionados da vendedor: dos Namorados e Nash. Isso resulta em um total de oito posições este eixo (8 = 4 * 2).  
  
 Cada coordenada é representada como uma posição com dois membros — entre a dimensão de vendedor e outra da dimensão Geografia:  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 O eixo y tem apenas uma dimensão, que contém as posições de oito seguintes:  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Conjuntos de células, células, eixos e posições são todos representadas no ADO MD por objetos correspondentes: [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), e [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
