---
title: Trabalhando com dados multidimensionais | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb1f29a3037cafdddc14973f77d7bb3d8c52f296
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350262"
---
# <a name="working-with-multidimensional-data"></a>Manipular dados multidimensionais
Um *conjunto de células* é o resultado de uma consulta em dados multidimensionais. Ele consiste em uma coleção de eixos, normalmente não mais do que quatro eixos e normalmente apenas dois ou três. Uma *eixo* é uma coleção de membros de uma ou mais dimensões, que é usada para localizar ou filtrar valores específicos em um cubo.  
  
 Um *posição* é um ponto ao longo do eixo. Para um eixo que consiste em uma única dimensão, essas posições são um subconjunto dos membros de dimensão. Se um eixo consiste em mais de uma dimensão e, em seguida, cada posição é uma entidade composta, que tem *n* partes where *n* é o número de dimensões orientados ao longo desse eixo. Cada parte da posição é um membro de uma dimensão constituinte.  
  
 Por exemplo, se as dimensões de Geografia e o produto de um cubo que contém dados de vendas são orientadas ao longo do eixo x de um conjunto de células, uma posição ao longo deste eixo pode conter os membros "EUA" e "Computadores". Neste exemplo, determinar uma posição ao longo do eixo x requer que os membros de cada dimensão são orientados ao longo do eixo.  
  
 Um *célula* é um objeto posicionado na interseção de coordenadas do eixo. Cada célula tem várias partes de informações associado a ele, incluindo os dados em si, uma cadeia de caracteres formatada (o formulário de exibição dos dados da célula) e o valor ordinal da célula. (Cada célula é um valor ordinal exclusivo no conjunto de células. O valor ordinal da primeira célula no conjunto de células é zero, enquanto a célula mais à esquerda na segunda linha de um conjunto de células com oito colunas teria um valor ordinal de oito.)  
  
 Por exemplo, um cubo tem as seguintes seis dimensões (Observe que esse esquema de cubo é ligeiramente diferente do exemplo fornecido em [visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Vendedor  
  
-   Geografia (hierarquia natural) — continentes, países, Estados e assim por diante  
  
-   Trimestres — Dias de trimestres, meses,  
  
-   Years  
  
-   Medidas, Vendas, PercentChange, BudgetedSales  
  
-   Products  
  
 O conjunto de células a seguir representa as vendas de 1991 para todos os produtos:  
  
> [!NOTE]
>  No exemplo, os valores de célula podem ser exibidos como pares ordenados de ordinais de posição do eixo onde o primeiro dígito representa a posição do eixo x e o segundo dígito a posição do eixo y.  
  
 As características deste conjunto de células são da seguinte maneira:  
  
-   Dimensões de eixo: trimestres, vendedor, geografia  
  
-   Dimensões de filtro: medidas, anos, os produtos  
  
-   Dois eixos: coluna (x, ou eixo 0) e linha (y ou eixo 1)  
  
-   eixo x: dois aninhados dimensões, o vendedor e Geografia  
  
-   eixo y: dimensão trimestres  
  
 O eixo x tem duas dimensões aninhadas: vendedor e Geografia. De geografia, quatro membros são selecionados: Seattle, Boston, Sul dos EUA e Japão. Dois membros são selecionados de vendedor: Valentine e Nash. Isso resulta em um total de oito posições nesse eixo (8 = 4 * 2).  
  
 Cada coordenada é representada como uma posição com dois membros — uma dimensão de vendedor e outro da dimensão Geografia:  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 O eixo y tem apenas uma dimensão, que contém as seguintes oito posições:  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Conjuntos de células, células, eixos e posições são todos representadas no ADO MD por objetos correspondentes: [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md), e [posição](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
