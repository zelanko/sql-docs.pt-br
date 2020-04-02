---
title: Ingressar o SQL Server em Linux no Active Directory
titleSuffix: SQL Server
description: Este artigo fornece orientações sobre como ingressar um computador host Linux do SQL Server em um domínio do AD. Você pode usar um pacote SSSD interno ou provedores do AD de terceiros.
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: c787409d4e8772d89fc748d39c605506f5dcb520
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80216185"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Ingressar o SQL Server em um host Linux em um domínio do Active Directory

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo oferece diretrizes gerais sobre como ingressar um computador host Linux do SQL Server em um domínio do AD (Active Directory). Há dois métodos: usar um pacote SSSD interno ou usar provedores de Active Directory de terceiros. Os exemplos de produtos de ingresso no domínio de terceiros são are [PBIS (Serviços de Identidade PowerBroker)](https://www.beyondtrust.com/), [One Identity](https://www.oneidentity.com/products/authentication-services/) e [Centrify](https://www.centrify.com/). Este guia inclui etapas para verificar a configuração do Active Directory. No entanto, ele não pretende fornecer instruções sobre como ingressar um computador em um domínio ao usar utilitários de terceiros.

## <a name="prerequisites"></a>Pré-requisitos

Antes de configurar a autenticação do Active Directory, é necessário configurar um controlador de domínio do Active Directory, Windows, em sua rede. Em seguida, ingresse o host SQL Server em Linux em um domínio do Active Directory.

> [!IMPORTANT]
> As etapas de exemplo descritas neste artigo são apenas para orientação e referem-se aos sistemas operacionais Ubuntu 16.04, Red Hat Enterprise Linux (RHEL) 7.x e SUSE Enterprise Linux (SLES) 12. As etapas reais podem ser ligeiramente diferentes em seu ambiente, dependendo de como o ambiente geral está configurado e da versão do sistema operacional. Por exemplo, o Ubuntu 18.04 usa o netplan enquanto o Red Hat Enterprise Linux (RHEL) 8.x usa o nmcli entre outras ferramentas para gerenciar e configurar a rede. É recomendável envolver os administradores do sistema e do domínio do seu ambiente para ferramentas específicas, configuração, personalização e qualquer solução de problemas necessária.

## <a name="check-the-connection-to-a-domain-controller"></a>Verificar a conexão com um controlador de domínio

Verifique se você pode contatar o controlador de domínio com os nomes curto e totalmente qualificado do domínio:

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> Este tutorial usa **contoso.com** e **CONTOSO.COM** como nomes de domínio e realm de exemplo, respectivamente. Ele também usa **DC1.CONTOSO.COM** como o nome de domínio totalmente qualificado de exemplo do controlador de domínio. É necessário substituir esses nomes por seus próprios valores.

Se uma dessas verificações de nome falhar, atualize sua lista de pesquisa de domínio. As seções a seguir fornecem instruções para Ubuntu, RHEL (Red Hat Enterprise Linux) e SLES (SUSE Linux Enterprise Server), respectivamente.

### <a name="ubuntu-1604"></a>Ubuntu 16.04

1. Edite o arquivo **/etc/network/interfaces** para que seu domínio do Active Directory esteja na lista de pesquisa de domínio:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > O adaptador de rede, `eth0`, pode ser diferente para diferentes computadores. Para descobrir qual você está usando, execute **ifconfig**. Em seguida, copie a interface que tem um endereço IP e os bytes transmitidos e recebidos.

1. Após editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. Em seguida, verifique se o arquivo **/etc/resolv.conf** contém uma linha semelhante ao do exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel-7x"></a>RHEL 7.x

1. Edite o arquivo **/etc/sysconfig/network-scripts/ifcfg-eth0** para que o domínio do Active Directory esteja na lista de pesquisa de domínio. Ou edite outro arquivo de configuração de interface, conforme apropriado:

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. Após editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo systemctl restart network
   ```

1. Agora, verifique se o arquivo **/etc/resolv.conf** contém uma linha semelhante ao do exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. Se você ainda não conseguir executar o ping do controlador de domínio, localize o nome de domínio totalmente qualificado e o endereço IP do controlador de domínio. Um nome de domínio de exemplo é **DC1.CONTOSO.COM**. Adicione a seguinte entrada a **/etc/hosts**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles-12"></a>SLES 12

1. Edite o arquivo **/etc/sysconfig/network/config** para que o IP do controlador de domínio do Active Directory seja usado para consultas DNS e para que o domínio do Active Directory esteja na lista de pesquisa de domínio:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. Após editar esse arquivo, reinicie o serviço de rede:

   ```bash
   sudo systemctl restart network
   ```

1. Em seguida, verifique se o arquivo **/etc/resolv.conf** contém uma linha semelhante ao do exemplo a seguir:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>Ingressar no domínio do AD

Depois que a configuração básica e a conectividade com o controlador de domínio for verificada, haverá duas opções para ingressar um computador host do Linux do SQL Server com o controlador de domínio do Active Directory:

- [Opção 1: usar um pacote SSSD](#option1)
- [Opção 2: usar utilitários de provedor openldap de terceiros](#option2)

### <a name="option-1-use-sssd-package-to-join-ad-domain"></a><a id="option1"></a> Opção 1: usar o pacote SSSD para ingressar no domínio do AD

Esse método ingressa o host SQL Server em um domínio do AD usando os pacotes **realmd** e **sssd**.

> [!NOTE]
> Esse é o método preferencial de ingressar um host Linux em um controlador de domínio do AD.

Use as etapas a seguir para ingressar um host SQL Server em um domínio do Active Directory:

1. Use [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) para ingressar seu computador host em seu domínio do AD. Você deve primeiro instalar os pacotes **realmd** e do cliente Kerberos no computador host SQL Server usando o gerenciador de pacotes da distribuição do Linux:

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

1. Se a instalação do pacote de cliente Kerberos solicitar um nome de realm, insira seu nome de domínio em letras maiúsculas.

1. Após confirmar se seu DNS está configurado adequadamente, ingresse o domínio executando o comando a seguir. É necessário autenticar-se usando uma conta do AD com privilégios suficientes no AD para ingressar um novo computador no domínio. Este comando cria uma conta do computador no AD, cria o arquivo keytab do host **/etc/krb5.keytab**, configura o domínio no **/etc/sssd/sssd.conf** e atualiza o **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   Você deve ver a mensagem, `Successfully enrolled machine in realm`.

   A seguinte tabela lista algumas mensagens de erro que você poderia receber e sugestões sobre como resolvê-las:

   | Mensagem de erro | Recomendação |
   |---|---|
   | `Necessary packages are not installed` | Instale esses pacotes usando o gerenciador de pacotes da distribuição do Linux antes de executar o comando de ingresso no realm novamente. |
   | `Insufficient permissions to join the domain` | Verifique com um administrador de domínio se você tem permissões suficientes para ingressar computadores Linux em seu domínio. |
   | `KDC reply did not match expectations` | Talvez você não tenha especificado o nome de realm correto do usuário. Nomes de realm diferenciam maiúsculas de minúsculas, geralmente são escritos em maiúsculas e podem ser identificados com o comando realm discover contoso.com. |

   O SQL Server usa SSSD e NSS para mapear contas de usuário e grupos para SIDs (identificadores de segurança). O SSSD deve ser configurado e estar em execução para o SQL Server criar logons do AD com êxito. **realmd** geralmente faz isso automaticamente como parte de ingressar o domínio, mas, em alguns casos, você deve fazer isso separadamente.

   Para saber mais, confira como [configurar SSSD manualmente](https://access.redhat.com/articles/3023951) e [configurar NSS para funcionar com SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. Verifique se você pode coletar informações sobre um usuário do domínio e se pode adquirir um tíquete do Kerberos como esse usuário. O exemplo a seguir usa os comandos **id**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) e [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) para isso.

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
   > - Se **id user\@contoso.com** retornar `No such user`, verifique se o serviço SSSD foi iniciado com êxito executando o comando `sudo systemctl status sssd`. Se o serviço estiver em execução e você ainda vir o erro, tente habilitar o log detalhado para SSSD. Para saber mais, confira a documentação do Red Hat para [Solucionar problemas de SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > - Se **kinit user\@CONTOSO.COM** retornar `KDC reply did not match expectations while getting initial credentials`, verifique se você especificou o realm em letras maiúsculas.

Para saber mais, confira a documentação do Red Hat para [Descobrir e ingressar domínios de identidade](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html).

### <a name="option-2-use-third-party-openldap-provider-utilities"></a><a id="option2"></a> Opção 2: usar utilitários de provedor openldap de terceiros

Você pode usar utilitários de terceiros, como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) ou [Centrify](https://www.centrify.com/). Este artigo não aborda etapas para cada utilitário individual. Primeiro, você deve usar um desses utilitários para ingressar o host Linux do SQL Server no domínio antes de continuar.  

O SQL Server não usa o código ou a biblioteca de um integrador de terceiros para nenhuma consulta relacionada ao AD. O SQL Server sempre consulta o AD usando chamadas de biblioteca openldap diretamente nesta instalação. Os integradores de terceiros são usados apenas para ingressar o host Linux no domínio do AD e o SQL Server não tem nenhuma comunicação direta com esses utilitários.

> [!IMPORTANT]
> Confira as recomendações para usar a opção de configuração do **mssql-conf** `network.disablesssd` na seção **Opções de configuração adicional** do artigo [Usar autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md#additionalconfig).

Verifique se **/etc/krb5.conf** está configurado corretamente. Para a maioria dos provedores do Active Directory de terceiros, essa configuração é feita automaticamente. No entanto, verifique se, em **/etc/krb5.conf**, há os seguintes valores para evitar problemas futuros:

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Verifique se o DNS inverso está configurado corretamente

O comando a seguir deve retornar o FQDN (nome de domínio totalmente qualificado) do host que executa o SQL Server. Um exemplo é **SqlHost.contoso.com**.

```bash
host **<IP address of SQL Server host>**
```

A saída deste comando deve ser semelhante a `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`. Se esse comando não retornar o FQDN do host ou se o FQDN estiver incorreto, adicione uma entrada de DNS inversa para seu host SQL Server em Linux ao servidor DNS.

## <a name="next-steps"></a>Próximas etapas

Este artigo aborda o pré-requisito de como configurar um SQL Server em um computador host Linux com a Autenticação do Active Directory. Para concluir a configuração do SQL Server em Linux para dar suporte a contas do Active Directory, siga as instruções em [Usar a autenticação do Active Directory com o SQL Server em Linux](sql-server-linux-active-directory-authentication.md).
