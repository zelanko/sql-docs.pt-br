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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014303"
---
# <a name="create-construct-and-query-geography-instances"></a>Criar, construir e consultar instâncias de geografia
  O tipo de dados espacial de geografia, `geography`, representa dados em um sistema de coordenadas de terra redonda. Este tipo é implementado como um tipo de dados CLR (Common Language Runtime) .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `geography` armazena dados elipsoidais (globo terrestre), como as coordenadas de latitude e longitude de GPS.  
  
 O tipo `geography` é predefinido e está disponível em cada banco de dados. É possível criar colunas de tabelas do tipo `geography` e operar em dados de `geography` da mesma maneira como outros tipos fornecidos pelo sistema são usados.  
  
##  <a name="creating"></a>Criando ou construindo uma nova instância de Geografia  
  
###  <a name="existing"></a>Criando uma nova instância de geografia a partir de uma instância existente  
 O tipo de dados `geography` fornece vários métodos internos que podem ser usados para criar novas instâncias de `geography` baseadas em instâncias existentes.  
  
 **Para criar um buffer em uma geografia**  
 [Tipo de dados de Geografia de &#40;de armazenamento&#41;](/sql/t-sql/spatial-geography/stbuffer-geography-data-type)  
  
 **Para criar um buffer em uma geografia, permitindo uma tolerância**  
 [BufferWithTolerance &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/bufferwithtolerance-geography-data-type)  
  
 **Para criar uma geografia da interseção de duas instâncias de Geografia**  
 [O tipo de dados de Geografia &#40;a interseção&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Para criar uma geografia da União de duas instâncias de Geografia**  
 [&#40;de tipo de dados de Geografia de União&#41;](/sql/t-sql/spatial-geography/stunion-geography-data-type)  
  
 **Para criar uma geografia dos pontos em que uma geografia não se sobrepõe a outra**  
 [A diferença &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
###  <a name="wkt"></a>Construindo uma instância de Geografia de uma entrada de texto bem conhecida  
 O tipo de dados de `geography` fornece vários métodos internos que geram uma geografia da representação WKT do Open Geospatial Consortium (OGC). O padrão WKT é uma cadeia de caracteres de texto que permite que dados de geografia sejam trocados em formulário textual.  
  
 **Para construir qualquer tipo de instância de Geografia de entrada WKT**  
 [STGeomFromText &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
 [Analisar &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/parse-geography-data-type)  
  
 **Para construir uma instância de ponto de Geografia de entrada WKT**  
 [STPointFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stpointfromtext-geography-data-type)  
  
 **Para construir uma instância de MultiPoint de Geografia de entrada WKT**  
 [STMPointFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmpointfromtext-geography-data-type)  
  
 **Para construir uma instância de LineString de geography de entrada WKT**  
 STLineFromText (tipo de dados de geografia)  
  
 **Para construir uma instância de MultiLineString de Geografia de entrada WKT**  
 [STMLineFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmlinefromtext-geography-data-type)  
  
 **Para construir uma instância de Polygon de Geografia de entrada WKT**  
 [STPolyFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stpolyfromtext-geography-data-type)  
  
 **Para construir uma instância de MultiPolygon de Geografia de entrada WKT**  
 [STMPolyFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmpolyfromtext-geography-data-type)  
  
 **Para construir uma instância de GeometryCollection de Geografia de entrada WKT**  
 [STGeomCollFromText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stgeomcollfromtext-geography-data-type)  
  
###  <a name="wkb"></a>Construindo uma instância de geography de uma entrada binária bem conhecida  
 WKB é um formato binário especificado pelo OGC que permite que dados de `Geography` sejam trocados entre um aplicativo cliente e um banco de dados SQL. As seguintes funções aceitam entrada WKB para construir instâncias de geografia:  
  
 **Para construir qualquer tipo de instância de Geografia de entrada WKB**  
 [STGeomFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stgeomfromwkb-geography-data-type)  
  
 **Para construir uma instância de ponto de Geografia de entrada WKB**  
 [STPointFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stpointfromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiPoint de Geografia de entrada WKB**  
 [STMPointFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmpointfromwkb-geography-data-type)  
  
 **Para construir uma instância de LineString de geography de entrada WKB**  
 [STLineFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stlinefromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiLineString de Geografia de entrada WKB**  
 [STMLineFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmlinefromwkb-geography-data-type)  
  
 **Para construir uma instância de Polygon de Geografia de entrada WKB**  
 [STPolyFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stpolyfromwkb-geography-data-type)  
  
 **Para construir uma instância de MultiPolygon de Geografia de entrada WKB**  
 [STMPolyFromWKB &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stmpolyfromwkb-geography-data-type)  
  
 **Para construir uma instância de GeometryCollection de Geografia de entrada WKB**  
 [STGeomCollFromWKB &#40;tipo de dados de geografia&#41;](/sql/t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type) STGeomCollFromWKB (tipo de dados geography)  
  
###  <a name="gml"></a>Construindo uma instância de geography de entrada de texto GML  
 O `geography` tipo de dados fornece um método que gera `geography` uma instância de GML, uma representação XML de `geography` uma instância. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a um subconjunto de GML.  
  
 Para obter mais informações sobre Geography Markup Language, veja a Especificação do OGC: [OGC Specifications, Geography Markup Language.](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 **Para construir qualquer tipo de instância de Geografia de entrada GML**  
 [GeomFromGML &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/geomfromgml-geography-data-type)  
  
##  <a name="returning"></a>Retornando texto bem conhecido e binário bem conhecido de uma instância de Geografia  
 É possível usar os seguintes métodos para retornar o formato WKT ou WKB de uma instância de `geography`:  
  
 **Para retornar a representação WKT de uma instância de geography**  
 [STAsText &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stastext-geography-data-type)  
  
 [ToString &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/tostring-geography-data-type)  
  
 **Para retornar a representação WKT de uma instância de geography, incluindo os valores Z e M**  
 [AsTextZM &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/astextzm-geography-data-type)  
  
 **Para retornar a representação WKB de uma instância de geography**  
 [STAsBinary &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stasbinary-geography-data-type)  
  
 **Para retornar uma representação GML de uma instância de geography**  
 [AsGml &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/asgml-geography-data-type)  
  
##  <a name="query"></a>Consultando as propriedades e comportamentos de instâncias de Geografia  
 Todas `geography` as instâncias têm várias propriedades que podem ser recuperadas por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] métodos que o fornece. Os tópicos a seguir definem as propriedades e comportamentos de tipos de geografia e os métodos de consulta de cada um.  
  
###  <a name="valid"></a>Informações de validade, tipo de instância e GeometryCollection  
 Depois que `geography` uma instância é construída, você pode usar os métodos a seguir para retornar o tipo de instância ou, se `GeometryCollection` for uma instância, retornar `geography` uma instância específica.  
  
 **Para retornar o tipo de instância de uma geografia**  
 [STGeometryType &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stgeometrytype-geography-data-type)  
  
 **Para determinar se uma geografia é um determinado tipo de instância**  
 [O tipo de dados de Geografia &#40;de InstanceOf&#41;](/sql/t-sql/spatial-geography/instanceof-geography-data-type)  
  
 **Para determinar se uma instância de Geografia está bem formada para seu tipo de instância**  
 [STNumGeometries &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stnumgeometries-geography-data-type)  
  
 **Para retornar uma geografia específica em uma instância de GeometryCollection**  
 [Tipo de dados Geogeometry &#40;geography&#41;](/sql/t-sql/spatial-geography/stgeometryn-geography-data-type) Codegeometryn (tipo de dados geography)  
  
###  <a name="number"></a>Número de pontos  
 Todas as instâncias `geography` não vazias são compostas de *pontos*. Esses pontos representam as coordenadas de latitude e longitude da terra nas quais as instâncias de `geography` são obtidas. O tipo de dados `geography` fornece vários métodos internos de consulta de pontos de uma instância.  
  
 **Para retornar o número de pontos que compõem uma instância**  
 [STNumPoints &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stnumpoints-geography-data-type)  
  
 **Para retornar um ponto específico em uma instância**  
 [STPointN &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **Para retornar o ponto inicial de uma instância**  
 [&#40;de tipo de dados de Geografia de distartpoint&#41;](/sql/t-sql/spatial-geography/ststartpoint-geography-data-type)  
  
 **Para retornar o ponto de extremidade de uma instância**  
 [Ponto de extremidade &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stendpoint-geography-data-type)  
  
###  <a name="dimension"></a>Dimensões  
 Uma instância `geography` não vazia pode ser zero, uni ou bidimensional. Instâncias com dimensões `geography` zero, como `Point` e `MultiPoint`, não têm comprimento ou área. Objetos unidimensionais, como `LineString, CircularString`, `CompoundCurve` e `MultiLineString`, têm comprimento. Instâncias bidimensionais, como `Polygon, CurvePolygon`, e `MultiPolygon`têm área e comprimento. Instâncias vazias relatam uma dimensão de -1 e uma `GeometryCollection` relata a dimensão máxima de seu conteúdo.  
  
 **Para retornar a dimensão de uma instância**  
 [&#40;de tipo de dados de Geografia de dimensão&#41;](/sql/t-sql/spatial-geography/stdimension-geography-data-type)  
  
 **Para retornar o comprimento de uma instância**  
 [STLength &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/stlength-geography-data-type)  
  
 **Para retornar a área de uma instância**  
 [&#40;tipo de dados de Geografia de área de&#41;](/sql/t-sql/spatial-geography/starea-geography-data-type)  
  
###  <a name="empty"></a>Esvaziá  
 Uma instância *vazia* `geography` não tem nenhum ponto. O comprimento de instâncias de `LineString, CircularString`, `CompoundCurve` e `MultiLineString` vazias é 0. A área de instâncias `Polygon, CurvePolygon` e `MultiPolygon` vazias é 0.  
  
 **Para determinar se uma instância está vazia**  
 [STIsEmpty &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stisempty-geography-data-type)  
  
###  <a name="closure"></a>Closure  
 Uma instância *fechada* `geography` é uma figura cujos pontos inicial e final são os mesmos. As instâncias `Polygon` são consideradas fechadas. As instâncias `Point` não estão fechadas.  
  
 Um anel é uma instância de `LineString` simples e fechada.  
  
 **Para determinar se uma instância está fechada**  
 [STIsClosed &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stisclosed-geography-data-type)  
  
 **Para retornar o número de anéis em uma instância de Polygon**  
 [NumRings &#40;tipo de dados geography&#41;](/sql/t-sql/spatial-geography/numrings-geography-data-type)  
  
 **Para retornar um anel especificado de uma instância de geography**  
 [Tipo de dados &#40;de Geografia de aneln&#41;](/sql/t-sql/spatial-geography/ringn-geography-data-type)  
  
###  <a name="srid"></a>ID de referência espacial (SRID)  
 A ID de referência espacial (SRID) é um identificador que especifica o sistema de coordenadas elipsoidais no qual a instância `geography` é representada. Duas instâncias `geography` com SRIDs diferentes não podem ser comparadas.  
  
 **Para definir ou retornar o SRID de uma instância**  
 [STSrid &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stsrid-geography-data-type)  
  
 Essa propriedade pode ser modificada.  
  
##  <a name="rel"></a>Determinando relações entre instâncias de Geografia  
 O tipo de dados `geography` fornece vários métodos internos que podem ser usados para determinar relações entre duas instâncias de `geography`.  
  
 **Para determinar se duas instâncias compõem o mesmo conjunto de pontos**  
 [&#40;de tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **Para determinar se duas instâncias estão desassociadas**  
 [STDisjoint &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **Para determinar se duas instâncias se interseccionam**  
 [STIntersects &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **Para determinar o ponto ou pontos em que duas instâncias se interseccionam**  
 [O tipo de dados de Geografia &#40;a interseção&#41;](/sql/t-sql/spatial-geography/stintersection-geography-data-type)  
  
 **Para determinar a distância mais curta entre os pontos em duas instâncias de Geografia**  
 [&#40;tipo de dados geometry de interdistância&#41;](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
 **Para determinar a diferença em pontos entre duas instâncias de Geografia**  
 [A diferença &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stdifference-geography-data-type)  
  
 **Para derivar a diferença simétrica, ou pontos exclusivos, de uma instância de Geografia comparada com outra instância**  
 [STSymDifference &#40;tipo de dados de Geografia&#41;](/sql/t-sql/spatial-geography/stsymdifference-geography-data-type)  
  
##  <a name="supportedsrid"></a>as instâncias de Geografia devem usar SRID com suporte  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a SRIDs baseadas nos padrões do EPSG. Um SRID com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instâncias de `geography` deve ser usado ao executar cálculos ou usar métodos com dados espaciais de geografia. A SRID deve corresponder a uma das SRIDs exibidos na exibição de catálogo **sys.spatial_reference_systems** . Conforme mencionado anteriormente, ao executar cálculos nos dados espaciais usando o tipo de dados de `geography`, os resultados dependerão de qual elipsoide foi usado na criação dos dados, pois cada elipsoide recebe um SRID ( spatial reference identifier) específico.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o SRID padrão de 4326, que é mapeado para o sistema de referência espacial WGS 84 ao usar métodos nas instâncias de `geography`. Se você usar dados de um sistema de referência espacial diferente de WGS 84 (ou SRID 4326), será necessário determinar o SRID específico de seus dados espaciais de geografia.  
  
##  <a name="examples"></a> Exemplos  
 Os exemplos a seguir mostram como adicionar e consultar dados de geografia.  
  
-   O primeiro exemplo cria uma tabela com uma coluna de identidade e uma coluna de `geography``GeogCol1`. Uma terceira coluna renderiza a coluna de `geography` em sua representação WKT (Well-Known Text) do Open Geospatial Consortium (OGC) e usa o método `STAsText()` . Em seguida, duas linhas são inseridas: uma linha que contém uma instância `LineString` de `geography`e uma linha que contém uma instância de `Polygon` .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Dados espaciais &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
