---
title: Criar, construir e consultar instâncias de geometria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- dbe-spatial
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 259a55908c97286805566ad0642391487aab77cd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158963"
---
# <a name="create-construct-and-query-geometry-instances"></a>Criar, construir e consultar instâncias de geometria
  O tipo de dados espaciais planares, `geometry`, representa dados em um sistema de coordenadas Euclidiano (plano). Este tipo é implementado como um tipo de dados CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O `geometry` tipo é predefinido e está disponível em cada banco de dados. Você pode criar colunas de tabela do tipo `geometry` e operar em `geometry` dados da mesma maneira como você usaria a outros tipos CLR.  
  
 O tipo de dados de `geometry` (planar) que tem suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está de acordo com os Recursos Simples do Open Geospatial Consortium (OGC) para o SQL Specification versão 1.1.0.  
  
 Para obter mais informações sobre especificações do OCG, consulte o seguinte:  
  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](http://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC Specifications, Simple Feature Access Part 2 – SQL Options](http://go.microsoft.com/fwlink/?LinkId=93629)  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a um subconjunto do padrão GML 3.1 existente que é definido no seguinte esquema: [http://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](http://go.microsoft.com/fwlink/?LinkId=230959).  
  
##  <a name="creating"></a> Criando ou construindo uma nova instância de geometria  
  
###  <a name="existing"></a> Criando uma nova instância de geometria de uma instância existente  
 O `geometry` tipo de dados fornece vários métodos internos que você pode usar para criar um novo `geometry` instâncias baseiam em instâncias existentes.  
  
 **Para criar um buffer em torno de uma geometria**  
 [STBuffer &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stbuffer-geometry-data-type)  
  
 [BufferWithTolerance &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type)  
  
 **Para criar uma versão simplificada de uma geometria**  
 [Reduce &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/reduce-geometry-data-type)  
  
 **Para cria o casco convexo de uma geometria**  
 [STConvexHull &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stconvexhull-geometry-data-type)  
  
 **Para criar uma geometria da interseção de duas geometrias**  
 [STIntersection &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stintersection-geometry-data-type)  
  
 **Para criar uma geometria da união de duas geometrias**  
 [STUnion &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stunion-geometry-data-type)  
  
 **Para criar uma geometria dos pontos onde uma geometria não sobrepõe outra**  
 [STDifference &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stdifference-geometry-data-type)  
  
 **Para criar uma geometria dos pontos onde duas geometrias não se sobrepõem**  
 [STSymDifference &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stsymdifference-geometry-data-type)  
  
 **Para criar uma instância de Point arbitrária que está em uma geometria existente**  
 [STPointOnSurface &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
  
  
###  <a name="wkt"></a> Construindo uma instância de geometria da entrada de texto conhecida  
 O tipo de dados de `geometry` fornece vários métodos internos que geram uma geometria da representação WKT do Open Geospatial Consortium (OGC). O padrão WKT é uma cadeia de caracteres de texto que permite que dados de geometria sejam trocados em formulário textual.  
  
 **Para construir qualquer tipo de instância de geometria de entrada WKT**  
 [STGeomFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)  
  
 [Parse &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/parse-geometry-data-type)  
  
 **Para construir uma instância de Point de geometria de entrada WKT**  
 [STPointFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromtext-geometry-data-type)  
  
 **Para construir uma instância de MultiPoint de geometria de entrada WKT**  
 [STMPointFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromtext-geometry-data-type)  
  
 **Para construir uma instância de LineString de geometria de entrada WKT**  
 [STLineFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromtext-geometry-data-type)  
  
 **Para construir uma instância de MultiLineString de geometria de entrada WKT**  
 [STMLineFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromtext-geometry-data-type)  
  
 **Para construir uma instância de Polygon de geometria de entrada WKT**  
 [STPolyFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromtext-geometry-data-type)  
  
 **Para construir uma instância de MultiPolygon de geometria de entrada WKT**  
 [STMPolyFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type)  
  
 **Para construir uma instância de GeometryCollection de geometria de entrada WKT**  
 [STGeomCollFromText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type)  
  
  
  
###  <a name="wkb"></a> Construindo uma instância de geometria da entrada binária conhecida  
 WKB é um formato binário especificado pelo Open geoespaciais Consortium (OGC) que permite que `geometry` dados a serem trocados entre um aplicativo cliente e um banco de dados SQL. As seguintes funções aceitam entrada WKB para construir geometrias:  
  
 **Para construir qualquer tipo de instância de geometria de entrada WKB**  
 [STGeomFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type)  
  
 **Para construir uma instância de Point de geometria de entrada WKB**  
 [STPointFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointfromwkb-geometry-data-type)  
  
 **Para construir uma instância de MultiPoint de geometria de entrada WKB**  
 [STMPointFromWKB &#40;tipo de dados de geometry&#41;](/sql/t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type)  
  
 **Para construir uma instância de LineString de geometria de entrada WKB**  
 [STLineFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stlinefromwkb-geometry-data-type)  
  
 **Para construir uma instância de MultiLineString de geometria de entrada WKB**  
 [STMLineFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type)  
  
 **Para construir uma instância de Polygon de geometria de entrada WKB**  
 [STPolyFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type)  
  
 **Para construir uma instância de MultiPolygon de geometria de entrada WKB**  
 [STMPolyFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type)  
  
 **Para construir uma instância de GeometryCollection de geometria de entrada WKB**  
 [STGeomCollFromWKB &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type)  
  
  
  
###  <a name="gml"></a> Construindo uma instância de geometria de entrada de texto GML  
 O `geometry` tipo de dados fornece um método que gera um `geometry` instância de GML, uma representação XML de objetos geométricos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a um subconjunto de GML.  
  
 **Para construir qualquer tipo de instância de geometria de entrada GML**  
 [GeomFromGml &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/geomfromgml-geometry-data-type)  
  
  
  
##  <a name="returning"></a> Retornando texto conhecido e binário conhecido de uma instância de geometria  
 Você pode usar os seguintes métodos para retornar o formato WKT ou WKB de uma `geometry` instância:  
  
 **Para retornar a representação WKT de uma instância de geometria**  
 [STAsText &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stastext-geometry-data-type)  
  
 [ToString &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/tostring-geometry-data-type)  
  
 **Para retornar a representação WKT de uma instância de geometria incluindo qualquer valor Z e M**  
 [AsTextZM &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/astextzm-geometry-data-type)  
  
 **Para retornar a representação WKB de uma instância de geometria**  
 [STAsBinary &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stasbinary-geometry-data-type)  
  
 **Para retornar uma representação GML de uma instância de geometria**  
 [AsGml &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/asgml-geometry-data-type)  
  
  
  
##  <a name="querying"></a> Consultando as propriedades e comportamentos de instâncias de geometria  
 Todos os `geometry` instâncias têm várias propriedades que podem ser recuperados por meio de métodos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece. Os tópicos a seguir definem propriedades e comportamentos de tipos de geometria e os métodos de consulta de cada um.  
  
###  <a name="valid"></a> Informações de validade, tipo de instância e GeometryCollection  
 Uma vez um `geometry` instância é construída, você pode usar os métodos a seguir para determinar se ela está bem formada, retornar o tipo de instância ou, se ela for uma instância de coleção, retornar um determinado `geometry` instância.  
  
 **Para retornar o tipo de instância de uma geometria**  
 [STGeometryType &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeometrytype-geometry-data-type)  
  
 **Para determinar se uma geometria é um determinado tipo de instância**  
 [InstanceOf &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/instanceof-geometry-data-type)  
  
 **Para determinar se uma instância de geometria está bem formada para seu tipo de instância**  
 [STIsValid &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
 **Para converter uma instância de geometria em uma instância de geometria bem formada com um tipo de instância**  
 [MakeValid &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
  
 **Para retornar o número de geometrias em uma instância de coleção de geometrias**  
 [STNumGeometries &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stnumgeometries-geometry-data-type)  
  
 Para retornar uma geometria específica em uma instância coleção de geometrias  
 [STGeometryN &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stgeometryn-geometry-data-type)STGeometryN (tipo de dados geometry)  
  
  
  
###  <a name="number"></a> Número de pontos  
 Todos os não vazio `geometry` consistem em instâncias *pontos*. Esses pontos representam as coordenadas X e Y do plano no qual as geometrias são obtidas. `geometry` fornece vários métodos internos de consulta de pontos de uma instância.  
  
 **Para retornar o número de pontos que compõem uma instância**  
 [STNumPoints &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
  
 **Para retornar um ponto específico em uma instância**  
 [STPointN](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Para retornar um ponto arbitrário que está em uma instância**  
 [STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
 **Para retornar o ponto inicial de uma instância**  
 [STStartPoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)  
  
 **Para retornar o ponto de extremidade de uma instância**  
 [STEndpoint](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
  
 **Para retornar a coordenada X de uma instância de Point**  
 [STX &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)  
  
 **Para retornar a coordenada Y de uma instância de Point**  
 [STY](/sql/t-sql/spatial-geometry/sty-geometry-data-type)  
  
 **Para retornar o ponto do centro geométrico de uma instância de Polygon, CurvePolygon ou MultiPolygon**  
 [STCentroid](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)  
  
  
  
###  <a name="dimension"></a> Dimensão  
 Um nonempty `geometry` instância pode ser 0, 1- ou 2-dimensional. Com dimensional zero `geometries`, como `Point` e `MultiPoint`, não têm nenhum comprimento ou área. Objetos unidimensionais, como `LineString, CircularString, CompoundCurve`, e `MultiLineString`, têm comprimento. Instâncias bidimensionais, como `Polygon`, `CurvePolygon` e `MultiPolygon`, têm área e comprimento. Instâncias vazias relatarão uma dimensão de -1 e uma `GeometryCollection` relatará uma área dependente dos tipos de seu conteúdo.  
  
 **Para retornar a dimensão de uma instância**  
 [STDimension](/sql/t-sql/spatial-geometry/stdimension-geometry-data-type)  
  
 **Para retornar o comprimento de uma instância**  
 [STLength](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
  
 **Para retornar a área de uma instância**  
 [STArea](/sql/t-sql/spatial-geometry/starea-geometry-data-type)  
  
  
  
###  <a name="empty"></a> Empty (vazio)  
 Uma *vazio* `geometry` instância não tem pontos. O comprimento de `LineString, CircularString`, `CompoundCurve`, e `MultiLineString` instâncias é zero. A área de vazio `Polygon`, `CurvePolygon`, e `MultiPolygon` instâncias é 0.  
  
 **Para determinar se uma instância está vazia**  
 [STIsEmpty](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type).  
  
  
  
###  <a name="simple"></a> Simple (simples)  
 Para um `geometry` da instância a ser *simples*, ele deve atender a estes dois requisitos:  
  
-   Não deve haver interseção de nenhuma figura da instância consigo mesma, exceto em seus pontos de extremidade.  
  
-   Não pode haver nenhuma interseção entre duas figuras da instância em nenhum ponto que não esteja nos seus dois limites.  
  
> [!NOTE]  
>  Geometrias vazias são sempre simples.  
  
 **Para determinar se uma instância é simples**  
 [STIsSimple](/sql/t-sql/spatial-geometry/stissimple-geometry-data-type).  
  
  
  
###  <a name="boundary"></a> Limite, interior e exterior  
 O *interior* de uma `geometry` instância é o espaço ocupado pela instância e o *exterior* é o espaço não ocupado por ela.  
  
 O*Limite* é definido pelo OGC da seguinte maneira:  
  
-   Instâncias de `Point` e `MultiPoint` não têm um limite.  
  
-   Limites de `LineString` e `MultiLineString` são formados pelos pontos iniciais e de extremidade removendo os que ocorrem um número par de vezes.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 O limite de uma `Polygon` ou `MultiPolygon` instância é o conjunto de seus anéis.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **Para retornar o limite de uma instância**  
 [STBoundary](/sql/t-sql/spatial-geometry/stboundary-geometry-data-type)  
  
  
  
###  <a name="envelope"></a> Envelope  
 O *envelope* de uma `geometry` da instância, também conhecido como o *caixa delimitadora*, é o retângulo alinhado por eixo formado por mínimo coordenadas máxima e (X, Y) da instância.  
  
 **Para retornar o envelope de uma instância**  
 [STEnvelope](/sql/t-sql/spatial-geometry/stenvelope-geometry-data-type)  
  
  
  
###  <a name="closure"></a> Fechamento  
 Um *fechada* `geometry` instância é uma figura cujos pontos inicial e final são os mesmos. `Polygon` instâncias são consideradas fechadas. As instâncias `Point` não estão fechadas.  
  
 Um anel é uma simples e fechada `LineString` instância.  
  
 **Para determinar se uma instância está fechada**  
 [STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
  
 **Para determinar se uma instância é um anel**  
 [STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
  
 **Para retornar o anel exterior de uma instância de Polygon**  
 [STExteriorRing](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)  
  
 **Para retornar o número de anéis interiores em um Polígono**  
 [STNumInteriorRing](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)  
  
 **Para retornar um anel interior especificado de um Polígono**  
 [STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)  
  
  
  
###  <a name="srid"></a> SRID (Spatial Reference ID)  
 A ID de referência espacial (SRID) é um identificador que especifica o sistema de coordenadas no qual a instância `geometry` é representada. Duas instâncias com SRIDs diferentes são incomparáveis.  
  
 **Para definir ou retornar o SRID de uma instância**  
 [STSrid](/sql/t-sql/spatial-geometry/stsrid-geometry-data-type)  
  
 Essa propriedade pode ser modificada.  
  
  
  
##  <a name="rel"></a> Determinando relações entre instâncias de geometria  
 O `geometry` tipo de dados fornece vários métodos internos que você pode usar para determinar relações entre duas `geometry` instâncias.  
  
 **Para determinar se duas instâncias abrangem o mesmo conjunto de pontos**  
 [STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar se duas instâncias são não contíguas**  
 [STDisjoint](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar se há interseção entre duas instâncias**  
 [STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Para determinar se duas instâncias se tocam**  
 [STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)  
  
 **Para determinar se duas instâncias se sobrepõem**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Para determinar se duas instâncias se cruzam**  
 [STCrosses](/sql/t-sql/spatial-geometry/stcrosses-geometry-data-type)  
  
 **Para determinar se uma instância está dentro de outra**  
 [STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)  
  
 **Para determinar se uma instância contém outra**  
 [STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)  
  
 **Para determinar se uma instância sobrepõe outra**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **Para determinar se duas instâncias estão espacialmente relacionadas**  
 [STRelate](/sql/t-sql/spatial-geometry/strelate-geometry-data-type)  
  
 **Para determinar a distância mais curta entre pontos em duas instâncias de geometria**  
 [STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
  
  
##  <a name="defaultsrid"></a> Padrão de instâncias de geometria para SRID zero  
 O padrão de SRID para instâncias de `geometry` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é 0. Com dados espaciais de `geometry`, o SRID da instância espacial não é necessário para executar cálculos. Portanto as instâncias podem residir em espaço planar não definido. Para indicar espaço planar não definido nos cálculos de métodos de tipo de dados de `geometry`, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa SRID 0.  
  
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
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
