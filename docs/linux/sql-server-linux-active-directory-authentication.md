---
title: "Autenticação do Active Directory com o SQL Server no Linux | Microsoft Docs"
description: "Este tutorial fornece as etapas de configuração para a autenticação do AAD para o SQL Server no Linux."
author: meet-bhagdev
ms.date: 10/09/2017
ms.author: meetb
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 09a837b606b0fad62c77db982000cf3d7dc5c48f
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="active-directory-authentication-with-sql-server-on-linux"></a>Autenticação do Active Directory com o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tutorial explica como configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para oferecer suporte à autenticação do Active Directory (AD), também conhecido como a autenticação. Autenticação do AD permite que os clientes de domínio no Windows ou Linux para autenticar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando suas credenciais de domínio e o protocolo Kerberos.

Autenticação do AD tem as seguintes vantagens sobre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticação:

* Os usuários autenticados por meio de logon único, sem precisar inserir uma senha.   
* Ao criar logons para grupos do AD, você pode gerenciar o acesso e permissões em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando associações de grupo do AD.  
* Cada usuário tem uma única identidade na sua organização, para que você não precisa manter o controle de qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] logons correspondem às quais pessoas.   
* AD permite que você aplique uma política de senha centralizado na sua organização.   

Neste tutorial consiste das seguintes tarefas:

> [!div class="checklist"]
> * Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de serviço
> * Criar logons baseado no AD no Transact-SQL
> * Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

## <a name="prerequisites"></a>Pré-requisitos

Antes de configurar a autenticação do AD, você precisa:

