---
title: Criar a URL de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: a19c9022d26ed7aa0af4443583553b441059e97c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="building-the-connection-url"></a>Construindo a URL de conexão
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O formato geral da URL de conexão é  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 onde:  
  
-   **JDBC: / /** (obrigatório) é conhecido como o subprotocolo e é constante.  
  
-   **serverName** (opcional) é o endereço do servidor para se conectar ao. Pode ser um endereço IP ou DNS, ou pode ser localhost ou 127.0.0.1 para o computador local. Se não for especificado na URL de conexão, o nome do servidor deverá ser especificado na coleção de propriedades.  
  
-   **instanceName** (opcional) é a instância para a conexão em serverName. Se não for especificada, será feita uma conexão com a instância padrão.  
  
-   **portNumber** (opcional) é a porta de conexão em serverName. O padrão é 1433. Se estiver usando o padrão, você não precisará especificar a porta, nem os dois-pontos (':') que a precedem, na URL.  
  
    > [!NOTE]  
    >  Para um desempenho de conexão ideal, recomenda-se definir o portNumber ao se estabelecer conexão com uma instância nomeada. Isso evitará uma viagem de ida e volta ao servidor para determinar o número da porta. Se forem usados um portNumber e um instanceName, o portNumber terá precedência e o instanceName será ignorado.  
  
-   **propriedade** (opcional) é uma ou mais propriedades de conexão de opção. Para obter mais informações, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md). Qualquer propriedade da lista pode ser especificada. As propriedades só podem ser delimitadas com o uso de ponto-e-vírgula (';') e não podem ser duplicadas.  
  
> [!CAUTION]  
>  Para fins de segurança, recomenda-se evitar construir as URLs de conexão com base na entrada do usuário. Convém especificar apenas o nome do servidor e o driver na URL. Para os valores de nome de usuário e senha, use as coleções de propriedades de conexão. Para obter mais informações sobre a segurança nos aplicativos JDBC, consulte [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md).  
  
## <a name="connection-examples"></a>Exemplos de conexão  
 Conectar ao banco de dados padrão no computador local usando um nome de usuário e senha:  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  Embora o exemplo anterior utilize um nome de usuário e uma senha na cadeia de conexão, você deve usar a segurança integrada, que é mais segura. Para obter mais informações, consulte o [conexão com a autenticação integrada](#Connectingintegrated) seção mais adiante neste tópico.  
  
 A cadeia de conexão a seguir mostra um exemplo de como se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando a autenticação integrada e Kerberos de um aplicativo em execução em qualquer sistema operacional com suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]:  
  
```  
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 Conectar ao banco de dados padrão no computador local usando a autenticação integrada:  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 Conectar a um banco de dados nomeado em um servidor remoto:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Conectar na porta padrão ao servidor remoto:  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Conectar especificando um nome de aplicativo personalizado:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>Instâncias nomeadas e várias instâncias do SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permite a instalação de várias instâncias de banco de dados por servidor. Cada instância é identificada por um nome específico. Para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode especificar o número da porta da instância nomeada (preferido) ou você pode especificar o nome da instância como uma propriedade URL do JDBC ou uma **datasource** propriedade. Se nenhuma propriedade de nome de instância ou número de porta for especificada, será criada uma conexão com a instância padrão. Consulte os exemplos a seguir:  
  
 Para usar um número de porta, faça o seguinte:  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 Para usar uma propriedade URL do JDBC, faça o seguinte:  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>Escapando valores na URL de conexão  
 Pode ser necessário escapar certas partes dos valores da URL de conexão devido à inclusão de caracteres especiais como espaços, ponto-e-vírgulas e aspas. O driver JDBC dará suporte ao escape desses caracteres se eles estiverem entre chaves. Por exemplo, {;} escapa um ponto-e-vírgula.  
  
 Os valores escapados podem conter caracteres especiais (principalmente '=', ';', '[]' e espaço), mas não podem conter chaves. Convém adicionar os valores que devem ser escapados e contêm chaves a uma coleção de propriedades.  
  
> [!NOTE]  
>  O espaço em branco dentro das chaves é literal e não é cortado.  
  
##  <a name="Connectingintegrated"></a> Conectar-se com a autenticação integrada no Windows  
 O driver JDBC dá suporte ao uso da autenticação integrada do Tipo 2 em sistemas operacionais Windows por meio da propriedade de cadeia de conexão integratedSecurity. Para usar a autenticação integrada, copie o arquivo sqljdbc_auth.dll para um diretório no caminho do sistema Windows no computador em que o driver JDBC está instalado.  
  
 Os arquivos sqljdbc_auth.dll estão instalados no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \auth\  
  
 Para qualquer sistema operacional compatível com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [usando a autenticação integrada Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) para obter uma descrição de um recurso adicionado no [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] que permite que um aplicativo para se conectar a um o banco de dados usando a autenticação integrada com Kerberos tipo 4.  
  
> [!NOTE]  
>  Se você estiver executando uma Máquina Virtual Java (JVM) de 32 bits, use o arquivo sqljdbc_auth.dll na pasta x86, mesmo se o sistema operacional for a versão x64. Se estiver executando uma JVM de 64 bits em um processador x64, use o arquivo sqljdbc_auth.dll na pasta x64.  
  
 Como alternativa, você pode definir a propriedade do sistema java.libary.path para especificar o diretório de sqljdbc_auth.dll. Por exemplo, se o driver JDBC for instalado no diretório padrão, você poderá especificar o local da DLL usando o seguinte argumento de máquina virtual (VM) quando o aplicativo Java for iniciado:  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>Conectando com endereços IPv6  
 O driver JDBC oferece suporte ao uso de endereços IPv6 com a coleção de propriedades de conexão e com a propriedade de cadeia de conexão serverName. O valor de serverName inicial, como jdbc:*sqlserver*://*serverName*, não há suporte para endereços IPv6 em cadeias de caracteres de conexão. Usando um nome para *serverName* em vez de um IPv6 bruto endereço funcionará em todos os casos em que a conexão. Os exemplos a seguir fornecem mais informações.  
  
 **Para usar a propriedade serverName**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **Para usar a coleção de propriedades**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
