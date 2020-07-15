---
title: Conectar seu SQL Server usando a autenticação do Windows (Kerberos)
description: Saiba como habilitar o Kerberos a usar a Autenticação do Active Directory no Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.topic: conceptual
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c2e6b303217d420d439d510fc3fc24886657684b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774665"
---
# <a name="connect-azure-data-studio-to-your-sql-server-using-windows-authentication---kerberos"></a>Conectar o Azure Data Studio ao SQL Server usando a autenticação do Windows – Kerberos

O Azure Data Studio dá suporte à conexão com o SQL Server usando o Kerberos.

Para usar a autenticação integrada (autenticação do Windows) no macOS ou no Linux, você precisará configurar um **tíquete do Kerberos** vinculando o usuário atual a uma conta de domínio do Windows.

## <a name="prerequisites"></a>Pré-requisitos

- Acesso a um computador ingressado no domínio do Windows para consultar o controlador de domínio do Kerberos.
- O SQL Server deve ser configurado para permitir a autenticação Kerberos. Para o driver de cliente em execução no UNIX, só há suporte para a autenticação integrada com o uso do Kerberos. Para obter mais informações, veja [Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). Deve haver SPNs registrados para cada instância do SQL Server à qual você está tentando se conectar. Para obter mais informações, confira [Registrar um Nome da Entidade de Serviço](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats).


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Como verificar se o SQL Server tem a Configuração Kerberos

Faça logon no computador host do SQL Server. No prompt de comando do Windows, use o `setspn -L %COMPUTERNAME%` para listar todos os nomes da entidade de serviço para o host. Você deverá ver entradas que começam com MSSQLSvc/HostName.Domain.com, o que significa que o SQL Server registrou um SPN e está pronto para aceitar a autenticação Kerberos. 
- Se você não tiver acesso ao host do SQL Server, em qualquer outro sistema operacional Windows ingressado no mesmo Active Directory, você poderá usar o comando, `setspn -L <SQLSERVER_NETBIOS>` em que <SQLSERVER_NETBIOS> é o nome do computador do host do SQL Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obter o centro de distribuição de chaves Kerberos

Localize o valor de configuração do KDC (centro de distribuição de chaves) do Kerberos. Execute o seguinte comando em um computador Windows que esteja ingressado em seu Domínio do Active Directory: 

Inicie `cmd.exe` e execute `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie o nome do controlador de domínio que é o valor de configuração do KDC necessário, nesse caso, dc-33.domain.company.com

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Ingressar o sistema operacional no controlador de domínio do Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Edite o arquivo `/etc/network/interfaces` para que o endereço IP do controlador de domínio do AD esteja listado como um dns-nameserver. Por exemplo: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> O adaptador de rede (eth0) pode ser diferente para computadores diferentes. Para descobrir qual deles você está usando, execute ifconfig e copie a interface que tem um endereço IP e os bytes transmitidos e recebidos.

Após editar esse arquivo, reinicie o serviço de rede:

```bash
sudo ifdown eth0 && sudo ifup eth0
```

Agora, verifique se o arquivo `/etc/resolv.conf` contém uma linha semelhante à seguinte:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>Red Hat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

Edite o arquivo `/etc/sysconfig/network-scripts/ifcfg-eth0` (ou outro arquivo de configuração de interface, conforme apropriado), de modo que o endereço IP do controlador de domínio do AD seja listado como um servidor DNS:

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

Após editar esse arquivo, reinicie o serviço de rede:

```bash
sudo systemctl restart network
```

Agora, verifique se o arquivo `/etc/resolv.conf` contém uma linha semelhante à seguinte:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Ingresse o macOS no controlador de domínio do Active Directory seguindo estas etapas:



## <a name="configure-kdc-in-krb5conf"></a>Configure o KDC em krb5.conf

Edite o `/etc/krb5.conf` em um editor de sua escolha. Configure as seguintes chaves

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Em seguida, salve o arquivo krb5.conf e saia

> [!NOTE]
> O domínio precisa estar em MAIÚSCULAS


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Teste a recuperação do Tíquete de Concessão de Tíquete

Obtenha um TGT (Tíquete de Concessão de Tíquete) do KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Exiba os tíquetes disponíveis usando klist. Se o kinit for bem-sucedido, você deverá ver um tíquete. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-azure-data-studio"></a>Conectar usando o Azure Data Studio

* Crie um perfil de conexão

* Escolha **Autenticação do Windows** como o tipo de autenticação

* Conclua o perfil de conexão e clique em **Conectar**

Depois que você se conectar com êxito, o servidor será exibido na barra lateral *Servidores*.
