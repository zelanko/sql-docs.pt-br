---
title: Junte-se do SQL Server no Linux para o Active Directory
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: Dylan.Gray
ms.reviewer: rothja
ms.date: 04/01/2019
manager: craigg
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6ccc94acb42fa7043912099c4888834cf4ff3e71
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59243580"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Junte-se do SQL Server em um host Linux em um domínio do Active Directory

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece diretrizes gerais sobre como ingressar uma máquina de host do SQL Server Linux em um domínio do Active Directory (AD). Há dois métodos: usar um pacote SSSD internos ou usam provedores de Active Directory de terceiros. São exemplos de produtos de junção de domínio de terceiro [serviços de identidade PowerBroker (PBIS)](https://www.beyondtrust.com/), [uma identidade](https://www.oneidentity.com/products/authentication-services/), e [Centrify](https://www.centrify.com/). Este guia inclui etapas para verificar sua configuração do Active Directory. No entanto, ele não se destina para fornecer instruções sobre como ingressar uma máquina em um domínio ao usar os utilitários de terceiros.

## <a name="prerequisites"></a>Prerequisites

Antes de configurar a autenticação do Active Directory, você precisará configurar um controlador do Active Directory, Windows, em sua rede. Junte-se, em seguida, o SQL Server em um host Linux em um domínio do Active Directory.

> [!IMPORTANT]
> As etapas de exemplo descritas neste artigo são apenas para orientação. Etapas reais podem diferir ligeiramente em seu ambiente, dependendo de como seu ambiente geral está configurado. Entre em contato com seus administradores de sistema e de domínio para o seu ambiente para a configuração específica, personalização e quaisquer etapas de solução de problemas.

## <a name="check-the-connection-to-a-domain-controller"></a>Verifique a conexão a um controlador de domínio

Verifique que você pode contatar o controlador de domínio com os nomes curtos e totalmente qualificados do domínio:

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> Este tutorial usa **contoso.com** e **CONTOSO.COM** como exemplos de nomes de domínio e o realm, respectivamente. Ele também usa **DC1. CONTOSO.COM** conforme o exemplo totalmente qualificado do nome de domínio do controlador de domínio. Você deve substituir esses nomes pelos seus próprios valores.

Se qualquer uma dessas verificações de nome, atualize sua lista de pesquisa de domínio. As seções a seguir fornecem instruções para Ubuntu, Red Hat Enterprise Linux (RHEL) e SUSE Linux Enterprise Server (SLES), respectivamente.

### <a name="ubuntu"></a>Ubuntu

1. Editar o **/etc/network/interfaces** arquivo, para que seu domínio do Active Directory está na lista de domínios de pesquisa:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > A interface de rede, `eth0`, podem ser diferentes para diferentes computadores. Para descobrir qual deles você está usando, execute **ifconfig**. Em seguida, copie a interface que tem um endereço IP e os bytes transmitidos e recebidos.

1. Depois de editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. Em seguida, verifique se sua **/etc/resolv.conf** arquivo contém uma linha como o exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. Editar o **/etc/sysconfig/network-scripts/ifcfg-eth0** arquivo, para que seu domínio do Active Directory está na lista de domínios de pesquisa. Ou editar a outro arquivo de configuração de interface, conforme apropriado:

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. Depois de editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo systemctl restart network
   ```

1. Agora, verifique se sua **/etc/resolv.conf** arquivo contém uma linha como o exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. Se você ainda não é possível executar o ping no controlador de domínio, localize o nome de domínio totalmente qualificado e o endereço IP do controlador de domínio. Um exemplo de nome de domínio é **DC1. CONTOSO.COM**. Adicione a seguinte entrada à **/etc/hosts**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. Editar o **/etc/sysconfig/network/config** arquivo, para que o IP do controlador de domínio do Active Directory é usado para consultas DNS e domínio do Active Directory está na lista de domínios de pesquisa:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. Depois de editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo systemctl restart network
   ```

1. Em seguida, verifique se sua **/etc/resolv.conf** arquivo contém uma linha como o exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>Ingressar no domínio do AD

Depois que a configuração básica e a conectividade com o controlador de domínio for verificado, há duas opções para ingressar em um computador de host do SQL Server Linux com o controlador de domínio do Active Directory:

- [Opção 1: Usar um pacote SSSD](#option1)
- [Opção 2: Usar utilitários de provedor de terceiros openldap](#option2)

### <a id="option1"></a> Opção 1: Use o pacote SSSD para ingressar em domínio do AD

Esse método une o host do SQL Server para um domínio de AD usando **realmd** e **sssd** pacotes.

> [!NOTE]
> Esse é o método preferencial de ingressar em um host do Linux para um controlador de domínio do AD.

Use as etapas a seguir para associar um host do SQL Server em um domínio do Active Directory:

1. Use [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join.md) para ingressar em sua máquina host para seu domínio do AD. Você deve primeiro instalar ambos os **realmd** e pacotes de Kerberos do cliente no computador host do SQL Server usando o Gerenciador de pacotes da distribuição Linux:

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Se a instalação do pacote de cliente Kerberos solicitar um nome de realm, insira seu nome de domínio em letras maiusculas.

1. Depois de confirmar se o DNS está configurado corretamente, ingresse no domínio executando o comando a seguir. Você deve autenticar usando uma conta do AD que tenha privilégios suficientes no Active Directory para associar uma nova máquina ao domínio. Esse comando cria uma nova conta de computador no AD, cria o **/etc/krb5.keytab** hospedar arquivo keytab, configura o domínio no **/etc/sssd/sssd.conf**e as atualizações **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   Você deve ver a mensagem, `Successfully enrolled machine in realm`.

   A tabela a seguir lista algumas mensagens de erro que você pode receber e obter sugestões sobre como resolvê-los:

   | Mensagem de erro | Recomendação |
   |---|---|
   | `Necessary packages are not installed` | Instale esses pacotes usando o Gerenciador de pacotes da distribuição Linux antes de executar o comando de junção de território novamente. |
   | `Insufficient permissions to join the domain` | Verifique com o administrador de domínio que você tenha permissões suficientes para ingressar computadores Linux no seu domínio. |
   | `KDC reply did not match expectations` | Provavelmente você não especificou o nome de realm correto para o usuário. Nomes de realm diferenciam maiusculas de minúsculas, geralmente em maiusculas e podem ser identificados com o realm de comando descobrir contoso.com. |

   SQL Server usa SSSD e o NSS para mapear contas de usuário e grupos para identificadores de segurança (SIDs). SSSD deve ser configurado e em execução para o SQL Server criar logons do AD com êxito. **realmd** normalmente faz isso automaticamente como parte do ingresso no domínio, mas em alguns casos, você deve fazer isso separadamente.

   Para obter mais informações, consulte como [configurar manualmente o SSSD](https://access.redhat.com/articles/3023951), e [configurar NSS para trabalhar com SSSD](https://access.redhat.com/documentation/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. Verifique se agora você pode reunir informações sobre um usuário do domínio e que você pode adquirir um tíquete Kerberos como esse usuário. O exemplo a seguir usa **identificação**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html), e [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) comandos para isso.

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - Se **identificação user@contoso.com**  retorna, `No such user`, certifique-se de que o serviço SSSD iniciado com êxito, executando o comando `sudo systemctl status sssd`. Se o serviço está em execução e você ainda verá o erro, tente habilitar o log detalhado para SSSD. Para obter mais informações, consulte a documentação do Red Hat [solução de problemas SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > - Se **kinit user@CONTOSO.COM**  retorna, `KDC reply did not match expectations while getting initial credentials`, verifique se você especificou o realm em letras maiusculas.

Para obter mais informações, consulte a documentação do Red Hat [descobrindo e ingressar em domínios de identidade](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html).

### <a id="option2"></a> Opção 2: Usar utilitários de provedor de terceiros openldap

Você pode usar os utilitários de terceiros, como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/), ou [Centrify](https://www.centrify.com/). Este artigo não abrange as etapas para cada utilitário individual. Primeiro, você deve usar um desses utilitários para unir o host do Linux para SQL Server no domínio antes de continuar.  

SQL Server não usa código ou a biblioteca do integrador de terceiros para todas as consultas relacionadas ao AD. Consultas do SQL Server sempre usando chamadas para a biblioteca openldap diretamente nesta instalação do AD. Os integradores de terceiros são usados somente para unir o host do Linux ao domínio do AD e do SQL Server não tem nenhuma comunicação direta com esses utilitários.

> [!IMPORTANT]
> Consulte as recomendações para usar o **mssql-conf** `network.disablesssd` opção de configuração de **opções de configuração adicionais** seção do artigo [Use Active Directory Autenticação do SQL Server no Linux com o](sql-server-linux-active-directory-authentication.md#additionalconfig).

Verifique sua **/etc/krb5.conf** está configurado corretamente. Para a maioria dos provedores do Active Directory de terceiros, essa configuração é feita automaticamente. No entanto, verifique **/etc/krb5.conf** para os seguintes valores evitar quaisquer problemas futuros:

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Verifique se o DNS reverso está configurado corretamente

O comando a seguir deve retornar o nome de domínio totalmente qualificado (FQDN) do host que executa o SQL Server. Um exemplo é **SqlHost.contoso.com**.

```bash
host **<IP address of SQL Server host>**
```

A saída desse comando deve ser semelhante ao `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`. Se esse comando não retornar o FQDN do host, ou se o FQDN estiver incorreto, adicione uma entrada DNS reversa para o SQL Server no host do Linux para o servidor DNS.

## <a name="next-steps"></a>Próximas etapas

Este artigo aborda o pré-requisito de como configurar um SQL Server em uma máquina de host do Linux com a autenticação do Active Directory. Para concluir a configuração do SQL Server no Linux para dar suporte a contas do Active Directory, siga as instruções em [autenticação de usar o Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md).