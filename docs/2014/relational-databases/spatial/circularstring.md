---
title: Circularstring | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: b3eacaba2ad0ddc2c0475d29b151d0a50be98fc0
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688713"
---
# <a name="circularstring"></a>CircularString
  Uma `CircularString` é uma coleção de zero ou mais segmentos de arco circulares contínuos. Um segmento de arco circular é um segmento curvo definido por três pontos em um plano bidimensional; o primeiro ponto não pode ser igual ao terceiro ponto. Se todos os três pontos de um segmento de arco circular forem colineares, o segmento de arco será tratado como um segmento de linha.  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos dos novos recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo o subtipo `CircularString`, baixe os white paper [novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
## <a name="circularstring-instances"></a>Instâncias CircularString  
 O desenho abaixo mostra as instâncias de `CircularString` válidas:  
  
 ![](../../database-engine/media/5ff17e34-b578-4873-9d33-79500940d0bc.png "5ff17e34-b578-4873-9d33-79500940d0bc")  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Uma instância de `CircularString` será aceita se estiver vazia ou contiver um número ímpar de pontos, n, em que n > 1. As instâncias de `CircularString` a seguir são aceitas.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` mostra que `CircularString` instância pode ser aceita, mas não é válida. A declaração da instância CircularString a seguir não é aceita. Essa declaração gera um `System.FormatException`.  
  
```sql
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância de `CircularString` válida deve estar vazia ou ter os seguintes atributos:  
  
-   Ele deve conter pelo menos um segmento de arco circular (ou seja, ter um mínimo de três pontos).  
  
-   O último ponto de extremidade para cada segmento de arco circular na sequência, exceto para o último segmento, deve ser o primeiro ponto de extremidade para o próximo segmento na sequência.  
  
-   Ele deve ter um número ímpar de pontos.  
  
-   Ele não pode se sobrepor por um intervalo.  
  
-   Embora `CircularString` instâncias possam conter segmentos de linha, esses segmentos de linha devem ser definidos por três pontos colineares.  
  
 O exemplo a seguir mostra instâncias de `CircularString` válidas.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 Uma instância de `CircularString` deve conter pelo menos dois segmentos de arco circular para definir um círculo completo. Uma instância de `CircularString` não pode usar um único segmento de arco circular (como (1 1, 3 1, 1 1)) para definir um círculo completo. Use (1 1, 2 2, 3 1, 2 0, 1 1) para definir o círculo.  
  
 O exemplo a seguir mostra instâncias CircularString que não são válidas.  
  
```sql
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### <a name="instances-with-collinear-points"></a>Instâncias com pontos de colineares  
 Nos casos a seguir, um segmento de arco circular será tratado como um segmento de linha:  
  
-   Quando todos os três pontos são colineares (por exemplo, (1 3, 4 4, 7 5)).  
  
-   Quando o primeiro e o ponto do meio são os mesmos, mas o terceiro ponto é diferente (por exemplo, (1 3, 1 3, 7 5)).  
  
-   Quando o meio e o último ponto são os mesmos, mas o primeiro ponto é diferente (por exemplo, (1 3, 4 4, 4 4)).  
  
## <a name="examples"></a>Disso  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-circularstring"></a>um. Instanciando uma instância de geometry com uma Circularstring vazia  
 Este exemplo mostra como criar uma instância de `CircularString` vazia:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>b. Criando uma instância de geometry usando uma CircularString com um segmento de arco circular  
 O exemplo a seguir mostra como criar uma instância de `CircularString` com um único segmento de arco circular (meio-círculo):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>&. Criando uma instância de geometry usando uma CircularString com vários segmentos de arco circular  
 O exemplo a seguir mostra como criar uma instância de `CircularString` com mais de um segmento de arco circular (círculo completo):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 Isso produz a seguinte saída:  
  
```  
Circumference = 6.28319  
```  
  
 Compare a saída quando `LineString` for usada em vez de `CircularString`:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 Isso produz a seguinte saída:  
  
```  
Perimeter = 5.65685  
```  
  
 Observe que o valor do exemplo de `CircularString` é próximo de 2&#x03c0; (2 * PI), que é a circunferência real do círculo.  
  
### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. Declarando e instanciando uma instância de geometry com um Circularstring na mesma instrução  
 Este trecho de código mostra como declarar e criar uma instância de `geometry` com um `CircularString` na mesma instrução:  
  
```sql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>Oriental. Instanciando uma instância de geography com uma Circularstring  
 O exemplo a seguir mostra como declarar e criar uma instância de `geography` com uma `CircularString`:  
  
```sql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>fixo. Instanciar uma instância de geometry com uma Circularstring que é uma linha reta  
 O exemplo a seguir mostra como criar uma instância de `CircularString` que é uma linha reta:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos tipos de dados espaciais](spatial-data-types-overview.md)    
 @No__t_1 [CompoundCurve](compoundcurve.md)  
 @No__t_3 de [tipos &#40;&#41; de dados de Geografia MakeValid](/sql/t-sql/spatial-geography/makevalid-geography-data-type)  
 @No__t_3 de [tipo &#40;&#41; de dados geometry de MakeValid](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
 [Tipo&#41; de &#40;dados geometry de preisvalid](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)    
 [Tipo&#41; de dados de Geografia de inisvalid &#40;](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)    
 @No__t_3 de [tipo &#40;&#41; de dados geometry de tamanho](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
 [Tipo&#41; de &#40;dados geometry de costartpoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)    
 @No__t_3 de [tipo &#40;&#41; de dados geometry de ponto de extremidade](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
 @No__t_3 de [tipos &#40;&#41; de dados de geometria de ponto](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
 @No__t_3 de [tipo &#40;&#41; de dados geometry de STNumPoints](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
 @No__t_3 de [tipo &#40;&#41; de dados geometry de STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
 @No__t_3 de [tipo &#40;&#41; de dados geometry de STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
 @No__t_3 de [tipo &#40;&#41; de dados geometry de STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
 [LineString](linestring.md)  
  
  
