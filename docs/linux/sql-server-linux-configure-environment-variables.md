---
title: Configurar variáveis de ambiente para o SQL Server em Linux
description: Este artigo descreve como usar variáveis de ambiente para definir configurações específicas do SQL Server 2017 em Linux.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: f768a79512059025ebd6dfe6a6f339175b6149f3
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558365"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Definir configurações do SQL Server com variáveis de ambiente em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Você pode usar diversas variáveis de ambiente diferentes para configurar o SQL Server 2017 em Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Você pode usar diversas variáveis de ambiente diferentes para configurar o SQL Server 2019 em Linux. Essas variáveis são usadas em dois cenários:

::: moniker-end

- Para configurar a instalação inicial com o comando `mssql-conf setup`.
- Para configurar um novo [contêiner do SQL Server no Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se você precisar configurar o SQL Server após esses cenários de instalação, confira [Configurar o SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variáveis de ambiente

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variável de ambiente | DESCRIÇÃO |
|-----|-----|
| **ACCEPT_EULA** | Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário do SA. |
| **MSSQL_PID** | Defina a edição ou a chave do produto (Product Key) do SQL Server. Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto (Product Key)**</br></br>Se você especificar uma chave do produto (Product Key), ela deverá estar no formato #####-#####-#####-#####-#####, em que '#' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID de idioma a ser usada para o SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define a ordenação padrão para o SQL Server. Isso substitui o mapeamento padrão da ID de idioma (LCID) na ordenação. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que o SQL Server pode usar. Por padrão, essa quantidade corresponde a 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP em que o SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Define o endereço IP. Atualmente, o endereço IP deve ser no estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina a localização do diretório de backup Padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório no qual os arquivos de dados (.mdf) do novo banco de dados do SQL Server são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório no qual os arquivos de log (.ldf) do novo banco de dados do SQL Server são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que o SQL Server depositará os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilite o Grupo de Disponibilidade. Por exemplo, '1' é habilitado e '0' ´é desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilite o SQL Server Agent. Por exemplo, 'true' é habilitado e 'false' é desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define a localização do arquivo de dados do banco de dados mestre. Deve chamar-se **master.mdf** até a primeira execução do SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define a localização do arquivo de log do banco de dados mestre. Deve chamar-se **mastlog.ldf** até a primeira execução do SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define a localização dos arquivos de log de erros. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variável de ambiente | DESCRIÇÃO |
|-----|-----|
| **ACCEPT_EULA** | Defina a variável **ACCEPT_EULA** com qualquer valor para confirmar sua aceitação dos [Termos de Licença](https://go.microsoft.com/fwlink/?LinkId=746388). Configuração exigida para a imagem do SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure a senha de usuário do SA. |
| **MSSQL_PID** | Defina a edição ou a chave do produto (Product Key) do SQL Server. Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto (Product Key)**</br></br>Se você especificar uma chave do produto (Product Key), ela deverá estar no formato #####-#####-#####-#####-#####, em que '#' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID de idioma a ser usada para o SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define a ordenação padrão para o SQL Server. Isso substitui o mapeamento padrão da ID de idioma (LCID) na ordenação. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que o SQL Server pode usar. Por padrão, essa quantidade corresponde a 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP em que o SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Define o endereço IP. Atualmente, o endereço IP deve ser no estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina a localização do diretório de backup Padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório no qual os arquivos de dados (.mdf) do novo banco de dados do SQL Server são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório no qual os arquivos de log (.ldf) do novo banco de dados do SQL Server são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que o SQL Server depositará os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilite o Grupo de Disponibilidade. Por exemplo, '1' é habilitado e '0' ´é desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilite o SQL Server Agent. Por exemplo, 'true' é habilitado e 'false' é desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define a localização do arquivo de dados do banco de dados mestre. Deve chamar-se **master.mdf** até a primeira execução do SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Define a localização do arquivo de log do banco de dados mestre. Deve chamar-se **mastlog.ldf** até a primeira execução do SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Define a localização dos arquivos de log de erros. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usar com a configuração inicial

Este exemplo executa o `mssql-conf setup` com variáveis de ambiente configuradas. As seguintes variáveis de ambiente são especificadas:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSQL_PID** especifica a Developer Edition licenciada gratuitamente do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define como 1234 a porta TCP em que o SQL Server escuta.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Usar com o Docker

Este comando do Docker de exemplo usa as seguintes variáveis de ambiente para criar um novo contêiner do SQL Server:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSQL_PID** especifica a Developer Edition licenciada gratuitamente do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define como 1234 a porta TCP em que o SQL Server escuta. Isso significa que, em vez de mapear a porta 1433 (padrão) para uma porta de host, a porta TCP personalizada deve ser mapeada com o comando `-p 1234:1234` neste exemplo.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Se você estiver executando o Docker em Linux/macOS, use a seguinte sintaxe com aspas simples:

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

Se você estiver executando o Docker em Linux/macOS, use a seguinte sintaxe com aspas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

Se você estiver executando o Docker no Windows, use a seguinte sintaxe com aspas duplas:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para outras configurações do SQL Server não listadas aqui, confira [Configurar SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

Para obter mais informações sobre como instalar e executar o SQL Server em Linux, confira [Instalar o SQL Server em Linux](sql-server-linux-setup.md).
