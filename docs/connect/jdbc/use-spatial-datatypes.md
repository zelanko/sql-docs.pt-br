---
title: Usando tipos de dados espaciais | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 726711458f62011fc7bcaef268887813c9c9c3d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841996"
---
# <a name="using-spatial-datatypes"></a>Usando tipos de dados espaciais

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Tipos de dados espaciais (geometria e Geografia) são suportados começando da versão de visualização do Driver JDBC 6.5.0. Tipos de dados espaciais no momento, não têm suporte com procedimentos armazenados, parâmetros com valores da tabela (TVP), BulkCopy e sempre criptografados. Esta página mostra que vários casos de tipos de dados Geometry e Geography de uso com o Driver JDBC. Para obter uma visão geral sobre tipos de dados espaciais, verifique [visão geral dos tipos de dados espaciais](https://docs.microsoft.com/en-us/sql/relational-databases/spatial/spatial-data-types-overview) página.

## <a name="creating-a-geometry--geography-object"></a>Criar uma geometria / objeto de Geografia

Há duas maneiras principais para criar uma geometria / objeto de Geografia - a conversão de um WKT (texto conhecido) ou um Well-Known Binary WKB ().

### <a name="creating-from-wkt"></a>Criando de WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Isso criará um objeto de geometria LINESTRING com o sistema identificador (SRID de referência espacial) 0 e um objeto de Geografia com SRID 4326.

### <a name="creating-from-wkb"></a>Criando a partir do WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Isso criará um objeto de geometria e Geografia é equivalente àqueles criados a partir de WKT anteriormente.

## <a name="working-with-a-geometry--geography-object"></a>Trabalhando com uma geometria / objeto de Geografia

Supondo que o usuário tem uma tabela no SQL Server, como abaixo:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Um exemplo de script para inserir um valor de geometria seria:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

O mesmo pode ser feito para o equivalente de geografia, usando uma coluna de Geografia e **setGeography()** método.

Para ler uma geometria / coluna de Geografia:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

O mesmo pode ser feito para o equivalente de geografia, usando uma coluna de Geografia e **getGeography()** método.

## <a name="newly-introduced-apis"></a>Recentemente introduzida de APIs

Essas são as novas APIs públicas que foram introduzidas com esse acréscimo, nas classes **SQLServerPreparedStatement**, **SQLServerResultSet**, **geometria**e  **Geografia**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|Descrição|
|:------|:----------|
|void setGeometry (int n, geometria x)| Define o parâmetro designado como o objeto da classe microsoft.sql.Geometry determinado.
|void setGeography (int n, geografia x)| Define o parâmetro designado como o objeto da classe microsoft.sql.Geography determinado.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|Descrição|
|:------|:----------|
|Geometria getGeometry (colunIndex int)| Retorna o valor da coluna designada na linha atual deste objeto de conjunto de resultados como um objeto de com.microsoft.sqlserver.jdbc.Geometry na linguagem de programação Java.
|Geometria getGeometry (columnName de cadeia de caracteres)| Retorna o valor da coluna designada na linha atual deste objeto de conjunto de resultados como um objeto de com.microsoft.sqlserver.jdbc.Geometry na linguagem de programação Java.
|Geografia getGeography (colunIndex int)| Retorna o valor da coluna designada na linha atual deste objeto de conjunto de resultados como um objeto de com.microsoft.sqlserver.jdbc.Geography na linguagem de programação Java.
|Geografia getGeography (columnName de cadeia de caracteres)| Retorna o valor da coluna designada na linha atual deste objeto de conjunto de resultados como um objeto de com.microsoft.sqlserver.jdbc.Geography na linguagem de programação Java.

### <a name="geometry"></a>Geometria

|Método|Descrição|
|:------|:----------|
|Geometria STGeomFromText (cadeia de caracteres de wkt, int SRID)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|STGeomFromWKB geometria (Well-Known byte [])| Construtor para uma instância de Geometry de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Geometrias desserializar (Well-Known byte [])| Construtor para uma instância de um formato interno do SQL Server para dados espaciais de geometria.
|Análise de geometria WKT (Well de cadeia de caracteres)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). Identificador de referência espacial é padronizado como 0.
|Ponto de geometria (double x, y duplo int SRID)| Construtor para uma instância de geometria que representa uma instância de ponto de seus valores X e Y e um identificador de referência espacial.
|Stastext () da cadeia de caracteres| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|Byte [] Stasbinary| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|Byte [] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geometry.
|hasM() booliano| Retorna se o objeto contém um valor M (medida).
|hasZ() booliano| Retorna se o objeto contém um valor Z (elevação).
|GetX() duplo| Retorna o valor da coordenada X.
|GetY() duplo| Retorna o valor da coordenada Y.
|GetM() duplo| Retorna o valor de M (medida) do objeto.
|GetZ() duplo| Retorna o valor Z (elevação) do objeto.
|int getSrid()| Retorna o valor do identificador de referência espacial (SRID).
|IsNull () booliano| Retorna se o objeto Geometry é nulo.
|int stnumpoints)| Retorna o número de pontos no objeto de geometria.
|Stgeometrytype () da cadeia de caracteres| Retorna o nome do tipo OGC (Open Geospatial Consortium) representado por uma instância geométrica.
|Astextzm de cadeia de caracteres| Retorna a representação WKT (texto conhecido) do objeto Geometry.
|String ToString)| Retorna a representação da cadeia de caracteres do objeto Geometry.

