---
title: Trabalhar com uma conexão JDBC
description: Exemplos dos diferentes modos de se conectar a um banco de dados do SQL Server usando a classe SQLServerConnection do Microsoft JDBC Driver for SQL Server.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1253c2ec5822fef83d6da71279752202f2d93ebd
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631946"
---
# <a name="working-with-a-connection"></a>Trabalhando com uma conexão

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

As seções a seguir fornecem exemplos dos modos diferentes de se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a classe [SQLServerConnection](reference/sqlserverconnection-class.md) do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

> [!NOTE]  
> Se você tiver problemas para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o driver JDBC, veja [Solução de problemas de conectividade](troubleshooting-connectivity.md) para obter sugestões de como corrigir isto.

## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>Criando uma conexão usando a classe DriverManager

A abordagem mais simples para criar uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é carregar o driver JDBC e chamar o método getConnection da classe DriverManager da seguinte maneira:

```java
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```

Esta técnica criará uma conexão de banco de dados usando o primeiro driver disponível na lista de drivers que podem se conectar com êxito à URL fornecida.

> [!NOTE]  
> Ao usar a biblioteca de classes sqljdbc4.jar, os aplicativos não precisam registrar explicitamente ou carregar o driver usando o método Class.forName. Quando o método getConnection da classe DriverManager é chamado, um driver apropriado é localizado no conjunto de drivers JDBC registrados. Para obter mais informações, consulte Usando JDBC Driver.

## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>Criando uma conexão usando a classe SQLServerDriver

Se você tiver que especificar um driver específico na lista de drivers para DriverManager, poderá criar uma conexão de banco de dados usando o método [connect](reference/connect-method-sqlserverdriver.md) da classe [SQLServerDriver](reference/sqlserverdriver-class.md) da seguinte maneira:

```java
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```

## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>Criando uma conexão usando a classe SQLServerDataSource

Se você tiver que criar uma conexão usando a classe [SQLServerDataSource](reference/sqlserverdatasource-class.md), poderá usar vários métodos setter da classe antes de chamar o método [getConnection](reference/getconnection-method.md), como a seguir:

```java
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```

## <a name="creating-a-connection-that-targets-a-specific-data-source"></a>Criar uma conexão que visa uma fonte de dados específica

Para fazer uma conexão de banco de dados que visa uma fonte de dados específica, há várias abordagens. Cada abordagem depende das propriedades que você define usando a URL de conexão.

Para conectar-se à instância padrão em um servidor remoto, use o seguinte exemplo:

```java
String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"
```

Para conectar-se a uma porta específica em um servidor, use o seguinte exemplo:

```java
String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"
```

Para conectar-se a uma instância nomeada em um servidor, use o seguinte exemplo:

```java
String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"
```

Para conectar-se a um banco de dados específico em um servidor, use o seguinte exemplo:

```java
String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"
```

Para obter mais exemplos de URL de conexão, confira [Construindo a URL de conexão](building-the-connection-url.md).

## <a name="creating-a-connection-with-a-custom-login-timeout"></a>Criar uma conexão com um tempo limite de logon personalizado

Se você tiver que ajustar para carga de servidor ou tráfego de rede, poderá criar uma conexão com um valor de tempo limite de logon específico descrito em segundos, como no seguinte exemplo:

```java
String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"
```

## <a name="create-a-connection-with-application-level-identity"></a>Criar uma conexão com identidade de nível de aplicativo

Se você tiver que usar log e perfil, terá que identificar sua conexão como originária de um aplicativo específico, como no seguinte exemplo:

```java
String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"
```

## <a name="closing-a-connection"></a>Fechando uma conexão

Você pode fechar uma conexão de banco de dados explicitamente chamando o método [close](reference/close-method-sqlserverconnection.md) da classe SQLServerConnection, da seguinte maneira:

```java
con.close();
```

Isso liberará os recursos de banco de dados que o objeto SQLServerConnection está usando ou retornará a conexão para o pool de conexão em cenários em pool.

> [!NOTE]  
> Chamar o método close também reverterá qualquer transação pendente.

## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](connecting-to-sql-server-with-the-jdbc-driver.md)
