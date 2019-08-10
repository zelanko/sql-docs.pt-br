---
title: 'Tutorial: Usar Autenticação do AD para SQL Server em Linux'
titleSuffix: SQL Server
description: Este tutorial oferece as etapas de configuração para a autenticação do AD para SQL Server em Linux.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 69bbeb31f8da4023bd0630ae0d944165407e2dec
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027333"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Usar autenticação do Active Directory com o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

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

## <a name="prerequisites"></a>Prerequisites

Antes de iniciar a Autenticação do AD, é necessário:

* Configurar um controlador de domínio do AD (Windows) em sua rede  
* Instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Ingressar o host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio do AD

É necessário ingressar o host Linux do SQL Server com um controlador de domínio do Active Directory. Para saber mais sobre como ingressar um domínio do Active Directory, confira [Ingressar SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Criar usuário do AD (ou MSA) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir SPN

> [!NOTE]
> As seguintes etapas usam seu [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se você estiver no **Azure**, deverá **[criar um](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. No controlador de domínio, execute o comando do PowerShell [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) para criar um usuário do AD com uma senha que nunca expira. O exemplo a seguir dá à conta o nome `mssql`, mas o nome dela poderá ser qualquer coisa que você quiser. Você deverá inserir uma nova senha para a conta.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > É uma melhor prática de segurança ter uma conta do AD dedicada para o SQL Server, para que as credenciais do SQL Server não sejam compartilhadas com outros serviços usando a mesma conta. No entanto, opcionalmente, você poderá reutilizar uma conta existente do AD se souber a senha da conta (necessária para gerar um arquivo keytab na próxima etapa).

2. Defina o SPN (ServicePrincipalName) para essa conta usando a ferramenta **setspn.exe**. O SPN deve ser formatado exatamente como especificado no exemplo a seguir. É possível localizar o nome de domínio totalmente qualificado do computador host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executando `hostname --all-fqdns` no host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A porta TCP deve ser 1433, a menos que você tenha configurado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar um número da porta diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se você receber um erro, `Insufficient access rights`, verifique com seu administrador de domínio se você tem permissões suficientes para definir um SPN nessa conta.
   >
   > Se você alterar a porta TCP no futuro, deverá executar o comando **setspn** novamente com o novo número da porta. Você também precisa adicionar o novo SPN ao keytab do serviço SQL Server seguindo as etapas na próxima seção.

Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar keytab do serviço do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Há duas maneiras diferentes de configurar os arquivos keytab do serviço SQL Server. A primeira opção é usar uma conta de computador (UPN), enquanto a segunda opção usa um MSA (conta de serviço gerenciado) na configuração keytab. Os dois mecanismos são igualmente funcionais e você pode escolher o método que funciona melhor para seu ambiente.

Nos dois casos, o SPN criado na etapa anterior é necessário e deve estar registrado no keytab.

Para configurar o arquivo keytab do serviço SQL Server:

1. Configure as [entradas keytab do SPN](#spn) na próxima seção.

1. Em seguida, [adicione as entradas UPN](#upn) (opção 1) ou [MSA](#msa) (opção 2) no arquivo keytab seguindo as etapas nas respectivas seções.

> [!IMPORTANT]
> Se a senha UPN/MSA for alterada ou a senha da conta à qual os SPNs são atribuídos for alterada, você deverá atualizar o keytab com a nova senha e o KVNO (número de versão da chave). Alguns serviços também podem girar as senhas automaticamente. Examine as políticas de rotação de senha das contas em questão e alinhe-as com as atividades de manutenção agendada para evitar tempo de inatividade inesperado.

### <a id="spn"></a> Entradas keytab do SPN

1. Verifique o KVNO (número de versão da chave) da conta do AD criada na etapa anterior. Normalmente, é 2, mas poderia ser outro inteiro se você alterasse a senha da conta várias vezes. No computador host do SQL Server, execute os seguintes comandos:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM
   ```

   > [!NOTE]
   > Os SPNs poderão levar vários minutos para serem propagados por meio de seu domínio, principalmente se ele for grande. Se você receber o erro `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, aguarde alguns minutos e tente novamente.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Adicione entradas keytab para cada SPN usando os seguintes comandos:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Escreva o keytab em um arquivo e, em seguida, saia do ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > A ferramenta **ktutil** não valida a senha; portanto, insira-a corretamente quando solicitado.

### <a id="upn"></a> Opção 1: Usar UPN para configurar o keytab

Adicione a conta do computador ao keytab com **ktutil**. A conta do computador (também chamada de UPN) está presente em **/etc/krb5.keytab** no formato `<hostname>$@<realm.com>` (por exemplo, `sqlhost$@CONTOSO.COM`). Copie essas entradas de **/etc/krb5.keytab** para **mssql.keytab**.

1. Inicie **ktuil** com o seguinte comando:

   ```bash
   sudo ktutil
   ```

1. Use o comando **rkt** para ler todas as entradas em **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. Em seguida, liste as entradas.

   ```bash
   list
   ```

1. Exclua todas as entradas por seu número de slot que não seja o UPN. Faz isso, uma por vez, repetindo o seguinte comando:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Quando uma entrada é excluída, como o slot 1, todos os valores deslizam para cima para ocupar seu lugar. Isso significa que a entrada no slot 2 move-se para o slot 1 quando a entrada deste é excluída.

1. Liste as entradas novamente até que restem apenas as entradas UPN.

   ```bash
   list
   ```

1. Quando restarem somente entradas UPN, acrescente estes valores a **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Saia do **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opção 2:  Usar MSA para configurar o keytab

Para a opção MSA, você precisa criar o keytab Kerberos do SQL Server. Ele deve conter todos os [SPNs registrados na primeira etapa](#spn) e as credenciais do MSA na qual os SPNs são registrados. 

1. Após criação das entradas keytab SPN, execute os seguintes comandos em um computador Linux ingressado no domínio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   Essa etapa exibe o KVNO para a conta de usuário que recebeu a propriedade SPN. Para que essa etapa funcione, o SPN deve ter sido atribuído à conta MSA durante sua criação. Se o SPN não tiver sido atribuído à MSA, o KVNO exibido será da conta do proprietário SPN atual e seu uso para configuração estará incorreto.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Adicione a MSA com os seguintes dois comandos:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Escreva o keytab em um arquivo e, em seguida, saia do ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Ao usar a abordagem da MSA, uma opção de configuração precisa ser definida com a ferramenta **mssql-conf** para especificar a MSA a ser usada ao acessar o arquivo keytab. Verifique se os valores abaixo estão em **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Inclua apenas o nome da MSA e não o nome do domínio ou da conta.

## <a id="securekeytab"></a> Proteger o arquivo keytab

Qualquer pessoa com acesso ao esse arquivo keytab pode representar o SQL Server no domínio; portanto, restrinja o acesso ao arquivo de tal forma que apenas a conta mssql tenha acesso de leitura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configurar o SQL Server para usar o arquivo keytab para autenticação Kerberos

Use as etapas a seguir para configurar o SQL Server para iniciar usando o arquivo keytab para autenticação Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

Opcionalmente, desabilite as conexões UDP para o controlador de domínio para melhorar o desempenho. Em muitos casos, as conexões UDP falham consistentemente ao conectar-se a um controlador de domínio; portanto, você pode definir as opções de configuração no **/etc/krb5.conf** para ignorar chamadas UDP. Edite **/etc/krb5.conf** e defina as seguintes opções:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

Neste ponto, você está pronto para usar logons baseados no AD no SQL Server da seguinte maneira.

## <a id="createsqllogins"></a> Criar logons baseados em AD no Transact-SQL

1. Conecte-se ao SQL Server e crie um logon baseado no AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Verifique se o logon agora está listado na exibição do catálogo do sistema [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md):

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectar-se ao SQL Server usando a Autenticação do AD

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

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS em um cliente Windows ingressado em domínio

Faça logon em um cliente Windows ingressado em domínio usando suas credenciais de domínio. Verifique se o SQL Server Management Studio está instalado e conecte-se à sua instância do SQL Server ( por exemplo, `mssql-host.contoso.com`) especificando a **Autenticação do Windows** na caixa de diálogo **Conectar ao servidor**.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticação do AD usando outros drivers do cliente

A tabela a seguir descreve recomendações para outros drivers do cliente:

| Driver do cliente | Recomendação |
|---|---|
| **JDBC** | Use a Autenticação Integrada Kerberos para conectar o SQL Server. |
| **ODBC** | Use a Autenticação Integrada. |
| **ADO.NET** | Sintaxe de Cadeia de Conexão. |

## <a id="additionalconfig"></a> Opções de configuração adicionais

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

Primeiro, defina **disablessd** e **enablekdcfromkrb5conf** como true e reinicie o SQL Server:

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
