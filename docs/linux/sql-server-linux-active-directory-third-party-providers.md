---
title: Use os provedores do Active Directory de terceiros com o SQL Server no Linux | Microsoft Docs
description: Este tutorial fornece as etapas de configuração para a autenticação do AD com provedores de terceiros
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: 288f46a2084166a1b7164ff8f0c0ef82b81fb16b
ms.sourcegitcommit: ca5430ff8e3f20b5571d092c81b1fb4c950ee285
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381511"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>Use os provedores do Active Directory de terceiros com o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar uma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador de host do Linux com a autenticação do AD ao usar os provedores de AD de terceiros, como [serviços de identidade PowerBroker (PBIS)](https://www.beyondtrust.com/), [Vintela autenticação Services (VAS)](https://www.oneidentity.com/products/authentication-services/), e [Centrify](https://www.centrify.com/). Este guia inclui etapas para verificar sua configuração do AD e não se destina para instruir sobre como ingressar uma máquina em um domínio. Para obter instruções detalhadas sobre como ingressar em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] hospedar em um domínio usando o REALM e SSSD, consulte [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).

## <a name="prerequisites"></a>Prerequisites

Antes de configurar a autenticação do AD, você precisará configurar um controlador de domínio do AD (Windows) em sua rede e junção seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no host do Linux para um domínio do AD. Você pode usar [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), ou [Centrify](https://www.centrify.com/).

> [!NOTE]
>
>Este tutorial usa "contoso.com" e "CONTOSO.COM" como nomes de domínio e o realm de exemplo, respectivamente. Ele também usa "DC1. CONTOSO.COM"como nome de domínio totalmente qualificado de exemplo do controlador de domínio. Você deve substituí-las com seus próprios valores.

## <a name="check-connection-to-domain-controller"></a>Verifique a Conexão ao controlador de domínio

Verifique se que você pode contatar o controlador de domínio com o nome curto e totalmente qualificado do domínio.

   ```bash
   ping contoso

   ping contoso.com
   ```

   Se qualquer uma delas falhar, atualize sua lista de pesquisa de domínio.

   - **Ubuntu**:

     Editar o `/etc/network/interfaces` arquivo para que seu domínio do AD está na lista de pesquisa de domínio: 

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
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   - **RHEL**:

     Editar o `/etc/sysconfig/network-scripts/ifcfg-eth0` arquivo (ou outra configuração de interface de arquivos conforme apropriado) para que seu domínio do AD está na lista de pesquisa de domínio:

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

   Se você ainda não é possível executar o ping no controlador de domínio, localize o nome de domínio totalmente qualificado (por exemplo, o DC1. CONTOSO.COM) e o endereço IP do controlador de domínio e adicione a seguinte entrada à `/etc/hosts`

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

   - **SLES**:

     Editar o `/etc/sysconfig/network/config` arquivo para que o IP do controlador de domínio AD será usado para consultas DNS e seu domínio do AD está na lista de pesquisa de domínio:

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

## <a name="check-reverse-dns-is-properly-configured"></a>Verificar o que DNS reverso está configurado corretamente

O comando a seguir deve retornar o nome de domínio totalmente qualificado do host que executa o SQL Server (por exemplo "SqlHost.contoso.com").

   ```bash
   host **<IP address of SQL Server host>**
   # **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
   ```

   Se isso não retornar o FQDN do host ou o FQDN estiver incorreto, adicione uma entrada DNS reversa para seu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no host do Linux para o servidor DNS.

## <a name="check-your-krb5-configuration-is-correct"></a>Verifique sua configuração KRB5 está correta

Verifique seu `/etc/krb5.conf` está configurado corretamente. Para a maioria dos provedores de AD de terceiros, isso é feito automaticamente. No entanto, verifique `/etc/krb5.conf` para os seguintes valores evitar quaisquer problemas futuros:

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

Neste artigo, abordamos como configurar um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador de host do Linux com a autenticação do AD ao usar os provedores de AD de terceiros. Para concluir a configuração [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para dar suporte a contas do AD, siga as instruções em [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).

> [!div class="nextstepaction"]
> [Usar autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> Você pode ignorar a seção "Host de associação SQL Server ao domínio do AD" [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md) como assim que tiver feito isso neste tutorial.