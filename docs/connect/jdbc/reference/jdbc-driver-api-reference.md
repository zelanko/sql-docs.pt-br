---
title: Referência da API do JDBC Driver | Microsoft Docs
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
ms.topic: article
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2104aa05efd1720abe67ad281b14a5bda69c0d43
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="jdbc-driver-api-reference"></a>Referência de API do JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece uma API que pode ser usada em Java código de programação para se conectar a e interagir com um [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados.  
  
> [!NOTE]  
>  Para obter informações conceituais sobre como usar o driver JDBC, consulte [visão geral do Driver JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Para JDBC 4.1 e 4.2 suporte de conformidade, use o Microsoft JDBC Driver 4.2 (ou superior) para o SQL Server. As versões anteriores do Microsoft JDBC Drivers 4.1 e 4.0 não dão suporte aos novos métodos introduzidos com JDBC 4.1 ou 4.2.  
>   
>  Detalhes de API para conformidade JDBC 4.1 não estão nesta seção. Consulte [JDBC 4.1 conformidade para o Driver JDBC](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  Detalhes de API para conformidade JDBC 4.2 não estão nesta seção. Consulte [JDBC 4.2 conformidade para o Driver JDBC](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  Detalhes de API de cópia em massa, disponível a partir do Microsoft JDBC Driver 4.2 para SQL Server, não são encontrados nesta seção. Consulte [usando a cópia em massa com o Driver JDBC](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  Detalhes de API para sempre criptografado disponível iniciando com o Microsoft JDBC Driver 6.0 para SQL Server, não são encontrados nesta seção. Consulte [sempre criptografado referência de API para o Driver JDBC](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  Detalhes de API para parâmetros de Using Table-Valued, disponível a partir do Microsoft JDBC Driver 6.0 para SQL Server, não são encontrados nesta seção. Consulte [usando parâmetros com valor de tabela](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.4 dá suporte à compilação com JDK 7.0, 8.0 e 9.0.  
>   
>  6.2 do Microsoft JDBC Driver dá suporte à compilação com JDK 7.0 e 8.0.  
>   
>  Microsoft JDBC Drivers 6.0 e compilação de suporte 4.2 com JDK 5.0, 6.0, 7.0 e 8.0.  
>   
>  Microsoft JDBC Driver 4.1 dá suporte à compilação com JDK 5.0, 6.0 e 7.0.  

## <a name="interfaces"></a>Interfaces  
  
|Nome da interface|Description|  
|--------------------|-----------------|  
|[Interface ISQLServerCallableStatement](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Permite especificar o nome do procedimento armazenado para chamar juntamente com os parâmetros de entrada e saída.|  
|[Interface ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Representa uma conexão JDBC para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados.|  
|[Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Representa uma lista de propriedades específicas para se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados usando um [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Representa a implementação básica da funcionalidade de instrução preparada JDBC.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Representa um conjunto de resultados JDBC.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Representa a implementação básica da funcionalidade de instrução JDBC.|  
  
## <a name="classes"></a>Classes  
  
|Nome de classe|Description|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|Representa um objeto do tipo microsoft.sql.DateTimeOffset.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Representa um BLOB (objeto binário grande).|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementa ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Representa um CLOB (objeto binário grande de caractere).|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementa ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Representa conexões de banco de dados físicas para gerentes de pool de conexões.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Representa os metadados do banco de dados.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Representa uma lista de propriedades específicas para se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados usando um [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Representa um alocador de objeto para materializar fontes de dados da JNDI (Java Naming and Directory Interface).|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Representa o JDBC driver. Essa classe inclui métodos para se conectar a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados e para obter informações sobre o driver JDBC.|  
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
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Representa uma fábrica para [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) objetos que são usados internamente.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Representa um XAResource XA para o gerenciamento de transações distribuídas.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
