---
title: 'Tutorial: Usar a autenticação do AD para o SQL Server no Linux'
titleSuffix: SQL Server
description: Este tutorial fornece as etapas de configuração para a autenticação do AD para o SQL Server no Linux.
author: Dylan-MSFT
ms.author: Dylan.Gray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 3ab6fd05b0cf9486ded5b0e550101a374669be11
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097235"
---
# <a name="tutorial-use-active-directory-authentication-with-sql-server-on-linux"></a>Tutorial: Usar autenticação do Active Directory com o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial explica como configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para dar suporte à autenticação do Active Directory (AD), a autenticação integrada também conhecido como. Para obter uma visão geral, consulte [autenticação do Active Directory para o SQL Server no Linux](sql-server-linux-active-directory-auth-overview.md).

Neste tutorial consiste as seguintes tarefas:

> [!div class="checklist"]
> * Junte-se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD
> * Criar usuário do AD para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN
> * Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab do serviço
> * Proteger o arquivo keytab
> * Configurar o SQL Server para usar o arquivo keytab para a autenticação Kerberos
> * Criar logons do AD baseada em Transact-SQL
> * Conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a autenticação do AD

## <a name="prerequisites"></a>Prerequisites

Antes de configurar a autenticação do AD, você precisa:

* Configurar um controlador de domínio do AD (Windows) em sua rede  
* Instalar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
  * [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
  * [SUSE Linux Enterprise Server (SLES)](quickstart-install-connect-suse.md)
  * [Ubuntu](quickstart-install-connect-ubuntu.md)

## <a id="join"></a> Junte-se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host ao domínio do AD

Você deve associar seu host do SQL Server Linux com um controlador de domínio do Active Directory. Para obter informações sobre como ingressar em um domínio do Active Directory, consulte [junção SQL Server em um host Linux em um domínio do Active Directory](sql-server-linux-active-directory-join-domain.md).

## <a id="createuser"></a> Criar usuário do AD (ou MSA) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e definir o SPN

> [!NOTE]
> As seguintes etapas usam sua [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name). Se você estiver usando **Azure**, você deve **[criar um](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn)** antes de continuar.

1. No controlador de domínio, execute as [New-ADUser](https://technet.microsoft.com/library/ee617253.aspx) comando do PowerShell para criar um novo usuário do AD com uma senha que nunca expira. O exemplo a seguir nomes de conta `mssql`, mas o nome da conta pode ser qualquer coisa que você deseja. Você será solicitado a inserir uma nova senha para a conta.

   ```PowerShell
   Import-Module ActiveDirectory

   New-ADUser mssql -AccountPassword (Read-Host -AsSecureString "Enter Password") -PasswordNeverExpires $true -Enabled $true
   ```

   > [!NOTE]
   > É uma prática recomendada de segurança para ter uma conta dedicada do AD para o SQL Server, para que as credenciais do SQL Server não são compartilhadas com outros serviços usando a mesma conta. No entanto, você pode reutilizar uma conta existente do AD, opcionalmente, se você souber a senha da conta (o que é necessário para gerar um arquivo keytab na próxima etapa).

2. Definir o SPN (ServicePrincipalName) para esta conta usando o **setspn.exe** ferramenta. O SPN deve ser formatado exatamente conforme especificado no exemplo a seguir. Você pode encontrar o nome de domínio totalmente qualificado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] máquina host executando `hostname --all-fqdns` sobre o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] host. A porta TCP deve ser 1433, a menos que você configurou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar um número de porta diferente.

   ```PowerShell
   setspn -A MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>** mssql
   setspn -A MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>** mssql
   ```

   > [!NOTE]
   > Se você receber um erro, `Insufficient access rights`, verifique com seu administrador de domínio que você tenha permissões suficientes para definir um SPN nessa conta.
   >
   > Se você alterar a porta TCP no futuro, você deve executar o **setspn** comando novamente com o novo número de porta. Você também precisará adicionar o novo o SPN para o SQL Server service keytab, seguindo as etapas na próxima seção.

Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).

## <a id="configurekeytab"></a> Configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] keytab do serviço

Há duas maneiras diferentes para configurar arquivos keytab de serviço do SQL Server. A primeira opção é usar uma conta de computador (UPN), enquanto a segunda opção usa uma conta de serviço gerenciado (MSA) na configuração keytab. Ambos os mecanismos são igualmente funcionais, e você pode escolher o método que funciona melhor para seu ambiente.

