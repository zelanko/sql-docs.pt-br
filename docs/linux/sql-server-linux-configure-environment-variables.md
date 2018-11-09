---
title: Configurar configurações do SQL Server com variáveis de ambiente | Microsoft Docs
description: Este artigo descreve como usar variáveis de ambiente para configurar as configurações específicas do SQL Server 2017 no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 87e4d1ed1bdb1ce78e2f45fcb49019175fcdfefd
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269689"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configurar configurações do SQL Server com variáveis de ambiente no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Você pode usar diversas variáveis de ambiente diferentes para configurar o SQL Server 2017 no Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Você pode usar diversas variáveis de ambiente diferentes para configurar a visualização de 2019 do SQL Server no Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end

- Para configurar a instalação inicial com o `mssql-conf setup` comando.
- Para configurar uma nova [contêiner do SQL Server no Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se você precisar configurar o SQL Server após a esses cenários de instalação, consulte [configurar o SQL Server no Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variáveis de ambiente

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variável de ambiente | Description |
|-----|-----|
| **ACCEPT_EULA** | Aceite o contrato de licença do SQL Server quando definido como qualquer valor (por exemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário de SA. |
| **MSSQL_PID** | Defina a chave de produto ou edição do SQL Server. Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto**</br></br>Se especificar uma chave de produto, ele deverá ser na forma de # # #-# # #-# # #-# # #-# # #, onde '#' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID do idioma a ser usado para o SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define o agrupamento padrão do SQL Server. Isso substitui o mapeamento padrão de id de idioma (LCID) para agrupamento. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que pode usar o SQL Server. Por padrão é 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP que o SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Defina o endereço IP. Atualmente, o endereço IP deve ser o estilo do IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina o local do diretório de backup padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório onde os arquivos de dados de banco de dados do SQL Server de novo (. mdf) são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório onde os novos arquivos de log (. ldf) do banco de dados do SQL Server são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que a do SQL Server será depositar os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilitar o grupo de disponibilidade. Por exemplo, '1' está habilitado e o '0' está desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilite o SQL Server Agent. Por exemplo, 'true' está habilitado e 'false' está desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define o local do arquivo de dados banco de dados mestre. Deve ser nomeado **Master. mdf** até que a primeira execução do SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define o local do arquivo de log de banco de dados mestre. Deve ser nomeado **Mastlog** até que a primeira execução do SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define o local dos arquivos de log de erros. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variável de ambiente | Description |
|-----|-----|
| **ACCEPT_EULA** | Aceite o contrato de licença do SQL Server quando definido como qualquer valor (por exemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário de SA. |
| **MSSQL_PID** | Defina a chave de produto ou edição do SQL Server. Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto**</br></br>Se especificar uma chave de produto, ele deverá ser na forma de # # #-# # #-# # #-# # #-# # #, onde '#' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID do idioma a ser usado para o SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define o agrupamento padrão do SQL Server. Isso substitui o mapeamento padrão de id de idioma (LCID) para agrupamento. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que pode usar o SQL Server. Por padrão é 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP que o SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Defina o endereço IP. Atualmente, o endereço IP deve ser o estilo do IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina o local do diretório de backup padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório onde os arquivos de dados de banco de dados do SQL Server de novo (. mdf) são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório onde os novos arquivos de log (. ldf) do banco de dados do SQL Server são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que a do SQL Server será depositar os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilitar o grupo de disponibilidade. Por exemplo, '1' está habilitado e o '0' está desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilite o SQL Server Agent. Por exemplo, 'true' está habilitado e 'false' está desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define o local do arquivo de dados banco de dados mestre. Deve ser nomeado **Master. mdf** até que a primeira execução do SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define o local do arquivo de log de banco de dados mestre. Deve ser nomeado **Mastlog** até que a primeira execução do SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define o local dos arquivos de log de erros. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usar com a instalação inicial

Este exemplo executa `mssql-conf setup` com configurado variáveis de ambiente. As seguintes variáveis de ambiente são especificadas:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** Especifica a licenciadas gratuitamente Developer Edition do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que o SQL Server escuta para 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Use com o Docker

Este exemplo de comando do docker usa as seguintes variáveis de ambiente para criar um novo contêiner do SQL Server:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** Especifica a licenciadas gratuitamente Developer Edition do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que o SQL Server escuta para 1234. Isso significa que, em vez de mapeamento a porta 1433 (padrão) para uma porta de host, a porta TCP personalizada deve ser mapeada com o `-p 1234:1234` comando neste exemplo.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Se você estiver executando o Docker no Linux/macOS, use a seguinte sintaxe com aspas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Se você estiver executando o Docker no Windows, use a seguinte sintaxe com aspas duplas:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> O processo para executar edições de produção em contêineres é um pouco diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Se você estiver executando o Docker no Linux/macOS, use a seguinte sintaxe com aspas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

Se você estiver executando o Docker no Windows, use a seguinte sintaxe com aspas duplas:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para outras configurações do SQL Server não está listadas aqui, consulte [configurar o SQL Server no Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

Para obter mais informações sobre como instalar e executar o SQL Server no Linux, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).
