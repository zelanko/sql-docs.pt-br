---
title: Solução de problemas de contêineres do SQL Server no Docker
description: Explore as diferentes técnicas de solução de problemas que você pode usar para resolver erros comuns vistos durante o uso de contêineres do Docker no Linux com imagens do SQL Server
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 0a58ad0e4271833c7aef24333b14a61ef80a16c9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511551"
---
# <a name="troubleshooting-sql-server-docker-containers"></a>Solução de problemas de contêineres do SQL Server no Docker

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo aborda os erros comuns vistos durante a implantação e o uso de contêineres do SQL Server no Docker e fornece técnicas de solução de problemas para ajudar a resolver o problema.

## <a name="docker-command-errors"></a>Erros de comando do Docker

Se você receber erros para qualquer comando `docker`, verifique se o serviço do Docker está em execução e tente executar com permissões elevadas.

Por exemplo, no Linux, você pode receber o seguinte erro ao executar comandos `docker`:

```output
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se você receber esse erro no Linux, tente executar os mesmos comandos precedidos com `sudo`. Se isso falhar, verifique se o serviço do Docker está em execução e inicie-o, se necessário.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

No Windows, verifique se você está iniciando o PowerShell ou o prompt de comando como Administrador.

## <a name="sql-server-container-startup-errors"></a>Erros de inicialização do contêiner do SQL Server

Se a execução do contêiner do SQL Server falhar, tente os seguintes testes:

- Se você receber um erro como `failed to create endpoint CONTAINER_NAME on network bridge. Error starting proxy: listen tcp 0.0.0.0:1433 bind: address already in use.`, isso indicará que você está tentando mapear a porta de contêiner 1433 para uma porta que já está em uso. Isso poderá acontecer se você estiver executando o SQL Server localmente no computador host. Isso também poderá acontecer se você iniciar dois contêineres de SQL Server e tentar mapeá-los para a mesma porta de host. Se isso acontecer, use o parâmetro `-p` para mapear a porta de contêiner 1433 para uma porta de host diferente. Por exemplo: 

    <!--SQL Server 2017 on Linux -->
    ::: moniker range="= sql-server-linux-2017 || = sql-server-2017"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end
    
    <!--SQL Server 2019 on Linux-->
    ::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"
    
    ::: zone pivot="cs1-bash"
    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-powershell"
    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: zone pivot="cs1-cmd"
    ```cmd
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-latest`.
    ```
    ::: zone-end
    
    ::: moniker-end

- Se você receber um erro como `Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied` ao tentar iniciar um contêiner, adicione o usuário ao grupo do Docker no Ubuntu. Em seguida, faça logoff e logon novamente, pois essa alteração afetará novas sessões. 

   ```bash
    usermod -aG docker $USER
   ```

- Verifique se há alguma mensagem de erro do contêiner.

   ```bash
   docker logs e69e056c702d
   ```

