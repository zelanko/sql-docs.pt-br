---
title: Configurar e personalizar contêineres do SQL Server no Docker
description: Entenda as diferentes maneiras de personalizar os contêineres do SQL Server no Docker e como configurá-los de acordo com as suas necessidades
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 '
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: fbae468dfd0f68f2765dc781ad710e9b8525aeaf
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489886"
---
# <a name="configure-and-customize-sql-server-docker-containers"></a>Configurar e personalizar contêineres do SQL Server no Docker

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo explica como configurar e personalizar contêineres do SQL Server no Docker, persistir os dados, mover arquivos em contêineres e alterar as configurações padrão.

## <a name="create-a-customized-container"></a><a id="customcontainer"></a> Criar um contêiner personalizado

É possível criar seu próprio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para criar um contêiner personalizado do SQL Server. Para obter mais informações, confira [uma demonstração que combina o SQL Server com um aplicativo do Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Se você criar seu próprio Dockerfile, esteja ciente do processo em primeiro plano, pois esse processo controla a vida útil do contêiner. Se ele for encerrado, o contêiner será desligado. Por exemplo, se você quiser executar um script e iniciar o SQL Server, verifique se o processo do SQL Server é o comando mais à direita. Todos os outros comandos são executados em segundo plano. O comando a seguir ilustra isso dentro de um Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se você inverter os comandos no exemplo anterior, o contêiner será desligado quando o script do-my-sql-commands.sh for concluído.

## <a name="persist-your-data"></a><a id="persist"></a> Manter seus dados

Sua configuração do SQL Server muda e os arquivos de banco de dados são mantidos no contêiner mesmo que você reinicie o contêiner com `docker stop` e `docker start`. No entanto, se você remover o contêiner com `docker rm`, tudo no contêiner será excluído, incluindo o SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para persistir seus arquivos de banco de dados mesmo que os contêineres associados sejam excluídos.

> [!IMPORTANT]
> Para o SQL Server, é essencial que você compreenda a persistência de dados no Docker. Além da discussão nesta seção, confira a documentação do Docker sobre [como gerenciar dados em contêineres do Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório de host como volume de dados

A primeira opção é montar um diretório em seu host como um volume de dados em seu contêiner. Para fazer isso, use o comando `docker run` com o sinalizador `-v <host directory>:/var/opt/mssql`. Isso permite que os dados sejam restaurados entre as execuções do contêiner.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

Essa técnica também permite que você compartilhe e exiba os arquivos no host fora do Docker.

> [!IMPORTANT]
> Atualmente, o mapeamento de volume do host para o **Docker no Windows** não dá suporte ao mapeamento do diretório `/var/opt/mssql` completo. No entanto, você pode mapear um subdiretório, como `/var/opt/mssql/data` para o computador host.
>
> No momento, não há suporte para o mapeamento de volume do host no **Docker no Mac** com a imagem do SQL Server em Linux. Use contêineres de volume de dados em vez disso. Essa restrição é específica do diretório `/var/opt/mssql`. A leitura de um diretório montado funciona bem. Por exemplo, você pode montar um diretório de host usando -v no Mac e restaurar um backup de um arquivo .bak que reside no host.

### <a name="use-data-volume-containers"></a>Usar contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados especificando um nome de volume, em vez de um diretório de host com o parâmetro `-v`. O exemplo a seguir cria um volume de dados compartilhado chamado **sqlvolume**.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

> [!NOTE]
> Essa técnica para criar implicitamente um volume de dados no comando executar não funciona com versões anteriores do Docker. Nesse caso, use as etapas explícitas descritas na documentação do Docker, [Como criar e montar um contêiner de volume de dados](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Mesmo que você pare e remova esse contêiner, o volume de dados persiste. Você pode exibi-lo com o comando `docker volume ls`.

```command
docker volume ls
```

Se você criar outro contêiner com o mesmo nome de volume, o novo contêiner usará os mesmos dados do SQL Server contidos no volume.

Para remover um contêiner de volume de dados, use o comando `docker volume rm`.

> [!WARNING]
> Se você excluir o contêiner do volume de dados, qualquer dado do SQL Server no contêiner será excluído *permanentemente*.

### <a name="backup-and-restore"></a>Backup e restauração

Além dessas técnicas de contêiner, você também pode usar as técnicas padrão de backup e restauração do SQL Server. Você pode usar arquivos de backup para proteger seus dados ou mover os dados para outra instância do SQL Server. Para obter mais informações, confira [Fazer backup e restauração de bancos de dados do SQL Server em Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se você criar backups, crie ou copie os arquivos de backup fora do contêiner. Caso contrário, se o contêiner for removido, os arquivos de backup também serão excluídos.

## <a name="copy-files-from-a-container"></a>Copiar arquivos de um contêiner

Para copiar um arquivo do contêiner, use o seguinte comando:

```command
docker cp <Container ID>:<Container path> <host path>
```

Obtenha a ID do contêiner executando o comando `docker ps -a`.

**Exemplo:**

::: zone pivot="cs1-bash"
```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```
::: zone-end

## <a name="copy-files-into-a-container"></a>Copiar arquivos para um contêiner

Para copiar um arquivo para o contêiner, use o seguinte comando:

```command
docker cp <Host path> <Container ID>:<Container path>
```

**Exemplo:**

::: zone pivot="cs1-bash"
```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
::: zone-end

## <a name="configure-the-timezone"></a><a id="tz"></a> Configurar o fuso horário

Para executar o SQL Server em um contêiner do Linux com um fuso horário específico, configure a variável de ambiente `TZ`. Para localizar o valor de fuso horário correto, execute o comando `tzselect` de um prompt de Bash do Linux:

```command
tzselect
```

Depois de selecionar o fuso horário, o `tzselect` exibe uma saída semelhante à seguinte:

```output
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Você pode usar essas informações para definir a mesma variável de ambiente em seu contêiner do Linux. O exemplo a seguir mostra como executar o SQL Server em um contêiner no fuso horário `Americas/Los_Angeles`:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'A_PASSWORD=<YourStrong!Passw0rd>' \
-p 1433:1433 --name sql1 \
-e 'TZ=America/Los_Angeles'\
-d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-p 1433:1433 --name sql1 `
-e "TZ=America/Los_Angeles" `
-d mcr.microsoft.com/mssql/server:2017-latest 
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sudo docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-p 1433:1433 --name sql1 ^
-e "TZ=America/Los_Angeles" ^
-d mcr.microsoft.com/mssql/server:2017-latest 
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

::: zone pivot="cs1-bash"
```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="change-the-default-file-location"></a><a id="changefilelocation"></a> Alterar a localização do arquivo padrão

Adicione a variável `MSSQL_DATA_DIR` para alterar o diretório de dados em seu comando `docker run` e, em seguida, monte um volume para esse localização ao qual o usuário do contêiner tem acesso.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=MyStrongPassword' -e 'MSSQL_DATA_DIR=/my/file/path' -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=MyStrongPassword' -e 'MSSQL_DATA_DIR=/my/file/path' -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e 'ACCEPT_EULA=Y' -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- Comece a usar as imagens de contêiner do SQL Server 2017 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-2017&preserve-view=true)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

- Comece a usar as imagens de contêiner do SQL Server 2019 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-ver15)

::: moniker-end

- [Implantar contêineres do SQL Server no Docker e conectar-se a eles](sql-server-linux-docker-container-deployment.md)

- [Solução de problemas de contêineres do SQL Server no Docker](sql-server-linux-docker-container-troubleshooting.md)

- [Proteger contêineres do SQL Server no Docker](sql-server-linux-docker-container-security.md)
