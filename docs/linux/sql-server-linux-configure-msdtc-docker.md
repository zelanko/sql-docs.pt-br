---
title: Como usar transações distribuídas com o SQL Server no Docker | Microsoft Docs
description: Este artigo explica como usar Dprovides um passo a passo para configurar o MSDTC no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3242f0d074dc3c2f33fc83de4604a20bfdcbd64a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049387"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>Como usar transações distribuídas com o SQL Server no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o SQL Server no Docker para transações distribuídas.

Imagens de contêiner a partir da versão prévia do SQL Server 2019, dão suporte para o Microsoft Distributed Transaction Coordinator (MSDTC) exigido para transações distribuídas. Para entender os requisitos de comunicações para o MSDTC, consulte [como configurar o Microsoft Distributed Transaction coordenador (MSDTC) no Linux](sql-server-linux-configure-msdtc.md). Este artigo explica os requisitos especiais e os cenários relacionados a contêineres do Docker do SQL Server.

## <a name="configuration"></a>Configuração

Para habilitar a transação do MSDTC em contêineres do docker, você deve definir duas novas variáveis de ambiente:

- **MSSQL_RPC_PORT**: a porta TCP que o serviço de mapeador de ponto de extremidade RPC associa a e escuta.  
- **MSSQL_DTC_TCP_PORT** a porta que o serviço MSDTC está configurado para escutar em.

### <a name="pull-and-run"></a>Efetuar pull e executar

O exemplo a seguir mostra como usar essas variáveis de ambiente para efetuar pull e executar um contêiner configurado para o MSDTC. Isso permite que ele se comunique com qualquer aplicativo em todos os hosts.

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=13500' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 13500:13500 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

O comando a seguir mostra o mesmo comando para o Docker no Windows no PowerShell:

```PowerShell
docker run `
   -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -e "MSSQL_RPC_PORT=13500" -e "MSSQL_DTC_TCP_PORT=51000" `
   -p 51433:1433 -p 13500:13500 -p 51000:51000 `
   -d "mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu"
```

Neste comando, o **mapeador de ponto de extremidade RPC** serviço foi associado à porta 13500 e o **MSDTC** serviço foi associado à porta 51000 dentro da rede virtual do docker. A comunicação do SQL Server TDS ocorre na porta 1433 dentro da rede virtual do docker. Essas portas foram expostas externamente ao host como a porta do protocolo TDS 51433, porta de mapeador de ponto de extremidade RPC 13500 e porta do MSDTC 51000.

> [!NOTE]
> O mapeador de ponto de extremidade de RPC e a porta do MSDTC não precisa ser o mesmo no host e o contêiner. Portanto, enquanto a porta do mapeador de ponto de extremidade RPC foi configurada para ser 13500 no contêiner, ele poderia ser mapeado para a porta 13501 ou qualquer outra porta disponível no servidor host.

## <a name="configure-the-firewall"></a>Configurar o firewall

Para se comunicar com e através do host, você também deve configurar o firewall no servidor de host para os contêineres. Abra o firewall para todos os de portas que o docker contêiner expõe a comunicação externa. No exemplo anterior, isso seria portas 135, 51433 e 51000. Essas são as portas no próprio host e não as portas que são mapeados no contêiner. Portanto, se o ponto de extremidade RPC 51000 de porta de mapeador de recipiente foi mapeada para a porta de host 51001, em seguida, a porta 51001 (não 51000) deve ser aberto no firewall para comunicação com o host.  

O exemplo a seguir mostra como criar essas regras no Ubuntu.

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

O exemplo a seguir mostra como isso pode ser feito no Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>Configurar o roteamento de porta no host

Se o contêiner do docker participa de transações distribuídas com um servidor externo para o host, o host deve configurar o roteamento de porta. Para obter mais informações, consulte [configurar o roteamento de porta](sql-server-linux-configure-msdtc.md#configure-port-routing).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o MSDTC no Linux, consulte [como configurar o Microsoft Distributed Transaction coordenador (MSDTC) no Linux](sql-server-linux-configure-msdtc.md).