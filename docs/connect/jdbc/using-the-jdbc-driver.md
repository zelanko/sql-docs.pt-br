---
title: Usando o Driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03ea3e895fb7d70b392e0c25372536770308049d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015817"
---
# <a name="using-the-jdbc-driver"></a>Usando o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta seção fornece instruções de início rápido para fazer uma conexão simples com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Antes de você se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] deve primeiro ser instalado no computador local ou em um servidor, e o driver JDBC deve ser instalado no computador local.  
  
## <a name="choosing-the-right-jar-file"></a>Escolhendo o arquivo JAR correto  
 O Microsoft JDBC Driver 6.4 para SQL Server fornece **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, e **mssql-jdbc-6.4.0.jre9.jar** biblioteca de classes arquivos a serem usados dependendo das suas configurações preferenciais do Java Runtime Environment (JRE).  
 
 O Microsoft JDBC Driver 6.2 para SQL Server fornece **mssql-jdbc-6.2.1.jre7.jar**, e **mssql-jdbc-6.2.1.jre8.jar** arquivos de biblioteca a ser usado, dependendo de seu tempo de execução Java preferencial de classe Configurações de Environment (JRE).  
  
  Os Microsoft JDBC Drivers 6.0 e 4.2 for SQL Server fornece os arquivos da biblioteca de classes **sqljdbc41.jar** e **sqljdbc42.jar** a serem usados dependendo das suas configurações preferidas do JRE (Java Runtime Environment).  
  
 O Microsoft JDBC Driver 4.1 para SQL Server fornece o arquivo de biblioteca de classes **sqljdbc41.jar** a ser usado dependendo das suas configurações preferidas do JRE (Java Runtime Environment).  
    
 Sua escolha também determinará os recursos disponíveis. Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="setting-the-classpath"></a>Definindo o classpath  
 O JDBC driver não faz parte do Java SDK. Se você deseja usá-lo, deverá definir o caminho de classe para incluir os arquivos **sqljdbc.jar**, **sqljdbc4.jar**, **sqljdbc41.jar** ou **sqljdbc42.jar**. Se usar o JDBC Driver 6.2, definir o classpath para incluir a **mssql-jdbc-6.2.1.jre7.jar** ou **mssql-jdbc-6.2.1.jre8.jar**. Se usar o JDBC Driver 6.4, definir o classpath para incluir a **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** ou **mssql-jdbc-6.4.0.jre9.jar**. Se o classpath não tiver uma entrada, seu aplicativo lançará a exceção comum "Classe não encontrada".  
  
### <a name="for-microsoft-jdbc-driver-64"></a>Para o Microsoft JDBC Driver 6.4
 O **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** ou **mssql-jdbc-6.4.0.jre9.jar** arquivos são instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.4.0.jre9.jar
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 Certifique-se de que a instrução CLASSPATH contenha apenas um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como mssql-jdbc-6.4.0.jre7.jar, mssql-jdbc-6.4.0.jre8.jar ou mssql-jdbc-6.4.0.jre9.jar.   

### <a name="for-microsoft-jdbc-driver-62"></a>Para o Microsoft JDBC Driver 6.2
 O **mssql-jdbc-6.2.1.jre7.jar** ou **mssql-jdbc-6.2.1.jre8.jar** arquivos são instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \mssql-jdbc-6.2.1.jre8.jar
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 A seguir, veja um exemplo da instrução CLASSPATH que é usada para um aplicativo do Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 Certifique-se de que a instrução CLASSPATH contenha apenas um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como mssql-jdbc-6.2.1.jre7.jar ou mssql-jdbc-6.2.1.jre8.jar.  

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
  
 A instrução CLASSPATH deve conter somente um [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como qljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar.  
  
> [!NOTE]  
>  Em sistemas Windows, nomes de diretórios mais longos do que a convenção de arquivos de nome 8.3 ou nomes de pastas com espaços podem causar problemas com classpaths. Se você suspeitar desses tipos de problemas, deverá mover temporariamente os arquivos sqljdbc.jar, sqljdbc4.jar ou sqljdbc41.jar para um nome de diretório simples, como `C:\Temp`, alterar o caminho de classe e determinar se isso resolve o problema.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>Aplicativos que são executados diretamente no prompt de comando  
 O classpath é configurado no sistema operacional. Acrescente sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar ao classpath do sistema. Como alternativa, você pode especificar o caminho de classe na linha de comando do Java que executa o aplicativo usando a opção `java -classpath`.  
  
### <a name="applications-that-run-in-an-ide"></a>Aplicativos que executam em um IDE  
 Cada fornecedor de IDE oferece um método diferente para definir o classpath em seu IDE. Apenas definir o classpath no sistema operacional não funcionará. Você deve acrescentar sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar ao classpath do IDE.  
  
### <a name="servlets-and-jsps"></a>Servlets e JSPs  
 Servlets e JSPs são executados em um mecanismo de servlet/JSP como, por exemplo, Tomcat. O classpath deve ser definido de acordo com a documentação de mecanismo de servlet/JSP. Apenas definir o classpath no sistema operacional não funcionará. Alguns mecanismos de servlet/JSP fornecem telas de instalação que você pode usar para definir o classpath do mecanismo. Nessa situação, você deve acrescentar o arquivo JAR correto do JDBC Driver ao classpath de mecanismo existente e deve reiniciar o mecanismo. Em outras situações, você pode implantar o driver copiando sqljdbc.jar, sqljdbc4.jar, ou sqljdbc41.jar em um diretório específico, por exemplo, lib, durante a instalação do mecanismo. O classpath do driver de mecanismo também pode ser especificado em um arquivo de configuração específico do mecanismo.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 Enterprise Java Beans (EJB) são executados em um contêiner EJB. Contêineres EJB são originados de vários fornecedores. Miniaplicativos Java são executados em um navegador, mas são baixados de um servidor Web. Copie sqljdbc.jar, sqljdbc4.jar ou sqljdbc41.jar para a raiz do servidor Web e especifique o nome do arquivo JAR na guia do arquivo HTML do miniaplicativo, por exemplo, `<applet ... archive=sqljdbc.jar>`.  
  
## <a name="making-a-simple-connection-to-a-database"></a>Fazendo uma conexão simples com um banco de dados  
 Usando a biblioteca de classes sqljdbc.jar, os aplicativos devem primeiro registrar o driver como segue:  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 Quando o driver é carregado, você pode estabelecer uma conexão usando uma URL de conexão e o método getConnection da classe DriverManager:  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Na API do JDBC 4.0, o método DriverManager.getConnection foi aprimorado para carregar drivers de JDBC automaticamente. Portanto, os aplicativos não precisarão chamar o método Class.forName para registrar ou carregar o driver ao usar a biblioteca de classes sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar.  
  
 Quando o método getConnection da classe DriverManager é chamado, um driver apropriado é localizado no conjunto de drivers JDBC registrados. arquivo sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar inclui o arquivo de "META-INF/services/java.sql.Driver", que contém o **sqlserverdriver** como um driver registrado. Os aplicativos existentes, que atualmente carregam os drivers usando o método Class.forName, continuarão a funcionar sem modificação.  
  
> [!NOTE]  
>  A biblioteca de classes sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar não pode ser usada com versões anteriores do Java Runtime Environment (JRE). Ver [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para obter a lista de versões do JRE com suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Para obter mais informações sobre como se conectar com fontes de dados e use uma URL de conexão, consulte [construindo a URL de Conexão](../../connect/jdbc/building-the-connection-url.md) e [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
