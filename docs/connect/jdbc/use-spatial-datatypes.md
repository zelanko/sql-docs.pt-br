---
title: Usando tipos de dataespaciais | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2290aa8d7ebad7a40b5aea9d37c5a9a53e0d333
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916531"
---
# <a name="using-spatial-datatypes"></a>Usando tipos de dados espaciais

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os tipos de dataespaciais (Geometry e geography) têm suporte iniciando a versão de visualização do driver JDBC 6.5.0. Os tipos de dado espaciais não têm suporte atualmente com procedimentos armazenados, TVP (parâmetros com valor de tabela), BulkCopy e Always Encrypted. Esta página mostra vários casos de uso de tipos de dados geometry e geography com o driver JDBC. Para obter uma visão geral dos tipos de dados espaciais, verifique a página [visão geral dos tipos de dado espaciais](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) .

## <a name="creating-a-geometry--geography-object"></a>Criando um objeto Geometry/geography

Há duas maneiras principais de criar um objeto Geometry/geography-converta de um texto bem conhecido (WKT) ou um binário conhecido (WKB).

### <a name="creating-from-wkt"></a>Criando do WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Isso criará um objeto de geometria de LINEstring com SRID (identificador de sistema de referência espacial) 0 e um objeto de Geografia com SRID 4326.

### <a name="creating-from-wkb"></a>Criando do WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Isso criará um objeto Geometry e geography equivalente àqueles criados a partir do WKT anteriormente.

## <a name="working-with-a-geometry--geography-object"></a>Trabalhando com um objeto Geometry/geography

Supondo que o usuário tenha uma tabela em SQL Server como abaixo:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Um script de exemplo para inserir um valor de geometria seria:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

O mesmo pode ser feito para a contraparte de Geografia, usando uma coluna de Geografia e o método geography **()** .

Para ler uma coluna Geometry/geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

O mesmo pode ser feito para a contraparte de Geografia, usando uma coluna de Geografia e o método geography **()** .

## <a name="newly-introduced-apis"></a>APIs introduzidas recentemente

Essas são as novas APIs públicas que foram introduzidas com essa adição, nas classes **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**e **geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|Descrição|
|:------|:----------|
|void setGeometry(int n, Geometry x)| Define o parâmetro designado para o objeto de classe Microsoft. Sql. Geometry fornecido.
|void setGeography(int n, Geography x)| Define o parâmetro designado para o objeto de classe Microsoft. Sql. geography fornecido.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|Descrição|
|:------|:----------|
|Geometry GetGeometry (int colunIndex)| Retorna o valor da coluna designada na linha atual deste objeto ResultSet como um objeto com. Microsoft. SqlServer. JDBC. Geometry na linguagem de programação Java.
|Geometry GetGeometry (cadeia de caracteres columnName)| Retorna o valor da coluna designada na linha atual deste objeto ResultSet como um objeto com. Microsoft. SqlServer. JDBC. Geometry na linguagem de programação Java.
|Geografia geography (int colunIndex)| Retorna o valor da coluna designada na linha atual deste objeto ResultSet como um objeto com. Microsoft. SqlServer. JDBC. geography na linguagem de programação Java.
|Geografia geography (cadeia de caracteres ColumnName)| Retorna o valor da coluna designada na linha atual deste objeto ResultSet como um objeto com. Microsoft. SqlServer. JDBC. geography na linguagem de programação Java.

### <a name="geometry"></a>Geometry

