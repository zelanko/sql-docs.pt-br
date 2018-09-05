---
title: Tutorial de autenticação do Active Directory para o SQL Server no Linux | Microsoft Docs
description: Este tutorial fornece as etapas de configuração para a autenticação do AAD para o SQL Server no Linux.
author: meet-bhagdev
ms.date: 02/23/2018
ms.author: meetb
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 2804197643c96e21bd0f412cf757ba0b4e2bdfbc
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381254"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Autenticação usar o Active Directory com o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial explica como configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para dar suporte à autenticação do Active Directory (AD), a autenticação integrada também conhecido como. Para obter uma visão geral, consulte [autenticação do Active Directory para o SQL Server no Linux](sql-server-linux-active-directory-auth-overview.md).

Neste tutorial consiste as seguintes tarefas:

> [!div class="checklist"]
> * Junte-se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab do serviço
> * Criar logons do AD baseada em Transact-SQL
> * Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

> [!NOTE]
>
> Se você quiser configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para usar um provedor de AD de terceiros, consulte [usar provedores do Active Directory de terceiros com o SQL Server no Linux](./sql-server-linux-active-directory-third-party-providers.md).

## <a name="prerequisites"></a>Prerequisites

Antes de configurar a autenticação do AD, você precisa:

* Configurar um controlador de domínio do AD (Windows) em sua rede  
* Instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Junte-se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD

Use as seguintes etapas para ingressar um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a um domínio do Active Directory:

1. Use **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)** para ingressar em sua máquina host para seu domínio do AD. Se você ainda não fez isso, instalar o realmd e pacotes do cliente Kerberos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host usando o Gerenciador de pacotes da distribuição Linux:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Se a instalação do pacote de cliente Kerberos solicitar um nome de realm, insira seu nome de domínio em letras maiusculas.

   > [!NOTE]
   > Este passo a passo usa "contoso.com" e "CONTOSO.COM" como nomes de domínio e o realm de exemplo, respectivamente. Você deve substituí-las com seus próprios valores. Esses comandos diferenciam maiusculas de minúsculas, portanto, verifique se que você usar letras maiusculas independentemente de onde ele é usado neste passo a passo.

