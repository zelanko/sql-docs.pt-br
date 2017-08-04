---
title: Instalar o agente do SQL Server no Linux | Microsoft Docs
description: "Este tópico descreve como instalar o SQL Server Agent no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 1f6f741a87a13e5b5bc8ba83741e86b065378bad
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-agent-on-linux"></a>Instalar o agente do SQL Server no Linux

As etapas a seguir instala o SQL Server Agent (**mssql-server-agente**) no Linux. O [do SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) executa trabalhos agendados do SQL Server. Para obter informações sobre os recursos com suporte para esta versão do SQL Server Agent, consulte o [notas de versão](sql-server-linux-release-notes.md).

> [!NOTE]
> Antes de instalar o SQL Server Agent, primeiro [instalar o SQL Server RC2 +](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa quando você instala o **mssql-server-agente** pacote.

Instale o SQL Server Agent para sua plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Instalar em RHEL</a>

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

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no tópico [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Instalar no Ubuntu</a>

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

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no tópico [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Instalar em SLES</a>

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

Se você precisar de uma instalação offline, localize o download do pacote do SQL Server Agent no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no tópico [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o SQL Server Agent para criar, agendar e executar trabalhos, consulte [executar um trabalho do SQL Server Agent no Linux](sql-server-linux-run-sql-server-agent-job.md).

