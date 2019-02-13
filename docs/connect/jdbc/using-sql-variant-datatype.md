---
title: Usando o tipo de dados Sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8df6fcee7b79f0c85f1182442195eb2cdf8d7ac9
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737344"
---
# <a name="using-sqlvariant-data-type"></a>Usando o tipo de dados Sql_variant

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

A partir da versão 6.3.0, o driver JDBC dá suporte ao tipo de dados sql_variant. Sql_variant também é suportado quando usando recursos como parâmetros com valor de tabela e BulkCopy com algumas limitações mencionada posteriormente nesta página. Nem todos os tipos de dados podem ser armazenados no tipo de dados sql_variant. Para obter uma lista de tipos de dados com suporte com sql_variant, verifique o SQL Server [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql).

##  <a name="populating-and-retrieving-a-table"></a>Populando e recuperar uma tabela:
Supondo que uma tem uma tabela com uma coluna sql_variant como:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

Um exemplo de script para inserir valores usando a instrução:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

Inserindo o valor usando instrução preparada:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

Se o tipo subjacente dos dados que está sendo passados for conhecido, o setter da respectivo pode ser usado. Por exemplo, `preparedStatement.setInt()` pode ser usado ao inserir um valor inteiro.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

Para ler os valores da tabela, os respectivos getters podem ser usados. Por exemplo, `getInt()` ou `getString()` métodos podem ser usados se os valores provenientes do servidor são conhecidos:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>Usando procedimentos armazenados com sql_variant:   
Tendo como um procedimento armazenado:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
Parâmetros de saída devem ser registrados:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sqlvariant"></a>Limitações de sql_variant:
- Ao usar TVP para popular uma tabela com uma `datetime` / `smalldatetime` / `date` valor armazenado em uma sql_variant, chamar `getDateTime()` / `getSmallDateTime()` / `getDate()` em um ResultSet não funciona e gera a seguinte exceção:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    Solução alternativa: use `getString()` ou `getObject()` em vez disso. 
    
- Usando um TVP para popular uma tabela e enviar um valor nulo em uma sql_variant não é suportado e gerará uma exceção:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>Consulte Também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
