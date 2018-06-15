---
title: Usando o Kerberos de autenticação para se conectar ao SQL Server integrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e2019cba57870cf9e22bdeb4d27f52c055fcdc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852701"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Usando a autenticação integrada do Kerberos para se conectar ao SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A partir do [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar o **authenticationScheme** propriedade de conexão para indicar que deseja se conectar a um banco de dados usando a autenticação integrada Kerberos tipo 4. Consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) para obter mais informações sobre propriedades de conexão. Para obter mais informações sobre Kerberos, consulte [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758).  
  
 Ao usar a autenticação integrada com o Java **Krb5LoginModule**, você pode configurar o módulo usando [classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  
  
 O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para IBM Java VMs:  
  
-   **useDefaultCcache = true**  
  
-   **moduleBanner = false**  
  
 O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para todas as outras Java VMs:  
  
-   **useTicketCache = true**  
  
-   **doNotPrompt = true**  
  
## <a name="remarks"></a>Remarks  
 Antes de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], aplicativos podiam especificar a autenticação integrada (usando Kerberos ou NTLM, dependendo de qual estivesse disponível) usando o **integratedSecurity** propriedade de conexão e referenciando  **sqljdbc_auth.dll**, conforme descrito em [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).  
  
 A partir do [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar o **authenticationScheme** integrado de propriedade de conexão para indicar que deseja se conectar a um banco de dados usando o Kerberos, a autenticação usando o Kerberos Java puro implementação:  
  
-   Se você quiser usar a autenticação integrada **Krb5LoginModule**, você ainda deve especificar o **integratedSecurity = true** propriedade de conexão. Especifique também o **authenticationScheme = JavaKerberos** propriedade de conexão.  
  
-   Para continuar usando a autenticação integrada com **sqljdbc_auth.dll**, basta especificar **integratedSecurity = true** propriedade de conexão (e, opcionalmente, **authenticationScheme = NativeAuthentication**).  
  
-   Se você especificar **authenticationScheme = JavaKerberos** , mas não especificar também **integratedSecurity = true**, o driver ignorará a **authenticationScheme** propriedade de conexão e esperará a localização credenciais de nome e senha de usuário na cadeia de conexão.  
  
 Ao usar uma fonte de dados para criar conexões, você pode definir o esquema de autenticação usando setAuthenticationScheme e (opcionalmente) definir o SPN para conexões Kerberos usando **setServerSpn**.  
  
 Um novo agente foi adicionado para oferecer suporte à autenticação Kerberos: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Para obter mais informações, consulte [a operação de rastreamento do Driver](../../connect/jdbc/tracing-driver-operation.md).  
  
 As seguintes diretrizes ajudarão você a configurar o Kerberos:  
  
1.  Definir **AllowTgtSessionKey** como 1 no registro do Windows. Para obter mais informações, consulte [chaves de configuração do KDC no Windows Server 2003 e entradas do registro do protocolo Kerberos](http://support.microsoft.com/kb/837361).  
  
2.  Verifique se a configuração Kerberos (krb5.conf nos ambientes UNIX) indica o realm e KDC corretos para o seu ambiente.  
  
3.  Inicialize o cache TGT usando kinit ou logging no domínio.  
  
4.  Quando um aplicativo que usa **authenticationScheme = JavaKerberos** é executado no Windows 7 ou Windows Vista e sistemas operacionais, você deve usar uma conta de usuário padrão. No entanto, se você executar o aplicativo na conta de um administrador, o aplicativo deverá ser executado com privilégios de administrador.  
  
> [!NOTE]  
>  O atributo de conexão serverSpn só tem suporte pelo Microsoft JDBC Drivers 4.2 e superior.  
  
## <a name="service-principal-names"></a>Nomes de Entidade de Serviço  
 Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço.  
  
 Você pode especificar o SPN usando o **serverSpn** propriedade de conexão, ou simplesmente deixar que o driver compilá-lo para você (o padrão).  Essa propriedade está no formato: "MSSQLSvc/fqdn:port@REALM" em que fqdn é o nome de domínio totalmente qualificado, porta é o número de porta e REALM é o realm Kerberos do SQL Server em letras maiusculas.  A parte da área de autenticação dessa propriedade é opcional se a área de autenticação padrão do seu Kerberos for a mesma que a do servidor e não estiver incluída, por padrão.  Se você quiser dar suporte a um cenário de autenticação entre áreas de autenticação em que a área de autenticação padrão na configuração Kerberos é diferente do servidor, você deve definir o SPN com a propriedade serverSpn.  
  
 Por exemplo, o SPN pode parecer com: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433@ZZZZ.CORP.CONTOSO.COM"  
  
 Para obter mais informações sobre SPNs (nomes de entidade de serviço), consulte:  
  
-   [Como usar a autenticação Kerberos no SQL Server](http://support.microsoft.com/kb/319723)  
  
-   [Usando o Kerberos com o SQL Server](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> Antes de lançar 6.2.0 do driver JDBC, uso adequado de cruzada Realm Kerberos, você precisa definir explicitamente o **serverSpn**.
>
> A partir de 6.2.0 versão, o driver será capaz de criar o **serverSpn** por padrão, mesmo ao usar Cross Realm Kerberos. Embora você possa usar **serverSpn** explicitamente muito. 
  
## <a name="creating-a-login-module-configuration-file"></a>Criando um arquivo de configuração de módulo de logon  
 Se desejar, você pode especificar um arquivo de configuração Kerberos. Se um arquivo de configuração não for especificado, as configurações a seguir estarão em vigor:  
  
 Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule necessário useTicketCache = true;  
  
 IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule necessário useDefaultCcache = true;  
  
 Se você decidir criar um arquivo de configuração de módulo de logon, o arquivo deverá ter o seguinte formato:  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 Um arquivo de configuração de logon consiste em uma ou mais entradas, cada uma especificando qual tecnologia de autenticação subjacente deve ser usada para um ou mais aplicativos específicos. Por exemplo,  
  
```  
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 Portanto, cada entrada do arquivo de configuração de módulo de logon consiste em um nome seguido por uma ou mais entradas específicas de LoginModule, onde cada uma delas é encerrada com um ponto-e-vírgula e todo o grupo de entradas específicas de LoginModule é delimitado por chaves. Cada entrada do arquivo de configuração é encerrado com um ponto-e-vírgula.  
  
 Além de permitir que o driver obtenha credenciais Kerberos usando as configurações especificadas no arquivo de configuração de módulo de logon, o driver pode usar credenciais existentes. Isso poderá ser útil quando o aplicativo precisar criar conexões usando as credenciais de mais de um usuário.  
  
 O driver tentará usar as credenciais existentes se elas estiverem disponíveis, antes de tentar fazer logon usando o módulo de logon especificado. Desse modo, ao usar o método Subject.doAs para executar o código em um contexto específico, uma conexão será criada com as credenciais passadas para a chamada de Subject.doAs.  
  
 Para obter mais informações, consulte [arquivo de configuração de logon JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) e [classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).  

 A partir do Microsoft JDBC Driver 6.2, nome do arquivo de configuração do módulo de logon, opcionalmente, pode ser passado usando jaasConfigurationName de propriedade de conexão, isso permite que cada conexão ter sua própria configuração de logon.
 
## <a name="creating-a-kerberos-configuration-file"></a>Criando um arquivo de configuração Kerberos  
 Para obter mais informações sobre arquivos de configuração do Kerberos, consulte [requisitos do Kerberos](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).  
  
 Este é um arquivo de configuração de domínio de exemplo, em que YYYY e ZZZZ são nomes de domínio no seu site.  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
  
[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  
  
        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  
  
```  
  
## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>Habilitando o arquivo de configuração de domínio e o arquivo de configuração de módulo de logon  
 Você pode habilitar um arquivo de configuração de domínio com -Djava.security.krb5.conf. Você pode habilitar um arquivo de configuração do módulo de logon com **-Djava.security.auth.login.config**.  
  
 Por exemplo, quando você iniciar o aplicativo, poderá usar a seguinte linha de comando:  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Verificando se o SQL Server pode ser acessado via Kerberos  
 Execute a seguinte consulta no SQL Server Management Studio:  
  
 **Selecione auth_scheme de sys.DM exec_connections onde session_id = @@spid**  
  
 Verifique se você tem a permissão necessária para executar essa consulta.  

## <a name="constrained-delegation"></a>Delegação restrita
A partir do Microsoft JDBC Driver 6.2, o driver oferece suporte à delegação restrita de Kerberos. A credencial de delegado pode ser passada como objeto org.ietf.jgss.GSSCredential, essas credenciais são usadas pelo driver para estabelecer a conexão. 

```
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Usando nomes de entidade de segurança e a senha de Conexão de Kerberos
A partir do Microsoft JDBC Driver 6.2, o driver pode estabelecer Kerberos usando o nome da entidade e a senha de conexão passada na cadeia de caracteres de conexão. 
```
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
A propriedade de nome de usuário não requer REALM se o usuário pertence a default_realm definido no arquivo krb5 conf. Quando `userName` e `password` é definido com `integratedSecurity=true;` e `authenticationScheme=JavaKerberos;` propriedade, a conexão é estabelecida com o valor do nome de usuário como Principal do Kerberos junto com a senha fornecida.
 
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
