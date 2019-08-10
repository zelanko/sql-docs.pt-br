---
title: Como configurar o MSDTC no Linux
description: Este artigo fornece um passo a passo para configurar o MSDTC no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c44458e1a68c842b6433d7a137865ae8451c136c
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077616"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Como configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft) no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft) no Linux. O suporte a MSDTC no Linux foi introduzido na versão prévia do SQL Server 2019.

## <a name="overview"></a>Visão geral

As transações distribuídas são habilitadas no SQL Server em Linux, introduzindo o MSDTC e a funcionalidade de mapeador de pontos de extremidade RPC no SQL Server. Por padrão, um processo de mapeamento de ponto de extremidade RPC escuta na porta 135 para solicitações RPC de entrada e fornece informações de componentes registrados a solicitações remotas. As solicitações remotas podem usar as informações retornadas pelo mapeador de pontos de extremidade para se comunicarem com os componentes RPC registrados, tais como os serviços MSDTC. Um processo requer privilégios de superusuário para associar a portas conhecidas (números de porta menores que 1024) no Linux. Para evitar iniciar o SQL Server com privilégios de raiz para o processo do mapeador de pontos de extremidade RPC, os administradores do sistema devem usar iptables para criar a conversão de endereços de rede para rotear o tráfego na porta 135 para o processo de mapeamento de ponto de extremidade RPC do SQL Server.

O SQL Server 2019 apresenta dois parâmetros de configuração para o utilitário mssql-conf.

| configuração mssql-conf | Descrição |
|---|---|
| **network.rpcport** | A porta TCP à qual o processo do mapeador de pontos de extremidade RPC é associado. |
| **distributedtransaction.servertcpport** | A porta em que o servidor MSDTC escuta. Se esse parâmetro não for definido, o serviço MSDTC usará uma porta efêmera aleatória em reinicializações de serviço e as exceções de firewall precisarão ser reconfiguradas para garantir que o serviço MSDTC possa continuar a comunicação. |

