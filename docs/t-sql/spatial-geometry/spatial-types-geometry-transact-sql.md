---
title: geometria (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- geometry
dev_langs:
- TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a2b65decea6d737801ef1b0b37e44b0c8ae028af
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68101012"
---
# <a name="spatial-types---geometry-transact-sql"></a>Tipos espaciais – geometria (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O tipo de dados espaciais planares, **geometria**, é implementado como um tipo de dados do CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse tipo representa dados em um sistema de coordenadas euclidiano (plano).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é compatível com um conjunto de métodos para o tipo de dados espaciais de **geometria**. Esses métodos incluem aqueles baseados em **geometria** que são definidos pelo padrão OGC (Open Geospatial Consortium) e um conjunto de extensões do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para esse padrão.  
 
 A tolerância de erro para os métodos de geometria pode chegar até as extensões de 1.0e-7 *. As extensões referem-se à distância máxima aproximada entre os pontos do objeto de **geometria**.
  
## <a name="registering-the-geometry-type"></a>Registrando o tipo de geometria  
 O tipo **geometry** é predefinido e está disponível em cada banco de dados. É possível criar colunas de tabelas do tipo **geometry** e operar com dados **geometry** da mesma maneira como outros tipos CLR são usados. Pode ser usado em colunas computadas persistidas e não persistidas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>a. Mostrando como adicionar e consultar dados geométricos  
 Os dois exemplos a seguir mostram como adicionar e consultar dados geométricos. O primeiro exemplo cria uma tabela com uma coluna de identidade e uma coluna de `geometry`, a `GeomCol1`. Uma terceira coluna renderiza a coluna de `geometry` em sua representação WKT (Well-Known Text) do Open Geospatial Consortium (OGC) e usa o método `STAsText()` . Em seguida, duas linhas são inseridas: uma linha que contém uma instância `LineString` de `geometry`e uma linha que contém uma instância de `Polygon` .  
  
```sql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>B. Retornando a interseção de duas instâncias de geometria  
 O segundo exemplo usa o método `STIntersection()` para retornar os pontos onde as duas instâncias de `geometry` inseridas anteriormente se cruzam.  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>C. Usando geometria em uma coluna computada  
 O exemplo a seguir cria uma tabela com uma coluna computada persistente usando um tipo de **geometria**.  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>Consulte Também  
  [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
