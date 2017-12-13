---
title: "Criar, construir e consultar instâncias de geometria | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: spatial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e5c41d33b04553a63265313d0f380a98e15b9c79
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="create-construct-and-query-geometry-instances"></a>Criar, construir e consultar instâncias de geometria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] O tipo de dados espaciais planares, **geometry**, representa dados em um sistema de coordenadas euclidiano (plano). Este tipo é implementado como um tipo de dados CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O tipo **geometry** é predefinido e está disponível em cada banco de dados. É possível criar colunas de tabelas do tipo **geometry** e operar com dados **geometry** da mesma maneira como outros tipos CLR são usados.  
  
 O tipo de dados de **geometry** (planar) que tem suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está de acordo com os Recursos Simples do OGC (Open Geospatial Consortium) para o SQL Specification versão 1.1.0.  
  
 Para obter mais informações sobre especificações do OCG, consulte o seguinte:  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC Specifications, Simple Feature Access Part 2 – SQL Options](http://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a um subconjunto do padrão GML 3.1 existente, que é definido no seguinte esquema: [http://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](http://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating"></a> Criando ou construindo uma nova instância de geometria  
  
###  <a name="existing"></a> Criando uma nova instância de geometria de uma instância existente  
 O tipo de dados **geometry** fornece vários métodos internos que podem ser usados para criar novas instâncias **geometry** baseadas em instâncias existentes.  
  
 **Para criar um buffer em torno de uma geometria**  
 [STBuffer &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)  
  
 [BufferWithTolerance &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)  
  
 **Para criar uma versão simplificada de uma geometria**  
 [Reduce &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/reduce-geometry-data-type.md)  
  
 **Para cria o casco convexo de uma geometria**  
 [STConvexHull &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stconvexhull-geometry-data-type.md)  
  
 **Para criar uma geometria da interseção de duas geometrias**  
 [STIntersection &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stintersection-geometry-data-type.md)  
  
 **Para criar uma geometria da união de duas geometrias**  
 [STUnion &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stunion-geometry-data-type.md)  
  
 **Para criar uma geometria dos pontos onde uma geometria não sobrepõe outra**  
 [STDifference &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stdifference-geometry-data-type.md)  
  
 **Para criar uma geometria dos pontos onde duas geometrias não se sobrepõem**  
 [STSymDifference &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stsymdifference-geometry-data-type.md)  
  
 **Para criar uma instância de Point arbitrária que está em uma geometria existente**  
 [STPointOnSurface &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
  
###  <a name="wkt"></a> Construindo uma instância de geometria da entrada de texto conhecida  
 O tipo de dados **geometry** fornece vários métodos internos que geram uma geometria da representação WKT do OGC (Open Geospatial Consortium). O padrão WKT é uma cadeia de caracteres de texto que permite que dados de geometria sejam trocados em formulário textual.  
  
 **Para construir qualquer tipo de instância de geometria de entrada WKT**  
 [STGeomFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)  
  
 [Parse &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/parse-geometry-data-type.md)  
  
 **Para construir uma instância de Point de geometria de entrada WKT**  
 [STPointFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointfromtext-geometry-data-type.md)  
  
 **Para construir uma instância de MultiPoint de geometria de entrada WKT**  
 [STMPointFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stmpointfromtext-geometry-data-type.md)  
  
 **Para construir uma instância de LineString de geometria de entrada WKT**  
 [STLineFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlinefromtext-geometry-data-type.md)  
  
 **Para construir uma instância de MultiLineString de geometria de entrada WKT**  
 [STMLineFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stmlinefromtext-geometry-data-type.md)  
  
 **Para construir uma instância de Polygon de geometria de entrada WKT**  
 [STPolyFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpolyfromtext-geometry-data-type.md)  
  
 **Para construir uma instância de MultiPolygon de geometria de entrada WKT**  
 [STMPolyFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type.md)  
  
 **Para construir uma instância de GeometryCollection de geometria de entrada WKT**  
 [STGeomCollFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type.md)  
  
  
###  <a name="wkb"></a> Construindo uma instância de geometria da entrada binária conhecida  
 WKB é um formato binário especificado pelo OGC (Open Geospatial Consortium) que permite que dados **geometry** sejam trocados entre um aplicativo cliente e um banco de dados SQL. As seguintes funções aceitam entrada WKB para construir geometrias:  
  
 **Para construir qualquer tipo de instância de geometria de entrada WKB**  
 [STGeomFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de Point de geometria de entrada WKB**  
 [STPointFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointfromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de MultiPoint de geometria de entrada WKB**  
 [STMPointFromWKB &#40;tipo de dados de geometry&#41;](../../t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de LineString de geometria de entrada WKB**  
 [STLineFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlinefromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de MultiLineString de geometria de entrada WKB**  
 [STMLineFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de Polygon de geometria de entrada WKB**  
 [STPolyFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de MultiPolygon de geometria de entrada WKB**  
 [STMPolyFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type.md)  
  
 **Para construir uma instância de GeometryCollection de geometria de entrada WKB**  
 [STGeomCollFromWKB &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type.md)  
  
  
###  <a name="gml"></a> Construindo uma instância de geometria de entrada de texto GML  
 O tipo de dados **geometry** fornece um método que gera uma instância **geometry** de GML, uma representação XML de uma instância de objetos de geometria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a um subconjunto de GML.  
  
 **Para construir qualquer tipo de instância de geometria de entrada GML**  
 [GeomFromGml &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/geomfromgml-geometry-data-type.md)  
  
  
##  <a name="returning"></a> Retornando texto conhecido e binário conhecido de uma instância de geometria  
 É possível usar os seguintes métodos para retornar o formato WKT ou WKB de uma instância de **geometry** :  
  
 **Para retornar a representação WKT de uma instância de geometria**  
 [STAsText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)  
  
 [ToString &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/tostring-geometry-data-type.md)  
  
 **Para retornar a representação WKT de uma instância de geometria incluindo qualquer valor Z e M**  
 [AsTextZM &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
 **Para retornar a representação WKB de uma instância de geometria**  
 [STAsBinary &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stasbinary-geometry-data-type.md)  
  
 **Para retornar uma representação GML de uma instância de geometria**  
 [AsGml &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/asgml-geometry-data-type.md)  
  
  
##  <a name="querying"></a> Consultando as propriedades e comportamentos de instâncias de geometria  
 Todas as instâncias de **geometry** têm várias propriedades que podem ser recuperadas por meio de métodos fornecidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os tópicos a seguir definem propriedades e comportamentos de tipos de geometria e os métodos de consulta de cada um.  
  
###  <a name="valid"></a> Informações de validade, tipo de instância e GeometryCollection  
 Quando uma instância **geometry** é construída, é possível usar os seguintes métodos para determinar se ela está bem formada, para retornar o tipo da instância ou, se ela for uma instância de coleção, retornar uma instância **geometry** específica.  
  
 **Para retornar o tipo de instância de uma geometria**  
 [STGeometryType &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
 **Para determinar se uma geometria é um determinado tipo de instância**  
 [InstanceOf &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/instanceof-geometry-data-type.md)  
  
 **Para determinar se uma instância de geometria está bem formada para seu tipo de instância**  
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
 **Para converter uma instância de geometria em uma instância de geometria bem formada com um tipo de instância**  
 [MakeValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)  
  
 **Para retornar o número de geometrias em uma instância de coleção de geometrias**  
 [STNumGeometries &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumgeometries-geometry-data-type.md)  
  
 Para retornar uma geometria específica em uma instância coleção de geometrias  
 [STGeometryN &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeometryn-geometry-data-type.md)STGeometryN (tipo de dados geometry)  
  
  
###  <a name="number"></a> Número de pontos  
 Todas as instâncias de **geometry** não vazias são compostas por *pontos*. Esses pontos representam as coordenadas X e Y do plano no qual as geometrias são obtidas. **geometry** fornece vários métodos internos de consulta de pontos de uma instância.  
  
 **Para retornar o número de pontos que compõem uma instância**  
 [STNumPoints &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)  
  
 **Para retornar um ponto específico em uma instância**  
 [STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **Para retornar um ponto arbitrário que está em uma instância**  
 [STPointOnSurface](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)  
  
 **Para retornar o ponto inicial de uma instância**  
 [STStartPoint](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)  
  
 **Para retornar o ponto de extremidade de uma instância**  
 [STEndpoint](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)  
  
 **Para retornar a coordenada X de uma instância de Point**  
 [STX &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)  
  
 **Para retornar a coordenada Y de uma instância de Point**  
 [STY](../../t-sql/spatial-geometry/sty-geometry-data-type.md)  
  
 **Para retornar o ponto do centro geométrico de uma instância de Polygon, CurvePolygon ou MultiPolygon**  
 [STCentroid](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)  
  
  
###  <a name="dimension"></a> Dimensão  
 Uma instância **geometry** não vazia pode ser zero, uni ou bidimensional. Instâncias **geography**com dimensional zero, como **Point** e **MultiPoint**, não têm tamanho nem área. Objetos unidimensionais, como **LineString, CircularString, CompoundCurve**e **MultiLineString**, têm comprimento. Instâncias bidimensionais, como **Polygon**, **CurvePolygon**e **MultiPolygon**, têm área e comprimento. Instâncias vazias relatarão uma dimensão de -1 e uma **GeometryCollection** relatará uma área dependente dos tipos de seu conteúdo.  
  
 **Para retornar a dimensão de uma instância**  
 [STDimension](../../t-sql/spatial-geometry/stdimension-geometry-data-type.md)  
  
 **Para retornar o comprimento de uma instância**  
 [STLength](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)  
  
 **Para retornar a área de uma instância**  
 [STArea](../../t-sql/spatial-geometry/starea-geometry-data-type.md)  
  
  
###  <a name="empty"></a> Empty (vazio)  
 Uma instância *empty***geometry** não tem pontos. O comprimento de instâncias **LineString, CircularString**, **CompoundCurve**e **MultiLineString** é zero. A área de instâncias de **Polygon**, **CurvePolygon**e **MultiPolygon** vazias é 0.  
  
 **Para determinar se uma instância está vazia**  
 [STIsEmpty](../../t-sql/spatial-geometry/stisempty-geometry-data-type.md).  
  
  
###  <a name="simple"></a> Simple (simples)  
 Para que uma **geometry** da instância seja *simples*, ela deve atender a estes dois requisitos:  
  
-   Não deve haver interseção de nenhuma figura da instância consigo mesma, exceto em seus pontos de extremidade.  
  
-   Não pode haver nenhuma interseção entre duas figuras da instância em nenhum ponto que não esteja nos seus dois limites.  
  
> [!NOTE]  
>  Geometrias vazias são sempre simples.  
  
 **Para determinar se uma instância é simples**  
 [STIsSimple](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md).  
  
  
###  <a name="boundary"></a> Limite, interior e exterior  
 O *interior* de uma instância **geometry** é o espaço ocupado pela instância e o *exterior* é o espaço não ocupado por ela.  
  
 O*Limite* é definido pelo OGC da seguinte maneira:  
  
-   Instâncias de**Point** e **MultiPoint** não têm um limite.  
  
-   Os limites de**LineString** e **MultiLineString** boundaries are formed by the start points e end points, removing those that occur an even number of times.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 O limite de uma instância de **Polygon** ou **MultiPolygon** é o conjunto de seus anéis.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Para retornar o limite de uma instância**  
 [STBoundary](../../t-sql/spatial-geometry/stboundary-geometry-data-type.md)  
  
  
###  <a name="envelope"></a> Envelope  
 O *envelope* de uma instância **geometry** , também conhecido como a *caixa delimitadora*, é o retângulo alinhado com o eixo formado pelas coordenadas máxima e mínima (X,Y) da instância.  
  
 **Para retornar o envelope de uma instância**  
 [STEnvelope](../../t-sql/spatial-geometry/stenvelope-geometry-data-type.md)  
  
  
###  <a name="closure"></a> Fechamento  
 Uma instância *closed***geometry** é uma figura cujos pontos inicial e final são os mesmos. As instâncias**Polygon** são consideradas fechadas. As instâncias**Point** não estão fechadas.  
  
 Um anel é uma instância de **LineString** simples e fechada.  
  
 **Para determinar se uma instância está fechada**  
 [STIsClosed](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)  
  
 **Para determinar se uma instância é um anel**  
 [STIsRing](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)  
  
 **Para retornar o anel exterior de uma instância de Polygon**  
 [STExteriorRing](../../t-sql/spatial-geometry/stexteriorring-geometry-data-type.md)  
  
 **Para retornar o número de anéis interiores em um Polígono**  
 [STNumInteriorRing](../../t-sql/spatial-geometry/stnuminteriorring-geometry-data-type.md)  
  
 **Para retornar um anel interior especificado de um Polígono**  
 [STInteriorRingN](../../t-sql/spatial-geometry/stinteriorringn-geometry-data-type.md)  
  
  
###  <a name="srid"></a> SRID (Spatial Reference ID)  
 A SRID (ID de referência espacial) é um identificador que especifica o sistema de coordenadas no qual a instância **geometry** é representada. Duas instâncias com SRIDs diferentes são incomparáveis.  
  
 **Para definir ou retornar o SRID de uma instância**  
 [STSrid](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)  
  
 Essa propriedade pode ser modificada.  
  
  
##  <a name="rel"></a> Determinando relações entre instâncias de geometria  
 O tipo de dados **geometry** fornece vários métodos internos que podem ser usados para determinar relações entre duas instâncias **geometry** .  
  
 **Para determinar se duas instâncias abrangem o mesmo conjunto de pontos**  
 [STEquals](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **Para determinar se duas instâncias são não contíguas**  
 [STDisjoint](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **Para determinar se há interseção entre duas instâncias**  
 [STIntersects](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **Para determinar se duas instâncias se tocam**  
 [STTouches](../../t-sql/spatial-geometry/sttouches-geometry-data-type.md)  
  
 **Para determinar se duas instâncias se sobrepõem**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **Para determinar se duas instâncias se cruzam**  
 [STCrosses](../../t-sql/spatial-geometry/stcrosses-geometry-data-type.md)  
  
 **Para determinar se uma instância está dentro de outra**  
 [STWithin](../../t-sql/spatial-geometry/stwithin-geometry-data-type.md)  
  
 **Para determinar se uma instância contém outra**  
 [STContains](../../t-sql/spatial-geometry/stcontains-geometry-data-type.md)  
  
 **Para determinar se uma instância sobrepõe outra**  
 [STOverlaps](../../t-sql/spatial-geometry/stoverlaps-geometry-data-type.md)  
  
 **Para determinar se duas instâncias estão espacialmente relacionadas**  
 [STRelate](../../t-sql/spatial-geometry/strelate-geometry-data-type.md)  
  
 **Para determinar a distância mais curta entre pontos em duas instâncias de geometria**  
 [STDistance](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
  
##  <a name="defaultsrid"></a> Padrão de instâncias de geometria para SRID zero  
 A SRID padrão para instâncias **geometry** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é 0. Com dados espaciais de **geometry** , o SRID da instância espacial não é necessário para executar cálculos. Portanto as instâncias podem residir em espaço planar não definido. Para indicar espaço planar não definido nos cálculos de métodos de tipo de dados **geometry** , o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa SRID 0.  
  
##  <a name="examples"></a> Exemplos  
 Os dois exemplos a seguir mostram como adicionar e consultar dados geométricos.  
  
-   O primeiro exemplo cria uma tabela com uma coluna de identidade e uma coluna de `geometry` `GeomCol1`. Uma terceira coluna renderiza a coluna de `geometry` em sua representação WKT (Well-Known Text) do Open Geospatial Consortium (OGC) e usa o método `STAsText()` . Em seguida, duas linhas são inseridas: uma linha que contém uma instância `LineString` de `geometry`e uma linha que contém uma instância de `Polygon` .  
  
    ```  
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
  
-   O segundo exemplo usa o método `STIntersection()` para retornar os pontos onde as duas instâncias de `geometry` inseridas anteriormente se cruzam.  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
## <a name="see-also"></a>Consulte também  
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
