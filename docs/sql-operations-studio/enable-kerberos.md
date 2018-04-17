---
title: Usar autenticação do Active Directory (Kerberos) ao conectar-se com o SQL Operations Studio (preview) | Microsoft Docs
description: Saiba como habilitar o Kerberos usar autenticação do Active Directory para o SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd229a0106506f744074df760ee10f871474ebb
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>Conecte-se [!INCLUDE[name-sos](../includes/name-sos-short.md)] ao SQL Server usando a autenticação do Windows - Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] oferece suporte à conexão ao SQL Server usando o Kerberos.

Para usar a autenticação integrada (autenticação do Windows) no macOS ou Linux, você precisa configurar um **tíquete Kerberos** vinculando o usuário atual para uma conta de domínio do Windows. 

## <a name="prerequisites"></a>Prerequisites

- Acesso a uma máquina de domínio do Windows para consultar seu controlador de domínio do Kerberos.
- SQL Server deve ser configurado para permitir a autenticação Kerberos. Para o driver do cliente em execução em Unix, autenticação integrada tem suporte apenas usando o Kerberos. Para obter mais informações sobre como configurar o Sql Server para se autenticar usando Kerberos podem ser encontradas [aqui](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server). Deve haver SPNs registrados para cada instância do Sql Server que você está tentando se conectar. Os detalhes sobre o formato dos SPNs do SQL Server estão listados [aqui](https://technet.microsoft.com/en-us/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>Verificando se o Sql Server tem a instalação do Kerberos

Faça logon no computador host do Sql Server. No Prompt de comando do Windows, use o `setspn -L %COMPUTERNAME%` para listar todos os nomes de entidade de serviço para o host. Você deve ver as entradas que começam com MSSQLSvc/HostName.Domain.com que significa que o Sql Server tiver registrado um SPN e está pronto para aceitar a autenticação Kerberos. 
- Se você não tiver acesso ao Host do Sql Server, de qualquer outro sistema operacional Windows associado ao mesmo Active Directory, você pode usar o comando `setspn -L <SQLSERVER_NETBIOS>` onde < SQLSERVER_NETBIOS > é o nome do computador do host do Sql Server.


## <a name="get-the-kerberos-key-distribution-center"></a>Obter o Kerberos Key Distribution Center

Localize o valor de configuração do Kerberos KDC (Centro de distribuição de chaves). Execute o seguinte comando em um computador com Windows que é parte de seu domínio do Active Directory: 

Iniciar `cmd.exe` e executar `nltest`.

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where “DOMAIN.COMPANY.COM” maps to your domain’s name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
Copie o nome do controlador de domínio que é o valor de configuração necessário do KDC, neste controlador de domínio-33.domain.company.com caso

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>Ingressar em seu sistema operacional para o controlador de domínio do Active Directory

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

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
> A interface de rede (eth0) pode ser diferentes para computadores diferentes. Para descobrir qual deles você está usando, execute ifconfig e copie a interface que tem um endereço IP e bytes transmitidos e recebidos.

Depois de editar esse arquivo, reinicie o serviço de rede:

```bash
sudo ifdown eth0 && sudo ifup eth0
```

Verifique se agora o `/etc/resolv.conf` arquivo contém uma linha semelhante à seguinte:  

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

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- Unir o macOS para o controlador de domínio do Active Directory [siga estas etapas] (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US).



## <a name="configure-kdc-in-krb5conf"></a>Configure o KDC krb5

Editar o `/etc/krb5.conf` em um editor de sua escolha. Configurar as chaves a seguir

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

Em seguida, salve o arquivo krb5 conf e sair

> [!NOTE]
> Domínio deve ser todo em maiusculas


## <a name="test-the-ticket-granting-ticket-retrieval"></a>Testar a recuperação de tíquete de concessão de tíquete

Obter um tíquete de concessão de tíquete (TGT) do KDC.

```bash
kinit username@DOMAIN.COMPANY.COM
```

Exiba as permissões disponíveis usando o kinit. Se o kinit foi bem-sucedida, você verá um tíquete. 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>Conecte-se usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* Criar um novo perfil de conexão

* Escolha **autenticação do Windows** como o tipo de autenticação

* Complete o perfil de conexão, clique em **conectar**

Depois de se conectar com êxito, o servidor aparece no *servidores* barra lateral.
