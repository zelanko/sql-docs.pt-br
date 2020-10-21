---
title: 'Tutorial: Usar Autenticação do AD para SQL Server em Linux'
titleSuffix: SQL Server
description: Este tutorial fornece as etapas de configuração para autenticação do AD (Active Directory) no SQL Server em Linux.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 12/18/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 003001752ee656483d7b4a1820f191aafc044f25
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115919"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Usar autenticação do Active Directory com o SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este tutorial explica como configurar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para dar suporte à autenticação do AD (Active Directory), também conhecida como autenticação integrada. Para obter uma visão geral, confira [Autenticação do Active Directory para SQL Server em Linux](sql-server-linux-active-directory-auth-overview.md).

Este tutorial é composto pelas seguintes etapas:

> [!div class="checklist"]
> * Ingressar o host do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar keytab do serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Proteger o arquivo keytab
> * Configurar o SQL Server para usar o arquivo keytab para autenticação Kerberos
> * Criar logons baseados em AD no Transact-SQL
> * Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar a Autenticação do AD, é necessário:

* Configurar um controlador de domínio do AD (Windows) em sua rede  
* Instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a name="join-ssnoversion-host-to-ad-domain"></a><a id="join"></a> Ingressar o host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio do AD

Ingresse no host do SQL Server Linux com um controlador de domínio do Active Directory. Para saber mais sobre como ingressar um domínio do Active Directory, confira [Ingressar SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a name="create-ad-user-or-msa-for-ssnoversion-and-set-spn"></a><a id="createuser"></a> Criar usuário do AD (ou MSA) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir SPN

> [!NOTE]
> As seguintes etapas usam seu [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se você estiver no **Azure**, deverá **[criar um](/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. No controlador de domínio, execute o comando do PowerShell [New-ADUser](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617253(v=technet.10)) para criar um usuário do AD com uma senha que nunca expira. O exemplo a seguir dá à conta o nome `mssql`, mas o nome dela poderá ser qualquer coisa que você quiser. Você deverá inserir uma nova senha para a conta.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > É uma melhor prática de segurança ter uma conta do AD dedicada para o SQL Server, para que as credenciais do SQL Server não sejam compartilhadas com outros serviços usando a mesma conta. No entanto, opcionalmente, você poderá reutilizar uma conta existente do AD se souber a senha da conta (necessária para gerar um arquivo keytab na próxima etapa). Além disso, a conta deve ser habilitada para dar suporte à criptografia AES Kerberos de 128 bits e 256 bits (atributo **msDS-SupportedEncryptionTypes**) na conta do usuário.

2. Defina o SPN (ServicePrincipalName) para essa conta usando a ferramenta **setspn.exe**. O SPN deve ser formatado exatamente como especificado no exemplo a seguir. É possível localizar o nome de domínio totalmente qualificado do computador host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executando `hostname --all-fqdns` no host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A porta TCP deve ser 1433, a menos que você tenha configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar um número da porta diferente.

   ```PowerShell
   setspn -A MSSQLSvc/<fully qualified domain name of host machine>:<tcp port> mssql
   setspn -A MSSQLSvc/<netbios name of the host machine>:<tcp port> mssql
   ```

   > [!NOTE]
   > Se você receber um erro, `Insufficient access rights`, verifique com seu administrador de domínio se você tem permissões suficientes para definir um SPN nessa conta. A conta usada para registrar um SPN precisará das permissões **Write servicePrincipalName**. Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).
   >
   > Se você alterar a porta TCP no futuro, deverá executar o comando **setspn** novamente com o novo número da porta. Você também precisa adicionar o novo SPN ao keytab do serviço SQL Server seguindo as etapas na próxima seção.

Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a name="configure-ssnoversion-service-keytab"></a><a id="configurekeytab"></a> Configurar keytab do serviço do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

A configuração da autenticação do AD para o SQL Server em Linux exige uma conta do AD (uma conta de usuário do AD ou MSA) e o SPN criado na seção anterior.

> [!IMPORTANT]
> Se a senha da conta do AD for alterada ou a senha da conta à qual os SPNs são atribuídos for alterada, você precisará atualizar o keytab com a nova senha e o KVNO (número de versão da chave). Alguns serviços também podem girar as senhas automaticamente. Examine as políticas de rotação de senha das contas em questão e alinhe-as com as atividades de manutenção agendada para evitar tempo de inatividade inesperado.

### <a name="spn-keytab-entries"></a><a id="spn"></a> Entradas keytab do SPN

1. Verifique o KVNO (número de versão da chave) da conta do AD criada na etapa anterior. Normalmente, é 2, mas poderia ser outro inteiro se você alterasse a senha da conta várias vezes. No computador host do SQL Server, execute os seguintes comandos:

    - Os exemplos abaixo pressupõem que o `user` esteja no domínio `@CONTOSO.COM`. Modifique o usuário e o nome de domínio para seu nome de usuário e seu domínio.

   ```bash
   kinit user@CONTOSO.COM
   kvno user@CONTOSO.COM
   kvno MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM
   ```

   > [!NOTE]
   > Os SPNs poderão levar vários minutos para serem propagados por meio de seu domínio, principalmente se ele for grande. Se você receber o erro `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM`, aguarde alguns minutos e tente novamente.</br></br> Os comandos acima só funcionarão se o servidor tiver ingressado em um domínio do AD, que foi abordado na seção anterior.

1. Usando [**ktpass**](/windows-server/administration/windows-commands/ktpass), adicione entradas keytab para cada SPN usando os seguintes comandos em um prompt de comando do computador Windows:

    - `<DomainName>\<UserName>`: pode ser uma conta de usuário do AD ou MSA
    - `@CONTOSO.COM`: use o nome do seu domínio
    - `/kvno <#>`: substitua `<#>` pelo KVNO obtido em uma etapa anterior
    - `<StrongPassword>`: use uma senha forte

   ```bash
   ktpass /princ MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<fully qualified domain name of host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<netbios name of the host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ MSSQLSvc/<netbios name of the host machine>:<tcp port>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ <UserName>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto aes256-sha1 /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>

   ktpass /princ <UserName>@CONTOSO.COM /ptype KRB5_NT_PRINCIPAL /crypto rc4-hmac-nt /mapuser <DomainName>\<UserName> /in mssql.keytab /out mssql.keytab -setpass -setupn /kvno <#> /pass <StrongPassword>
   ```

   > [!NOTE]
   > Os comandos acima permitem codificações de criptografia AES e RC4 para autenticação do AD. O RC4 é uma codificação de criptografia mais antiga e, se um nível mais alto de segurança for necessário, você poderá optar por criar as entradas keytab apenas com a codificação de criptografia AES.
   > As duas últimas entradas de `UserName` devem estar em letras minúsculas, ou a autenticação da permissão poderá falhar.

1. Depois de executar o comando acima, você deverá ter um arquivo keytab chamado mssql.keytab. Copie o arquivo para o computador do SQL Server na pasta `/var/opt/mssql/secrets`.

1. Proteja o arquivo keytab.

    Qualquer pessoa com acesso ao esse arquivo keytab pode representar o SQL Server no domínio; portanto, restrinja o acesso ao arquivo de tal forma que apenas a conta mssql tenha acesso de leitura:

    ```bash
    sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
    sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
    ```

1. A opção de configuração a seguir precisa ser definida com a ferramenta **mssql-conf** para especificar a conta a ser usada ao acessar o arquivo keytab.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <username>
   ```

   > [!NOTE]
   > Inclua apenas o nome de usuário e não domainname\username ou username@domain. O SQL Server adiciona internamente o nome de domínio, conforme necessário, junto com esse nome de usuário, quando usado.

1. Use as etapas a seguir para configurar o SQL Server para ser iniciado usando o arquivo keytab para a autenticação Kerberos.

    ```bash
    sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
    sudo systemctl restart mssql-server
    ```

    > [!TIP]
    > Opcionalmente, desabilite as conexões UDP com o controlador de domínio para aprimorar o desempenho. Em muitos casos, as conexões UDP falham consistentemente ao conectar-se a um controlador de domínio; portanto, você pode definir as opções de configuração no **/etc/krb5.conf** para ignorar chamadas UDP. Edite **/etc/krb5.conf** e defina as seguintes opções:
    > ```bash
    > /etc/krb5.conf
    > [libdefaults]
    > udp_preference_limit=0
    > ```

Neste ponto, você está pronto para usar logons baseados no AD no SQL Server.

## <a name="create-ad-based-logins-in-transact-sql"></a><a id="createsqllogins"></a> Criar logons baseados em AD no Transact-SQL

1. Conecte-se ao SQL Server e crie um logon baseado no AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Verifique se o logon agora está listado na exibição do catálogo do sistema [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md):

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a name="connect-to-sql-server-using-ad-authentication"></a><a id="connect"></a> Conectar-se ao SQL Server usando a Autenticação do AD

Faça logon em um computador cliente usando suas credenciais de domínio. Agora você pode se conectar ao SQL Server sem reinserir sua senha usando a Autenticação do AD. Se você criar um logon para um grupo do AD, qualquer usuário do AD que seja membro desse grupo poderá se conectar da mesma maneira.

O parâmetro de cadeia de conexão específico para os clientes usarem a autenticação do AD depende de qual driver você está usando. Considere os exemplos nas seções a seguir.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>sqlcmd em um cliente Linux ingressado em domínio

Faça logon em um cliente Linux ingressado em domínio usando **SSH** e suas credenciais de domínio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Verifique se você instalou o pacote [mssql-tools](sql-server-linux-setup-tools.md) e conecte-se usando **sqlcmd** sem especificar credenciais:

```bash
sqlcmd -S mssql-host.contoso.com
```
Ao contrário das janelas do SQL, a autenticação Kerberos funciona para a conexão local no SQL Linux. No entanto, você ainda precisará fornecer o FQDN do host do SQL Linux e a Autenticação do AD não funcionará se você tentar se conectar a '.', 'localhost', '127.0.0.1' etc.

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS em um cliente Windows ingressado em domínio

Faça logon em um cliente Windows ingressado em domínio usando suas credenciais de domínio. Verifique se o SQL Server Management Studio está instalado e conecte-se à sua instância do SQL Server ( por exemplo, `mssql-host.contoso.com`) especificando a **Autenticação do Windows** na caixa de diálogo **Conectar ao servidor**.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticação do AD usando outros drivers do cliente

A tabela a seguir descreve recomendações para outros drivers do cliente:

| Driver do cliente | Recomendação |
|---|---|
| **JDBC** | Use a Autenticação Integrada Kerberos para conectar o SQL Server. |
| **ODBC** | Use a Autenticação Integrada. |
| **ADO.NET** | Sintaxe de Cadeia de Conexão. |

## <a name="additional-configuration-options"></a><a id="additionalconfig"></a> Opções de configuração adicionais

Se você estiver usando utilitários de terceiros, como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) ou [Centrify](https://www.centrify.com/) para ingressar o host Linux no domínio do AD e gostaria de forçar o SQL Server a usar a biblioteca openldap diretamente, poderá configurar a opção **disablesssd** com **mssql-conf** da seguinte maneira:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Há utilitários, como o **realmd**, que configuram o SSSD, enquanto outras ferramentas como PBIS, VAS e Centrify não configuram o SSSD. Se o utilitário usado para ingressar o domínio do AD não configura o SSSD, é recomendável configurar a opção **disablesssd** como `true`. Embora não seja necessário, pois o SQL Server tentará usar o SSSD para AD antes de fazer fallback para o mecanismo de openldap, seria mais eficaz configurá-lo para que SQL Server faça chamadas openldap que ignoram diretamente o mecanismo de SSSD.

Se o controlador de domínio der suporte ao LDAPS, será possível forçar todas as conexões do SQL Server com os controladores de domínio para ocorrerem pelo LDAPS. Para verificar se seu cliente pode contatar o controlador de domínio pelo LDAPS, execute o seguinte comando Bash, `ldapsearch -H ldaps://contoso.com:3269`. Para configurar o SQL Server para usar apenas LDAPS, execute o seguinte:

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

Isso usará o LDAPS pelo SSSD se o ingresso no domínio do AD no host for feito por meio do pacote SSSD e **disablesssd** não for definido como true. Se **disablesssd** for definido como true junto com **forcesecureldap** sendo definido como true, então ele usará o protocolo LDAPS por chamadas de biblioteca openldap feito pelo SQL Server.

### <a name="post-sql-server-2017-cu14"></a>Post SQL Server 2017 CU14

Do SQL Server 2017 CU14 em diante, se o SQL Server foi ingressado em um controlador de domínio do AD usando provedores de terceiros e foi configurado para usar chamadas openldap para pesquisa geral do AD definindo **disablesssd** como true, você pode usar a opção **enablekdcfromkrb5** para forçar o SQL Server a usar a biblioteca krb5 para pesquisa KDC, em vez de pesquisa DNS inversa para o servidor KDC.

Isso pode ser útil para o cenário em que convém configurar manualmente os controladores de domínio com os quais o SQL Server tenta se comunicar. E você usa o mecanismo de biblioteca openldap usando a lista KDC em **krb5.conf**.

Primeiro, defina **disablesssd** e **enablekdcfromkrb5conf** como true e, em seguida, reinicie o SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

Em seguida, configure a lista KDC em **no/etc/krb5.conf** da seguinte maneira:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Embora não seja recomendado, é possível usar utilitários, como **realmd**, que configuram o SSSD ao ingressar o host Linux no domínio e, mesmo tempo, configurar o **disablesssd** como true para que o SQL Server use chamadas openldap em vez do SSSD para chamadas relacionadas ao Active Directory.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, percorremos como configurar a autenticação do Active Directory com o SQL Server em Linux. Você aprendeu a:
> [!div class="checklist"]
> * Ingressar o host do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar keytab do serviço [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> * Criar logons baseados em AD no Transact-SQL
> * Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

Em seguida, explore outros cenários de segurança para o SQL Server em Linux.

> [!div class="nextstepaction"]
> [Criptografar conexões com o SQL Server em Linux](sql-server-linux-encrypted-connections.md)