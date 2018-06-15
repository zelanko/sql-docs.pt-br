---
title: Trabalhando com uma Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbcd46cd9da1ab189aeafe77c7275aa103ea51f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851921"
---
# <a name="working-with-a-connection"></a>Trabalhando com uma conexão
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  As seções a seguir fornecem exemplos de modos diferentes de se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
> [!NOTE]  
>  Se você tiver problemas para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o driver JDBC, consulte [Solucionando problemas de conectividade](../../connect/jdbc/troubleshooting-connectivity.md) para obter sugestões sobre como corrigi-lo.  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>Criando uma conexão usando a classe DriverManager  
 A abordagem mais simples para criar uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados é carregar o driver JDBC e chamar o método getConnection da classe DriverManager, como no exemplo a seguir:  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Esta técnica criará uma conexão de banco de dados usando o primeiro driver disponível na lista de drivers que podem se conectar com êxito à URL fornecida.  
  
> [!NOTE]  
>  Ao usar a biblioteca de classes sqljdbc4.jar, aplicativos não precisam registrar explicitamente ou carregar o driver usando o método Class. forName. Quando o método getConnection da classe DriverManager é chamado, um driver apropriado é localizado no conjunto de drivers JDBC registrados. Para obter mais informações, consulte Usando JDBC Driver.  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>Criando uma conexão usando a classe SQLServerDriver  
 Se você precisa especificar um driver específico na lista de drivers para o Gerenciador de driver, você pode criar uma conexão de banco de dados usando o [conectar](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) método o [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) classe, como no exemplo a seguir:  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>Criando uma conexão usando a classe SQLServerDataSource  
 Se você precisar criar uma conexão usando o [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) classe, você pode usar vários métodos setter da classe antes de chamar o [getConnection](../../connect/jdbc/reference/getconnection-method.md) método, como no exemplo a seguir:  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);   
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```  
  
## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>Criando uma conexão com destino a uma fonte de dados muito específica  
 Para fazer uma conexão de banco de dados com destino a uma fonte de dados muito específica, há várias abordagens. Cada abordagem depende das propriedades que você define usando a URL de conexão.  
  
 Para conectar-se à instância padrão em um servidor remoto, use o seguinte:  
  
 `String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"`  
  
 Para conectar-se a uma porta específica em um servidor, use o seguinte:  
  
 `String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"`  
  
 Para conectar-se a uma instância nomeada em um servidor, use o seguinte:  
  
 `String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"`  
  
 Para conectar-se a um banco de dados específico em um servidor, use o seguinte:  
  
 `String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"`  
  
 Para obter mais exemplos de URL de conexão, consulte [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>Criando uma conexão com um tempo limite de logon personalizado  
 Se você tiver que ajustar para carga de servidor ou tráfego de rede, poderá criar uma conexão que tem um valor de tempo limite de logon específico descrita em segundos, da seguinte maneira:  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>Criar uma conexão com identidade de nível de aplicativo  
 Se você tiver que usar log e perfil, terá que identificar sua conexão como originária de um aplicativo específico, da seguinte maneira:  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>Fechando uma conexão  
 Você pode fechar uma conexão de banco de dados explicitamente chamando o [fechar](../../connect/jdbc/reference/close-method-sqlserverconnection.md) método da classe SQLServerConnection, como no exemplo a seguir:  
  
 `con.close();`  
  
 Isso será liberar os recursos de banco de dados que o objeto SQLServerConnection está usando ou retornará a conexão para o pool de conexão em cenários em pool.  
  
> [!NOTE]  
>  Chamar o método close também reverterá qualquer transação pendente.  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
