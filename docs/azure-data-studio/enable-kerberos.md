---
title: Usar a autenticação do Active Directory (Kerberos)
titleSuffix: Azure Data Studio
description: Saiba como habilitar o Kerberos para usar autenticação do Active Directory para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
ms.openlocfilehash: 5c8fae6bf1333742b40e9c8aae4ee575736058cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959661"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Conectar-se [!INCLUDE[name-sos](../includes/name-sos-short.md)] ao SQL Server usando a autenticação do Windows - Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] oferece suporte à conexão ao SQL Server usando o Kerberos.

Para usar a autenticação integrada (autenticação do Windows) no macOS ou Linux, você precisa configurar uma **tíquete Kerberos** vinculando seu usuário atual para uma conta de domínio do Windows. 

## <a name="prerequisites"></a>Prerequisites

- Acesso a um computador ingressado no domínio do Windows para uma consulta seu controlador de domínio do Kerberos.
- SQL Server deve ser configurado para permitir a autenticação Kerberos. Para o driver de cliente em execução em Unix, a autenticação integrada tem suporte apenas usando o Kerberos. Para obter mais informações sobre como configurar o Sql Server para se autenticar usando Kerberos podem ser encontradas [aqui](https://support.microsoft.com/help/319723/how-to-use-kerberos-authentication-in-sql-server). Deve haver SPNs registrados para cada instância do Sql Server que você está tentando se conectar ao. Detalhes sobre o formato de SPNs do SQL Server estão listados [aqui](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Verificando se o Sql Server tem a instalação do Kerberos

Faça logon no computador host do Sql Server. No Prompt de comando do Windows, use o `setspn -L %COMPUTERNAME%` para listar todos os nomes de entidade de serviço para o host. Você deve ver as entradas que começam com MSSQLSvc/HostName.Domain.com que significa que o Sql Server tiver registrado um SPN e está pronto para aceitar a autenticação Kerberos. 
- Se você não tiver acesso ao Host do Sql Server, de qualquer outro Windows SO ingressado no mesmo Active Directory, você pode usar o comando `setspn -L <SQLSERVER_NETBIOS>` onde < SQLSERVER_NETBIOS > é o nome do computador do host do Sql Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obter o Kerberos Key Distribution Center

Localize o valor de configuração do Kerberos KDC (Centro de distribuição de chaves). Execute o seguinte comando em um computador Windows que é parte de seu domínio do Active Directory: 

Inicie `cmd.exe` e execute `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie o nome do controlador de domínio que é o valor de configuração necessário do KDC, nesse controlador de domínio-33.domain.company.com case

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Junte-se seu sistema operacional para o controlador de domínio do Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

Editar o `/etc/network/interfaces` arquivo para que o endereço IP do controlador de domínio do AD está listado como um servidor de nomes do dns. Por exemplo: 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
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

Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha semelhante à seguinte:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

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

Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha semelhante à seguinte:  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Junte-se o macOS para o controlador de domínio do Active Directory seguindo estas etapas:



## <a name="configure-kdc-in-krb5conf"></a>Configure o KDC krb5

Editar o `/etc/krb5.conf` em um editor de sua escolha. Configure as seguintes chaves

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Em seguida, salve o arquivo krb5.conf e sair

> [!NOTE]
> Domínio deve estar em letras maiusculas


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Testar a recuperação de tíquete de concessão de tíquete

Obtenha um tíquete de concessão de tíquete (TGT) do KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Exiba os tíquetes disponíveis usando klist. Se o kinit foi bem-sucedida, você deverá ver um tíquete. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Conecte-se usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Criar um novo perfil de conexão

* Escolher **autenticação do Windows** como o tipo de autenticação

* Conclua o perfil de conexão, clique em **Connect**

Depois de se conectar com êxito, o servidor aparece na *servidores* barra lateral.
