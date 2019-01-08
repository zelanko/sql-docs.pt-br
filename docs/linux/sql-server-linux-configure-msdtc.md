---
title: Como configurar o MSDTC no Linux | Microsoft Docs
description: Este artigo fornece um passo a passo para configurar o MSDTC no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 127f39075a1b84b1250a27003efeb28083d1adbd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513194"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>Como configurar o Microsoft Distributed Transaction coordenador (MSDTC) no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar o Microsoft Distributed Transaction coordenador (MSTDC) no Linux. Suporte do MSDTC no Linux foi introduzido na versão prévia do SQL Server de 2019.

## <a name="overview"></a>Visão geral

Transações distribuídas são habilitadas no SQL Server no Linux com a introdução de funcionalidade de mapeador de ponto de extremidade MSDTC e RPC no SQL Server. Por padrão, um processo de mapeamento de ponto de extremidade RPC escuta na porta 135 para solicitações RPC de entrada e encaminha que para componentes apropriados (como o serviço MSDTC). Um processo exige privilégios de superusuário para associar a portas bem conhecidas (números de porta de menor que 1024) no Linux. Para evitar iniciando o SQL Server com privilégios de raiz para o processo do mapeador de ponto de extremidade RPC, os administradores do sistema devem usar iptables para criar a tradução de NAT para rotear o tráfego na porta 135 para o processo de mapeamento de ponto de extremidade RPC do SQL Server.

SQL Server 2019 apresenta dois parâmetros de configuração para o utilitário mssql-conf.

| configuração de MSSQL-conf | Descrição |
|---|---|
| **Network.rpcport** | A porta TCP que o processo do mapeador de ponto de extremidade RPC associa ao. |
| **Network.servertcpport** | A porta que o servidor MSDTC escuta. Se não for definido, o serviço MSDTC usa uma porta efêmera aleatória na reinicialização do serviço e exceções do firewall precisarão ser reconfiguradas para garantir que o serviço MSDTC pode continuar a comunicação. |

