---
title: MultiLineString | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 9244f32b2ee9921d1caaa63b5d6aae9c324049ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014204"
---
# <a name="multilinestring"></a>MultiLineString
  Um `MultiLineString` é uma coleção de zero ou mais `geometry` instâncias ou **geographyLineString** .  
  
## <a name="multilinestring-instances"></a>Instâncias MultiLineString  
 A ilustração a seguir mostra exemplos de instâncias `MultiLineString`.  
  
 ![Exemplos das instâncias geométricas MultiLineString](../../database-engine/media/multilinestring.gif "Exemplos das instâncias geométricas MultiLineString")  
  
 Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma `MultiLineString` instância simples cujo limite é de quatro pontos de extremidade de seus `LineString` dois elementos.  
  
-   A Figura 2 é uma instância `MultiLineString` simples porque apenas os pontos de extremidade da interseção de elementos `LineString` se cruzam. O limite são os dois pontos de extremidade que não se sobrepõem.  
  
-   A Figura 3 é uma instância `MultiLineString` não simples porque apenas o interior de um de seus elementos `LineString` se cruzam. O limite dessa instância `MultiLineString` são os quatro pontos de extremidade.  
  
-   A Figura 4 é uma instância `MultiLineString` não simples, não fechada.  
  
-   A Figura 5 é uma instância `MultiLineString` simples, não fechada. Ele não está fechado porque seus `LineStrings` elementos não estão fechados. Ela é simples porque nenhum dos interiores de qualquer uma das instâncias `LineStrings` se cruzam.  
  
-   A Figura 6 é uma instância `MultiLineString` simples e fechada. Ela é fechada porque todos os seus elementos não estão fechados. Ela é simples porque nenhum de seus elementos se cruzam nos interiores.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Para uma instância `MultiLineString` ser aceita, ela precisa estar vazia ou conter apenas instâncias `LineString` que sejam aceitos. Para obter mais informações sobre `LineString` instâncias aceitas, consulte [LineString](../spatial/linestring.md). Veja a seguir exemplos de instâncias `MultiLineString` aceitas.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 O exemplo a seguir gera um `System.FormatException` porque a segunda instância `LineString` não é válida.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Para que uma instância `MultiLineString` seja válida, ela deve atender aos seguintes critérios:  
  
1.  Todas as instâncias contendo a instância `MultiLineString` devem ser instâncias `LineString` válidas.  
  
2.  Duas instâncias `LineString` contendo a instância `MultiLineString` não podem se sobrepor em um intervalo. Apenas em um número finito de pontos, é possível encontrar as instâncias `LineString` se cruzando ou se tocando umas com as outras, ou com outras instâncias `LineString`.  
  
 O exemplo a seguir mostra três instâncias `MultiLineString` válidas e uma instância `MultiLineString` que não é válida.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` não é válido porque a segunda instância `LineString` sobrepõe a primeira instância `LineString` em um intervalo. Elas se tocam em um número infinito de pontos.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância simples do `geometry``MultiLineString` , que contém dois elementos de `LineString` com o SRID 0.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 Para instanciar essa instância com um SRID diferente, use `STGeomFromText()` ou `STMLineStringFromText()`. Também é possível usar `Parse()` e, em seguida, modificar o SRID, conforme mostrado no exemplo a seguir.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STLength &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [LineString](../spatial/linestring.md)   
 [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
