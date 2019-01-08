---
title: Use os provedores do Active Directory de terceiros com o SQL Server no Linux
titleSuffix: SQL Server
description: Este tutorial fornece as etapas de configuração para a autenticação do Active Directory com provedores de terceiros
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: de28696efd16a2be61864a810b3fd713b1066258
ms.sourcegitcommit: de8ef246a74c935c5098713f14e9dd06c4733713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53160564"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Use os provedores do Active Directory de terceiros com o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em uma máquina de host do Linux com a autenticação do Active Directory ao usar os provedores do Active Directory de terceiros. Os exemplos são [serviços de identidade PowerBroker (PBIS)](https://www.beyondtrust.com/), [uma identidade](https://www.oneidentity.com/products/authentication-services/), e [Centrify](https://www.centrify.com/). Este guia inclui etapas para verificar sua configuração do Active Directory. Ele não deve instruir sobre como unir um computador a um domínio. Para obter instruções detalhadas sobre como ingressar em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] hospedar em um domínio usando o realmd e SSSD, consulte [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>Prerequisites

Antes de configurar a autenticação do Active Directory, você precisará configurar um controlador do Active Directory, Windows, em sua rede. Em seguida, ingressar seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no host do Linux para um domínio do Active Directory. Você pode usar [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), ou [Centrify](https://www.centrify.com/).

> [!NOTE]
>
>Este tutorial usa **`contoso.com`** e **`CONTOSO.COM`** como exemplos de nomes de domínio e o realm, respectivamente. Ele também usa **`DC1.CONTOSO.COM`** conforme o exemplo totalmente qualificado do nome de domínio do controlador de domínio. Você deve substituir esses nomes pelos seus próprios valores.

## <a name="check-the-connection-to-a-domain-controller"></a>Verifique a conexão a um controlador de domínio

Verifique que você pode contatar o controlador de domínio com os nomes curtos e totalmente qualificados do domínio:

```bash
ping contoso

ping contoso.com
```

Se qualquer uma dessas verificações de nome, atualize sua lista de pesquisa de domínio:

- **Ubuntu**

  Editar o `/etc/network/interfaces` arquivo, para que seu domínio do Active Directory está na lista de domínios de pesquisa: 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > A interface de rede **eth0**, podem ser diferentes para diferentes computadores. Para descobrir qual deles você está usando, execute **ifconfig**. Em seguida, copie a interface que tem um endereço IP e os bytes transmitidos e recebidos.

  Depois de editar esse arquivo, reinicie o serviço de rede:

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  Editar o `/etc/sysconfig/network-scripts/ifcfg-eth0` arquivo, para que seu domínio do Active Directory está na lista de domínios de pesquisa. Ou editar a outro arquivo de configuração de interface, conforme apropriado:

  ```/etc/sysconfig/network-scripts/ifcfg-eth0
  <...>
  PEERDNS=no
  DNS1=**<AD domain controller IP address>**
  DOMAIN="contoso.com com"
  ```

  Depois de editar esse arquivo, reinicie o serviço de rede:

  ```bash
  sudo systemctl restart network
  ```

  Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

  Se você ainda não é possível executar o ping no controlador de domínio, localize o nome de domínio totalmente qualificado e o endereço IP do controlador de domínio. Um exemplo de nome de domínio é `DC1.CONTOSO.COM`. Adicione a seguinte entrada ao `/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  Editar o `/etc/sysconfig/network/config` arquivo, para que o IP do controlador de domínio do Active Directory é usado para consultas DNS e domínio do Active Directory está na lista de domínios de pesquisa:

  ```/etc/sysconfig/network/config
  <...>
  NETCONFIG_DNS_STATIC_SEARCHLIST=""
  NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
  ```

  Depois de editar esse arquivo, reinicie o serviço de rede:

  ```bash
  sudo systemctl restart network
  ```

  Agora, verifique se seu `/etc/resolv.conf` arquivo contém uma linha como o exemplo a seguir:

  ```/etc/resolv.conf
  search contoso.com com
  nameserver **<AD domain controller IP address>**
  ```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Verifique se o DNS reverso está configurado corretamente

O comando a seguir deve retornar o nome de domínio totalmente qualificado do host que executa o SQL Server. Um exemplo é **`SqlHost.contoso.com`**.

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

Se esse comando não retornar o FQDN do host, ou se o FQDN estiver incorreto, adicione uma entrada DNS reversa para você é [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no host do Linux para o servidor DNS.

## <a name="check-that-your-krb5-configuration-is-correct"></a>Verifique se sua configuração KRB5 está correta

Verifique se seu `/etc/krb5.conf` está configurado corretamente. Para a maioria dos provedores do Active Directory de terceiros, essa configuração é feita automaticamente. No entanto, verifique `/etc/krb5.conf` para os seguintes valores evitar quaisquer problemas futuros:

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="next-steps"></a>Próximas etapas

Este artigo aborda como configurar um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em uma máquina de host do Linux com a autenticação do Active Directory ao usar os provedores do Active Directory de terceiros. Para concluir a configuração [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para dar suporte a contas do Active Directory, siga as instruções em [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).

> [!div class="nextstepaction"]
> [Usar autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> Você pode ignorar a **host ingressar o SQL Server para o domínio do Active Directory** seção [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md) como você acabou de fazer que neste tutorial.
