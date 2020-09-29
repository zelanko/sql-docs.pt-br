---
title: Conectar sua instância do SQL Server usando a autenticação do Windows (Kerberos)
description: Saiba como conectar o Azure Data Studio à sua instância do SQL Server usando a autenticação integrada do Microsoft Kerberos.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 7acc55d55afc3d994230a529243c26d5e1a626be
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364103"
---
# <a name="connect-azure-data-studio-to-sql-server-using-windows-authentication---kerberos"></a>Conectar o Azure Data Studio ao SQL Server usando a autenticação do Windows – Kerberos

O Azure Data Studio dá suporte à conexão com o SQL Server usando o Kerberos.

Para usar a autenticação integrada (Autenticação do Windows) no macOS ou no Linux, você precisa configurar um *tíquete do Kerberos* que vincule o usuário atual a uma conta de domínio do Windows.

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisa do seguinte:

- Acesso a um computador ingressado no domínio do Windows para consultar o controlador de domínio do Kerberos.
- O SQL Server deve ser configurado para permitir a autenticação Kerberos. Para o driver de cliente em execução no Unix, só há suporte para a autenticação integrada com o uso do Kerberos. Para obter mais informações, veja [Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). Deve haver SPNs (nomes da entidade de serviço) registrados para cada instância do SQL Server à qual você está tentando se conectar. Para obter mais informações, confira [Registrar um nome da entidade de serviço](/previous-versions/sql/sql-server-2008-r2/ms191153(v=sql.105)#SPN%20Formats).


## <a name="check-if-sql-server-has-a-kerberos-setup"></a>Verificar se o SQL Server tem uma configuração Kerberos

Entre no computador host do SQL Server. No prompt de comando do Windows, use `setspn -L %COMPUTERNAME%` para listar todos os SPNs do host. Você deverá ver entradas que começam com MSSQLSvc/HostName.Domain.com, o que significa que o SQL Server registrou um SPN e está pronto para aceitar a autenticação Kerberos.

Se você não tiver acesso ao host da instância do SQL Server, poderá usar o comando `setspn -L <SQLSERVER_NETBIOS>`, em que *<SQLSERVER_NETBIOS>* é o nome do computador do host da instância do SQL Server, em qualquer outro sistema operacional Windows ingressado no mesmo Active Directory.


## <a name="get-the-kerberos-key-distribution-center"></a>Obter o centro de distribuição de chaves Kerberos

Localize o valor de configuração do KDC (Centro de Distribuição de Chaves) do Kerberos. Execute o comando a seguir em um computador Windows que esteja ingressado em seu domínio do Active Directory.

Inicie `cmd.exe` e execute `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie o nome do controlador de domínio que é o valor de configuração do KDC necessário. Nesse caso, é dc-33.domain.company.com.

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Ingressar o sistema operacional no controlador de domínio do Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Edite o arquivo `/etc/network/interfaces` para que o endereço IP do controlador de domínio do Active Directory esteja listado como um dns-nameserver. Por exemplo:

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

Agora, verifique se seu arquivo `/etc/resolv.conf` contém uma linha semelhante à seguinte:

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

Edite o arquivo `/etc/sysconfig/network-scripts/ifcfg-eth0` (ou outro arquivo de configuração de interface, conforme apropriado), de modo que o endereço IP do controlador de domínio do Active Directory seja listado como um servidor DNS:

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

Após editar esse arquivo, reinicie o serviço de rede:

```bash
sudo systemctl restart network
```

Agora, verifique se seu arquivo `/etc/resolv.conf` contém uma linha semelhante à seguinte:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

Ingresse o macOS no controlador de domínio do Active Directory seguindo estas etapas.

## <a name="configure-kdc-in-krb5conf"></a>Configure o KDC em krb5.conf

Edite o arquivo `/etc/krb5.conf` em um editor de sua escolha. Configure as seguintes chaves:

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Em seguida, salve o arquivo krb5.conf e saia.

> [!NOTE]
> O domínio precisa estar em MAIÚSCULAS.


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

## <a name="connect-by-using-azure-data-studio"></a>Conectar-se usando o Azure Data Studio

1. Crie um perfil de conexão.

1. Selecione **Autenticação do Windows** como o tipo de autenticação.

1. Conclua o perfil de conexão e selecione **Conectar**.

Depois que você se conectar com êxito, o servidor será exibido na barra lateral **SERVIDORES**.
