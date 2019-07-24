---
title: Definir configurações de SQL Server com variáveis de ambiente
description: Este artigo descreve como usar variáveis de ambiente para definir configurações específicas de SQL Server 2017 no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419253"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Definir configurações de SQL Server com variáveis de ambiente no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Você pode usar várias variáveis de ambiente diferentes para configurar o SQL Server 2017 no Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Você pode usar várias variáveis de ambiente diferentes para configurar a versão prévia SQL Server 2019 no Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end

- Para configurar a instalação inicial com `mssql-conf setup` o comando.
- Para configurar um novo [contêiner de SQL Server no Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se você precisar configurar SQL Server após esses cenários de instalação, consulte [configurar SQL Server em Linux com a ferramenta MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variáveis de ambiente

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variável de ambiente | Descrição |
|-----|-----|
| **ACCEPT_EULA** | Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário do SA. |
| **MSSQL_PID** | Defina a edição de SQL Server ou a chave do produto (Product Key). Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto**</br></br>Se você especificar uma chave do produto (Product Key), ela deverá estar no formato # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, em que ' # ' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID de idioma a ser usada para SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define o agrupamento padrão para SQL Server. Isso substitui o mapeamento padrão da ID de idioma (LCID) no agrupamento. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que SQL Server pode usar. Por padrão, é 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP que SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Defina o endereço IP. Atualmente, o endereço IP deve ser o estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina o local do diretório de backup padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório no qual os arquivos de dados do novo SQL Server Database (. MDF) são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório onde os novos arquivos de log de banco de dados do SQL Server (. ldf) são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que SQL Server depositará os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilitar grupo de disponibilidade. Por exemplo, ' 1 ' está habilitado e ' 0 ' está desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilitar SQL Server Agent. Por exemplo, ' true ' está habilitado e ' false ' está desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define o local do arquivo de dados do banco de dados mestre. Deve ser nomeado **Master. MDF** até a primeira execução de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define o local do arquivo de log do banco de dados mestre. Deve ser nomeado **mastlog. ldf** até a primeira execução de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define o local dos arquivos de log de erros. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variável de ambiente | Descrição |
|-----|-----|
| **ACCEPT_EULA** | Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário do SA. |
| **MSSQL_PID** | Defina a edição de SQL Server ou a chave do produto (Product Key). Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto**</br></br>Se você especificar uma chave do produto (Product Key), ela deverá estar no formato # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, em que ' # ' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID de idioma a ser usada para SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define o agrupamento padrão para SQL Server. Isso substitui o mapeamento padrão da ID de idioma (LCID) no agrupamento. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que SQL Server pode usar. Por padrão, é 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP que SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Defina o endereço IP. Atualmente, o endereço IP deve ser o estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina o local do diretório de backup padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório no qual os arquivos de dados do novo SQL Server Database (. MDF) são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório onde os novos arquivos de log de banco de dados do SQL Server (. ldf) são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que SQL Server depositará os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilitar grupo de disponibilidade. Por exemplo, ' 1 ' está habilitado e ' 0 ' está desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilitar SQL Server Agent. Por exemplo, ' true ' está habilitado e ' false ' está desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define o local do arquivo de dados do banco de dados mestre. Deve ser nomeado **Master. MDF** até a primeira execução de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define o local do arquivo de log do banco de dados mestre. Deve ser nomeado **mastlog. ldf** até a primeira execução de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define o local dos arquivos de log de erros. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usar com a configuração inicial

Este exemplo é `mssql-conf setup` executado com variáveis de ambiente configuradas. As seguintes variáveis de ambiente são especificadas:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** especifica a edição de desenvolvedor licenciada gratuitamente do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que SQL Server escuta em 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Usar com o Docker

Este comando do Docker de exemplo usa as seguintes variáveis de ambiente para criar um novo contêiner de SQL Server:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** especifica a edição de desenvolvedor licenciada gratuitamente do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que SQL Server escuta em 1234. Isso significa que, em vez de mapear a porta 1433 (padrão) para uma porta de host, a porta TCP personalizada `-p 1234:1234` deve ser mapeada com o comando neste exemplo.

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
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

Se você estiver executando o Docker no Windows, use a seguinte sintaxe com aspas duplas:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para outras configurações de SQL Server não listadas aqui, consulte [configurar SQL Server em Linux com a ferramenta MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

Para obter mais informações sobre como instalar e executar o SQL Server em Linux, consulte [instalar SQL Server em Linux](sql-server-linux-setup.md).
