---
title: Usando tipos de dados básicos | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83bbe2c28e9b353e5a82fa630660756174ad0dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916365"
---
# <a name="using-basic-data-types"></a>Usando tipos de dados básicos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa os tipos de dados básicos JDBC para converter os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um formato que pode ser compreendido pela linguagem de programação Java e vice-versa. O driver JDBC fornece suporte para a API JDBC 4,0, que inclui o tipo de dados **SQLXML** e os tipos de dados nacionais (Unicode), como **nchar**, **nvarchar**, **LONGNVARCHAR**e **NClob**.  
  
## <a name="data-type-mappings"></a>Mapeamentos de tipo de dados

A tabela a seguir lista os mapeamentos padrão entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] básico, o JDBC e os tipos de dados da linguagem de programação Java:  
  
| Tipos de SQL Server   | Tipos JDBC (java.sql.Types)                        | Tipos da linguagem Java          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| BINARY             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | booleano                      |
| char               | CHAR                                               | Cadeia de caracteres                       |
| Data               | DATE                                               | java.sql.Date                |
| DATETIME           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| Decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | Cadeia de caracteres                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | Cadeia de caracteres                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | Cadeia de caracteres                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | Cadeia de caracteres                       |
| REAL               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | Cadeia de caracteres                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| timestamp          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | Cadeia de caracteres                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | Cadeia de caracteres                       |
| varchar(max)       | VARCHAR                                            | Cadeia de caracteres                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | Cadeia de caracteres<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| geometria           | VARBINARY                                          | byte[]                       |
| geografia          | VARBINARY                                          | byte[]                       |
  
(1) para usar java.sql.Time com o tipo time de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve definir a propriedade de conexão **sendTimeAsDatetime** como false.  
  
(2) você pode acessar de forma programática os valores de **DateTimeOffset** com a [classe DateTimeOffset](../../connect/jdbc/reference/datetimeoffset-class.md).  
  
As seções a seguir fornecem exemplos de como é possível usar o JDBC Driver e os tipos de dados básicos. Para obter exemplos mais detalhados sobre como usar os tipos de dados básicos em um aplicativo Java, veja [Amostra de tipos e dados básicos](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Recuperando dados como uma cadeia de caracteres

Se desejar recuperar dados de uma fonte de dados que mapeia para um dos tipos de dados básicos do JDBC para ser exibido como uma cadeia de caracteres, ou se não for necessário usar dados com rigidez de tipos, você poderá usar o método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), da seguinte maneira:  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Recuperando dados por tipo de dados

Se tiver que recuperar dados de uma fonte de dados e souber o tipo de dados que estão sendo recuperados, use um dos métodos get\<Type> da classe SQLServerResultSet, também conhecidos como *métodos getter*. Você pode usar um nome de coluna ou um índice de coluna com os métodos get\<Type>, da seguinte maneira:  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> O getUnicodeStream e o getBigDecimal com métodos de escala foram preteridos e não têm suporte do driver JDBC.

## <a name="updating-data-by-data-type"></a>Atualizando dados por tipo de dados

Se você precisar atualizar o valor de um campo em uma fonte de dados, use um dos métodos de\<> de tipo de atualização da classe SQLServerResultSet. No exemplo a seguir, o método [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) é usado junto com o método [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para atualizar os dados na fonte de dados:  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> O driver JDBC não pode atualizar uma coluna do SQL Server com um nome de coluna com mais de 127 caracteres. Se você tentar fazer uma atualização para uma coluna cujo nome tem mais de 127 caracteres, uma exceção será lançada.  
  
## <a name="updating-data-by-parameterized-query"></a>Atualizando dados através de consulta parametrizada

Se você tiver que atualizar dados em uma fonte de dados usando uma consulta parametrizada, poderá definir o tipo de dados dos parâmetros usando um dos métodos set\<Type> da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), também conhecida como *métodos setter*. No exemplo a seguir, o método [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) é usado para pré-compilar a consulta parametrizada e o método [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) é usado para definir o valor da cadeia de caracteres do parâmetro antes de o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) ser chamado.  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
Para obter mais informações sobre consultas parametrizadas, consulte [usando uma instrução SQL com parâmetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  

## <a name="passing-parameters-to-a-stored-procedure"></a>Passando parâmetros para um procedimento armazenado

Se você tiver que passar parâmetros de tipo em um procedimento armazenado, poderá definir os parâmetros através de índice ou pode nomear usando um dos métodos set\<Type> da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). No exemplo a seguir, o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) é usado para configurar a chamada ao procedimento armazenado e o método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) é usado para definir o parâmetro para a chamada antes de o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) ser chamado.  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> Neste exemplo, um conjunto de resultados é retornado com os resultados da execução do procedimento armazenado.

Para obter mais informações sobre como usar o driver JDBC com procedimentos armazenados e parâmetros de entrada, consulte [usando um procedimento armazenado com parâmetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>Recuperando parâmetros de um procedimento armazenado

Se você tiver que recuperar parâmetros de um procedimento armazenado, primeiro registre um parâmetro OUT por nome ou índice usando o método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) da classe SQLServerCallableStatement e, em seguida, atribua o parâmetro OUT retornado a uma variável apropriada depois de executar a chamada ao procedimento armazenado. No exemplo a seguir, o método prepareCall é usado para configurar a chamada ao procedimento armazenado, o método registerOutParameter é usado para configurar o parâmetro OUT e o método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) é usado para definir o parâmetro para a chamada antes de o método executeQuery ser chamado. O valor retornado pelo parâmetro OUT do procedimento armazenado é recuperado usando o método [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md).  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> Além do parâmetro OUT retornado, um conjunto de resultados também pode ser retornado com os resultados da execução do procedimento armazenado.  
  
Para obter mais informações sobre como usar o driver JDBC com procedimentos armazenados e parâmetros de saída, consulte [usando um procedimento armazenado com parâmetros de saída](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  

## <a name="see-also"></a>Consulte Também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
