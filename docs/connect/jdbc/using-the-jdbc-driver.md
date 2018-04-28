---
title: Usando o Driver JDBC | Microsoft Docs
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
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 03423c0e7d1c95ce193f915c8e80db90b0c237fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-the-jdbc-driver"></a>Usando o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta seção fornece instruções de início rápido para fazer uma conexão simple para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Antes de você se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] devem ser instalados primeiro no computador local ou em um servidor, e o driver JDBC deve ser instalado no computador local.  
  
## <a name="choosing-the-right-jar-file"></a>Escolhendo o arquivo JAR correto  
 O Microsoft JDBC Driver 6.4 para o SQL Server fornece **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, e **mssql-jdbc-6.4.0.jre9.jar** biblioteca de classes arquivos a serem usados dependendo de suas configurações preferenciais do Java Runtime Environment (JRE).  
 
 O Microsoft JDBC Driver 6.2 para o SQL Server fornece **mssql-jdbc-6.2.1.jre7.jar**, e **mssql-jdbc-6.2.1.jre8.jar** arquivos de biblioteca a ser usado, dependendo de seu tempo de execução Java preferencial de classe Configurações de Environment (JRE).  
  
  O Microsoft JDBC Drivers 6.0 e 4.2 para SQL Server fornecem **sqljdbc41.jar**, e **sqljdbc42.jar** classe arquivos de biblioteca a ser usado, dependendo de suas configurações preferidas do Java Runtime Environment (JRE).  
  
 O Microsoft JDBC Driver 4.1 para SQL Server fornece a **sqljdbc41.jar** arquivo de biblioteca de classe a ser usado, dependendo de suas configurações preferenciais do Java Runtime Environment (JRE).  
    
 Sua escolha também determinará os recursos disponíveis. Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="setting-the-classpath"></a>Definindo o classpath  
 O JDBC driver não faz parte do Java SDK. Se você quiser usá-lo, você deve definir o classpath para incluir o **sqljdbc.jar** arquivo, **sqljdbc4.jar** arquivo, o **sqljdbc41.jar** arquivo, ou o  **sqljdbc42.jar** arquivo. Se usar o JDBC Driver 6.2, definir o classpath para incluir o **mssql-jdbc-6.2.1.jre7.jar** ou **mssql-jdbc-6.2.1.jre8.jar**. Se usar 6.4 do Driver JDBC, definir o classpath para incluir o **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** ou **mssql-jdbc-6.4.0.jre9.jar**. Se o classpath não tiver uma entrada, seu aplicativo lançará a exceção comum "Classe não encontrada".  
  
### <a name="for-microsoft-jdbc-driver-64"></a>Para o Microsoft JDBC Driver 6.4
 O **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** ou **mssql-jdbc-6.4.0.jre9.jar** arquivos são instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre9.jar
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 Assegure-se de que a instrução CLASSPATH contenha apenas um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como mssql-jdbc-6.4.0.jre7.jar, mssql-jdbc-6.4.0.jre8.jar ou mssql-jdbc-6.4.0.jre9.jar.   

### <a name="for-microsoft-jdbc-driver-62"></a>Para o Microsoft JDBC Driver 6.2
 O **mssql-jdbc-6.2.1.jre7.jar** ou **mssql-jdbc-6.2.1.jre8.jar** arquivos são instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.2.1.jre8.jar
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 Assegure-se de que a instrução CLASSPATH contenha apenas um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como mssql-jdbc-6.2.1.jre7.jar ou mssql-jdbc-6.2.1.jre8.jar.  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Para o Microsoft JDBC Driver 6.0, 4.2 e 4.1
 Os arquivos sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar estão instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \sqljdbc.jar  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \sqljdbc4.jar  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \sqljdbc41.jar  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \sqljdbc42.jar  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 Assegure-se de que a instrução CLASSPATH contenha apenas um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar.  
  
> [!NOTE]  
>  Em sistemas Windows, nomes de diretórios mais longos do que a convenção de arquivos de nome 8.3 ou nomes de pastas com espaços podem causar problemas com classpaths. Se você suspeitar desses tipos de problemas, você deve mover temporariamente o arquivo sqljdbc.jar, sqljdbc4.jar arquivo ou o arquivo sqljdbc41.jar em um nome de diretório simples, como `C:\Temp`, altere o classpath e determinar se isso resolve o problema.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>Aplicativos que são executados diretamente no prompt de comando  
 O classpath é configurado no sistema operacional. Acrescente sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar ao classpath do sistema. Como alternativa, você pode especificar o classpath na linha de comando do Java que executa o aplicativo usando o `java -classpath` opção.  
  
### <a name="applications-that-run-in-an-ide"></a>Aplicativos que executam em um IDE  
 Cada fornecedor de IDE oferece um método diferente para definir o classpath em seu IDE. Apenas definir o classpath no sistema operacional não funcionará. Você deve acrescentar sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar ao classpath do IDE.  
  
### <a name="servlets-and-jsps"></a>Servlets e JSPs  
 Servlets e JSPs são executados em um mecanismo de servlet/JSP como, por exemplo, Tomcat. O classpath deve ser definido de acordo com a documentação de mecanismo de servlet/JSP. Apenas definir o classpath no sistema operacional não funcionará. Alguns mecanismos de servlet/JSP fornecem telas de instalação que você pode usar para definir o classpath do mecanismo. Nessa situação, você deve acrescentar o arquivo JAR correto do JDBC Driver ao classpath de mecanismo existente e deve reiniciar o mecanismo. Em outras situações, você pode implantar o driver copiando sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar em um diretório específico, por exemplo, lib, durante a instalação do mecanismo. O classpath do driver de mecanismo também pode ser especificado em um arquivo de configuração específico do mecanismo.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 Enterprise Java Beans (EJB) são executados em um contêiner EJB. Contêineres EJB são originados de vários fornecedores. Miniaplicativos Java são executados em um navegador, mas são baixados de um servidor Web. Copie sqljdbc.jar, sqljdbc4.jar ou sqljdbc41.jar para a raiz do servidor web e especifique o nome do arquivo JAR na guia do arquivo HTML do applet, por exemplo, `<applet ... archive=sqljdbc.jar>`.  
  
## <a name="making-a-simple-connection-to-a-database"></a>Fazendo uma conexão simples com um banco de dados  
 Usando a biblioteca de classes sqljdbc.jar, os aplicativos devem primeiro registrar o driver como segue:  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 Quando o driver foi carregado, você pode estabelecer uma conexão usando uma URL de conexão e o método getConnection da classe DriverManager:  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Na API do JDBC 4.0, o método DriverManager.getConnection é aprimorado para carregar drivers de JDBC automaticamente. Portanto, os aplicativos não precisam chamar o método Class. forName para registrar ou carregar o driver ao usar o sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar biblioteca de classe.  
  
 Quando o método getConnection da classe DriverManager é chamado, um driver apropriado é localizado no conjunto de drivers JDBC registrados. o arquivo sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar inclui o arquivo de "META-INF/services/java.sql.Driver", que contém o **sqlserverdriver** como um driver registrado. Os aplicativos existentes, que atualmente carregam os drivers usando o método Class. forName, continuará a funcionar sem modificação.  
  
> [!NOTE]  
>  A biblioteca de classes sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar não pode ser usada com versões anteriores do Java Runtime Environment (JRE). Consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para a lista de versões do JRE com suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Para obter mais informações sobre como se conectar com fontes de dados e usar uma URL de conexão, consulte [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md) e [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
