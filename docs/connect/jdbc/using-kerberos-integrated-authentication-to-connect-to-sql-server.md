---
title: Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8eaa889f12adb2470040cab4c0fba5df295a1cb2
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916232"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar a propriedade de conexão **authenticationScheme** para indicar que deseja se conectar a um banco de dados usando a autenticação integrada Kerberos tipo 4. Confira [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md) para obter mais informações sobre as propriedades de conexão. Para obter mais informações sobre o Kerberos, confira [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758).

Ao usar a autenticação integrada com o Java **Krb5LoginModule**, você pode configurar o módulo usando a [Classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para IBM Java VMs:

- **useDefaultCcache = true**
- **moduleBanner = false**

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para todas as outras VMs Java:

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Comentários

Antes do [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], os aplicativos podiam especificar a autenticação integrada (usando Kerberos ou NTLM, dependendo do que estava disponível) usando a propriedade de conexão **integratedSecurity** e referenciando **mssql-jdbc_auth-\<version>-\<arch>.dll**, conforme descrito em [Como criar a URL de conexão](../../connect/jdbc/building-the-connection-url.md).

Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar a propriedade de conexão **authenticationScheme** para indicar que deseja se conectar a um banco de dados usando a autenticação integrada Kerberos por meio da implementação Java Kerberos pura:

- Se você desejar a autenticação integrada usando o **Krb5LoginModule**, ainda poderá especificar a propriedade de conexão **integratedSecurity=true**. Você também deve especificar a propriedade de conexão **authenticationScheme=JavaKerberos**.

- Para continuar usando a autenticação integrada com **mssql-jdbc_auth-\<version>-\<arch>.dll**, basta especificar a propriedade de conexão **integratedSecurity=true** (e opcionalmente **authenticationScheme=NativeAuthentication**).

- Se você especificar **authenticationScheme=JavaKerberos**, mas não especificar também **integratedSecurity=true**, o driver ignorará a propriedade de conexão **authenticationScheme** e esperará encontrar as credenciais de nome de usuário e senha na cadeia de conexão.

Ao usar uma fonte de dados para criar conexões, você pode definir o esquema de autenticação de maneira programada usando **setAuthenticationScheme** e, opcionalmente, definir o SPN para conexões Kerberos usando **setServerSpn**.

Um novo agente foi adicionado para oferecer suporte à autenticação Kerberos: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Para obter mais informações, veja [Rastreamento de operação do driver](../../connect/jdbc/tracing-driver-operation.md).

As seguintes diretrizes ajudarão você a configurar o Kerberos:

1. Defina **AllowTgtSessionKey** como 1 no Registro para Windows. Para obter mais informações, veja o artigo sobre [Entradas de Registro do protocolo Kerberos e chaves de configuração do KDC no Windows Server 2003](https://support.microsoft.com/kb/837361).
2. Verifique se a configuração Kerberos (krb5.conf nos ambientes UNIX) indica o realm e KDC corretos para o seu ambiente.
3. Inicialize o cache TGT usando kinit ou logging no domínio.
4. Quando um aplicativo que usa **authenticationScheme=JavaKerberos** é executado nos sistemas operacionais Windows Vista ou Windows 7, você deve usar uma conta de usuário padrão. No entanto, se você executar o aplicativo na conta de um administrador, ele precisará ser executado com privilégios de administrador.

> [!NOTE]  
> O atributo de conexão serverSpn é compatível somente com os Microsoft JDBC Drivers 4.2 e superiores.

## <a name="service-principal-names"></a>Nomes de entidades de serviço

Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço.

Você pode especificar o SPN usando a propriedade de conexão **serverSpn**, ou simplesmente deixar que o driver o crie para você (o padrão). Esta propriedade está no formato de: "MSSQLSvc/fqdn:port\@REALM" em que fqdn é o nome de domínio totalmente qualificado, porta é o número da porta e REALM é o realm Kerberos do SQL Server em letras maiúsculas. A parte do realm dessa propriedade é opcional quando o realm padrão do Kerberos é o mesmo que o do servidor e não está incluído, por padrão. Se você quiser dar suporte a um cenário de autenticação entre áreas de autenticação em que a área de autenticação padrão na configuração Kerberos é diferente do servidor, você deve definir o SPN com a propriedade serverSpn.

Por exemplo, o SPN pode ser: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ.CORP.CONTOSO.COM"

Para obter mais informações sobre SPNs (nomes de entidade de serviço), consulte:

- [Registrar um nome de entidade de serviço para conexões de Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)

- [Uso de Kerberos com SQL Server](https://docs.microsoft.com/archive/blogs/sql_protocols/using-kerberos-with-sql-server)

> [!NOTE]  
> Antes da versão 6.2 do driver JDBC, para o uso adequado do Cross Realm Kerberos, você precisaria definir explicitamente o **serverSpn**.
>
> Começando com a versão 6.2, o driver poderá criar o **serverSpn** por padrão, mesmo ao usar o Cross Realm Kerberos. Embora seja possível usar o **serverSpn** explicitamente também.

## <a name="creating-a-login-module-configuration-file"></a>Criando um arquivo de configuração de módulo de logon

Se desejar, você pode especificar um arquivo de configuração Kerberos. Se um arquivo de configuração não for especificado, as configurações a seguir estarão em vigor:

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

Se você decidir criar um arquivo de configuração de módulo de logon, o arquivo deverá ter o seguinte formato:

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

Um arquivo de configuração de logon consiste em uma ou mais entradas, cada uma especificando qual tecnologia de autenticação subjacente deve ser usada para um ou mais aplicativos específicos. Por exemplo,

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

Portanto, cada entrada do arquivo de configuração de módulo de logon consiste em um nome seguido por uma ou mais entradas específicas de LoginModule, onde cada uma delas é encerrada com um ponto-e-vírgula e todo o grupo de entradas específicas de LoginModule é delimitado por chaves. Cada entrada do arquivo de configuração é encerrado com um ponto-e-vírgula.

Além de permitir que o driver obtenha credenciais Kerberos usando as configurações especificadas no arquivo de configuração de módulo de logon, o driver pode usar credenciais existentes. Isso poderá ser útil quando o aplicativo precisar criar conexões usando as credenciais de mais de um usuário.

O driver tentará usar as credenciais existentes se elas estiverem disponíveis, antes de tentar fazer logon usando o módulo de logon especificado. Portanto, ao usar o método `Subject.doAs` para executar o código em um contexto específico, uma conexão será criada com as credenciais passadas para a chamada `Subject.doAs`.

Para obter mais informações, veja [Arquivo de configuração de logon JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) e [Classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).

Começando com o Microsoft JDBC Driver 6.2, o nome do arquivo de configuração do módulo de logon pode, opcionalmente, ser passado usando a propriedade de conexão `jaasConfigurationName`, isso permite que cada conexão tenha uma configuração de logon própria.

## <a name="creating-a-kerberos-configuration-file"></a>Criando um arquivo de configuração Kerberos

Para obter mais informações sobre os arquivos de configuração Kerberos, leia o artigo sobre [Requisitos do Kerberos](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).

Este é um arquivo de configuração de domínio de exemplo, em que YYYY e ZZZZ são os nomes de domínio.

```ini
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

Você pode habilitar um arquivo de configuração de domínio com -Djava.security.krb5.conf. Você pode habilitar um arquivo de configuração de módulo de logon com **-Djava.security.auth.login.config**.

Por exemplo, o seguinte comando pode ser usado para iniciar o aplicativo:

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Verificando se o SQL Server pode ser acessado via Kerberos

Execute a seguinte consulta no SQL Server Management Studio:

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

Verifique se você tem a permissão necessária para executar essa consulta.

## <a name="constrained-delegation"></a>Delegação restrita

Começando com o Microsoft JDBC Driver 6.2, o driver é compatível com a Delegação restrita de Kerberos. A credencial delegada pode ser passada como o objeto org.ietf.jgss.GSSCredential, essas credenciais são usadas pelo driver para estabelecer a conexão.

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Conexão Kerberos usando nomes de entidade de segurança e senha

Começando com o Microsoft JDBC Driver 6.2, o driver pode estabelecer a conexão Kerberos usando o nome da entidade de segurança e a senha passadas em uma cadeia de conexão.

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

A propriedade de nome de usuário não exigirá o REALM se o usuário pertencer ao default_realm configurado no arquivo krb5.conf. Quando `userName` e `password` são configurados juntamente com a propriedade `integratedSecurity=true;` e `authenticationScheme=JavaKerberos;`, a conexão será estabelecida com o valor de userName como a Entidade de Segurança do Kerberos juntamente com a senha fornecida.

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>Usando a autenticação Kerberos de computadores UNIX no mesmo domínio

Este guia pressupõe que já exista uma instalação do Kerberos em funcionamento. Execute o código a seguir em um computador Windows com autenticação Kerberos em funcionamento para verificar se o mencionado acima é verdade. O código exibirá "Esquema de autenticação: KERBEROS" para o console se for bem-sucedido. Não são necessários sinalizadores de runtime adicionais, dependências ou configurações de driver além daqueles fornecidos. O mesmo bloco de código pode ser executado no Linux para verificar conexões bem-sucedidas.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. Realize o ingresso no domínio do computador cliente no mesmo domínio do servidor.
2. (Opcional) Defina a localização do tíquete Kerberos padrão. Isso é feito de maneira mais conveniente configurando a variável de ambiente `KRB5CCNAME`.
3. Obtenha o tíquete Kerberos, gerando um novo ou colocando um existente na localização padrão do tíquete Kerberos. Para gerar um tíquete, basta usar um terminal e inicializar o tíquete por meio de `kinit USER@DOMAIN.AD` em que "USER" e "DOMAIN.AD" são a entidade de segurança e o domínio, respectivamente. Por exemplo: `kinit SQL_SERVER_USER03@MICROSOFT.COM`. O tíquete será gerado na localização de tíquete padrão ou no caminho de `KRB5CCNAME`, caso tenha sido definido.
4. O terminal solicitará uma senha, digite a senha.
5. Verifique as credenciais no tíquete por meio de `klist` e confirme se as credenciais são aquelas que você pretende usar para autenticação.
6. Execute o código de exemplo acima e confirme se a Autenticação Kerberos foi bem-sucedida.

## <a name="see-also"></a>Confira também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
