---
title: Usar tipos de dados JDBC básicos
description: O Microsoft JDBC Driver for SQL Server usa tipos de dados JDBC básicos para converter tipos de dados do SQL Server em um formato que possa ser compreendido pelo Java.
ms.custom: ''
ms.date: 08/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c26c3c065ddf415d966c8fd3613e284c3c7a2b6
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807000"
---
# <a name="using-basic-data-types"></a>Como usar tipos de dados básicos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa os tipos de dados básicos JDBC para converter os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um formato que pode ser compreendido pela linguagem de programação Java e vice-versa. O JDBC Driver dá suporte à API do JDBC 4.0, que inclui o tipo de dados **SQLXML** e tipos de dados Nacionais (Unicode), como **NCHAR**, **NVARCHAR**, **LONGNVARCHAR** e **NCLOB**.  
  
## <a name="data-type-mappings"></a>Mapeamentos de tipo de dados

A tabela a seguir lista os mapeamentos padrão entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] básico, o JDBC e os tipos de dados da linguagem de programação Java:  
  
| Tipos de SQL Server   | Tipos JDBC (java.sql.Types)                        | Tipos da linguagem Java          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| binary             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | booleano                      |
| char               | CHAR                                               | String                       |
| date               | DATE                                               | java.sql.Date                |
| datetime<sup>3</sup>          | timestamp                               | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset<sup>2</sup> | microsoft.sql.Types.DATETIMEOFFSET         | microsoft.sql.DateTimeOffset |
| decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| numeric            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| real               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME<sup>1</sup>                                   | java.sql.Time<sup>1</sup>            |
| timestamp          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| Xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Objeto                       |
| geometria           | VARBINARY                                          | byte[]                       |
| geografia          | VARBINARY                                          | byte[]                       |
  
<sup>1</sup> Para usar java.sql.Time com o tipo time do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve definir a propriedade de conexão **sendTimeAsDatetime** como false.  
  
<sup>2</sup> Você pode acessar programaticamente os valores de **datetimeoffset** com [DateTimeOffset Class](reference/datetimeoffset-class.md).  
  
<sup>3</sup> Observe que os valores java.sql.Timestamp não podem mais ser usados para comparar valores de uma coluna datetime no SQL Server 2016. Essa limitação se deve a uma alteração no lado do servidor que converte datetime em datetime2 de modo diferente, resultando em valores não justos. A solução alternativa para esse problema é alterar as colunas datetime para datetime2(3), usar String em vez de java.sql.Timestamp ou alterar o nível de compatibilidade do banco de dados para 120 ou menos.
  
As seções a seguir fornecem exemplos de como é possível usar o JDBC Driver e os tipos de dados básicos. Para obter exemplos mais detalhados sobre como usar os tipos de dados básicos em um aplicativo Java, veja [Amostra de tipos e dados básicos](basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Recuperando dados como uma cadeia de caracteres

Se desejar recuperar dados de uma fonte de dados que mapeia para um dos tipos de dados básicos do JDBC para ser exibido como uma cadeia de caracteres, ou se não for necessário usar dados com rigidez de tipos, você poderá usar o método [getString](reference/getstring-method-sqlserverresultset.md) da classe [SQLServerResultSet](reference/sqlserverresultset-class.md), da seguinte maneira:  
  
[!code[JDBC#UsingBasicDataTypes1](codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Recuperando dados por tipo de dados

Se tiver que recuperar dados de uma fonte de dados e souber o tipo de dados que estão sendo recuperados, use um dos métodos get\<Type> da classe SQLServerResultSet, também conhecidos como *métodos getter*. Você pode usar um nome de coluna ou um índice de coluna com os métodos get\<Type>, da seguinte maneira:  
  
[!code[JDBC#UsingBasicDataTypes2](codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> Os métodos getUnicodeStream e getBigDecimal com escala são substituídos e não têm suporte no JDBC Driver.

## <a name="updating-data-by-data-type"></a>Atualizando dados por tipo de dados

Se você tiver que atualizar o valor de um campo em uma fonte de dados, use um dos métodos update\<Type> da classe SQLServerResultSet. No exemplo a seguir, o método [updateInt](reference/updateint-method-sqlserverresultset.md) é usado junto com o método [updateRow](reference/updaterow-method-sqlserverresultset.md) para atualizar os dados na fonte de dados:  
  
[!code[JDBC#UsingBasicDataTypes3](codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> O driver JDBC não pode atualizar uma coluna do SQL Server com um nome de coluna com mais de 127 caracteres. Se você tentar fazer uma atualização para uma coluna cujo nome tem mais de 127 caracteres, uma exceção será lançada.  
  
## <a name="updating-data-by-parameterized-query"></a>Atualizando dados por consulta parametrizada

Se você tiver que atualizar dados em uma fonte de dados usando uma consulta parametrizada, poderá definir o tipo de dados dos parâmetros usando um dos métodos set\<Type> da classe [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md), também conhecidos como *métodos setter*. No exemplo a seguir, o método [prepareStatement](reference/preparestatement-method-sqlserverconnection.md) é usado para pré-compilar a consulta parametrizada e o método [setString](reference/setstring-method-sqlserverpreparedstatement.md) é usado para definir o valor da cadeia de caracteres do parâmetro antes de o método [executeUpdate](reference/executeupdate-method.md) ser chamado.  
  
[!code[JDBC#UsingBasicDataTypes4](codesnippet/Java/using-basic-data-types_4.java)]  
  
Confira mais informações sobre consultas parametrizadas em [Como usar uma instrução SQL com parâmetros](using-an-sql-statement-with-parameters.md).  

## <a name="passing-parameters-to-a-stored-procedure"></a>Passando parâmetros para um procedimento armazenado

Se você tiver que passar parâmetros de tipo em um procedimento armazenado, poderá definir os parâmetros por índice ou nome usando um dos métodos set\<Type> da classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). No exemplo a seguir, o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) é usado para configurar a chamada ao procedimento armazenado e o método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) é usado para definir o parâmetro para a chamada antes de o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) ser chamado.  
  
[!code[JDBC#UsingBasicDataTypes5](codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> Neste exemplo, um conjunto de resultados é retornado com os resultados da execução do procedimento armazenado.

Confira mais informações sobre como usar o JDBC Driver com procedimentos armazenados e parâmetros de entrada em [Como usar um procedimento armazenado com parâmetros de entrada](using-a-stored-procedure-with-input-parameters.md).  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>Recuperando parâmetros de um procedimento armazenado

Se você tiver que recuperar parâmetros de um procedimento armazenado, primeiro registre um parâmetro OUT por nome ou índice usando o método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) da classe SQLServerCallableStatement e, em seguida, atribua o parâmetro OUT retornado a uma variável apropriada depois de executar a chamada ao procedimento armazenado. No exemplo a seguir, o método prepareCall é usado para configurar a chamada ao procedimento armazenado, o método registerOutParameter é usado para configurar o parâmetro OUT e o método [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) é usado para definir o parâmetro para a chamada antes de o método executeQuery ser chamado. O valor retornado pelo parâmetro OUT do procedimento armazenado é recuperado usando o método [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md).  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> Além do parâmetro OUT retornado, um conjunto de resultados também pode ser retornado com os resultados da execução do procedimento armazenado.  
  
Confira mais informações sobre como usar o JDBC Driver com procedimentos armazenados e parâmetros de saída em [Como usar um procedimento armazenado com parâmetros de saída](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  

## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
