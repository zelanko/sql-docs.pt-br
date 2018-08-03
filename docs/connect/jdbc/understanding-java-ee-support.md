---
title: Noções básicas sobre o suporte ao Java EE | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5cc306a407e818a79d67cfc4c4340e1a9c2b22
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278857"
---
# <a name="understanding-java-ee-support"></a>Entendendo suporte ao Java EE
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  As seções a seguir documentam como o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece suporte para a Plataforma Java EE (Enterprise Edition) e os recursos opcionais de API do JDBC 3.0. Os exemplos de código-fonte fornecidos neste sistema de Ajuda fornecem uma boa referência de introdução a esses recursos.  
  
 Primeiro, tenha certeza de que seu ambiente Java (JDK, JRE) inclua o pacote javax.sql. Este é um pacote exigido por qualquer aplicativo do JDBC que usa a API opcional. O JDK 1.5 e as versões posteriores já contêm esse pacote; portanto, você não precisará instalá-lo separadamente.  
  
## <a name="driver-name"></a>Nome do driver  
 O nome de classe do driver é **com.microsoft.sqlserver.jdbc.SQLServerDriver**. Para os JDBC Drivers 4.1, 4.2 e 6.0, o driver está contido no arquivo sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar. Para o JDBC Driver 6.2, o driver está contido no mssql-jdbc-6.2.1.jre7.jar ou mssql-jdbc-6.2.1.jre8.jar. Para o JDBC Driver 6.4, o driver está contido no mssql-jdbc-6.4.0.jre7.jar, mssql-jdbc-6.4.0.jre8.jar ou mssql-jdbc-6.4.0.jre9.jar.
  
 O nome de classe é usado sempre que você carrega o driver com a classe DriverManager do JDBC. Também é usado sempre que você precisa especificar o nome de classe do driver em uma configuração de driver. Por exemplo, a configuração de uma fonte de dados em um servidor de aplicativos do Java EE pode exigir que você insira o nome de classe do driver.  
  
## <a name="data-sources"></a>Fontes de dados  
 O JDBC driver dá suporte a fontes de dados para Java EE/JDBC 3.0. A classe [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) do driver JDBC é implementada por **com.microsoft.sqlserver.jdbc.SQLServerXADataSource**.  
  
### <a name="datasource-names"></a>Nomes da fonte de dados  
 Você pode fazer conexões de banco de dados usando fontes de dados. As fontes de dados disponíveis com o JDBC driver são descritas na tabela a seguir:  
  
|Tipo de fonte de dados|Nome de classe e descrição|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> A fonte de dados de não pooling.|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> A fonte de dados para configurar pools de conexão de servidor de aplicativos do JAVA EE. Geralmente usado quando o aplicativo é executado dentro de um servidor de aplicativos do JAVA EE.|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> A fonte de dados para configurar fontes de dados do JAVA EE XA. Geralmente usado quando o aplicativo é executado dentro de um servidor de aplicativos do JAVA EE e um gerenciador de transações XA.|  
  
### <a name="data-source-properties"></a>Propriedades de fonte de dados  
 Todas as fontes de dados oferecem suporte à capacidade de definir e obter qualquer propriedade que está associada com o conjunto de propriedades do driver subjacente.  
  
 Exemplos:  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 Veja a seguir como um aplicativo é conectado usando uma fonte de dados:  
  
```java
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 Para obter mais informações sobre as propriedades de fonte de dados, consulte [definindo propriedades de fonte de dados](../../connect/jdbc/setting-the-data-source-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
