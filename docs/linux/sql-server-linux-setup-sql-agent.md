---
title: Instalar o SQL Server Agent no Linux
description: Este artigo descreve como instalar o SQL Server Agent no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: c27a31a5e6b9ed771df82e942087d7be88270038
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032473"
---
# <a name="install-sql-server-agent-on-linux"></a>Instalar o SQL Server Agent no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 O [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) executa trabalhos do SQL Server agendados. Do SQL Server 2017 CU4 em diante, o SQL Server Agent está incluído no pacote **mssql-server** e está desabilitado por padrão. Para obter informações sobre os recursos compatíveis com esta versão do SQL Server Agent juntamente com as informações sobre a versão, confira as [Notas sobre a versão](sql-server-linux-release-notes.md).

 Instalar/habilitar o SQL Server Agent:
- [Para as versões 2017 CU4 e superiores, habilite o SQL Server Agent](#EnableAgentAfterCU4)
- [Para as versões 2017 CU3 e inferiores, instale o SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">Para as versões 2017 CU4 e superiores, habilite o SQL Server Agent</a>

 Para habilitar o SQL Server Agent, siga as etapas abaixo.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Se você estiver atualizando do 2017 CU3 ou inferior com o Agent instalado, SQL Server Agent será habilitado automaticamente e os pacotes de agente anteriores serão desinstalados.  

## <a name="InstallAgentBelowCU4">Para as versões 2017 CU3 e inferiores, instale o SQL Server Agent</a>

> [!NOTE]
> As instruções de instalação a seguir aplicam-se ao SQL Server Versões 2017 CU3 e inferiores. Antes de instalar o SQL Server Agent, primeiro [instale o SQL Server](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa ao instar o pacote **mssql-server-agent**.

Instale o SQL Server Agent para sua plataforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Instalar no RHEL</a>

Use as seguintes etapas para instalar o **mssql-server-agent** no Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, poderá atualizar para a versão mais recente com os seguintes comandos:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent nas [Notas sobre a versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Instalar no Ubuntu</a>

Use as etapas a seguir para instalar o **mssql-server-agent** no Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, poderá atualizar para a versão mais recente com os seguintes comandos:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent nas [Notas sobre a versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Instalar no SLES</a>

Use as seguintes etapas para instalar o **mssql-server-agent** no SUSE Linux Enterprise Server. 

Instalar o **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, poderá atualizar para a versão mais recente com os seguintes comandos:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent nas [Notas sobre a versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o SQL Server Agent para criar, agendar e executar trabalhos, confira [Executar um trabalho do SQL Server Agent no Linux](sql-server-linux-run-sql-server-agent-job.md).
