---
description: Manipular dados multidimensionais
title: Trabalhando com dados multidimensionais | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: rothja
ms.author: jroth
ms.openlocfilehash: 0589b1fe5ca6da29f088e26b2236cfc5205bfe0c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978567"
---
# <a name="working-with-multidimensional-data"></a>Manipular dados multidimensionais
Um *células* é o resultado de uma consulta em dados multidimensionais. Ele consiste em uma coleção de eixos, geralmente não mais do que quatro eixos e geralmente apenas dois ou três. Um *eixo* é uma coleção de membros de uma ou mais dimensões, que é usada para localizar ou filtrar valores específicos em um cubo.  
  
 Uma *posição* é um ponto ao longo de um eixo. Para um eixo que consiste em uma única dimensão, essas posições são um subconjunto dos membros da dimensão. Se um eixo consistir em mais de uma dimensão, cada posição será uma entidade composta, que tem *n* partes em que *n* é o número de dimensões orientadas ao longo desse eixo. Cada parte da posição é um membro de uma dimensão constituinte.  
  
 Por exemplo, se as dimensões de Geografia e produto de um cubo que contém dados de vendas forem orientadas ao longo do eixo x de um células, uma posição ao longo desse eixo poderá conter os membros "EUA" e "computadores". Neste exemplo, a determinação de uma posição ao longo do eixo x requer que os membros de cada dimensão sejam orientados ao longo do eixo.  
  
 Uma *célula* é um objeto posicionado na interseção de coordenadas do eixo. Cada célula tem várias informações associadas a ela, incluindo os dados em si, uma cadeia de caracteres formatada (a forma de exibição de dados da célula) e o valor ordinal da célula. (Cada célula é um valor ordinal exclusivo no células. O valor ordinal da primeira célula no células é zero, enquanto a célula mais à esquerda na segunda linha de um células com oito colunas teria um valor ordinal de oito.)  
  
 Por exemplo, um cubo tem as seis dimensões a seguir (Observe que esse esquema de cubos difere ligeiramente do exemplo fornecido em [visão geral dos dados e esquemas multidimensionais](./overview-of-multidimensional-schemas-and-data.md)):  
  
-   Salesperson  
  
-   Geografia (hierarquia natural)-continentes, países, Estados e assim por diante  
  
-   Trimestres-trimestres, meses, dias  
  
-   Years  
  
-   Medidas-vendas, PercentChange, BudgetedSales  
  
-   Produtos  
  
 O células a seguir representa as vendas de 1991 para todos os produtos:  
  
> [!NOTE]
>  Os valores de célula no exemplo podem ser exibidos como pares ordenados de ordinais de posição do eixo em que o primeiro dígito representa a posição do eixo x e o segundo dígito a posição do eixo y.  
  
 As características desse células são as seguintes:  
  
-   Dimensões do eixo: trimestres, vendedor, Geografia  
  
-   Dimensões de filtro: medidas, anos, produtos  
  
-   Dois eixos: coluna (x ou eixo 0) e linha (y ou eixo 1)  
  
-   eixo x: duas dimensões aninhadas, vendedor e Geografia  
  
-   eixo y: dimensão de trimestres  
  
 O eixo x tem duas dimensões aninhadas: vendedor e geografia. Na geografia, quatro membros são selecionados: Seattle, Boston, EUA-Sul e Japão. Dois membros são selecionados do vendedor: namorado e Nash. Isso produz um total de oito posições neste eixo (8 = 4 * 2).  
  
 Cada coordenada é representada como uma posição com dois membros – um da dimensão vendedor e outro da dimensão Geografia:  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 O eixo y tem apenas uma dimensão, contendo as oito posições a seguir:  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Células, Cells, Axes e Positions são todos representados em ADO MD por objetos correspondentes: [células](../../reference/ado-md-api/cellset-object-ado-md.md), [Cell](../../reference/ado-md-api/cell-object-ado-md.md), [Axis](../../reference/ado-md-api/axis-object-ado-md.md)e [Position](../../reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de objeto ADO MD](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](./ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas multidimensionais e dados](./overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](./programming-with-ado-md.md)   
 [Usar o ADO com ADO MD](./using-ado-with-ado-md.md)