---
title: Visão geral de esquemas Multidimensional e de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e4681bb9e1fd1028ee1ddc2bd7f72efc03fb6c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923184"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Visão geral de dados e esquemas multidimensionais
## <a name="understanding-multidimensional-schemas"></a>Noções básicas sobre esquemas Multidimensional  
 O objeto de metadados centrais no ADO MD é o *cubo*, que consiste em um conjunto estruturado de dimensões relacionadas, hierarquias, níveis e membros.  
  
 Um *dimensão* é uma categoria independente dos dados do banco de dados multidimensional, derivado de suas entidades de negócios. Normalmente, uma dimensão contém itens a serem usados como critérios de consulta para as medidas do banco de dados.  
  
 Um *hierarquia* é um caminho de agregação de uma dimensão. Uma dimensão pode ter vários níveis de granularidade, que têm relações pai-filho. Uma hierarquia define como esses níveis são relacionados.  
  
 Um *nível* é uma etapa de agregação em uma hierarquia. Para dimensões com várias camadas de informação, cada camada é um nível.  
  
 Um *membro* é um item de dados em uma dimensão. Normalmente, você pode cria uma legenda ou descreve uma medida de banco de dados usando os membros.  
  
 Os cubos são representados por [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objetos em MD ADO. Dimensões, hierarquias, níveis e membros também são representados por seus objetos do ADO MD correspondentes: [Dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md), e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensões  
 As dimensões de um cubo dependem de suas entidades de negócios e os tipos de dados a ser modelada no banco de dados. Normalmente, cada dimensão é um ponto de entrada independente ou um mecanismo para selecionar os dados.  
  
 Por exemplo, um cubo que contém dados de vendas tem as seguintes cinco dimensões: Vendedor, geografia, hora, produtos e medidas. A dimensão de medidas contém valores de dados de vendas reais, enquanto as outras dimensões representam maneiras para categorizar e agrupar os valores de dados de vendas.  
  
 A dimensão Geografia tem o seguinte conjunto de membros:  
  
```console
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
 Na dimensão Geografia, exemplo ilustrada na figura anterior, cada caixa representa um nível na hierarquia.  
  
 Cada nível tem um conjunto de membros, da seguinte maneira:  
  
-   O mundo `= {All}`  
  
-   Continentes `= {North America, Europe}`  
  
-   Países `= {Canada, USA, UK, Germany}`  
  
-   Regiões `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Cidades `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Members  
 Os membros no nível folha de uma hierarquia não têm filhos, e os membros no nível raiz não têm nenhum pai. Todos os outros membros têm pelo menos um pai e pelo menos um filho. Por exemplo, uma passagem parcial da árvore de hierarquia na dimensão Geografia, gera as seguintes relações de pai-filho:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Os membros podem ser consolidados ao longo de um ou mais hierarquias por dimensão. Considere uma dimensão de tempo em que há duas maneiras de Rollup para o nível ano do nível de dias:  
  
 Este exemplo também ilustra outra característica: Alguns membros do nível da hierarquia de ano semana semana não aparecem em qualquer nível da hierarquia de trimestre do ano. Portanto, uma hierarquia não precisa incluir todos os membros de uma dimensão.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
