---
title: Referência de API do JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14e597d2788e57eb49903f52ebd40132ead9a35f
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174903"
---
# <a name="jdbc-driver-api-reference"></a>Referência de API do JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece uma API que pode ser usada no código de programação Java para se conectar a um banco de dados do [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e interagir com ele.



### <a name="javadocio-website-is-primary"></a>Site JavaDoc.io é primário

A documentação de referência de API do Microsoft JDBC está hospedada para sua exibição no site da JavaDoc.io. JavaDoc.io agora é nosso site primário para documentação de referência do JDBC. Nossa documentação de referência do JDBC em JavaDoc.io está disponível no seguinte link direto:

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JavaDoc.io tem nossa documentação de referência do JDBC começando com a versão 6.0.

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>Documentação do JDBC somente herdada está aqui no Docs

A documentação de referência de API do JDBC aqui artigos sobre **https://docs.microsoft.com/sql/connect/jdbc/reference/** não estão mais sendo atualizadas quando as classes do JDBC são atualizadas para novas versões. No entanto, os artigos aqui contêm todos os a referência para versões do JDBC 4.1 e 4.2.

Documentação de versão do JDBC 6.0 e algumas versões posteriores, também está aqui. Mas, para qualquer versão 6.0 ou posterior, use o site JavaDoc.io.



### <a name="important-notes"></a>Observações importantes

> [!NOTE]  
>  Para obter informações conceituais sobre como usar o driver JDBC, consulte [visão geral do Driver JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Para obter o suporte de conformidade do JDBC 4.1 e 4.2, use o Microsoft JDBC Driver 4.2 (ou superior) for SQL Server. As versões anteriores do Microsoft JDBC Drivers 4.1 e 4.0 não dão suporte aos novos métodos introduzidos com JDBC 4.1 ou 4.2.  
>   
>  Detalhes de API para conformidade JDBC 4.1 não estão nesta seção. Confira [Conformidade do JDBC 4.1 com o JDBC Driver](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  Detalhes de API para conformidade JDBC 4.2 não estão nesta seção. Confira [Conformidade do JDBC 4.2 com o JDBC Driver](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  Detalhes de API para a Cópia em Massa, disponíveis do Microsoft JDBC Driver 4.2 for SQL Server em diante, não são encontrados nesta seção. Confira [Usando a cópia em massa com o JDBC Driver](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  Detalhes de API para o Always Encrypted, disponíveis do Microsoft JDBC Driver 6.0 for SQL Server em diante, não são encontradas nesta seção. Confira [Referência de API do Always Encrypted para o JDBC Driver](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  Detalhes de API para parâmetros de Using Table-Valued, disponível a partir do Microsoft JDBC Driver 6.0 para SQL Server, não são encontrados nesta seção. Confira [Usando parâmetros com valor de tabela](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  O Microsoft JDBC Driver 6.4 dá suporte à compilação com o JDK 7.0, 8.0 e 9.0.  
>   
>  O Microsoft JDBC Driver 6.2 dá suporte à compilação com o JDK 7.0 e 8.0.  
>   
>  Os Microsoft JDBC Drivers 6.0 e 4.2 dão suporte à compilação com o JDK 5.0, 6.0, 7.0 e 8.0.  
>   
>  Microsoft JDBC Driver 4.1 dá suporte à compilação com JDK 5.0, 6.0 e 7.0.  



## <a name="interfaces"></a>Interfaces  
  
|Nome da interface|Descrição|  
|--------------------|-----------------|  
|[Interface ISQLServerCallableStatement](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Permite especificar o nome do procedimento armazenado para chamar juntamente com os parâmetros de entrada e saída.|  
|[Interface ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Representa uma conexão JDBC com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Representa uma lista de propriedades específicas da conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando um objeto [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Representa a implementação básica da funcionalidade de instrução preparada JDBC.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Representa um conjunto de resultados JDBC.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Representa a implementação básica da funcionalidade de instrução JDBC.|
| &nbsp; | &nbsp; |


  
## <a name="classes"></a>Classes  
  
|Nome de classe|Descrição|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|Representa um objeto do tipo microsoft.sql.DateTimeOffset.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Representa um BLOB (objeto binário grande).|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementa ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Representa um CLOB (objeto binário grande de caractere).|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementa ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Representa conexões de banco de dados físicas para gerentes de pool de conexões.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Representa os metadados do banco de dados.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Representa uma lista de propriedades específicas da conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando um objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Representa um alocador de objeto para materializar fontes de dados da JNDI (Java Naming and Directory Interface).|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Representa o JDBC driver. Essa classe inclui métodos para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e para obter informações sobre o driver JDBC.|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|Representa uma execução malsucedida ou incompleta de uma instrução SQL.|  
|[Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)|Representa um CLOB que usa o conjunto de caracteres nacional.|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|Representa os metadados para parâmetros de instrução preparada.|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|Representa uma conexão de banco de dados física em um pool de conexões.|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|Implementa: ISQLServerPreparedStatement.|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|Representa um recurso de cadeia de caracteres de erro localizada. Essa classe destina-se somente ao uso interno.|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|Implementa ISQLServerResultSet.|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|Representa os metadados das colunas contidas em um conjunto de resultados.|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|Representa o ponto de verificação para o qual uma transação pode ser revertida.|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|Implementa ISQLServerStatement.|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|Representa conexões JDBC que podem participar de transações distribuídas (XA).|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Representa um alocador para objetos [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) que é usado internamente.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Representa um XAResource para o gerenciamento de transações distribuídas XA.|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

