---
title: Visão geral de esquemas multidimensionais e dados | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a4a2f6dbd2c5d075bb888e61bb01e1094c8ef5c0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748085"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Visão geral de dados e esquemas multidimensionais
## <a name="understanding-multidimensional-schemas"></a>Noções básicas sobre esquemas multidimensionais  
 O objeto de metadados central no ADO MD é o *cubo*, que consiste em um conjunto estruturado de dimensões, hierarquias, níveis e membros relacionados.  
  
 Uma *dimensão* é uma categoria independente de dados de seu banco de dado multidimensional, derivadas de suas entidades comerciais. Normalmente, uma dimensão contém itens a serem usados como critérios de consulta para as medidas do banco de dados.  
  
 Uma *hierarquia* é um caminho de agregação de uma dimensão. Uma dimensão pode ter vários níveis de granularidade, que têm relações pai-filho. Uma hierarquia define como esses níveis são relacionados.  
  
 Um *nível* é uma etapa da agregação em uma hierarquia. Para dimensões com várias camadas de informações, cada camada é um nível.  
  
 Um *membro* é um item de dados em uma dimensão. Normalmente, você cria uma legenda ou descreve uma medida do banco de dados usando membros.  
  
 Os cubos são representados por objetos [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) no ADO MD. Dimensões, hierarquias, níveis e membros também são representadas por seus objetos ADO MD correspondentes: [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md)e [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensões  
 As dimensões de um cubo dependem de suas entidades de negócios e tipos de dados a serem modelados no banco de dado. Normalmente, cada dimensão é um ponto de entrada independente ou mecanismo para a seleção de dados.  
  
 Por exemplo, um cubo que contém dados de vendas tem as cinco dimensões a seguir: vendedor, geografia, hora, produtos e medidas. A dimensão medidas contém valores de dados de vendas reais, enquanto as outras dimensões representam maneiras de categorizar e agrupar os valores de dados de vendas.  
  
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
 As hierarquias definem as maneiras em que os níveis de uma dimensão podem ser "acumulados" ou agrupados. Uma dimensão pode ter mais de uma hierarquia. Existe uma hierarquia natural na dimensão Geografia:  
  
### <a name="levels"></a>Níveis  
 Na dimensão Geografia de exemplo, mostrada na figura anterior, cada caixa representa um nível na hierarquia.  
  
 Cada nível tem um conjunto de membros, da seguinte maneira:  
  
-   O mundo`= {All}`  
  
-   Continentes`= {North America, Europe}`  
  
-   Países`= {Canada, USA, UK, Germany}`  
  
-   Regiões`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Primeiras`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Membros  
 Os membros no nível folha de uma hierarquia não têm filhos e os membros no nível raiz não têm nenhum pai. Todos os outros membros têm pelo menos um pai e pelo menos um filho. Por exemplo, uma passagem parcial da árvore de hierarquia na dimensão Geografia produz as seguintes relações pai-filho:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Os membros podem ser consolidados ao longo de uma ou mais hierarquias por dimensão. Considere uma dimensão de tempo em que há duas maneiras de se acumular no nível de ano a partir do nível de dias:  
  
 Este exemplo também ilustra outra característica: alguns membros do nível semana da hierarquia ano-semana não aparecem em nenhum nível da hierarquia ano-trimestre. Portanto, uma hierarquia não precisa incluir todos os membros de uma dimensão.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
