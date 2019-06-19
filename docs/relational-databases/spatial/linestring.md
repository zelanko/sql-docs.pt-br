---
title: LineString | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c340ec4e6b650784823869b8715579448229fb4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935202"
---
# <a name="linestring"></a>LineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um **LineString** é um objeto unidimensional que representa uma sequência de pontos e os segmentos de linha que os conectam.  
  
## <a name="linestring-instances"></a>Instâncias LineString  
 A ilustração abaixo mostra exemplos de instâncias **LineString** .  
  
 ![Exemplos de instâncias geométricas LineString](../../relational-databases/spatial/media/linestring.gif "Exemplos de instâncias geométricas LineString")  
  
Conforme mostrado na ilustração:  
  
-   A Figura 1 é uma instância **LineString** simples, não fechada.  
  
-   A Figura 2 é uma instância **LineString** não simples, não fechada.  
  
-   A Figura 3 é uma instância **LineString** fechada, simples e, portanto, é um anel.  
  
-   A Figura 4 é uma instância **LineString** fechada, não simples e, portanto, não é um anel.  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
As instâncias **LineString** aceitas podem ser inseridas em uma variável geometry, mas talvez não sejam instâncias **LineString** válidas. Os critérios a seguir devem ser atendidos para que uma instância **LineString** seja aceita. A instância deve ser formada por pelo menos dois pontos ou deve estar vazia. As instâncias LineString a seguir são aceitas.  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
`@g3` mostra que uma instância **LineString** pode ser aceita, mas não válida.  
  
A instância **LineString** a seguir não é aceita. Ela irá gerar um `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
Para que uma instância **LineString** seja válida, ela deve atender aos critérios a seguir.  
  
1.  A instância **LineString** deve ser aceita.  
2.  Se uma instância **LineString** não for vazia, ela deverá conter, pelo menos, dois pontos distintos.  
3.  A instância **LineString** não pode se sobrepor sobre um intervalo de dois ou mais pontos consecutivos.  
  
As instâncias **LineString** a seguir são válidas.  
  
```sql  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
As instâncias **LineString** a seguir não são válidas.  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
> A detecção de sobreposições de **LineString** baseia-se em cálculos de pontos flutuantes, os quais não são exatos.  
  
## <a name="examples"></a>Exemplos  
### <a name="example-a"></a>Exemplo A.    
O exemplo a seguir mostra como criar uma instância `geometry``LineString` com três pontos e uma SRID de 0:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
### <a name="example-b"></a>Exemplo B.   
Cada ponto na instância `LineString` pode conter valores Z (elevação) e M (medida). Esse exemplo adiciona valores de M à instância `LineString` criada no exemplo acima. M e Z podem ser valores nulos.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
### <a name="example-c"></a>Exemplo C.   
O exemplo a seguir mostra como criar uma instância `geometry LineString` com dois pontos iguais. Uma chamada para `IsValid` indica que a instância **LineString** não é válida e uma chamada para `MakeValid` converterá a instância **LineString** em um **Point**.  
  
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
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
