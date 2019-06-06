---
title: Instalar o SQL Server Agent no Linux | Microsoft Docs
description: Este artigo descreve como instalar o SQL Server Agent no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 1cb2a630dab67875db8a9731fe98895599f3290a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705053"
---
# <a name="install-sql-server-agent-on-linux"></a>Instalar o SQL Server Agent no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 O [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) executa trabalhos agendados do SQL Server. Começando com o SQL Server 2017 CU4, SQL Server Agent está incluído com o **mssql-server** empacotar e é desabilitada por padrão. Para obter informações sobre os recursos com suporte para esta versão do SQL Server Agent, juntamente com informações de versão, consulte a [notas de versão](sql-server-linux-release-notes.md).

 Instalar/habilitar o SQL Server Agent:
- [Para versões 2017 CU4 e posterior, habilitar o SQL Server Agent](#EnableAgentAfterCU4)
- [Para versões 2017 CU3 e a seguir, instale o SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">Para versões 2017 CU4 e posterior, habilitar o SQL Server Agent</a>

 Para habilitar o SQL Server Agent, siga as etapas abaixo.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Pacotes de agente serão desinstalados se você estiver atualizando do 2017 CU3 ou abaixo com o agente instalado, SQL Server Agent será automaticamente habilitada e a anterior.  

## <a name="InstallAgentBelowCU4">Para versões 2017 CU3 e a seguir, instale o SQL Server Agent</a>

> [!NOTE]
> As instruções de instalação abaixo se aplicam ao SQL Server versões 2017 CU3 e abaixo. Antes de instalar o SQL Server Agent, primeiro [instalar o SQL Server](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa quando você instala o **mssql-server-agent** pacote.

Instale o SQL Server Agent para sua plataforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Instalar no RHEL</a>

Use as etapas a seguir para instalar o **mssql-server-agent** no Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent na [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Instalar no Ubuntu</a>

Use as etapas a seguir para instalar o **mssql-server-agent** no Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent na [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Instalar no SLES</a>

Use as etapas a seguir para instalar o **mssql-server-agent** no SUSE Linux Enterprise Server. 

Install **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agent** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent na [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [Instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o SQL Server Agent para criar, agendar e executar trabalhos, consulte [executar um trabalho do SQL Server Agent no Linux](sql-server-linux-run-sql-server-agent-job.md).
