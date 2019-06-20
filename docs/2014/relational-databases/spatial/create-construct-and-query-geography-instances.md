---
title: Criar, construir e consultar instâncias de geografia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5dde7575a3f657b89d29fefa0da52002bcd6af28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014303"
---
# <a name="create-construct-and-query-geography-instances"></a>Criar, construir e consultar instâncias de geografia
  O tipo de dados espacial de geografia, `geography`, representa dados em um sistema de coordenadas de terra redonda. Este tipo é implementado como um tipo de dados CLR (Common Language Runtime) .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` tipo de dados armazena dados de elipsoidais (Terra redonda), como coordenadas de latitude e longitude GPS.  
  
 O tipo `geography` é predefinido e está disponível em cada banco de dados. É possível criar colunas de tabelas do tipo `geography` e operar em dados de `geography` da mesma maneira como outros tipos fornecidos pelo sistema são usados.  
  
##  <a name="creating"></a> Criando ou construindo uma nova instância de geografia  
  
###  <a name="existing"></a> Criando uma nova instância de geografia de uma instância existente  
 O tipo de dados `geography` fornece vários métodos internos que podem ser usados para criar novas instâncias de `geography` baseadas em instâncias existentes.  
  
 **Para criar um buffer em torno de uma geografia**  
 [STBuffer &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **Para criar um buffer em torno de uma geografia, permitindo uma tolerância**  
 [BufferWithTolerance &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **Para criar uma geografia da interseção de duas instâncias de geografia**  
 [STIntersection &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Para criar uma geografia da união de duas instâncias de geografia**  
 [STUnion &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **Para criar uma geografia dos pontos onde uma geografia não sobrepõe outra**  
 [STDifference &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a> Construindo uma instância de geografia da entrada de texto conhecida  
 O tipo de dados de `geography` fornece vários métodos internos que geram uma geografia da representação WKT do Open Geospatial Consortium (OGC). O padrão WKT é uma cadeia de caracteres de texto que permite que dados de geografia sejam trocados em formulário textual.  
  
 **Para construir qualquer tipo de instância de geografia de entrada WKT**  
 [STGeomFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [Parse &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **Para construir uma instância de Point de geografia de entrada WKT**  
 [STPointFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **Para construir uma instância de MultiPoint de geografia de entrada WKT**  
 [STMPointFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **Para construir uma instância de LineString de geografia de entrada WKT**  
 STLineFromText (tipo de dados de geografia)  
  
 **Para construir uma instância de MultiLineString de geografia de entrada WKT**  
 [STMLineFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **Para construir uma instância de Polygon de geografia de entrada WKT**  
 [STPolyFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **Para construir uma instância de MultiPolygon de geografia de entrada WKT**  
 [STMPolyFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **Para construir uma instância de GeometryCollection de geografia de entrada WKT**  
 [STGeomCollFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a> Construindo uma instância de geografia da entrada binária conhecida  
 WKB é um formato binário especificado pelo OGC que permite que dados de `Geography` sejam trocados entre um aplicativo cliente e um banco de dados SQL. As seguintes funções aceitam entrada WKB para construir instâncias de geografia:  
  
 **Para construir qualquer tipo de instância de geografia de entrada WKB**  
 [STGeomFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **Para construir uma instância de Point de geografia de entrada WKB**  
 [STPointFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiPoint de geografia de entrada WKB**  
 [STMPointFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **Para construir uma instância de LineString de geografia de entrada WKB**  
 [STLineFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiLineString de geografia de entrada WKB**  
 [STMLineFromWKB &#40;Tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **Para construir uma instância de Polygon de geografia de entrada WKB**  
 [STPolyFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiPolygon de geografia de entrada WKB**  
 [STMPolyFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **Para construir uma instância de GeometryCollection de geografia de entrada WKB**  
 [STGeomCollFromWKB &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type)STGeomCollFromWKB (tipo de dados geography)  
  
###  <a name="gml"></a> Construindo uma instância de geografia de entrada de texto GML  
 O `geography` tipo de dados fornece um método que gera uma `geography` instância de GML, uma representação XML de um `geography` instância. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a um subconjunto de GML.  
  
 Para obter mais informações sobre Geography Markup Language, veja a especificação do OGC: [Especificações OGC, Geography Markup Language.](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 **Para construir qualquer tipo de instância de geografia de entrada GML**  
 [GeomFromGML &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a> Retornando Well-Known Text e Well-Known Binary de uma instância de geografia  
 É possível usar os seguintes métodos para retornar o formato WKT ou WKB de uma instância de `geography`:  
  
 **Para retornar a representação WKT de uma instância de geografia**  
 [STAsText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [ToString &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **Para retornar a representação WKT de uma instância de geometria incluindo qualquer valor Z e M**  
 [AsTextZM &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **Para retornar a representação WKB de uma instância de geografia**  
 [STAsBinary &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **Para retornar a representação GML de uma instância de geografia**  
 [AsGml &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a> Consultando as propriedades e comportamentos de instâncias de geografia  
 Todos os `geography` instâncias têm várias propriedades que podem ser recuperados por meio de métodos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece. Os tópicos a seguir definem as propriedades e comportamentos de tipos de geografia e os métodos de consulta de cada um.  
  
###  <a name="valid"></a> Informações de validade, tipo de instância e GeometryCollection  
 Depois de um `geography` instância é construída, você pode usar os seguintes métodos para retornar o tipo de instância, ou se ele for um `GeometryCollection` da instância, retornar um determinado `geography` instância.  
  
 **Para retornar o tipo de instância de uma geografia**  
 [STGeometryType &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **Para determinar se uma geografia é um determinado tipo de instância**  
 [InstanceOf &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **Para determinar se uma instância de geografia é bem formada para seu tipo de instância**  
 [STNumGeometries &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **Para retornar uma geografia específica em uma instância GeometryCollection**  
 [STGeometryN &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type)STGeometryN (tipo de dados geography)  
  
###  <a name="number"></a> Número de pontos  
 Todos os não vazio `geography` consistem em instâncias *pontos*. Esses pontos representam as coordenadas de latitude e longitude da terra nas quais as instâncias de `geography` são obtidas. O tipo de dados `geography` fornece vários métodos internos de consulta de pontos de uma instância.  
  
 **Para retornar o número de pontos que compõem uma instância**  
 [STNumPoints &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **Para retornar um ponto específico em uma instância**  
 [STPointN &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Para retornar o ponto inicial de uma instância**  
 [STStartPoint &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **Para retornar o ponto de extremidade de uma instância**  
 [STEndpoint &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a> Dimensão  
 Uma instância `geography` não vazia pode ser zero, uni ou bidimensional. Com dimensional zero `geography` instâncias, como `Point` e `MultiPoint`, não têm nenhum comprimento ou área. Objetos unidimensionais, como `LineString, CircularString`, `CompoundCurve` e `MultiLineString`, têm comprimento. Instâncias bidimensionais, como `Polygon, CurvePolygon`, e `MultiPolygon`, têm área e comprimento. Instâncias vazias relatam uma dimensão de -1 e uma `GeometryCollection` relata a dimensão máxima de seu conteúdo.  
  
 **Para retornar a dimensão de uma instância**  
 [STDimension &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **Para retornar o comprimento de uma instância**  
 [STLength &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **Para retornar a área de uma instância**  
 [STArea &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a> Empty (vazio)  
 Uma *vazio* `geography` instância não tem pontos. O comprimento de instâncias de `LineString, CircularString`, `CompoundCurve` e `MultiLineString` vazias é 0. A área de instâncias `Polygon, CurvePolygon` e `MultiPolygon` vazias é 0.  
  
 **Para determinar se uma instância está vazia**  
 [STIsEmpty &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a> Fechamento  
 Um *fechada* `geography` instância é uma figura cujos pontos inicial e final são os mesmos. As instâncias `Polygon` são consideradas fechadas. As instâncias `Point` não estão fechadas.  
  
 Um anel é uma instância de `LineString` simples e fechada.  
  
 **Para determinar se uma instância está fechada**  
 [STIsClosed &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **Para retornar o número de anéis em uma instância de Polígono**  
 [NumRings &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **Para retornar um anel especificado de uma instância de geografia**  
 [RingN &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a> SRID (Spatial Reference ID)  
 A ID de referência espacial (SRID) é um identificador que especifica o sistema de coordenadas elipsoidais no qual a instância `geography` é representada. Duas instâncias `geography` com SRIDs diferentes não podem ser comparadas.  
  
 **Para definir ou retornar o SRID de uma instância**  
 [STSrid &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 Essa propriedade pode ser modificada.  
  
##  <a name="rel"></a> Determinando relações entre instâncias de geografia  
 O tipo de dados `geography` fornece vários métodos internos que podem ser usados para determinar relações entre duas instâncias de `geography`.  
  
 **Para determinar se duas instâncias abrangem o mesmo conjunto de pontos**  
 [STEquals &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar se duas instâncias são não contíguas**  
 [STDisjoint &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar se há interseção entre duas instâncias**  
 [STIntersects &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Para determinar o ponto ou pontos de interseção de duas instâncias**  
 [STIntersection &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Para determinar a distância mais curta entre pontos em duas instâncias de geografia**  
 [STDistance &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **Para determinar a diferença em pontos entre duas instâncias de geografia**  
 [STDifference &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **Para derivar a diferença simétrica ou pontos exclusivos de uma instância de geografia comparada com outra instância**  
 [STSymDifference &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a> Instâncias de geografia devem usar SRID com suporte  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a SRIDs baseadas nos padrões do EPSG. Um SRID com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias de `geography` deve ser usado ao executar cálculos ou usar métodos com dados espaciais de geografia. A SRID deve corresponder a uma das SRIDs exibidos na exibição de catálogo **sys.spatial_reference_systems** . Conforme mencionado anteriormente, ao executar cálculos nos dados espaciais usando o tipo de dados de `geography`, os resultados dependerão de qual elipsoide foi usado na criação dos dados, pois cada elipsoide recebe um SRID ( spatial reference identifier) específico.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o SRID padrão de 4326, que é mapeado para o sistema de referência espacial WGS 84 ao usar métodos nas instâncias de `geography`. Se você usar dados de um sistema de referência espacial diferente de WGS 84 (ou SRID 4326), será necessário determinar o SRID específico de seus dados espaciais de geografia.  
  
##  <a name="examples"></a> Exemplos  
 Os exemplos a seguir mostram como adicionar e consultar dados de geografia.  
  
-   O primeiro exemplo cria uma tabela com uma coluna de identidade e uma coluna de `geography` `GeogCol1`. Uma terceira coluna renderiza a coluna de `geography` em sua representação WKT (Well-Known Text) do Open Geospatial Consortium (OGC) e usa o método `STAsText()` . Em seguida, duas linhas são inseridas: uma linha que contém uma instância `LineString` de `geography`e uma linha que contém uma instância de `Polygon` .  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeogCol1 geography,   
        GeogCol2 AS GeogCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
    INSERT INTO SpatialTable (GeogCol1)  
    VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
    GO  
    ```  
  
-   O segundo exemplo usa o método `STIntersection()` para retornar os pontos onde as duas instâncias de `geography` inseridas anteriormente se cruzam.  
  
    ```  
    DECLARE @geog1 geography;  
    DECLARE @geog2 geography;  
    DECLARE @result geography;  
  
    SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geog1.STIntersection(@geog2);  
    SELECT @result.STAsText();  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
