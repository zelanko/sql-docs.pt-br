---
title: Como usar transações distribuídas com o SQL Server no Docker
description: Este artigo explica passo a passo como configurar o MSDTC em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 09/25/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 8304bc95a15a5a9cf74ab23bc2e8e47bf7cf72d1
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476054"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Como usar transações distribuídas com o SQL Server no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar os contêineres do Linux do SQL Server no Docker para transações distribuídas.

Do SQL Server 2019 (versão prévia) em diante, as imagens de contêiner são compatíveis com o MSDTC (Coordenador de Transações Distribuídas da Microsoft) necessário para transações distribuídas. Para entender os requisitos de comunicação do MSDTC, confira [Como configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft) em Linux](sql-server-linux-configure-msdtc.md). Este artigo explica os requisitos especiais e os cenários relacionados a contêineres do Docker do SQL Server.

## <a name="configuration"></a>Configuração

Para habilitar a transação MSDTC em contêineres para o Docker, você deve definir duas novas variáveis de ambiente:

- **MSSQL_RPC_PORT**: a porta TCP à qual o serviço mapeador de ponto de extremidade RPC se associa e na qual escuta.  
- **MSSQL_DTC_TCP_PORT**: a porta configurada para o serviço MSDTC escutar.

### <a name="pull-and-run"></a>Efetuar pull e executar

O exemplo a seguir mostra como usar essas variáveis de ambiente para efetuar pull e executar um único contêiner do SQL Server configurado para o MSDTC. Isso permite que ele se comunique com qualquer aplicativo em qualquer host.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-CTP3.2-ubuntu
```

> [!IMPORTANT]
> O comando anterior funciona apenas para o Docker em execução em Linux. Para o Docker em Windows, o host do Windows já escuta na porta 135. Você pode remover o parâmetro `-p 135:135` para o Docker em Windows, mas ele tem algumas limitações. O contêiner resultante então pode não ser usado para transações distribuídas que envolvem o host. Ele pode participar somente de transações distribuídas entre contêineres do Docker no host.

Neste comando, o serviço **Mapeador de Ponto de Extremidade RPC** foi associado à porta 135 e o serviço **MSDTC** foi associado à porta 51000 na rede virtual do Docker. A comutador do TDS do SQL Server ocorre na porta 1433 na rede virtual do Docker. Essas portas foram expostas externamente ao host como a porta 51433 do TDS, a porta 135 do mapeador de ponto de extremidade RPC e porta 51000 do MSDTC.

> [!NOTE]
> A porta do Mapeador de Ponto de Extremidade RPC e do MSDTC não precisam ser iguais no host e no contêiner. Assim, enquanto a porta do Mapeador de Ponto de Extremidade RPC tiver sido configurada para ser a 135 no contêiner, ela poderá ser mapeada para a porta 13501 ou qualquer outra porta disponível no servidor host.

## <a name="configure-the-firewall"></a>Configurar o firewall

Para comunicar-se com e por meio do host, você também deve configurar o firewall no servidor host para os contêineres. Abra o firewall para todas as portas que o contêiner do Docker expõe para comunicação externa. No exemplo anterior, seriam as portas 135, 51433 e 51000. Essas são as portas no próprio host, e não as portas para as quais eles mapeiam no contêiner. Portanto, se a porta 51000 do mapeador de ponto de extremidade RPC do contêiner tiver sido mapeada para a porta de host 51001, a porta 51001 (não 51000) deverá ser aberta no firewall para comunicação com o host.  

O exemplo a seguir mostra como criar essas regras no Ubuntu.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

O exemplo a seguir mostra como isso pode ser feito no RHEL (Red Hat Enterprise Linux):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>Configurar o roteamento de porta no host

No exemplo anterior, como um único contêiner do Docker mapeia a porta 135 RPC para a porta 135 no host, as transações distribuídas com o host agora devem funcionar sem nenhuma configuração adicional. Observe que é possível usar diretamente a porta 135 no contêiner, porque o SQL Server é executado com privilégios elevados em um contêiner. Para o SQL Server fora de um contêiner, uma porta efêmera diferente deve ser usada e o tráfego para a porta 135 então deve ser roteado para essa porta.

No entanto, se você decidir mapear a porta 135 do contêiner para uma porta diferente no host, como a 13500, precisará configurar o roteamento de porta no host. Isso permite que o contêiner do Docker participe de transações distribuídas com o host e com outros servidores externos. Para saber mais, confira [Configurar o roteamento de porta](sql-server-linux-configure-msdtc.md#configure-port-routing).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o MSDTC em Linux, confira [Como configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft) em Linux](sql-server-linux-configure-msdtc.md).