Para obter mais informações sobre essas configurações e outras configurações relacionadas do MSDTC, consulte [configurar o SQL Server no Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#msdtc).

## <a name="supported-msdtc-configurations"></a>Configurações com suporte do MSDTC

Há suporte para as seguintes configurações de MSDTC:

- Transações distribuídas OLE TX contra o SQL Server no Linux para provedores de JDBC e ODBC.
- Transações distribuídas XA contra o SQL Server no Linux usando provedores JDBC.
- Transações distribuídas no servidor vinculado.

Para limitações e problemas conhecidos para o MSDTC em versão prévia, consulte [notas de versão para versão prévia de 2019 do SQL Server no Linux](sql-server-linux-release-notes-2019.md#msdtc).

## <a name="msdtc-configuration-steps"></a>Etapas de configuração do MSDTC

Há três etapas para configurar a funcionalidade e a comunicação do MSDTC. Se as etapas de configuração necessárias não são realizadas, do SQL Server não permitirá a funcionalidade do MSDTC.

- Configure **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.
- Configurar o firewall para permitir a comunicação **rpcport**, **servertcpport**e a porta 135.
- Configurar o roteamento de servidor Linux, para que a comunicação de RPC na porta 135 é redirecionada para o SQL Server **network.rpcport**.

As seções a seguir fornecem instruções detalhadas para cada etapa.

## <a name="configure-rpc-and-msdtc-ports"></a>Configurar portas RPC e o MSDTC

Primeiro, configure **network.rpcport** e **distributedtransaction.servertcpport** usando mssql-conf.

1. Use o mssql-conf para definir a **network.rpcport** valor. O exemplo a seguir define a ele como 13500.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. Defina as **distributedtransaction.servertcpport** valor. O exemplo a seguir define a ele como 51999.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. Reinicie o SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>Configurar o firewall

A etapa final é configurar o firewall para permitir a comunicação **rpcport**, **servertcpport**e a porta 135.  Isso permite que o processo MSDTC para se comunicar externamente com outros gerenciadores de transações e os coordenadores e o processo de mapeamento de ponto de extremidade RPC. As etapas reais para isso varia dependendo da sua distribuição do Linux e do firewall. 

O exemplo a seguir mostra como criar essas regras no Ubuntu.

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

O exemplo a seguir mostra como isso pode ser feito no Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

É importante configurar o firewall antes de configurar o roteamento de porta na próxima seção. Atualizar o firewall pode desmarcar as regras de roteamento de porta em alguns casos.

## <a name="configure-port-routing"></a>Configurar o roteamento de porta

Configurar a tabela de roteamento do servidor Linux, de modo que a comunicação de RPC na porta 135 é redirecionada para o SQL Server **network.rpcport**. Mecanismo de configuração do encaminhamento de porta em distribuição diferente pode ser diferente. Em distribuições que não usam o serviço firewalld, regras de iptable são um mecanismo eficiente para fazer isso. Exemplo de tal distrubution são Ubuntu 16.04 e v12 SUSE Enterprise Linux. As regras de iptable não podem persistir durante as reinicializações, portanto, os comandos a seguir também fornecem instruções para restaurar as regras após uma reinicialização.

1. Crie regras de roteamento para a porta 135. No exemplo a seguir, a porta 135 é direcionada para a porta RPC, 13500, definida na seção anterior. Substitua `<ipaddress>` com o endereço IP do seu servidor.

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   O `--comment RpcEndPointMapper` parâmetro nos comandos anteriores ajuda a gerenciar essas regras em comandos posteriores.

2. Exiba as regras de roteamento que você criou com o seguinte comando:

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. Salve as regras de roteamento em um arquivo em seu computador.

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. Para recarregar as regras após uma reinicialização, adicione o seguinte comando para `/etc/rc.local` (para Ubuntu ou RHEL) ou `/etc/init.d/after.local` (para o SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

O **salvar iptables** e **iptables restauração** comandos fornecem um mecanismo básico para salvar e restaurar iptables entradas. Dependendo de sua distribuição do Linux, lá pode ser mais avançado ou automatizado opções disponíveis. Por exemplo, uma alternativa de Ubuntu é o **iptables persistente** pacote para tornar as entradas persistente. 

Em distribuições que usam o serviço firewalld, o mesmo serviço pode ser usado para ambos os abrindo a porta no servidor e o encaminhamento de porta interno. Por exemplo, no Red Hat Enterprise Linux, você deve usar o serviço firewalld (por meio do utilitário de configuração de firewall-cmd com - Adicionar-forward-porta ou opções semelhantes) para criar e gerenciar regras em vez de usar iptables de encaminhamento de porta persistente.

```bash
firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
```

> [!IMPORTANT]
> As etapas anteriores supõem que um endereço IP fixo. Se o endereço IP para sua instância do SQL Server for alterado (devido a intervenção manual ou DHCP), remova e recrie as regras de roteamento se eles foram criados com iptables. Se você precisar recriar ou excluir regras de roteamentos existentes, você pode usar o comando a seguir para remover o antigo `RpcEndPointMapper` regras:
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

## <a name="verify"></a>Verifique se

Neste ponto, o SQL Server deve ser capaz de participar de transações distribuídas. Para verificar se o SQL Server está escutando, execute as **netstat** comando (se você estiver usando o RHEL, você talvez precise instalar primeiro o **net-tools** pacote):

```bash
sudo netstat -tulpn | grep sqlservr
```

Você deve ver saídas semelhantes ao seguinte:

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

No entanto, após uma reinicialização do SQL Server não inicia escutando a **servertcpport** até que a transação distribuída do primeiro. Nesse caso, você não verá escutando na porta 51999 neste exemplo até que a primeira transação distribuída do SQL Server.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o SQL Server no Linux, consulte [SQL Server no Linux](sql-server-linux-overview.md).
