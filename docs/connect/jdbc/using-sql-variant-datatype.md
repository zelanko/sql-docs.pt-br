---
title: Como usar o tipo de dados sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025838"
---
# <a name="using-sql_variant-data-type"></a>Como usar o tipo de dados sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir da versão 6.3.0, o driver JDBC dá suporte ao tipo de dados sql_variant. O sql_variant também tem suporte ao usar recursos como parâmetros com valor de tabela e BulkCopy com algumas limitações mencionadas posteriormente nesta página. Nem todos os tipos de dados podem ser armazenados no tipo de dados sql_variant. Para obter uma lista de tipos de dados com suporte com sql_variant, verifique o SQL Server [docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>Populando e recuperando uma tabela:
Supondo que haja uma tabela com uma coluna sql_variant como:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Um script de exemplo para inserir valores usando a instrução:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserindo valor usando a instrução preparada:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Se o tipo subjacente dos dados que estão sendo passados for conhecido, o respectivo setter poderá ser usado. Por exemplo, `preparedStatement.setInt()` pode ser usado ao inserir um valor inteiro.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Para ler valores da tabela, os respectivos getters podem ser usados. Por exemplo, `getInt()` ou `getString()` métodos podem ser usados se os valores provenientes do servidor forem conhecidos:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Como usar procedimentos armazenados com sql_variant:   
Tendo um procedimento armazenado, como:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
Os parâmetros de saída devem ser registrados:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Limitações do sql_variant:
- Ao usar TVP para popular uma tabela com um `datetime` `date` `smalldatetime` / / valor armazenado em uma sql_variant, `getSmallDateTime()` chamando `getDateTime()` / / em um`getDate()` ResultSet não funciona e gera a seguinte exceção:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Solução alternativa: `getString()` use `getObject()` ou em vez disso. 
    
- O uso de TVP para popular uma tabela e o envio de um valor nulo em um sql_variant não tem suporte e gera uma exceção:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
