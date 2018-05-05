---
title: Usando tipos de dados básicos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45af02973f4049d81ad386220b88ac4cce867e90
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-basic-data-types"></a>Usando tipos de dados básicos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa os tipos de dados básicos JDBC para converter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados em um formato que pode ser compreendido pela linguagem de programação Java e vice-versa. O driver JDBC fornece suporte para a API do JDBC 4.0, que inclui o **SQLXML** tipo de dados e tipos de dados nacionais (Unicode), como **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, e **NCLOB**.  
  
## <a name="data-type-mappings"></a>Mapeamentos de tipo de dados  
 A tabela a seguir lista os mapeamentos padrão entre o básico [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC e os tipos de dados da linguagem de programação Java:  
  
|Tipos de SQL Server|Tipos JDBC (java.sql.Types)|Tipos da linguagem Java|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|BINARY|BINARY|byte[]|  
|bit|BIT|booleano|  
|char|CHAR|Cadeia de caracteres|  
|date|DATE|java.sql.Date|  
|datetime|TIMESTAMP|java.sql.Timestamp|  
|datetime2|TIMESTAMP|java.sql.Timestamp|  
|datetimeoffset (2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|Decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|image|LONGVARBINARY|byte[]|  
|int|INTEGER|int|  
|money|DECIMAL|java.math.BigDecimal|  
|NCHAR|CHAR<br /><br /> NCHAR (Java SE 6.0)|Cadeia de caracteres|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|Cadeia de caracteres|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|Cadeia de caracteres|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|Cadeia de caracteres|  
|real|REAL|float|  
|smalldatetime|TIMESTAMP|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|text|LONGVARCHAR|Cadeia de caracteres|  
|time|TIME (1)|java.sql.Time (1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|Cadeia de caracteres|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|Cadeia de caracteres|  
|varchar(max)|VARCHAR|Cadeia de caracteres|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|Cadeia de caracteres<br /><br /> SQLXML|  
|SqlVariant|SQLVARIANT|Objeto|  
  
 (1) para usar Java.SQL. time com o tempo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo, você deve definir o **sendTimeAsDatetime** a propriedade de conexão como false.  
  
 (2) você pode acessar programaticamente os valores de **datetimeoffset** com [DateTimeOffset classe](../../connect/jdbc/reference/datetimeoffset-class.md).  
  
 As seções a seguir fornecem exemplos de como é possível usar o JDBC Driver e os tipos de dados básicos. Para obter um exemplo mais detalhado de como usar os tipos de dados básicos em um aplicativo Java, consulte [exemplo básico de tipos de dados](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Recuperando dados como uma cadeia de caracteres  
 Se você tem que recuperar dados de uma fonte de dados que mapeia para nenhum dos tipos de dados básicos JDBC para ser exibido como uma cadeia de caracteres ou se rigidez de tipos de dados não forem necessários, você pode usar o [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe, como no exemplo a seguir:  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Recuperando dados por tipo de dados  
 Se você tem que recuperar dados de uma fonte de dados, e você souber o tipo de dados que estão sendo recuperados, use um dos get\<tipo > métodos do SQLServerResultSet classe, também conhecido como o *métodos getter*. Você pode usar um nome de coluna ou um índice de coluna com get\<tipo > métodos, como no exemplo a seguir:  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  O getUnicodeStream getBigDecimal com métodos de escala são substituídos e não há suporte para o driver JDBC.  
  
## <a name="updating-data-by-data-type"></a>Atualizando dados por tipo de dados  
 Se você tiver que atualizar o valor de um campo em uma fonte de dados, use uma da atualização\<tipo > métodos da classe SQLServerResultSet. No exemplo a seguir, o [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) método é usado em conjunto com o [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) método para atualizar os dados na fonte de dados:  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  O driver JDBC não pode atualizar uma coluna do SQL Server com um nome de coluna com mais de 127 caracteres. Se você tentar fazer uma atualização para uma coluna cujo nome tem mais de 127 caracteres, uma exceção será lançada.  
  
## <a name="updating-data-by-parameterized-query"></a>Atualizando dados através de consulta parametrizada  
 Se você tiver que atualizar dados em uma fonte de dados usando uma consulta parametrizada, você pode definir o tipo de dados dos parâmetros usando um conjunto de\<tipo > métodos do [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe, também conhecido como o *métodos setter*. No exemplo a seguir, o [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) método é usado para pré-compilar a consulta parametrizada e, em seguida, o [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) método é usado para definir o valor de cadeia de caracteres do parâmetro antes do [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) método é chamado.  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 Para obter mais informações sobre consultas parametrizadas, consulte [usando uma instrução SQL com parâmetros](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>Passando parâmetros para um procedimento armazenado  
 Se você tiver que passar parâmetros de tipo em um procedimento armazenado, você pode definir os parâmetros de índice ou nome usando um conjunto de\<tipo > métodos do [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe. No exemplo a seguir, o [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método é usado para configurar a chamada ao procedimento armazenado e, em seguida, o [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) método é usado para definir o parâmetro para a chamada antes do [ executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método é chamado.  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  Neste exemplo, um conjunto de resultados é retornado com os resultados da execução do procedimento armazenado.  
  
 Para obter mais informações sobre como usar o driver JDBC com procedimentos armazenados e parâmetros de entrada, consulte [usando um procedimento armazenado com parâmetros de entrada](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>Recuperando parâmetros de um procedimento armazenado  
 Se você tiver que recuperar parâmetros de um procedimento armazenado, você deve primeiro registrar um parâmetro out por nome ou índice usando o [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método da classe SQLServerCallableStatement e, em seguida, atribua o retornado parâmetro out a uma variável apropriada depois de executar a chamada ao procedimento armazenado. No exemplo a seguir, o método prepareCall é usado para configurar a chamada ao procedimento armazenado, o método registerOutParameter é usado para configurar o parâmetro de saída e, em seguida, o [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) método é usado para definir o parâmetro para o chamada antes que o método executeQuery é chamado. O valor retornado pelo parâmetro out do procedimento armazenado é recuperado usando o [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) método.  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  Além do parâmetro OUT retornado, um conjunto de resultados também pode ser retornado com os resultados da execução do procedimento armazenado.  
  
 Para obter mais informações sobre como usar o driver JDBC com procedimentos armazenados e parâmetros de saída, consulte [usando um procedimento armazenado com parâmetros de saída](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
