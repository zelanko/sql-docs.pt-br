---
title: Visão geral dos dados e esquemas multidimensionais | Microsoft Docs
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
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7dad7be35de7e15ae560f56c3ad51f7222be53b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Visão geral de esquemas Multidimensional e de dados
## <a name="understanding-multidimensional-schemas"></a>Noções básicas sobre esquemas Multidimensional  
 O objeto de metadados centrais no ADO MD é o *cubo*, que consiste em um conjunto estruturado de dimensões relacionadas, hierarquias, níveis e membros.  
  
 Um *dimensão* é uma categoria independente de dados do banco de dados multidimensional, derivado de suas entidades de negócios. Geralmente, uma dimensão contém itens a ser usado como critério de consulta para as medidas do banco de dados.  
  
 Um *hierarquia* é um caminho de agregação de uma dimensão. Uma dimensão pode ter vários níveis de granularidade, que têm relações pai-filho. Uma hierarquia define como esses níveis são relacionados.  
  
 Um *nível* é uma etapa de agregação em uma hierarquia. Para dimensões com várias camadas de informações, cada camada é um nível.  
  
 Um *membro* é um item de dados em uma dimensão. Normalmente, você cria uma legenda ou descreve uma medida do banco de dados usando membros.  
  
 Os cubos são representados por [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objetos MD ADO. Dimensões, hierarquias, níveis e membros também são representados por seus objetos correspondentes do ADO MD: [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md), e [ Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensões  
 As dimensões de um cubo dependem de suas entidades de negócios e os tipos de dados a ser modelada no banco de dados. Normalmente, cada dimensão é um ponto de entrada independentes ou de um mecanismo para selecionar os dados.  
  
 Por exemplo, um cubo que contém dados de vendas tem as seguintes cinco dimensões: vendedor, geografia, hora, produtos e medidas. A dimensão de medidas contém valores de dados de vendas reais, enquanto outras dimensões representam maneiras de classificar e agrupar os valores de dados de vendas.  
  
 A dimensão Geografia tem o seguinte conjunto de membros:  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>Hierarquias  
 Hierarquias definem as maneiras em que os níveis de uma dimensão podem ser "acumulados" ou agrupados. Uma dimensão pode ter mais de uma hierarquia. Existe uma hierarquia natural na dimensão Geografia:  
  
### <a name="levels"></a>Levels  
 Na dimensão Geografia, exemplo mostrada na figura anterior, cada caixa representa um nível na hierarquia.  
  
 Cada nível tem um conjunto de membros, da seguinte maneira:  
  
-   O mundo `= {All}`  
  
-   Continentes `= {North America, Europe}`  
  
-   Países `= {Canada, USA, UK, Germany}`  
  
-   Regiões `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Cidades `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Membros  
 Membros do nível folha de uma hierarquia não têm filhos e membros no nível raiz não tem um pai. Todos os outros membros tem pelo menos um pai e pelo menos um filho. Por exemplo, uma passagem parcial da árvore de hierarquia na dimensão Geografia gera as seguintes relações pai-filho:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Membros podem ser consolidados em um ou mais hierarquias por dimensão. Considere uma dimensão de tempo em que há duas maneiras de Rollup para o nível de ano do nível de dias:  
  
 Este exemplo também ilustra outra característica: alguns membros do nível da hierarquia da semana do ano semana não aparecem em qualquer nível da hierarquia de trimestre do ano. Portanto, uma hierarquia não precisa incluir todos os membros de uma dimensão.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