|Método|Descrição|
|:------|:----------|
|Geometry STGeomFromText (String WKT, int SRID)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|Geometry STGeomFromWKB (Byte [] WKB)| Construtor para uma instância de Geometry de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Geometrias de desserialização (Byte [] WKB)| Construtor para uma instância de geometry de um formato de SQL Server interno para dados espaciais.
|Análise de geometria (cadeia de caracteres WKT)| Construtor para uma instância de Geometry de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). O identificador de referência espacial é padronizado como 0.
|Ponto de geometria (x duplo, y duplo, int SRID)| Construtor para uma instância de geometry que representa uma instância de Point de seus valores X e Y e um identificador de referência espacial.
|String STAsText()| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|byte[] STAsBinary()| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geometry. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|byte[] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geometry.
|hasM booliano ()| Retorna se o objeto contém um valor M (Measure).
|hasZ booliano ()| Retorna se o objeto contém um valor Z (elevação).
|GetX duplo ()| Retorna o valor da coordenada X.
|GetY duplo ()| Retorna o valor da coordenada Y.
|GetM duplo ()| Retorna o valor M (Measure) do objeto.
|Duplo getZ ()| Retorna o valor Z (elevação) do objeto.
|int getSrid ()| Retorna o valor do SRID (identificador de referência espacial).
|booliano isNull ()| Retorna se o objeto Geometry é nulo.
|int STNumPoints()| Retorna o número de pontos no objeto Geometry.
|Filegeometrytype () da cadeia de caracteres| Retorna o nome do tipo OGC (Open Geospatial Consortium) representado por uma instância geométrica.
|String asTextZM()| Retorna a representação WKT (Well-Known Text) do objeto Geometry.
|Cadeia de caracteres toString ()| Retorna a representação da cadeia de caracteres do objeto Geometry.

### <a name="geography"></a>Geografia

|Método|Descrição|
|:------|:----------|
|Geography STGeomFromText (cadeia de caracteres WKT, int SRID)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) aumentada com valores Z (elevação) e M (medida) presentes na instância.
|Geography STGeomFromWKB (Byte [] WKB)| Construtor para uma instância de Geography de uma representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium).
|Desserialização de Geografia (Byte [] WKB)| Construtor de uma instância de geography de um formato de SQL Server interno para dados espaciais.
|Análise de Geografia (cadeia de caracteres WKT)| Construtor para uma instância de Geography de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium). O identificador de referência espacial é padronizado como 0.
|Ponto de Geografia (Lon duplo, Lat duplo, int SRID)| Construtor de uma instância de Geography que representa uma instância de Point de seus valores de latitude e de longitude e um identificador de referência espacial.
|String STAsText()| Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.
|byte[] STAsBinary())| Retorna a representação WKB (Well-Known Binary) do OGC (Open Geospatial Consortium) de uma instância de Geography. Esse valor não conterá nenhum valor Z ou M executado pela instância.
|byte[] serialize()| Retorna os bytes que representam um formato SQL Server interno do tipo Geography.
|hasM booliano ()| Retorna se o objeto contém um valor M (Measure).
|hasZ booliano ()| Retorna se o objeto contém um valor Z (elevação).
|Duplo getlatitude ()| Retorna o valor de latitude.
|Double getLongitude()| Retorna o valor de longitude.
|GetM duplo ()| Retorna o valor M (Measure) do objeto.
|Duplo getZ ()| Retorna o valor Z (elevação) do objeto.
|int getSrid ()| Retorna o valor do SRID (identificador de referência espacial).
|booliano isNull ()| Retorna se o objeto geography é nulo.
|int STNumPoints()| Retorna o número de pontos no objeto geography.
|String geographtype ()| Retorna o nome de tipo OGC (Open Geospatial Consortium) representado por uma instância geográfica.
|String asTextZM()| Retorna a representação WKT (Well-Known Text) do objeto geography.
|Cadeia de caracteres toString ()| Retorna a representação da cadeia de caracteres do objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitações de tipos de dataespaciais

1. Os subtipos de cotação **circularstring**, **CompoundCurve**, **CurvePolygon**e **FullGlobe** só têm suporte a partir de SQL Server 2012 e superior.

2. Always Encrypted não pode ser usado com tipos de dataespaciais.

3. Atualmente, não há suporte para operações de procedimentos armazenados, TVP e BulkCopy com tipos de texto espaciais.

## <a name="see-also"></a>Consulte Também

[Exemplo de tipos de dados espaciais (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
