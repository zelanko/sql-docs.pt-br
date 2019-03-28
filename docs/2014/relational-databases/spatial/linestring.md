---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 543e248f19e76b0d2caca3ee595778fe430334ea
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531878"
---
# <a name="linestring"></a>LineString
  Um `LineString` é um objeto unidimensional que representa uma sequência de pontos e os segmentos de linha que os conectam.  
  
## <a name="linestring-instances"></a>Instâncias LineString  
 A ilustração a seguir mostra exemplos de instâncias `LineString`.  
  
 ![Exemplos de instâncias geométricas LineString](../../database-engine/media/linestring.gif "Exemplos de instâncias geométricas LineString")  
  
 Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma instância `LineString` simples, não fechada.  
  
-   A Figura 2 é uma instância `LineString` não simples, não fechada.  
  
-   A Figura 3 é uma instância `LineString` fechada, simples e portanto é um anel.  
  
-   A Figura 4 é uma instância `LineString` fechada, não simples e, por isso, não é um anel.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 As instâncias `LineString` aceitas podem ser inseridas em uma variável geometry, mas talvez não sejam instâncias `LineString` válidas. Os seguintes critérios devem ser atendidos para que uma instância `LineString` seja aceita. A instância deve ser formada por pelo menos dois pontos ou deve estar vazia. As instâncias LineString a seguir são aceitas.  
  
```  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
 `@g3` mostra que uma instância `LineString` pode ser aceita, mas não válida.  
  
 A instância `LineString` a seguir não é aceita. Ela irá gerar um `System.FormatException`.  
  
```  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Para que uma instância `LineString` seja válida, ela deve atender aos seguintes critérios.  
  
1.  A instância `LineString` deve ser aceita.  
  
2.  Se uma instância `LineString` não for vazia, ela deverá conter pelo menos dois pontos distintos.  
  
3.  A instância `LineString` não pode se sobrepor sobre um intervalo de dois ou mais pontos consecutivos.  
  
 As instâncias `LineString` a seguir são válidas.  
  
```  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
  
```  
  
 As instâncias `LineString` a seguir não são válidas.  
  
```  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
>  A detecção de sobreposições de `LineString` baseia-se em cálculos de pontos flutuantes, os quais não são exatos.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como criar uma instância `geometry``LineString` com três pontos e uma SRID de 0:  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
 Cada ponto na instância `LineString` pode conter valores Z (elevação) e M (medida). Esse exemplo adiciona valores de M à instância `LineString` criada no exemplo acima. M e Z podem ser valores nulos.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
 O exemplo a seguir mostra como criar uma instância `geometry LineString` com dois pontos iguais. Uma chamada para `IsValid` indica que a instância `LineString` não é válida e uma chamada para `MakeValid` converterá a instância `LineString` em um `Point`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);  
IF @g.STIsValid() = 1  
  BEGIN  
     SELECT @g.ToString() + ' is a valid LineString.';    
  END  
ELSE  
  BEGIN  
     SELECT @g.ToString() + ' is not a valid LineString.';  
     SET @g = @g.MakeValid();  
     SELECT @g.ToString() + ' is a valid Point.';    
  END  
  
```  
  
 Os snippets de código acima irão retornar o seguinte:  
  
```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>Consulte também  
 [STLength &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