* Configurar um controlador de domínio do AD (Windows) em sua rede  
* Instalar o[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

> [!IMPORTANT]
> Limitações:
> - Neste momento, o único método de autenticação com suporte para o ponto de extremidade de espelhamento de banco de dados é o certificado. Método de autenticação do WINDOWS será habilitado em uma versão futura.
> - Não há suporte para ferramentas de terceiros AD 3º como Centrify, Powerbroker e Vintela 

## <a name="join-includessnoversionincludesssnoversion-mdmd-host-to-ad-domain"></a>Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD

Use as seguintes etapas para adicionar um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host a um domínio do Active Directory:

1. Use  **[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.html)**  para unir sua máquina host para seu domínio do AD. Se você ainda não fez isso, instale os pacotes de cliente Kerberos e realmd no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina de host usando o Gerenciador de pacotes de distribuição Linux:

   ```bash
   # RHEL
   sudo yum install realmd krb5-workstation

   # SUSE
   sudo zypper install realmd krb5-client

   # Ubuntu
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Se a instalação do pacote de cliente Kerberos solicita um nome de território, insira seu nome de domínio em letras maiusculas.

   > [!NOTE]
   > Este passo a passo usa "contoso.com" e "CONTOSO.COM" como nomes de domínio e o realm de exemplo, respectivamente. Você deve substituí-las com seus próprios valores. Esses comandos diferenciam maiusculas de minúsculas, portanto certifique-se de que usar maiusculas sempre que ele é usado neste passo a passo.

1. Configurar seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina de host para usar o endereço IP do controlador de domínio AD como um servidor de nomes DNS. 

   - **Ubuntu**:

      Editar o `/etc/network/interfaces` arquivos de forma que o endereço IP do controlador de domínio AD está listado como um servidor de nomes do dns. Por exemplo: 

      ```/etc/network/interfaces
      <...>
      # The primary network interface
      auth eth0
      iface eth0 inet dhcp
      dns-nameservers **<AD domain controller IP address>**
      dns-search **<AD domain name>**
      ```

      > [!NOTE]
      > A interface de rede (eth0) pode ser diferentes para differnet máquinas. Para descobrir qual deles você está usando, execute ifconfig e copie a interface que tem um endereço IP e bytes transmitidos e recebidos.

      Depois de editar esse arquivo, reinicie o serviço de rede:

      ```bash
      sudo ifdown eth0 && sudo ifup eth0
      ```

      Verifique se agora o `/etc/resolv.conf` arquivo contém uma linha semelhante à seguinte:  

      ```Code
      nameserver **<AD domain controller IP address>**
      ```

   - **RHEL**:

     Editar o `/etc/sysconfig/network-scripts/ifcfg-eth0` arquivo (ou outra configuração de interface de arquivos conforme apropriado) para que o endereço IP do controlador de domínio AD está listado como um servidor DNS:

     ```/etc/sysconfig/network-scripts/ifcfg-eth0
     <...>
     PEERDNS=no
     DNS1=**<AD domain controller IP address>**
     ```

     Depois de editar esse arquivo, reinicie o serviço de rede:

     ```bash
     sudo systemctl restart network
     ```

     Verifique se agora o `/etc/resolv.conf` arquivo contém uma linha semelhante à seguinte:  

     ```Code
     nameserver **<AD domain controller IP address>**
     ```

1. Ingressar no domínio

   Depois de confirmar que o DNS está configurado corretamente, ingresse no domínio executando o comando a seguir. Você precisará autenticar usando uma conta que tenha privilégios suficientes no AD para associar uma nova máquina ao domínio do AD.

   Especificamente, este comando será criar uma nova conta de computador no AD, crie o `/etc/krb5.keytab` arquivo keytab de host e configurar o domínio no `/etc/sssd/sssd.conf`:

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   <...>
   * Successfully enrolled machine in realm
   ```

   > [!NOTE]
   > Se você vir um erro, "pacotes necessários não estão instalados", você deve instalar esses pacotes usando o Gerenciador de pacotes de distribuição Linux antes de executar o `realm join` comando novamente.
   >
   > Se você receber um erro, "Permissões insuficientes para ingressar no domínio", em seguida, você precisará verificar com um administrador de domínio que você tem permissões suficientes para adicionar máquinas Linux ao domínio.

1. Verifique se que você agora pode reunir informações sobre um usuário do domínio e que você pode adquirir um tíquete Kerberos como esse usuário.

   We will use **id**, **[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)** and **[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)** commands for this.

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
   > Se `id user@contoso.com` retorna, "Usuário não existe," Certifique-se de que o serviço SSSD iniciado com êxito, executando o comando `sudo systemctl status sssd`. Se o serviço está em execução e ainda receber o erro "Usuário não existe", tente habilitar o log detalhado para SSSD. Para obter mais informações, consulte a documentação do Red Hat para [SSSD de solução de problemas](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > Se `kinit user@CONTOSO.COM` retorna, "resposta do KDC não correspondeu às expectativas ao obter credenciais inicias," Verifique se você especificou o realm em letras maiusculas.

Para obter mais informações, consulte a documentação do Red Hat para [descobrindo e ingressar em domínios de identidade](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html). 

## <a name="create-ad-user-for-includessnoversionincludesssnoversion-mdmd-and-set-spn"></a>Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN

  > [!NOTE]
  > As próximas etapas, nós usaremos seu [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se você estiver usando **Azure**, você terá que  **[criar um](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/portal-create-fqdn)**  antes de continuar.

1. No controlador de domínio, execute o [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando do PowerShell para criar um novo usuário do AD com uma senha que nunca expira. Este exemplo denomina a conta "mssql", mas o nome da conta pode ser qualquer coisa que você deseja. Você será solicitado a inserir uma nova senha para a conta:

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > É uma prática recomendada de segurança para ter uma conta dedicada do AD para o SQL Server, para que as credenciais do SQL Server não são compartilhadas com outros serviços usando a mesma conta. No entanto, você pode reutilizar uma conta existente do AD se preferir, se você souber a senha da conta (necessária para gerar um arquivo keytab na próxima etapa).

2. Definir o ServicePrincipalName (SPN) para esta conta usando o `setspn.exe` ferramenta. O SPN deve ser formatado exatamente conforme especificado no exemplo a seguir: você pode encontrar o nome de domínio totalmente qualificado de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host executando `hostname --all-fqdns` no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host e a porta TCP devem ser 1433, a menos que você configurou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar um número de porta diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se você receber um erro, "direitos de acesso insuficientes", em seguida, você precisa verificar com um administrador de domínio que você tem permissões suficientes para definir um SPN nessa conta.
   >
   > Se você alterar a porta TCP no futuro, você precisará executar o comando setspn novamente com o novo número de porta. Você também precisará adicionar o novo SPN para o SQL Server service keytab seguindo as etapas na próxima seção.

3. Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a name="configure-includessnoversionincludesssnoversion-mdmd-service-keytab"></a>Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de serviço

1. Verificar o número de versão de chave (kvno) para a conta de AD criado na etapa anterior. Geralmente é 2, mas pode ser outro inteiro se você tiver alterado a senha da conta várias vezes. Sobre o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina de host, execute o seguinte:

   ```bash
   kinit user@CONTOSO.COM

   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

2. Crie um arquivo keytab para o usuário do AD que você criou na etapa anterior. Para fazer isso, usamos o  **[ktutil](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/ktutil.html)**. Quando solicitado, insira a senha para essa conta do AD.

   ```bash
   sudo ktutil

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96

   ktutil: addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac

   ktutil: wkt /var/opt/mssql/secrets/mssql.keytab

   quit
   ```

   > [!NOTE]
   > A ferramenta ktutil não validar a senha, portanto, verifique se que digitou corretamente.

3. Qualquer pessoa com acesso a esse `keytab` representar o arquivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no domínio, portanto, verifique se você restringir o acesso a esse arquivo que somente o `mssql` conta tem acesso de leitura:

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
   sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
   ```

4. Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usá-lo `keytab` arquivo para a autenticação Kerberos:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
   sudo systemctl restart mssql-server
   ```

## <a name="create-ad-based-logins-in-transact-sql"></a>Criar logons baseado no AD no Transact-SQL

1. Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e crie um logon de novo, baseado no AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

2. Verificar se o logon está agora listado no [sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição de catálogo do sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a name="connect-to-includessnoversionincludesssnoversion-mdmd-using-ad-authentication"></a>Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

Faça logon um computador cliente usando suas credenciais de domínio. Agora você pode se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sem precisar reinserir a senha, usando a autenticação do AD. Se você criar um logon para um grupo do AD, qualquer usuário do AD que seja membro desse grupo pode se conectar da mesma maneira.

O parâmetro de cadeia de caracteres de conexão específicas para os clientes usarem a autenticação do AD depende de qual driver você está usando. A seguir estão alguns exemplos.

* `sqlcmd`em um cliente Linux ingressado no domínio

   Faça logon um cliente do Linux de domínio usando `ssh` e suas credenciais de domínio:

   ```bash
   ssh -l user@contoso.com client.contoso.com
   ```

   Verifique se você instalou o [mssql ferramentas](sql-server-linux-setup-tools.md) do pacote, em seguida, conecte-se usando `sqlcmd` sem especificar quaisquer credenciais:

   ```bash
   sqlcmd -S mssql.contoso.com
   ```

* SSMS em um cliente do Windows ingressado no domínio

   Faça logon um cliente do Windows ingressado no domínio usando suas credenciais de domínio. Certifique-se de [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] está instalado e se conectar ao seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância especificando **autenticação do Windows** no **conectar ao servidor** caixa de diálogo.

* Usando outros drivers de cliente de autenticação do AD

  * JDBC: [usando Kerberos integrada a autenticação para conexão do SQL Server](https://docs.microsoft.com/sql/connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server)
  * ODBC: [usando a autenticação integrada](https://docs.microsoft.com/sql/connect/odbc/linux/using-integrated-authentication)
  * ADO.NET: [sintaxe de cadeia de caracteres de Conexão](https://msdn.microsoft.com/library/system.data.sqlclient.sqlauthenticationmethod(v=vs.110).aspx)
  
## <a name="next-steps"></a>Próximas etapas

Neste tutorial, percorremos como configurar a autenticação do Active Directory com o SQL Server no Linux. Você aprendeu como para:
> [!div class="checklist"]
> * Unir [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab de serviço
> * Criar logons baseado no AD no Transact-SQL
> * Conecte-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

Em seguida, explore a outros cenários de segurança para o SQL Server no Linux.

> [!div class="nextstepaction"]
>[Criptografar conexões ao SQL Server no Linux](sql-server-linux-encrypted-connections.md)

