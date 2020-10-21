---
title: Configurar o SQL Server Agent no Linux
description: Saiba como habilitar ou instalar o SQL Server Agent em Linux. Do SQL Server 2017 CU4 em diante, o SQL Server Agent está incluído no pacote mssql-server.
author: VanMSFT
ms.author: vanto
ms.date: 12/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 9492b8fcdbcd4ddf930d9f5d1d5ee43415fb2a1c
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115761"
---
# <a name="install-sql-server-agent-on-linux"></a>Instalar o SQL Server Agent no Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo descreve como habilitar ou instalar o SQL Server Agent no Linux.

O [SQL Server Agent](../ssms/agent/sql-server-agent.md) executa trabalhos do SQL Server agendados. Do SQL Server 2017 CU4 em diante, o SQL Server Agent está incluído no pacote **mssql-server** e está desabilitado por padrão. Para obter informações sobre os recursos compatíveis com esta versão do SQL Server Agent juntamente com as informações sobre a versão, confira as [Notas sobre a versão](sql-server-linux-release-notes.md).

## <a name="instructions"></a>Instruções

Antes de usar o SQL Server Agent no Linux, siga estas etapas para habilitá-lo ou instalá-lo.

1. Adicione seu nome de host (com e sem domínio) nos arquivos de `/etc/hosts`. As linhas a seguir mostram um exemplo do formato destas entradas:

   ```bash
   "IP Address" "hostname"
   "IP Address" "hostname.domain.com"
   ```

1. Siga as instruções em uma das seções a seguir com base em sua versão do SQL Server:

   | Versões | Instruções |
   |---|---|
   | SQL Server 2017 CU4 e superior</br>SQL Server 2019 | [Habilitar o SQL Server Agent](#EnableAgentAfterCU4) |
   | SQL Server 2017 CU3 e inferior | [Instalar o SQL Server Agent](#InstallAgentBelowCU4) |

## <a name="enable-the-sql-server-agent"></a><a id="EnableAgentAfterCU4"></a>Habilitar o SQL Server Agent

Para o SQL Server 2019 e o SQL Server 2017 CU4 e superiores, você só precisa habilitar o SQL Server Agent. Você não precisa instalar um pacote separado.

Para habilitar o SQL Server Agent, siga as etapas abaixo.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Se você estiver atualizando do 2017 CU3 ou inferior com o Agent instalado, SQL Server Agent será habilitado automaticamente e os pacotes de agente anteriores serão desinstalados.  

## <a name="install-the-sql-server-agent"></a><a name="InstallAgentBelowCU4"></a>Instalar o SQL Server Agent

Para o SQL Server 2017 CU3 e anteriores, você deve instalar o pacote do SQL Server Agent.

> [!NOTE]
> As instruções de instalação a seguir aplicam-se ao SQL Server Versões 2017 CU3 e inferiores. Antes de instalar o SQL Server Agent, primeiro [instale o SQL Server](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usa ao instar o pacote **mssql-server-agent**.

Instale o SQL Server Agent para sua plataforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name=""></a><a name="RHEL">Instalar no RHEL</a>

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

### <a name=""></a><a name="ubuntu">Instalar no Ubuntu</a>

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

### <a name=""></a><a name="SLES">Instalar no SLES</a>

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