### <a name="geography"></a>Geografia

|Método|Descrição|
|:------|:----------|
|Geografia STGeomFromText (cadeia de caracteres de wkt, int SRID)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|STGeomFromWKB geografia (Well-Known byte [])| Construtor para uma instância de Geography de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Geografia desserializar (Well-Known byte [])| Construtor para uma instância de um formato interno do SQL Server para dados espaciais de Geografia.
|Análise de Geografia WKT (Well de cadeia de caracteres)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). Identificador de referência espacial é padronizado como 0.
|Ponto de Geografia (duplas lat, lon duplo, int SRID)| Construtor para uma instância de Geography que representa uma instância de Point de seus valores de latitude e de longitude e um identificador de referência espacial.
|Stastext () da cadeia de caracteres| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|Byte [] STAsBinary())| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|Byte [] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geography.
|hasM() booliano| Retorna se o objeto contém um valor M (medida).
|hasZ() booliano| Retorna se o objeto contém um valor Z (elevação).
|GetLatitude() duplo| Retorna o valor de latitude.
|GetLongitude() duplo| Retorna o valor de longitude.
|GetM() duplo| Retorna o valor de M (medida) do objeto.
|GetZ() duplo| Retorna o valor Z (elevação) do objeto.
|int getSrid()| Retorna o valor do identificador de referência espacial (SRID).
|IsNull () booliano| Retorna se o objeto de Geografia é nulo.
|int stnumpoints)| Retorna o número de pontos no objeto de Geografia.
|Cadeia de caracteres STGeographyType()| Retorna o nome de tipo OGC (Open Geospatial Consortium) representado por uma instância geográfica.
|Astextzm de cadeia de caracteres| Retorna a representação WKT (texto conhecido) do objeto de Geografia.
|String ToString)| Retorna a representação da cadeia de caracteres do objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitações dos tipos de dados espaciais

1. A subtipos de dados espaciais **CircularString**, **CompoundCurve**, **CurvePolygon**, e **FullGlobe** têm suporte apenas no SQL Server 2012 e superior.

2. Sempre criptografado não pode ser usado com tipos de dados espaciais.

3. Procedimentos armazenados, TVP e BulkCopy operações atualmente não têm suporte com tipos de dados espaciais.

## <a name="see-also"></a>Consulte Também

[Exemplo de tipos de dados espaciais (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
