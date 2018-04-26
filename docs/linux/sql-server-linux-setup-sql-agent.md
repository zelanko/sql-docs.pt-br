---
title: Instalar o agente do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como instalar o SQL Server Agent no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 1135e7844515ffd051e937c7804c654b3143ac36
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Instalar o agente do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 O [do SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) executa trabalhos agendados do SQL Server. Começando com o SQL Server de 2017 CU4, SQL Server Agent está incluído com o **mssql server** do pacote e é desabilitada por padrão. Para obter informações sobre os recursos com suporte para esta versão do SQL Server Agent juntamente com informações de versão, consulte o [notas de versão](sql-server-linux-release-notes.md).

 Instalar/ativar o SQL Server Agent:
- [Para versões de 2017 CU4 e superior, habilitar o SQL Server Agent](#EnableAgentAfterCU4)
- [Para versões de 2017 CU3 e abaixo, instale o SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">Para versões de 2017 CU4 e superior, habilitar o SQL Server Agent</a>

 Para habilitar o SQL Server Agent, siga as etapas abaixo.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Se você estiver atualizando de 2017 CU3 ou abaixo com o agente instalado, o SQL Server Agent serão automaticamente habilitados e a anterior pacotes de agente serão desinstalados.  

## <a name="InstallAgentBelowCU4">Para versões de 2017 CU3 e abaixo, instale o SQL Server Agent</a>

> [!NOTE]
> As instruções de instalação abaixo se aplicam ao SQL Server versões 2017 CU3 e abaixo. Antes de instalar o SQL Server Agent, primeiro [instalar o SQL Server 2017](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa quando você instala o **mssql-server-agente** pacote.

Instale o SQL Server Agent para sua plataforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Instalar em RHEL</a>

Use as etapas a seguir para instalar o **mssql-server-agente** no Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agente** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Instalar no Ubuntu</a>

Use as etapas a seguir para instalar o **mssql-server-agente** no Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agente** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Instalar em SLES</a>

Use as etapas a seguir para instalar o **mssql-server-agente** no SUSE Linux Enterprise Server. 

Instalar **mssql de servidor de agente** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Se você já tiver **mssql-server-agente** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o SQL Server Agent para criar, agendar e executar trabalhos, consulte [executar um trabalho do SQL Server Agent no Linux](sql-server-linux-run-sql-server-agent-job.md).
