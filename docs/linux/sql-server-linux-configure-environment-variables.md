---
title: Configurar o SQL Server com variáveis de ambiente | Microsoft Docs
description: Este artigo descreve como usar variáveis de ambiente para configurar as configurações específicas de 2017 do SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: 09d75b1505594397b619e71d78f9a32f5e293426
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configurar o SQL Server com variáveis de ambiente no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode usar diversas variáveis de ambiente diferentes para configurar o SQL Server 2017 no Linux. Essas variáveis são usadas em dois cenários:

- Para configurar a instalação inicial com o `mssql-conf setup` comando.
- Para configurar um novo [contêiner do SQL Server no Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se você precisa configurar o SQL Server após esses cenários de instalação, consulte [configurar o SQL Server no Linux com a ferramenta mssql conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variáveis de ambiente

| Variável de ambiente | Description |
|-----|-----|
| **ACCEPT_EULA** | Aceite o contrato de licença do SQL Server quando definido como qualquer valor (por exemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configure a senha do usuário. |
| **MSSQL_PID** | Defina a chave de produto ou a edição do SQL Server. Os valores possíveis incluem: </br></br>**Evaluation**</br>**Desenvolvedor**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Uma chave do produto**</br></br>Se especificar uma chave de produto, ela deve ser na forma de # # #-# # #-# # #-# # #-# # #, onde '#' é um número ou uma letra.|
| **MSSQL_LCID** | Define a ID do idioma a ser usado para o SQL Server. Por exemplo, 1036 é francês. |
| **MSSQL_COLLATION** | Define o agrupamento padrão do SQL Server. Isso substitui o mapeamento padrão de id de idioma (LCID) para agrupamento. |
| **MSSQL_MEMORY_LIMIT_MB** | Define a quantidade máxima de memória (em MB) que pode usar o SQL Server. Por padrão é 80% da memória física total. |
| **MSSQL_TCP_PORT** | Configure a porta TCP que o SQL Server escuta (padrão 1433). |
| **MSSQL_IP_ADDRESS** | Defina o endereço IP. Atualmente, o endereço IP deve ser IPv4 estilo (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Defina o local do diretório de backup padrão. |
| **MSSQL_DATA_DIR** | Altere o diretório onde os arquivos de dados de banco de dados do SQL Server de novo (. mdf) são criados. |
| **MSSQL_LOG_DIR** | Altere o diretório em que os novos arquivos de log (. ldf) do banco de dados do SQL Server são criados. |
| **MSSQL_DUMP_DIR** | Altere o diretório em que a do SQL Server será colocar os despejos de memória e outros arquivos de solução de problemas por padrão. |
| **MSSQL_ENABLE_HADR** | Habilitar o grupo de disponibilidade. Por exemplo, '1' está habilitada e '0' está desabilitado |
| **MSSQL_AGENT_ENABLED** | Habilite o SQL Server Agent. Por exemplo, 'true' está habilitada e 'false' está desabilitado. Por padrão, o agente está desabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Define o local do arquivo de dados do banco de dados mestre. |
| **MSSQL_MASTER_LOG_FILE** | Define o local do arquivo de log do banco de dados mestre. |
| **MSSQL_ERROR_LOG_FILE** | Define o local dos arquivos de log de erros. |


## <a name="example-initial-setup"></a>Exemplo: instalação inicial

Este exemplo executa `mssql-conf setup` com configurado variáveis de ambiente. As seguintes variáveis de ambiente especificadas:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** Especifica o Licenciado livremente Developer Edition do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que o SQL Server escuta 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>Exemplo: Docker

Este exemplo de comando do docker usa as seguintes variáveis de ambiente para criar um novo contêiner de 2017 do SQL Server:

- **ACCEPT_EULA** aceita o contrato de licença de usuário final.
- **MSSSQL_PID** Especifica o Licenciado livremente Developer Edition do SQL Server para uso de não produção.
- **MSSQL_SA_PASSWORD** define uma senha forte.
- **MSSQL_TCP_PORT** define a porta TCP que o SQL Server escuta 1234. Isso significa que, em vez de mapeamento a porta 1433 (padrão) para uma porta de host, a porta TCP personalizada deve ser mapeada com o `-p 1234:1234` comando neste exemplo.

Se você estiver executando o Docker no Linux/macOS, use a seguinte sintaxe com aspas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

Se você estiver executando o Docker no Windows, use a seguinte sintaxe com aspas duplas:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> O processo para executar edições de produção em contêineres é um pouco diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production).

## <a name="next-steps"></a>Próximas etapas

Para outras configurações do SQL Server não está listadas aqui, consulte [configurar o SQL Server no Linux com a ferramenta mssql conf](sql-server-linux-configure-mssql-conf.md).

Para obter mais informações sobre como instalar e executar o SQL Server no Linux, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).