Em ambos os casos, o SPN criado na etapa anterior é necessário e o SPN deve ser registrado no keytab.

Para configurar o arquivo keytab de serviço do SQL Server:

1. Configurar o [entradas do SPN keytab](#spn) na próxima seção.

1. Em seguida, ambos [adicionar UPN](#upn) (opção 1) ou [MSA](#msa) entradas (opção 2) no arquivo keytab, seguindo as etapas em suas respectivas seções.

> [!IMPORTANT]
> Se a senha para o UPN/MSA for alterada ou a senha da conta de que os SPNs são atribuídos a é alterada, você deve atualizar o keytab com a nova senha e o número de versão da chave (KVNO). Alguns serviços podem também Girar automaticamente as senhas. Examine a qualquer política de rotação de senha para as contas em questão e alinhá-los com atividades de manutenção agendada para evitar tempo de inatividade inesperado.

### <a id="spn"></a> Entradas de keytab SPN

1. Verifique o número de versão de chave (KVNO) para a conta do AD criada na etapa anterior. Normalmente, é 2, mas pode ser outro inteiro se você tiver alterado a senha da conta várias vezes. No computador host do SQL Server, execute os seguintes comandos:

   ```bash
   kinit user@CONTOSO.COM
   kvno MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**
   ```

   > [!NOTE]
   > Os SPNs podem levar vários minutos para propagar por meio de seu domínio, especialmente se o domínio for grande. Se você receber o erro `kvno: Server not found in Kerberos database while getting credentials for MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM`, aguarde alguns minutos e tente novamente.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Adicione entradas de keytab para cada SPN usando os seguintes comandos:

   ```bash
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<fully qualified domain name of host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e aes256-cts-hmac-sha1-96
   addent -password -p MSSQLSvc/**<netbios name of the host machine>**:**<tcp port>**@CONTOSO.COM -k **<kvno from above>** -e rc4-hmac
   ```

1. Escreva o keytab para um arquivo e, em seguida, feche o ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

   > [!NOTE]
   > O **ktutil** ferramenta não valida a senha, portanto, verifique se digitou corretamente quando for solicitado.

### <a id="upn"></a> Opção 1: Usando o UPN para configurar o keytab

Adicione a conta de computador ao seu keytab com **ktutil**. A conta do computador (também chamada de um UPN) está presente no **/etc/krb5.keytab** no formulário `<hostname>$@<realm.com>` (por exemplo, `sqlhost$@CONTOSO.COM`). Copiar essas entradas de **/etc/krb5.keytab** à **mssql.keytab**.

1. Inicie **ktuil** com o seguinte comando:

   ```bash
   sudo ktutil
   ```

1. Use o **rkt** comando para ler todas as entradas de **/etc/krb5.keytab**.

   ```bash
   rkt /etc/krb5.keytab
   ```

1. Em seguida, liste as entradas.

   ```bash
   list
   ```

1. Exclua todas as entradas por seus números de slot que não são o UPN. Faça um de cada vez, repetindo o seguinte comando:

   ```bash
   delent <slot num>
   ```

   > [!IMPORTANT]
   > Quando uma entrada é excluída, como o slot 1, todos os slides de valores para cima um para assumir seu lugar. Isso significa que a entrada no slot 2 move para o slot 1 ao slot da 1 entrada é excluída.

1. Listar as entradas novamente até que restam apenas entradas UPN.

   ```bash
   list
   ```

1. Quando forem deixadas apenas entradas UPN, acrescentar esses valores para **mssql.keytab**:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   ```

1. Encerre **ktutil**.

   ```bash
   quit
   ```

### <a id="msa"></a> Opção 2:  Usar MSA para configurar o keytab

Para a opção de MSA, você deve criar keytab do Kerberos do SQL Server. Ela deve conter todos os [SPNs registrados na primeira etapa](#spn) e as credenciais para a MSA para que os SPNs estiverem registrados. 

1. Após o SPN keytab entradas são criadas, execute os comandos a seguir em uma máquina Linux que está ingressado no domínio:

   ```bash
   kinit <AD user>
   kvno <any SPN registered in step 1>
      <spn>@CONTOSO.COM: kvno = <KVNO>
   ```

   Esta etapa exibe o KVNO para a conta de usuário atribuída a propriedade SPN. Para esta etapa funcione, o SPN deve atribuído à conta MSA durante sua criação. Se o SPN não foi atribuído a MSA, o KVNO exibido será da conta de proprietário SPN atual e estar incorreto a ser usado para configuração.  

1. Inicie **ktutil**:

   ```bash
   sudo ktutil
   ```

1. Adicione o MSA com os dois comandos a seguir:

   ```bash
   addent -password -p <MSA> -k <kvno from command above> -e aes256-cts-hmac-sha1-96
   addent -password -p <MSA> -k <kvno from command above> -e rc4-hmac
   ```

1. Escreva o keytab para um arquivo e, em seguida, feche o ktutil:

   ```bash
   wkt /var/opt/mssql/secrets/mssql.keytab
   quit
   ```

1. Ao usar a abordagem do MSA, uma opção de configuração precisa ser definido com o **mssql-conf** ferramenta para especificar a MSA a ser usado ao acessar o arquivo keytab. Verifique se os valores a seguir estão na **/var/opt/mssql/mssql.conf**.

   ```bash
   sudo mssql-conf set network.privilegedadaccount <MSA_Name>
   ```

   > [!NOTE]
   > Inclua somente o nome do MSA e não o nome de domínio \ conta.

## <a id="securekeytab"></a> Proteger o arquivo keytab

Qualquer pessoa com acesso a este arquivo keytab pode representar o SQL Server no domínio, portanto, verifique se que você restringir o acesso ao arquivo, de modo que somente a conta de mssql tem acesso de leitura:

```bash
sudo chown mssql:mssql /var/opt/mssql/secrets/mssql.keytab
sudo chmod 400 /var/opt/mssql/secrets/mssql.keytab
```

## <a id="keytabkerberos"></a> Configurar o SQL Server para usar o arquivo keytab para a autenticação Kerberos

Use as seguintes etapas para configurar o SQL Server para começar a usar o arquivo keytab para a autenticação Kerberos.

```bash
sudo mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
sudo systemctl restart mssql-server
```

Opcionalmente, desabilite conexões UDP para o controlador de domínio para melhorar o desempenho. Em muitos casos, as conexões UDP consistentemente falharem ao se conectar a um controlador de domínio, portanto, você pode definir opções de configuração no **/etc/krb5.conf** para ignorar chamadas UDP. Edite **/etc/krb5.conf** e defina as seguintes opções:

```/etc/krb5.conf
[libdefaults]
udp_preference_limit=0
```

Neste ponto, você está pronto para usar logons do AD com base no SQL Server da seguinte maneira.

## <a id="createsqllogins"></a> Criar logons do AD baseada em Transact-SQL

1. Conectar-se ao SQL Server e crie um logon novo, baseado no AD:

   ```sql
   CREATE LOGIN [CONTOSO\user] FROM WINDOWS;
   ```

1. Verifique se que o logon agora está listado na [sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição de catálogo do sistema:

   ```sql
   SELECT name FROM sys.server_principals;
   ```

## <a id="connect"></a> Conectar-se ao SQL Server usando a autenticação do AD

Faça logon em um computador cliente usando suas credenciais de domínio. Agora você pode se conectar ao SQL Server sem precisar reinserir a sua senha usando a autenticação do AD. Se você criar um logon para um grupo do AD, qualquer usuário do AD que é um membro desse grupo pode conectar-se da mesma maneira.

O parâmetro de cadeia de caracteres de conexão específicas para os clientes usarem a autenticação do AD depende de qual driver você está usando. Considere os exemplos nas seções a seguir.

### <a name="sqlcmd-on-a-domain-joined-linux-client"></a>Sqlcmd em um cliente de Linux ingressado no domínio

Faça logon em um cliente do Linux ingressado no domínio usando **ssh** e suas credenciais de domínio:

```bash
ssh -l user@contoso.com client.contoso.com
```

Verifique se você instalou o [mssql-tools](sql-server-linux-setup-tools.md) do pacote, em seguida, conecte-se usando **sqlcmd** sem especificar quaisquer credenciais:

```bash
sqlcmd -S mssql-host.contoso.com
```

### <a name="ssms-on-a-domain-joined-windows-client"></a>SSMS em um cliente do Windows ingressados no domínio

Faça logon em um cliente de Windows ingressados no domínio usando suas credenciais de domínio. Verifique se o SQL Server Management Studio é instalado e, em seguida, conecte-se à instância do SQL Server (por exemplo, `mssql-host.contoso.com`), especificando **autenticação do Windows** no **conectar ao servidor** caixa de diálogo.

### <a name="ad-authentication-using-other-client-drivers"></a>Autenticação do AD usando outros drivers de cliente

A tabela a seguir descreve as recomendações para outros drivers de cliente:

| Driver de cliente | Recomendação |
|---|---|
| **JDBC** | Use a autenticação integrada Kerberos para conectar o SQL Server. |
| **ODBC** | Use a autenticação integrada. |
| **ADO.NET** | Sintaxe de cadeia de caracteres de Conexão. |

## <a id="additionalconfig"></a> Opções de configuração adicionais

Se você estiver usando os utilitários de terceiros, como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), ou [Centrify](https://www.centrify.com/) para unir o host do Linux para o AD domínio e você gostaria de forçar o SQL server usando o openldap biblioteca diretamente, você pode configurar o **disablesssd** com a opção **mssql-conf** da seguinte maneira:

```bash
sudo mssql-conf set network.disablesssd true
systemctl restart mssql-server
```

> [!NOTE]
> Há utilitários, como **realmd** SSSD, que configura enquanto outras ferramentas, como PBIS, VAS e Centrify não configurar o SSSD. Se o utilitário usado para unir o domínio do AD não faz a configuração do SSSD, é recomendável configurar **disablesssd** opção `true`. Embora não seja necessário como o SQL Server tentará usar SSSD para AD antes de fazer fallback para o mecanismo de openldap, seria mais eficaz para configurá-lo para que o SQL Server faz chamadas de openldap ignorando diretamente o mecanismo do SSSD.

Se seu controlador de domínio oferece suporte a LDAPS, você pode forçar todas as conexões do SQL Server com os controladores de domínio seja por meio de LDAPS. Para verificar o seu cliente pode contatar o controlador de domínio por meio de ldaps, executados o seguinte comando do bash, `ldapsearch -H ldaps://contoso.com:3269`. Para configurar o SQL Server para usar somente o LDAPS, execute o seguinte:

```bash
sudo mssql-conf set network.forcesecureldap true
systemctl restart mssql-server
```

Isso vai usar LDAPS pela SSSD se ingressar no domínio do AD no host foi feito por meio do pacote SSSD e **disablesssd** não está definido como true. Se **disablesssd** é definido como true, juntamente com **forcesecureldap** sendo definida como true, ele usará o protocolo LDAPS pela openldap biblioteca chamadas feitas pelo SQL Server.

### <a name="post-sql-server-2017-cu14"></a>Post SQL Server 2017 CU14

Começando com CU14 de 2017 do SQL Server, se o SQL Server ingressou em um controlador de domínio do AD usando provedores de terceiros e é configurado para usar openldap chamadas para pesquisa geral do AD, definindo **disablesssd** para true, você também pode usar **enablekdcfromkrb5** opção para forçar o SQL Server para usar a biblioteca krb5 para pesquisa KDC em vez de pesquisa inversa de DNS para o servidor do KDC.

Isso pode ser útil para o cenário em que você deseja configurar manualmente os controladores de domínio do SQL Server tenta se comunicar com. E você usar o mecanismo de biblioteca openldap usando a lista do KDC no **krb5**.

Primeiro, defina **disablessd** e **enablekdcfromkrb5conf** como true e, em seguida, reinicie o SQL Server:

```bash
sudo mssql-conf set network.disablesssd true
sudo mssql-conf set network.enablekdcfromkrb5conf true
systemctl restart mssql-server
```

Em seguida, configure a lista do KDC no **/etc/krb5.conf** da seguinte maneira:

```/etc/krb5.conf
[realms]
CONTOSO.COM = {
  kdc = dcWithGC1.contoso.com
  kdc = dcWithGC2.contoso.com
}
```

> [!NOTE]
> Embora não seja recomendado, é possível usar os utilitários, como **realmd**, que configurou SSSD ao unir o host do Linux ao domínio, ao configurar **disablesssd** como true para que o SQL Server usa chamadas OpenLDAP em vez disso, do SSSD para o Active Directory chamadas relacionadas.

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