1. Configurar seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computador host para usar o endereço IP do controlador de domínio do AD como um servidor de nomes DNS. 

   - **Ubuntu**:

      Editar o `/etc/network/interfaces` arquivo para que o endereço IP do controlador de domínio do AD está listado como um servidor de nomes do dns. Por exemplo: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auto eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > A interface de rede (eth0) pode ser diferentes para diferentes computadores. Para descobrir qual deles você está usando, execute ifconfig e copie a interface que tem um endereço IP e os bytes transmitidos e recebidos.

      Depois de editar esse arquivo, reinicie o serviço de rede:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:  

      ```/etc/resolv.conf
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     Editar o `/etc/sysconfig/network-scripts/ifcfg-eth0` arquivo (ou outra configuração de interface de arquivos conforme apropriado) para que o endereço IP do controlador de domínio do AD está listado como um servidor DNS:

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     Depois de editar esse arquivo, reinicie o serviço de rede:

     ```bash
     sudo systemctl restart network
     ```

     Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:  

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

   - **SLES**:

     Editar o `/etc/sysconfig/network/config` arquivo para que o IP do controlador de domínio AD será usado para consultas DNS e o seu domínio do AD está na lista de pesquisa de domínio:

     ```/etc/sysconfig/network/config
     <...>
     NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
     ```

     Depois de editar esse arquivo, reinicie o serviço de rede:

     ```bash
     sudo systemctl restart network
     ```

     Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:

     ```/etc/resolv.conf
     nameserver **<AD domain controller IP address>**
     ```

1. Ingressar no domínio

   Depois de confirmar se o DNS está configurado corretamente, ingresse no domínio executando o comando a seguir. Você deve autenticar usando uma conta do AD que tenha privilégios suficientes no Active Directory para associar uma nova máquina ao domínio.

   Especificamente, este comando cria uma nova conta de computador no AD, crie o `/etc/krb5.keytab` hospedar arquivo keytab e configurar o domínio no `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Se você vir um erro, "os pacotes necessários não estão instalados", então você deve instalar esses pacotes usando o Gerenciador de pacotes da distribuição Linux antes de executar o `realm join` comando novamente.
   >
   > Se você receber um erro, "Permissões insuficientes para ingressar no domínio", em seguida, você precisará verificar com um administrador de domínio que você tenha permissões suficientes para ingressar computadores Linux no seu domínio.
   >
   > Se você receber um erro "a resposta do KDC não correspondeu ao expectativas,", em seguida, você talvez não tenha especificado o nome de realm correto para o usuário. Nomes de realm diferenciam maiusculas de minúsculas, geralmente em maiusculas e podem ser identificados com o comando `realm discover contoso.com`.
   
   > SQL Server usa SSSD e o NSS para mapear contas de usuário e grupos para identificadores de segurança (SID). SSSD deve ser configurado e em execução na ordem para o SQL Server criar logons do AD com êxito. Realmd normalmente faz isso automaticamente como parte do ingresso no domínio, mas em alguns casos você deve fazer isso separadamente.
   >
   > Confira o seguinte para configurar [SSSD manualmente](https://access.redhat.com/articles/3023951), e [configurar NSS para trabalhar com o SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)

  
5. Verifique se agora você pode reunir informações sobre um usuário do domínio e que você pode adquirir um tíquete Kerberos como esse usuário.

   O exemplo a seguir usa **identificação**,  **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)**, e **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** comandos para isso.

   ```bash
   id user@contoso.com
   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM
   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   <...>
   ```

   > [!NOTE]
   > Se `id user@contoso.com` retorna, "O usuário não," Certifique-se de que o serviço SSSD iniciado com êxito, executando o comando `sudo systemctl status sssd`. Se o serviço está em execução e você vir o erro "O usuário não", tente habilitar o log detalhado para SSSD. Para obter mais informações, consulte a documentação do Red Hat [solução de problemas SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Se `kinit user@CONTOSO.COM` retorna, "resposta do KDC não correspondeu às expectativas durante a obtenção de credenciais inicias," Verifique se você especificou o realm em letras maiusculas.

Para obter mais informações, consulte a documentação do Red Hat [descobrindo e ingressar em domínios de identidade](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a id="createuser"></a> Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN

  > [!NOTE]
  > A próxima etapas usam sua [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se você estiver usando **Azure**, você deve **[criar um](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. No controlador de domínio, execute as [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando do PowerShell para criar um novo usuário do AD com uma senha que nunca expira. Este exemplo denomina a conta "mssql", mas o nome da conta pode ser qualquer coisa que você deseja. Você será solicitado a inserir uma nova senha para a conta:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > É uma prática recomendada de segurança para ter uma conta dedicada do AD para o SQL Server, para que as credenciais do SQL Server não são compartilhadas com outros serviços usando a mesma conta. No entanto, você pode reutilizar uma conta do AD existente se você preferir, se você souber a senha da conta (necessária para gerar um arquivo keytab na próxima etapa).

2. Definir o SPN (ServicePrincipalName) para esta conta usando o `setspn.exe` ferramenta. O SPN deve ser formatado exatamente conforme especificado no exemplo a seguir. Você pode encontrar o nome de domínio totalmente qualificado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host executando `hostname --all-fqdns` sobre o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host e a porta TCP devem ser 1433, a menos que você configurou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar um número de porta diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se você receber um erro, "direitos de acesso insuficientes", você precisará verificar com um administrador de domínio que você tenha permissões suficientes para definir um SPN nessa conta.
   >
   > Se você alterar a porta TCP no futuro, você precisa executar o comando setspn novamente com o novo número de porta. Você também precisará adicionar o novo o SPN para o SQL Server service keytab, seguindo as etapas na próxima seção.

3. Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab do serviço

1. Verificar o número de versão de chave (kvno) para a conta do AD criada na etapa anterior. Normalmente, é 2, mas pode ser outro inteiro se você tiver alterado a senha da conta várias vezes. Sobre o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host, execute o seguinte:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > Os SPNs podem levar vários minutos para propagar por meio de seu domínio, especialmente se o domínio for grande. Se você receber o erro "kvno: servidor não encontrado no banco de dados do Kerberos ao obter as credenciais para MSSQLSvc /\*\*\<nome de domínio totalmente qualificado do computador host\>\*\*:\* \* \<porta tcp\>\*\*\@CONTOSO.COM ", aguarde alguns minutos e tente novamente.

2. Crie um arquivo keytab com **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)** para o usuário do AD que você criou na etapa anterior. Quando solicitado, insira a senha para essa conta do AD.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > A ferramenta ktutil não validar a senha, portanto, verifique se que você o digitou corretamente.

3. Adicione a conta de computador ao seu keytab com  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. A conta do computador (também chamada de um UPN) está presente no `/etc/krb5.keytab` no formato "\<hostname\>$\@\<realm.com\>" (por exemplo, sqlhost$\@CONTOSO.COM). Podemos copiar essas entradas de `/etc/krb5.keytab` para `mssql.keytab`.

   ```bash
   sudo ktutil

   # Read all entries from /etc/krb5.keytab
   ktutil: rkt /etc/krb5.keytab

   # List all entries
   ktutil: list

   # Delete all entries by their slot number which are not the UPN one at a
   # time.
   # Warning: when an entry is deleted (e.g. slot 1), all values slide up by
   # one to take its place (e.g. the entry in slot 2 moves to slot 1 when slot
   # 1's entry is deleted)
   ktutil: delent <slot num>
   ktutil: delent <slot num>
   ...

   # List all entries to ensure only UPN entries are left
   ktutil: list

   # When only UPN entries are left, append these values to mssql.keytab
   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

4. Qualquer pessoa com acesso a este `keytab` arquivo pode representar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio, portanto, verifique se você restringir o acesso ao arquivo, que apenas o `mssql` conta tem acesso de leitura:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

5. Configure [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usá-lo `keytab` arquivo para a autenticação Kerberos:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

6. Opcional: Desabilitar conexões UDP para o controlador de domínio para melhorar o desempenho. Em muitos casos, as conexões UDP sempre irá falhar ao se conectar a um controlador de domínio, portanto, você pode definir opções de configuração no `/etc/krb5.conf` para ignorar chamadas UDP. Editar `/etc/krb5.conf` e defina as seguintes opções:

   ```/etc/krb5.conf
   [libdefaults]
   udp_preference_limit=0
   ```

## <a id="createsqllogins"></a> Criar logons do AD baseada em Transact-SQL

1. Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e crie um logon novo, baseado no AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Verifique se que o logon agora está listado na [sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição de catálogo do sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

Faça logon em um computador cliente usando suas credenciais de domínio. Agora você pode se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sem precisar reinserir a senha, usando a autenticação do AD. Se você criar um logon para um grupo do AD, qualquer usuário do AD que é um membro desse grupo pode conectar-se da mesma maneira.

O parâmetro de cadeia de caracteres de conexão específicas para os clientes usarem a autenticação do AD depende de qual driver você está usando. Considere os seguintes exemplos:

* `sqlcmd` em um cliente de Linux ingressado no domínio

   Faça logon em um cliente do Linux ingressado no domínio usando `ssh` e suas credenciais de domínio:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Verifique se você instalou o [mssql-tools](sql-server-linux-setup-tools.md) do pacote, em seguida, conecte-se usando `sqlcmd` sem especificar quaisquer credenciais:

   ```bash
   sqlcmd -S mssql-host.contoso.com
   ```

* SSMS em um cliente do Windows ingressados no domínio

   Faça logon em um cliente de Windows ingressados no domínio usando suas credenciais de domínio. Certifique-se [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] está instalado e, em seguida, se conectar ao seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância (por exemplo, "mssql-host.contoso.com"), especificando **autenticação do Windows** no **conectar ao servidor** caixa de diálogo.

* Autenticação do AD usando outros drivers de cliente

  * JDBC: [usando o Kerberos de autenticação para conectar-se o SQL Server integrada](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [usando a autenticação integrada](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [sintaxe da cadeia de Conexão](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)

## <a name="performance-improvements"></a>Melhorias no desempenho
Se você notar que pesquisas de conta do AD estão demorando um pouco, e você verificou a configuração do AD é válida com as etapas em [uso de autenticação do Active Directory com o SQL Server no Linux por meio de provedores de AD de terceiros](sql-server-linux-active-directory-third-party-providers.md), você pode adicionar o linhas abaixo para `/var/opt/mssql/mssql.conf` ignorar chamadas SSSD e usar diretamente as chamadas de LDAP.

```/var/opt/mssql/mssql.conf
[network]
disablesssd = true
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, percorremos como configurar a autenticação do Active Directory com o SQL Server no Linux. Você aprendeu como para:
> [!div class="checklist"]
> * Junte-se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab do serviço
> * Criar logons do AD baseada em Transact-SQL
> * Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

Em seguida, explore outros cenários de segurança para o SQL Server no Linux.

> [!div class="nextstepaction"]
>[Criptografar conexões ao SQL Server no Linux](sql-server-linux-encrypted-connections.md)
