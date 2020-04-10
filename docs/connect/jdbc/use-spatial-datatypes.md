---
title: Usar tipos de dados espaciais | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83f64df45036091985ccb6e26b86907882939313
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916792"
---
# <a name="using-spatial-datatypes"></a>Como usar tipos de dados espaciais

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Há suporte para tipos de dados espaciais (Geometry e Geography) da versão prévia do JDBC Driver 6.5.0 em diante. No momento, não há suporte para tipos de dados espaciais com procedimentos armazenados, TVP (Parâmetros com Valor de Tabela), BulkCopy e Always Encrypted. Esta página mostra vários casos de uso de tipos de dados Geometry e Geography com o JDBC Driver. Para obter uma visão geral sobre tipos de dados espaciais, confira a página [Visão geral de tipos de dado espaciais](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview).

## <a name="creating-a-geometry--geography-object"></a>Criar um objeto geometry/geography

Há duas maneiras principais de criar um objeto Geometry/Geography – converter de um WKT (texto bem conhecido) ou um WKB (binário bem conhecido).

### <a name="creating-from-wkt"></a>Criar com base no WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Isso criará um objeto Geometry LINESTRING com SRID (Identificador de Sistema de Referência Espacial) 0 e um objeto Geography com SRID 4326.

### <a name="creating-from-wkb"></a>Criar com base no WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Isso criará um objeto Geometry e Geography equivalente àqueles criados com base no WKT anteriormente.

## <a name="working-with-a-geometry--geography-object"></a>Trabalhar com um objeto Geometry/Geography

Supondo que o usuário tenha uma tabela no SQL Server como a abaixo:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Um script de exemplo para inserir um valor Geometry seria:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

O mesmo pode ser feito para o equivalente de Geography, usando uma coluna Geography e o método **setGeography()** .

Para ler uma coluna Geometry/Geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

O mesmo pode ser feito para o equivalente de Geography, usando uma coluna Geography e o método **getGeography()** .

## <a name="newly-introduced-apis"></a>APIs recém-introduzidas

Essas são as novas APIs públicas que foram introduzidas com essa adição, nas classes **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**e **geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|DESCRIÇÃO|
|:------|:----------|
|void setGeometry(int n, Geometry x)| Define o parâmetro designado para o objeto Class microsoft.sql.Geometry fornecido.
|void setGeography(int n, Geography x)| Define o parâmetro designado para o objeto Class microsoft.sql.Geography fornecido.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|DESCRIÇÃO|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| Retorna o valor da coluna designada na linha atual do objeto ResultSet como um objeto Geometry com.microsoft.sqlserver.jdbc na linguagem de programação Java.
|Geometry getGeometry(String columnName)| Retorna o valor da coluna designada na linha atual do objeto ResultSet como um objeto Geometry com.microsoft.sqlserver.jdbc na linguagem de programação Java.
|Geography getGeography(int colunIndex)| Retorna o valor da coluna designada na linha atual do objeto ResultSet como um objeto Geography com.microsoft.sqlserver.jdbc na linguagem de programação Java.
|Geography getGeography(String columnName)| Retorna o valor da coluna designada na linha atual do objeto ResultSet como um objeto Geography com.microsoft.sqlserver.jdbc na linguagem de programação Java.

### <a name="geometry"></a>Geometry

|Método|DESCRIÇÃO|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|Geometry STGeomFromWKB(byte[] wkb)| Construtor para uma instância de Geometry de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Geometries deserialize(byte[] wkb)| Construtor para uma instância Geometry de um formato SQL Server interno para dados espaciais.
|Geometry parse(String wkt)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). O padrão do identificador de referência espacial é definido como 0.
|Geometry point(double x, double y, int SRID)| Construtor para uma instância Geometry que representa uma instância Point dos valores X e Y e um Identificador de Referência Espacial.
|String STAsText()| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|byte[] STAsBinary()| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|byte[] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geometry.
|boolean hasM()| Retornará se o objeto contiver um valor M (medida).
|boolean hasZ()| Retornará se o objeto contiver um valor Z (elevação).
|Double getX()| Retorna o valor da coordenada X.
|Double getY()| Retorna o valor da coordenada Y.
|Double getM()| Retorna o valor M (medida) do objeto.
|Double getZ()| Retorna o valor Z (elevação) do objeto.
|int getSrid()| Retorna o valor SRID (Identificador de Referência Espacial).
|boolean isNull()| Retornará se o objeto Geometry for nulo.
|int STNumPoints()| Retorna o número de pontos no objeto Geometry.
|String STGeometryType()| Retorna o nome do tipo OGC (Open Geospatial Consortium) representado por uma instância geométrica.
|String asTextZM()| Retorna a representação WKT (Texto Bem Conhecido) do objeto Geometry.
|String toString()| Retorna a representação da cadeia de caracteres do objeto Geometry.

### <a name="geography"></a>painel Geografia do app&#39;s selecionado

|Método|DESCRIÇÃO|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|Geography STGeomFromWKB(byte[] wkb)| Construtor para uma instância de Geography de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Geography deserialize(byte[] wkb)| Construtor para uma instância Geography de um formato SQL Server interno para dados espaciais.
|Geography parse(String wkt)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). O padrão do identificador de referência espacial é definido como 0.
|Geography point(double lon, double lat, int SRID)| Construtor de uma instância de Geography que representa uma instância de Point de seus valores de latitude e de longitude e um identificador de referência espacial.
|String STAsText()| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|byte[] STAsBinary())| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|byte[] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geography.
|boolean hasM()| Retornará se o objeto contiver um valor M (medida).
|boolean hasZ()| Retornará se o objeto contiver um valor Z (elevação).
|Double getLatitude()| Retorna o valor de latitude.
|Double getLongitude()| Retorna o valor de longitude.
|Double getM()| Retorna o valor M (medida) do objeto.
|Double getZ()| Retorna o valor Z (elevação) do objeto.
|int getSrid()| Retorna o valor SRID (Identificador de Referência Espacial).
|boolean isNull()| Retornará se o objeto Geography for nulo.
|int STNumPoints()| Retorna o número de pontos no objeto Geography.
|String STGeographyType()| Retorna o nome de tipo OGC (Open Geospatial Consortium) representado por uma instância geográfica.
|String asTextZM()| Retorna a representação WKT (Texto Bem Conhecido) do objeto Geography.
|String toString()| Retorna a representação da cadeia de caracteres do objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitações de tipos de dados espaciais

1. Só há suporte para os subtipos de dados espaciais **CircularString**, **CompoundCurve**, **CurvePolygon** e **FullGlobe** da versão SQL Server 2012 em diante.

2. Always Encrypted não pode ser usado com tipos de dados espaciais.

3. No momento, não há suporte para operações de procedimentos armazenados, TVP e BulkCopy com tipos de dados espaciais.

## <a name="see-also"></a>Confira também

[Exemplo de tipos de dados espaciais (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