Para obter mais informações sobre essas configurações e outras configurações relacionadas do MSDTC, confira [Configurar o SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configurações do MSDTC compatíveis

As configurações do MSDTC a seguir são compatíveis:

- Transações distribuídas OLE-TX em SQL Server em Linux para provedores ODBC.
- Transações distribuídas XA em SQL Server em Linux usando provedores ODBC e JDBC. Para transações XA a serem executadas usando o provedor ODBC, você precisa usar o Microsoft ODBC Driver for SQL Server versão 17.3 ou superior.
- Transações distribuídas no servidor vinculado.

Para ver as limitações e problemas conhecidos do MSDTC na versão prévia, confira as [Notas sobre a versão prévia do SQL Server 2019 em Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Etapas de configuração do MSDTC

Há três etapas para configurar a comunicação e a funcionalidade do MSDTC. Se as etapas de configuração necessárias não forem cumpridas, o SQL Server não habilitará a funcionalidade do MSDTC.

- Configure **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.
- Configure o firewall para permitir a comunicação em **distributedtransaction.servertcpport** e na porta 135.
- Configure o roteamento do servidor Linux para que a comunicação RPC na porta 135 seja redirecionada para a **network.rpcport** do SQL Server.

As seções a seguir fornecem instruções detalhadas para cada etapa.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurar portas RPC e MSDTC

Primeiro, configure **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf. Esta etapa é específica para o SQL Server e comum em todas as distribuições compatíveis.

1. Use mssql-conf para definir o valor de **network.rpcport**. O exemplo a seguir define-o para 13500.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. Defina o valor de **distributedtransaction.servertcpport**. O exemplo a seguir define-o para 51999.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. Reinicie o SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>Configurar o firewall

A segunda etapa é configurar o firewall para permitir a comunicação em **servertcpport** e na porta 135.  Isso permite que o processo de mapeamento de pontos de extremidade RPC e o processo do MSDTC se comuniquem externamente com outros gerenciadores de transação e coordenadores. As etapas reais para isso variam de acordo com a distribuição do Linux e o firewall. 

O exemplo a seguir mostra como criar essas regras no **Ubuntu**.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

O exemplo a seguir mostra como isso pode ser feito no **RHEL (Red Hat Enterprise Linux)** :

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

É importante configurar o firewall antes de configurar o roteamento de porta na próxima seção. A atualização do firewall pode limpar as regras de roteamento de porta em alguns casos.

## <a name="configure-port-routing"></a>Configurar roteamento de porta

Configure a tabela de roteamento do servidor Linux para que a comunicação RPC na porta 135 seja redirecionada para a **network.rpcport** do SQL Server. O mecanismo de configuração para encaminhamento de porta em outras distribuições pode ser diferente. As seções a seguir fornecem diretrizes para Ubuntu, SLES (SUS Enterprise Linux) e RHEL (Red Hat Enterprise Linux).

### <a name="port-routing-in-ubuntu-and-sles"></a>Roteamento de porta no Ubuntu e no SLES

O Ubuntu e o SLES não usam o serviço **firewalld**, portanto, as regras de **iptable** são um mecanismo eficiente para obter roteamento de porta. As regras de **iptable** podem não persistir durante reinicializações, portanto, os comandos a seguir também fornecem instruções para restaurar as regras após uma reinicialização.

1. Crie regras de roteamento para a porta 135. No exemplo a seguir, a porta 135 é direcionada para a porta RPC, 13500, definida na seção anterior. Substitua `<ipaddress>` pelo endereço IP do servidor.

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   O parâmetro `--comment RpcEndPointMapper` nos comandos anteriores ajuda a gerenciar essas regras em comandos posteriores.

2. Exiba as regras de roteamento que você criou com o seguinte comando:

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Salve as regras de roteamento em um arquivo no computador.

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. Para recarregar as regras após uma reinicialização, adicione o seguinte comando a `/etc/rc.local` (para Ubuntu) ou a `/etc/init.d/after.local` (para SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > Você deve ter privilégios de superusuário (sudo) para editar os arquivos **rc.local** ou **after.local**.

Os comandos **iptables-save** e **iptables-restore**, juntamente com a configuração de inicialização `rc.local`/`after.local`, fornecem um mecanismo básico para salvar e restaurar entradas de iptables. Dependendo de sua distribuição do Linux, pode haver opções mais avançadas ou automatizadas disponíveis. Por exemplo, uma alternativa do Ubuntu é o pacote **iptables-persistent** para tornar as entradas persistentes.

> [!IMPORTANT]
> As etapas anteriores pressupõem um endereço IP fixo. Se o endereço IP da instância do SQL Server for alterado (devido a intervenção manual ou DHCP), você deverá remover e recriar as regras de roteamento se elas tiverem sido criadas com iptables. Se precisar recriar ou excluir regras de roteamento existentes, você poderá usar o comando a seguir para remover regras `RpcEndPointMapper` antigas:
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>Roteamento de porta no RHEL

Em distribuições que usam o serviço **firewalld**, assim como o Red Hat Enterprise Linux, o mesmo serviço pode ser usado para abrir a porta no servidor e o encaminhamento de porta interno. Por exemplo, em Red Hat Enterprise Linux, você deve usar o serviço **firewalld** (por meio do utilitário de configuração **firewall-cmd** com `-add-forward-port` ou opções semelhantes) para criar e gerenciar regras de encaminhamento de porta persistentes em vez de usar iptables.

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>Verificar

Neste ponto, o SQL Server deve ser capaz de participar de transações distribuídas. Para verificar se o SQL Server está escutando, execute o comando **netstat** (se você estiver usando o RHEL, talvez precise instalar primeiro o pacote **net-tools**):

```bash
sudo netstat -tulpn | grep sqlservr
```

Será exibida uma saída semelhante à seguinte:

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

No entanto, após uma reinicialização, o SQL Server não começa a escutar em **servertcpport** até a primeira transação distribuída. Nesse caso, você não verá o SQL Server escutando na porta 51999 neste exemplo até a primeira transação distribuída.

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>Configurar a autenticação na comunicação RPC para o MSDTC

O MSDTC para SQL Server em Linux não usa autenticação na comunicação RPC por padrão. No entanto, quando o computador host é ingressado em um domínio do AD (Active Directory), é possível configurar o MSDTC para usar a comunicação RPC autenticada usando as seguintes configurações de **mssql-conf**:

| Configuração | Descrição |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | Configure chamadas RPC somente seguras para transações distribuídas. |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | Configure chamadas RPC somente de segurança para transações distribuídas. |
| **distributedtransaction.turnoffrpcsecurity**               | Habilitar ou desabilitar a segurança RPC para transações distribuídas. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server em Linux, confira [SQL Server em Linux](sql-server-linux-overview.md).