- Verifique se você atende aos requisitos mínimos de memória e disco especificados na seção [pré-requisitos](quickstart-install-connect-docker.md#requirements) do artigo de início rápido.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo sqlservr no contêiner é executado como raiz.

- Se o contêiner do SQL Server no Docker for encerrado imediatamente após a inicialização, verifique os logs do Docker. Se você estiver usando o PowerShell no Windows com o comando `docker run`, use aspas duplas em vez de aspas simples. Com o PowerShell Core, use aspas simples.

- Examine a [configuração do SQL Server e os logs de erro](#errorlogs).

## <a name="enable-dump-captures"></a>Habilitar capturas de despejo

Se o processo do SQL Server estiver falhando dentro do contêiner, você deverá criar um novo contêiner com **SYS_PTRACE** habilitado. Isso adiciona a funcionalidade do Linux para rastrear um processo, o que é necessário para criar um arquivo de despejo em uma exceção. O arquivo de despejo pode ser usado pelo suporte para ajudar a solucionar o problema. O comando de execução do Docker a seguir habilita essa funcionalidade.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -e 'MSSQL_PID=Developer' --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="sql-server-connection-failures"></a>Falhas de conexão do SQL Server

Se você não conseguir conectar-se à instância do SQL Server em execução no seu contêiner, tente os seguintes testes:

- Verifique se o contêiner do SQL Server está em execução examinando a coluna **STATUS** da saída `docker ps -a`. Caso contrário, use `docker start <Container ID>` para iniciá-lo.

- Se você mapeou para uma porta de host não padrão (não 1433), verifique se está especificando a porta na cadeia de conexão. Você pode ver o mapeamento de porta na coluna **PORTAS** da saída `docker ps -a`. Por exemplo, o comando a seguir conecta o sqlcmd a um contêiner escutando na porta 1401:

    ::: zone pivot="cs1-bash"
    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```
    ::: zone-end

    ::: zone pivot="cs1-powershell"
    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

    ::: zone pivot="cs1-cmd"
    ```cmd
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```
    ::: zone-end

- Se você usou `docker run` com um volume de dados mapeado existente ou um contêiner de volume de dados, SQL Server ignora o valor de `SA_PASSWORD`. Em vez disso, a senha de usuário do SA pré-configurada é usada dos dados do SQL Server no volume de dados ou no contêiner de volume de dados. Verifique se você está usando a senha SA associada aos dados aos quais você está anexando.

- Examine a [configuração do SQL Server e os logs de erro](#errorlogs).

## <a name="sql-server-availability-groups"></a>Grupos de Disponibilidade de SQL Server

Se você estiver usando o Docker com Grupos de Disponibilidade do SQL Server, haverá dois requisitos adicionais.

- Mapeie a porta usada para comunicação de réplica (padrão 5022). Por exemplo, especifique `-p 5022:5022` como parte do comando `docker run`.

- Defina explicitamente o nome do host do contêiner com o parâmetro `-h YOURHOSTNAME` do comando `docker run`. Esse nome de host é usado quando você configura seu grupo de disponibilidade. Se você não o especificar com `-h`, o padrão será a **ID do contêiner**.

## <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> Configuração e logs de erro do SQL Server

Você pode examinar a configuração e os logs de erro do SQL Server em **/var/opt/mssql/log**. Se o contêiner não estiver em execução, primeiro inicie-o. Em seguida, use um prompt de comando interativo para inspecionar os logs. Obtenha a ID do contêiner executando o comando `docker ps`.

```bash
docker start <ContainerID>
docker exec -it <ContainerID> "bash"
```

Na sessão de Bash dentro de seu contêiner, execute os seguintes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se você montou um diretório de host para **/var/opt/mssql** quando criou o contêiner, poderá procurar no subdiretório de **log** no caminho mapeado no host.

## <a name="execute-commands-in-a-container"></a>Executar comandos em um contêiner

Se você tiver um contêiner em execução, poderá executar comandos dentro do contêiner de um terminal de host.

Para obter a ID do contêiner, execute:

```bash
docker ps -a
```

Para iniciar um terminal de Bash na execução do contêiner:

```bash
docker exec -it <Container ID> /bin/bash
```

Agora, você pode executar comandos como se estivesse executando-os no terminal dentro do contêiner. Quando terminar, digite `exit`. Isso é encerrado na sessão de comando interativo, mas o contêiner continua a ser executado.

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- Obtenha uma introdução às imagens de contêiner do SQL Server 2017 no Docker com o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-2017).

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- Comece a usar as imagens de contêiner do SQL Server 2019 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-ver15).

::: moniker-end

- [Implantar contêineres do SQL Server no Docker e conectar-se a eles](sql-server-linux-docker-container-deployment.md)

- [Referenciar uma configuração e uma personalização adicionais em contêineres do Docker](sql-server-linux-docker-container-configure.md)

- [Proteger contêineres do SQL Server no Docker](sql-server-linux-docker-container-security.md)