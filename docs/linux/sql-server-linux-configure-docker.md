---
title: Opções de configuração do SQL Server no Docker
description: Explore diferentes maneiras de usar e interagir com as imagens de contêiner do SQL Server 2017 e 2019 no Docker. Isso inclui a persistência de dados, a cópia de arquivos e a solução de problemas.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340398"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurar imagens de contêiner do SQL Server no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar e usar a [imagem de contêiner mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) com o Docker. 

Para ver outros cenários de implantação, confira:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes – Clusters de Big Data](../big-data-cluster/deploy-get-started.md)

Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este artigo concentra-se especificamente no uso da imagem mssql-server-linux. A imagem do Windows não é abordada, mas há mais informações sobre ela na [página do Docker Hub do mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

> [!IMPORTANT]
> Antes de escolher executar um contêiner de SQL Server para casos de uso de produção, examine nossa [política de suporte para Contêineres do SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para certificar-se de que você está executando uma configuração com suporte.

Este vídeo de 6 minutos fornece uma introdução à execução do SQL Server em contêineres:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

Para efetuar pull e executar as imagens de contêiner do Docker para o SQL Server 2017 e o SQL Server 2019, siga os pré-requisitos e as etapas no guia de início rápido abaixo:

- [Executar a imagem de contêiner do SQL Server 2017 com o Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Executar a imagem de contêiner do SQL Server 2019 com o Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Este artigo de configuração apresenta cenários de uso adicionais nas seções a seguir.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> Executar imagens de contêiner baseadas em RHEL

A documentação para as imagens de contêiner do SQL Server Linux apontam para contêineres baseados em Ubuntu. Do SQL Server 2019 em diante, você pode usar contêineres com base em RHEL (Red Hat Enterprise Linux). Altere o repositório de contêiner de **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04** para **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8** em todos os comandos do Docker.

Por exemplo, o seguinte comando extrai a Atualização Cumulativa 1 do contêiner do SQL Server 2019 que usa o RHEL 8:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> Executar imagens de contêiner de produção

O início rápido na seção anterior executa a edição Developer gratuita do SQL Server do Docker Hub. A maioria das informações ainda se aplica se você deseja executar imagens de contêiner de produção, como as edições Enterprise, Standard ou Web. No entanto, há algumas diferenças descritas aqui.

- Você só poderá usar o SQL Server em um ambiente de produção se tiver uma licença válida. Você pode obter uma licença de produção do SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). As licenças do SQL Server Standard e do Enterprise Edition estão disponíveis por meio do [Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/default.aspx).


- A imagem de contêiner da edição Developer também pode ser configurada para executar as edições de produção. Use as seguintes etapas para executar as edições de produção:

Examine os requisitos e os procedimentos de execução no [guia de início rápido](quickstart-install-connect-docker.md). Você deve especificar sua edição de produção com a variável de ambiente **MSSQL_PID**. O exemplo a seguir mostra como executar a imagem de contêiner mais recente do SQL Server 2017 para a Enterprise Edition:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> Ao passar o valor **Y** para a variável de ambiente **ACCEPT_EULA** e um valor de edição para **MSSQL_PID**, você está expressando que tem uma licença válida e existente para a edição e a versão do SQL Server que você pretende usar. Você também concorda que o uso do software SQL Server em execução em uma imagem de contêiner do Docker será regido pelos termos de sua licença do SQL Server.

> [!NOTE]
> Para obter uma lista completa de valores possíveis para o **MSSQL_PID**, confira [Definir configurações do SQL Server com variáveis de ambiente no Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar o SQL Server em um contêiner de fora ou de dentro do contêiner. As seções a seguir explicam os dois cenários. 

### <a name="tools-outside-the-container"></a>Ferramentas fora do contêiner

Você pode se conectar à instância do SQL Server em seu computador do Docker usando qualquer ferramenta externa do macOS, do Windows ou do Linux que seja compatível com conexões SQL. Algumas ferramentas comuns incluem:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-manage-ssms.md)

O exemplo a seguir usa o **sqlcmd** para conectar-se ao SQL Server em execução em um contêiner do Docker. O endereço IP na cadeia de conexão é o endereço IP do computador host que está executando o contêiner.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se você tiver mapeado uma porta de host que não era a porta padrão **1433**, adicione essa porta à cadeia de conexão. Por exemplo, se você especificar `-p 1400:1433` em seu comando `docker run`, conecte-se explicitamente especificando a porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Ferramentas dentro do contêiner

Do SQL Server 2017, as [ferramentas de linha de comando SQL Server](sql-server-linux-setup-tools.md) são incluídas na imagem de contêiner. Se você anexar a imagem com um prompt de comando interativo, poderá executar as ferramentas localmente.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo `e69e056c702d` a seguir está é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Você nem sempre precisa especificar a toda a ID do contêiner. Você só precisa especificar caracteres suficientes para identificá-la exclusivamente. Portanto, neste exemplo, pode ser suficiente usar `e6` ou `e69`, em vez da ID completa.

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. Observe que o sqlcmd não está no caminho por padrão, portanto, você precisará especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, digite `exit`.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a name="run-multiple-sql-server-containers"></a>Executar vários contêineres do SQL Server

O Docker fornece uma maneira de executar vários contêineres do SQL Server no mesmo computador host. Use essa abordagem para cenários que exigem várias instâncias do SQL Server no mesmo host. Cada contêiner deve expor-se em uma porta diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

O exemplo a seguir cria dois contêineres SQL Server 2017 e os mapeia para as portas **1401** e **1402** no computador host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

O exemplo a seguir cria dois contêineres SQL Server 2019 e os mapeia para as portas **1401** e **1402** no computador host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Agora, há duas instâncias do SQL Server em execução em contêineres separados. Os clientes podem se conectar a cada instância do SQL Server usando o endereço IP do host do Docker e o número da porta do contêiner.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> Criar um contêiner personalizado

É possível criar seu próprio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para criar um contêiner personalizado do SQL Server. Para obter mais informações, confira [uma demonstração que combina o SQL Server com um aplicativo do Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Se você criar seu próprio Dockerfile, esteja ciente do processo em primeiro plano, pois esse processo controla a vida útil do contêiner. Se ele sair, o contêiner será desligado. Por exemplo, se você quiser executar um script e iniciar o SQL Server, verifique se o processo do SQL Server é o comando mais à direita. Todos os outros comandos são executados em segundo plano. O comando a seguir ilustra isso dentro de um Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se você inverter os comandos no exemplo anterior, o contêiner será desligado quando o script do-my-sql-commands.sh for concluído.

## <a id="persist"></a> Manter seus dados

Sua configuração do SQL Server muda e os arquivos de banco de dados são mantidos no contêiner mesmo que você reinicie o contêiner com `docker stop` e `docker start`. No entanto, se você remover o contêiner com `docker rm`, tudo no contêiner será excluído, incluindo o SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para persistir seus arquivos de banco de dados mesmo que os contêineres associados sejam excluídos.

> [!IMPORTANT]
> Para o SQL Server, é essencial que você compreenda a persistência de dados no Docker. Além da discussão nesta seção, confira a documentação do Docker sobre [como gerenciar dados em contêineres do Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório de host como volume de dados

A primeira opção é montar um diretório em seu host como um volume de dados em seu contêiner. Para fazer isso, use o comando `docker run` com o sinalizador `-v <host directory>:/var/opt/mssql`. Isso permite que os dados sejam restaurados entre as execuções do contêiner.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Essa técnica também permite que você compartilhe e exiba os arquivos no host fora do Docker.

> [!IMPORTANT]
> Atualmente, o mapeamento de volume do host para o **Docker no Windows** não dá suporte ao mapeamento do diretório `/var/opt/mssql` completo. No entanto, você pode mapear um subdiretório, como `/var/opt/mssql/data` para o computador host.

> [!IMPORTANT]
> No momento, não há suporte para o mapeamento de volume do host no **Docker no Mac** com a imagem do SQL Server em Linux. Use contêineres de volume de dados em vez disso. Essa restrição é específica do diretório `/var/opt/mssql`. A leitura de um diretório montado funciona bem. Por exemplo, você pode montar um diretório de host usando -v no Mac e restaurar um backup de um arquivo .bak que reside no host.

### <a name="use-data-volume-containers"></a>Usar contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados especificando um nome de volume, em vez de um diretório de host com o parâmetro `-v`. O exemplo a seguir cria um volume de dados compartilhado chamado **sqlvolume**.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> Essa técnica para criar implicitamente um volume de dados no comando executar não funciona com versões anteriores do Docker. Nesse caso, use as etapas explícitas descritas na documentação do Docker, [Como criar e montar um contêiner de volume de dados](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Mesmo que você pare e remova esse contêiner, o volume de dados persiste. Você pode exibi-lo com o comando `docker volume ls`.

```bash
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

## <a name="execute-commands-in-a-container"></a>Executar comandos em um contêiner

Se você tiver um contêiner em execução, poderá executar comandos dentro do contêiner de um terminal de host.

Para obter a ID do contêiner, execute:

```bash
docker ps
```

Para iniciar um terminal de Bash na execução do contêiner:

```bash
docker exec -it <Container ID> /bin/bash
```

Agora, você pode executar comandos como se estivesse executando-os no terminal dentro do contêiner. Quando terminar, digite `exit`. Isso é encerrado na sessão de comando interativo, mas o contêiner continua a ser executado.

## <a name="copy-files-from-a-container"></a>Copiar arquivos de um contêiner

Para copiar um arquivo do contêiner, use o seguinte comando:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Exemplo:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>Copiar arquivos para um contêiner

Para copiar um arquivo para o contêiner, use o seguinte comando:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Exemplo:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a> Configurar o fuso horário

Para executar o SQL Server em um contêiner do Linux com um fuso horário específico, configure a variável de ambiente `TZ`. Para localizar o valor de fuso horário correto, execute o comando `tzselect` de um prompt de Bash do Linux:

```bash
tzselect
```

Depois de selecionar o fuso horário, o `tzselect` exibe uma saída semelhante à seguinte:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Você pode usar essas informações para definir a mesma variável de ambiente em seu contêiner do Linux. O exemplo a seguir mostra como executar o SQL Server em um contêiner no fuso horário `Americas/Los_Angeles`:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a id="tags"></a> Executar uma imagem de contêiner específica do SQL Server

Há cenários em que você talvez não queira usar a imagem de contêiner do SQL Server mais recente. Para executar uma imagem de contêiner do SQL Server específica, use as seguintes etapas:

1. Identifique a **tag** do Docker para a versão que você deseja usar. Para ver todas as tags disponíveis, confira a [página do Docker Hub do mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server).

2. Efetue pull da imagem de contêiner do SQL Server com a tag. Por exemplo, para efetuar pull da imagem RC1, substitua `<image_tag>` no comando a seguir por `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para executar um novo contêiner com essa imagem, especifique o nome da tag no comando `docker run`. No comando a seguir, substitua `<image_tag>` pela versão que você deseja executar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Essas etapas também podem ser usadas para fazer downgrade de um contêiner existente. Por exemplo, talvez você queira reverter ou fazer downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas na [seção de atualização](#upgrade), mas especifique o nome da tag da versão mais antiga ao executar o novo contêiner.

## <a id="version"></a> Verificar a versão do contêiner

Se você quiser saber a versão do SQL Server em um contêiner do Docker em execução, execute o comando a seguir para exibi-la. Substitua `<Container ID or name>` pela ID ou pelo nome do contêiner de destino. Substitua `<YourStrong!Passw0rd>` pela senha do SQL Server do logon SA.

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

Você também pode identificar a versão e o número de build do SQL Server para uma imagem de contêiner de destino do Docker. O comando a seguir exibe informações de versão e build do SQL Server para a imagem **mcr.microsoft.com/mssql/server:2017-latest**. Ele faz isso executando um novo contêiner com uma variável de ambiente **PAL_PROGRAM_INFO = 1**. O contêiner resultante é fechado instantaneamente e o comando `docker rm` o remove.

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

Os comandos anteriores exibem informações de versão semelhantes à seguinte saída:

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a id="upgrade"></a> Atualizar o SQL Server em contêineres

Para atualizar a imagem de contêiner com o Docker, primeiro identifique a tag de versão para a atualização. Receba esta versão do Registro com o comando `docker pull`:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Isso atualiza a imagem do SQL Server para os novos contêineres que você criar, mas não atualiza o SQL Server em nenhum contêiner em execução. Para fazer isso, você deve criar um novo contêiner com a imagem de contêiner mais recente do SQL Server e migrar os dados para esse novo contêiner.

1. Verifique se você está usando uma das [técnicas de persistência de dados](#persist) para o contêiner do SQL Server existente. Isso permite que você inicie um novo contêiner com os mesmos dados.

1. Interrompa o contêiner do SQL Server com o comando `docker stop`.

1. Crie um novo contêiner do SQL Server com `docker run` e especifique um diretório de host mapeado ou um contêiner de volume de dados. Use a tag específica para a atualização do SQL Server. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

   > [!IMPORTANT]
   > Há suporte para a atualização apenas entre RC1, RC2 e GA no momento.

1. Verifique os bancos de dados e os dados no novo contêiner.

1. Opcionalmente, remova o contêiner antigo com `docker rm`.

## <a id="buildnonrootcontainer"></a> Compilar e executar contêineres não raiz do SQL Server 2017

Siga as etapas abaixo para criar um contêiner do SQL Server 2017 que é iniciado como o usuário `mssql` (não raiz).

> [!NOTE]
> Os contêineres do SQL Server 2019 são iniciados automaticamente como não raiz, portanto, as etapas a seguir se aplicam somente a contêineres SQL Server 2017, que iniciam como raiz por padrão.

1. Baixe o [Dockerfile de exemplo para o Contêiner do SQL Server não raiz](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile) e salve-o como `dockerfile`.

2. Execute o seguinte comando no contexto do diretório do Dockerfile para criar o contêiner de SQL Server não raiz:

```bash
cd <path to dockerfile>
docker build -t 2017-latest-non-root .
```

3. Inicie o contêiner.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
```

> [!NOTE]
> O sinalizador `--cap-add SYS_PTRACE` é necessário para contêineres de SQL Server não raiz para gerar despejos para fins de solução de problemas.

4. Verifique se o contêiner está sendo executado como um usuário não raiz:

docker exec no contêiner.
```bash
docker exec -it sql1 bash
```

Execute `whoami`, que retornará o usuário em execução dentro do contêiner.

```bash
whoami
```

## <a id="nonrootuser"></a> Executar o contêiner como um usuário não raiz diferente no host

Para executar o contêiner do SQL Server como um usuário não raiz diferente, adicione o sinalizador -u ao comando de execução do docker. O contêiner não raiz tem a restrição de que ele deve ser executado como parte do grupo raiz a menos que um volume seja montado para '/var/opt/mssql' que o usuário não raiz pode acessar. O grupo raiz não concede permissões de raiz extras ao usuário não raiz.

**Executar como um usuário com UID 4000**

Você pode iniciar o SQL Server com uma UID personalizada. Por exemplo, o comando a seguir inicia o SQL Server com UID 4000:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> Verifique se o contêiner do SQL Server tem um usuário nomeado como 'mssql' ou 'root' ou o SQLCMD não poderá ser executado no contêiner. Você pode verificar se o contêiner do SQL Server está sendo executado como um usuário nomeado executando `whoami` dentro do contêiner.

**Executar o contêiner não raiz como o usuário raiz**

Você pode executar o contêiner não raiz como o usuário raiz, se necessário. Isso também concederia todas as permissões de arquivo automaticamente para o contêiner porque é um privilégio mais alto.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Executar como um usuário em seu computador host**

Você pode iniciar o SQL Server com um usuário existente no computador host com o seguinte comando:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Executar como um usuário e grupo diferentes**

Você pode iniciar o SQL Server com um usuário e um grupo personalizados. Neste exemplo, o volume montado tem permissões configuradas para o usuário ou o grupo no computador host.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="storagepermissions"></a> Configurar permissões de armazenamento persistente para contêineres não raiz

Para permitir que o usuário não raiz acesse arquivos de banco de dados que estão em volumes montados, verifique se o usuário/grupo no qual você executa o contêiner pode tocar no armazenamento de arquivos persistente.  

Você pode obter a propriedade atual dos arquivos de banco de dados com este comando.

```bash
ls -ll <database file dir>
```

Execute um dos comandos a seguir se o SQL Server não tiver acesso aos arquivos de banco de dados persistentes.

**Conceder ao grupo raiz acesso de leitura/gravação aos arquivos de banco de dados**

Conceda as permissões do grupo raiz aos seguintes diretórios para que o contêiner do SQL Server não raiz tenha acesso aos arquivos de banco de dados.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**Defina o usuário não raiz como o proprietário dos arquivos.**

Esse pode ser o usuário não raiz padrão ou qualquer outro usuário não raiz que você queira especificar. Neste exemplo, definimos a UID 10001 como o usuário não raiz.

```bash
chown -R 10001:0 <database file dir>
```

## <a id="changefilelocation"></a> Alterar a localização do arquivo padrão

Adicione a variável `MSSQL_DATA_DIR` para alterar o diretório de dados em seu comando `docker run` e, em seguida, monte um volume para esse localização ao qual o usuário do contêiner tem acesso.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="troubleshooting"></a> Solução de problemas

As seções a seguir fornecem sugestões de solução de problemas para a execução do SQL Server em contêineres.

### <a name="docker-command-errors"></a>Erros de comando do Docker

Se você receber erros para qualquer comando `docker`, verifique se o serviço do Docker está em execução e tente executar com permissões elevadas.

Por exemplo, no Linux, você pode receber o seguinte erro ao executar comandos `docker`:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se você receber esse erro no Linux, tente executar os mesmos comandos precedidos com `sudo`. Se isso falhar, verifique se o serviço do Docker está em execução e inicie-o, se necessário.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

No Windows, verifique se você está iniciando o PowerShell ou o prompt de comando como Administrador.

### <a name="sql-server-container-startup-errors"></a>Erros de inicialização do contêiner do SQL Server

Se a execução do contêiner do SQL Server falhar, tente os seguintes testes:

- Se você receber um erro como '**falha ao criar o ponto de extremidade CONTAINER_NAME na ponte de rede. Erro ao iniciar o proxy: listen tcp 0.0.0.0:1433 bind: address já está em uso.'** , você está tentando mapear a porta 1433 do contêiner para uma porta que já está em uso. Isso poderá acontecer se você estiver executando o SQL Server localmente no computador host. Isso também poderá acontecer se você iniciar dois contêineres de SQL Server e tentar mapeá-los para a mesma porta de host. Se isso acontecer, use o parâmetro `-p` para mapear a porta de contêiner 1433 para uma porta de host diferente. Por exemplo: 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- Se você receber um erro como **"A permissão foi negada ao tentar conectar-se ao soquete do daemon do Docker em unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: permission denied"** ao tentar iniciar um contêiner, adicione o usuário ao grupo do Docker no Ubuntu. Em seguida, faça logoff e logon novamente, pois essa alteração afetará novas sessões. 

   ```bash
    usermod -aG docker $USER
   ```
- Verifique se há alguma mensagem de erro do contêiner.

    ```bash
    docker logs e69e056c702d
    ```

- Verifique se você atende aos requisitos mínimos de memória e disco especificados na seção [pré-requisitos](quickstart-install-connect-docker.md#requirements) do artigo de início rápido.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo sqlservr no contêiner é executado como raiz.

- Examine a [configuração do SQL Server e os logs de erro](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar capturas de despejo

Se o processo do SQL Server estiver falhando dentro do contêiner, você deverá criar um novo contêiner com **SYS_PTRACE** habilitado. Isso adiciona a funcionalidade do Linux para rastrear um processo, o que é necessário para criar um arquivo de despejo em uma exceção. O arquivo de despejo pode ser usado pelo suporte para ajudar a solucionar o problema. O comando de execução do Docker a seguir habilita essa funcionalidade.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Falhas de conexão do SQL Server

Se você não conseguir conectar-se à instância do SQL Server em execução no seu contêiner, tente os seguintes testes:

- Verifique se o contêiner do SQL Server está em execução examinando a coluna **STATUS** da saída `docker ps -a`. Caso contrário, use `docker start <Container ID>` para iniciá-lo.

- Se você mapeou para uma porta de host não padrão (não 1433), verifique se está especificando a porta na cadeia de conexão. Você pode ver o mapeamento de porta na coluna **PORTAS** da saída `docker ps -a`. Por exemplo, o comando a seguir conecta o sqlcmd a um contêiner escutando na porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se você usou `docker run` com um volume de dados mapeado existente ou um contêiner de volume de dados, SQL Server ignora o valor de `MSSQL_SA_PASSWORD`. Em vez disso, a senha de usuário do SA pré-configurada é usada dos dados do SQL Server no volume de dados ou no contêiner de volume de dados. Verifique se você está usando a senha SA associada aos dados aos quais você está anexando.

- Examine a [configuração do SQL Server e os logs de erro](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de Disponibilidade de SQL Server

Se você estiver usando o Docker com Grupos de Disponibilidade do SQL Server, haverá dois requisitos adicionais.

- Mapeie a porta usada para comunicação de réplica (padrão 5022). Por exemplo, especifique `-p 5022:5022` como parte do comando `docker run`.

- Defina explicitamente o nome do host do contêiner com o parâmetro `-h YOURHOSTNAME` do comando `docker run`. Esse nome de host é usado quando você configura seu grupo de disponibilidade. Se você não especificá-lo com `-h`, o padrão será a ID do contêiner.

### <a id="errorlogs"></a> Configuração e logs de erro do SQL Server

Você pode examinar a configuração e os logs de erro do SQL Server em **/var/opt/mssql/log**. Se o contêiner não estiver em execução, primeiro inicie-o. Em seguida, use um prompt de comando interativo para inspecionar os logs.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Na sessão de Bash dentro de seu contêiner, execute os seguintes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se você montou um diretório de host para **/var/opt/mssql** quando criou o contêiner, poderá procurar no subdiretório de **log** no caminho mapeado no host.

## <a name="next-steps"></a>Próximas etapas

Obtenha uma introdução às imagens de contêiner do SQL Server 2017 no Docker com o [guia de início rápido](quickstart-install-connect-docker.md).

Além disso, confira o [repositório do GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para obter recursos e conferir comentários e problemas conhecidos.

[Explorar alta disponibilidade para contêineres do SQL Server](sql-server-linux-container-ha-overview.md)
