---
title: MultiLineString | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 290ed8a0bfd3bfdb9733ea98d80aeaaf0f34602a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549676"
---
# <a name="multilinestring"></a>MultiLineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Uma **MultiLineString** é uma coleção de zero ou mais instâncias **geometry** ou **geographyLineString** .  
  
## <a name="multilinestring-instances"></a>Instâncias MultiLineString  
 A ilustração a seguir mostra exemplos de instâncias **MultiLineString** .  
  
 ![Exemplos de instâncias geométricas MultiLineString](../../relational-databases/spatial/media/multilinestring.gif "Exemplos de instâncias geométricas MultiLineString")  
  
 Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma instância **MultiLineString** simples cujo limite são os quatro pontos de extremidade de seus dois elementos **LineString** .  
  
-   A Figura 2 é uma instância **MultiLineString** simples porque apenas os pontos de extremidade da interseção de elementos **LineString** se cruzam. O limite são os dois pontos de extremidade que não se sobrepõem.  
  
-   A Figura 3 é uma instância **MultiLineString** não simples porque apenas o interior de um de seus elementos **LineString** se cruzam. O limite dessa instância **MultiLineString** são os quatro pontos de extremidade.  
  
-   A Figura 4 é uma instância **MultiLineString** não simples, não fechada.  
  
-   A Figura 5 é uma instância **MultiLineString**simples, não fechada. Ela não é fechada porque seus elementos **LineStrings** não estão fechados. Ela é simples porque nenhum dos interiores de qualquer uma das instâncias **LineStrings** se cruzam.  
  
-   A Figura 6 é uma instância **MultiLineString** simples e fechada. Ela é fechada porque todos os seus elementos não estão fechados. Ela é simples porque nenhum de seus elementos se cruzam nos interiores.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Para uma instância **MultiLineString** ser aceita, ela precisa estar vazia ou conter apenas instâncias **LineString** que sejam aceitos. Para obter mais informações sobre instâncias de **LineString** aceitas, consulte [LineString](../../relational-databases/spatial/linestring.md). Veja a seguir exemplos de instâncias **MultiLineString** aceitas.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 O exemplo a seguir gera um `System.FormatException` porque a segunda instância **LineString** não é válida.  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Para que uma instância **MultiLineString** seja válida, ela deve atender aos seguintes critérios:  
  
1.  Todas as instâncias contendo a instância **MultiLineString** devem ser instâncias **LineString** válidas.  
  
2.  Duas instâncias **LineString** contendo a instância **MultiLineString** não podem se sobrepor em um intervalo. Apenas em um número finito de pontos, é possível encontrar as instâncias **LineString** se cruzando ou se tocando umas com as outras, ou com outras instâncias **LineString** .  
  
 O exemplo a seguir mostra três instâncias **MultiLineString** válidas e uma instância **MultiLineString** que não é válida.  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` não é válido porque a segunda instância **LineString** sobrepõe a primeira instância **LineString** em um intervalo. Elas se tocam em um número infinito de pontos.  
  
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
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STIsClosed &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
