---
title: Opções de configuração para SQL Server no Docker
description: Explore diferentes maneiras de usar e interagir com as imagens de contêiner SQL Server 2017 e 2019 Preview no Docker. Isso inclui a persistência de dados, a cópia de arquivos e a solução de problemas.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388383"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurar SQL Server imagens de contêiner no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar e usar a [imagem de contêiner MSSQL-Server-Linux](https://hub.docker.com/_/microsoft-mssql-server) com o Docker. Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este artigo se concentra especificamente no uso da imagem MSSQL-Server-Linux. A imagem do Windows não é coberta, mas você pode aprender mais sobre ela na [página MSSQL-Server-Windows Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

Para efetuar pull e executar as imagens de contêiner do Docker para SQL Server 2017 e SQL Server 2019 Preview, siga os pré-requisitos e as etapas no guia de início rápido a seguir:

- [Executar a imagem de contêiner SQL Server 2017 com o Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Executar a imagem de contêiner SQL Server 2019 Preview com o Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Este artigo de configuração fornece cenários de uso adicionais nas seções a seguir.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>Executar imagens de contêiner com base em RHEL

Toda a documentação sobre SQL Server imagens de contêiner do Linux aponta para contêineres baseados no Ubuntu. A partir da versão prévia do SQL Server 2019, você pode usar contêineres com base em Red Hat Enterprise Linux (RHEL). Altere o repositório de contêiner de **MCR.Microsoft.com/MSSQL/Server:2019-CTP3.1-Ubuntu** para **MCR.Microsoft.com/MSSQL/RHEL/Server:2019-CTP3.1** em todos os comandos do Docker.

Por exemplo, o comando a seguir recebe o mais recente SQL Server contêiner de visualização 2019 que usa RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>Executar imagens de contêiner de produção

O guia de início rápido na seção anterior executa a edição gratuita Developer do SQL Server do Hub do Docker. A maioria das informações ainda se aplica se você quiser executar imagens de contêiner de produção, como Enterprise, Standard ou Web Editions. No entanto, há algumas diferenças descritas aqui.

- Você só poderá usar SQL Server em um ambiente de produção se tiver uma licença válida. Você pode obter uma licença de produção SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). As licenças SQL Server Standard e Enterprise Edition estão disponíveis por meio [do licenciamento por volume da Microsoft](https://www.microsoft.com/licensing/default.aspx).


- A imagem de contêiner do desenvolvedor também pode ser configurada para executar as edições de produção. Use as seguintes etapas para executar as edições de produção:

Examine os requisitos e procedimentos de execução no guia de [início rápido](quickstart-install-connect-docker.md). Você deve especificar sua edição de produção com a variável de ambiente **MSSQL_PID** . O exemplo a seguir mostra como executar a imagem de contêiner mais recente do SQL Server 2017 para o Enterprise Edition:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> Ao passar o valor **Y** para a variável de ambiente **ACCEPT_EULA** e um valor de edição para **MSSQL_PID**, você está expressando que tem uma licença válida e existente para a edição e a versão do SQL Server que pretende usar. Você também concorda que o uso de SQL Server software em execução em uma imagem de contêiner do Docker será regido pelos termos de sua licença de SQL Server.

> [!NOTE]
> Para obter uma lista completa de valores possíveis para **MSSQL_PID**, consulte [definir configurações de SQL Server com variáveis de ambiente no Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar SQL Server em um contêiner de fora do contêiner ou de dentro do contêiner. As seções a seguir explicam os dois cenários. 

### <a name="tools-outside-the-container"></a>Ferramentas fora do contêiner

Você pode se conectar à instância do SQL Server no computador do Docker de qualquer ferramenta externa do Linux, Windows ou macOS que ofereça suporte a conexões SQL. Algumas ferramentas comuns incluem:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-manage-ssms.md)

O exemplo a seguir usa o **sqlcmd** para se conectar ao SQL Server em execução em um contêiner do Docker. O endereço IP na cadeia de conexão é o endereço IP do computador host que está executando o contêiner.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se você mapeou uma porta de host que não era o padrão **1433**, adicione essa porta à cadeia de conexão. Por exemplo, se você especificou `-p 1400:1433` em seu `docker run` comando, conecte-se explicitamente especificando a porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Ferramentas dentro do contêiner

A partir da versão prévia do SQL Server 2017, as [ferramentas de linha de comando SQL Server](sql-server-linux-setup-tools.md) são incluídas na imagem de contêiner. Se você anexar a imagem com um prompt de comando interativo, poderá executar as ferramentas localmente.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo `e69e056c702d` a seguir, é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Você nem sempre precisa especificar a ID do contêiner inteiro. Você só precisa especificar caracteres suficientes para identificá-lo exclusivamente. Portanto, neste exemplo, pode ser suficiente usar `e6` ou `e69` , em vez da ID completa.

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. Observe que o sqlcmd não está no caminho por padrão, portanto, você precisa especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, `exit`digite.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a name="run-multiple-sql-server-containers"></a>Executar vários contêineres de SQL Server

O Docker fornece uma maneira de executar vários contêineres de SQL Server no mesmo computador host. Essa é a abordagem para cenários que exigem várias instâncias de SQL Server no mesmo host. Cada contêiner deve expor-se em uma porta diferente.

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

O exemplo a seguir cria dois SQL Server contêineres de visualização do 2019 e os mapeia para as portas **1401** e **1402** no computador host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Agora, há duas instâncias do SQL Server em execução em contêineres separados. Os clientes podem se conectar a cada instância de SQL Server usando o endereço IP do host do Docker e o número da porta do contêiner.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>Criar um contêiner personalizado

É possível criar seu próprio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para criar um contêiner de SQL Server personalizado. Para obter mais informações, consulte [uma demonstração que combina SQL Server e um aplicativo de nó](https://github.com/twright-msft/mssql-node-docker-demo-app). Se você criar seu próprio Dockerfile, esteja ciente do processo em primeiro plano, pois esse processo controla a vida útil do contêiner. Se ele sair, o contêiner será desligado. Por exemplo, se você quiser executar um script e iniciar SQL Server, verifique se o processo de SQL Server é o comando mais à direita. Todos os outros comandos são executados em segundo plano. Isso é ilustrado no seguinte comando dentro de um Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se você inverter os comandos no exemplo anterior, o contêiner será desligado quando o script do-my-sql-commands.sh for concluído.

## <a id="persist"></a>Manter seus dados

Seu SQL Server alterações de configuração e arquivos de banco de dados são mantidos no contêiner, mesmo se você reiniciar `docker stop` o `docker start`contêiner com e. No entanto, se você remover o `docker rm`contêiner com, tudo no contêiner será excluído, incluindo SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para persistir seus arquivos de banco mesmo se os contêineres associados forem excluídos.

> [!IMPORTANT]
> Por SQL Server, é essencial que você compreenda a persistência de dados no Docker. Além da discussão nesta seção, consulte a documentação do Docker sobre [como gerenciar dados em contêineres](https://docs.docker.com/engine/tutorials/dockervolumes/)do Docker.

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório de host como volume de dados

A primeira opção é montar um diretório em seu host como um volume de dados em seu contêiner. Para fazer isso, use o `docker run` comando com o `-v <host directory>:/var/opt/mssql` sinalizador. Isso permite que os dados sejam restaurados entre as execuções de contêiner.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Essa técnica também permite que você compartilhe e exiba os arquivos no host fora do Docker.

> [!IMPORTANT]
> Não há suporte para o mapeamento de volume do host para o Docker no Mac com a imagem de SQL Server em Linux no momento. Em vez disso, use contêineres de volume de dados. Essa restrição é específica para o `/var/opt/mssql` diretório. A leitura de um diretório montado funciona bem. Por exemplo, você pode montar um diretório de host usando-v no Mac e restaurar um backup de um arquivo. bak que reside no host.

### <a name="use-data-volume-containers"></a>Usar contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados especificando um nome de volume em vez de um diretório `-v` de host com o parâmetro. O exemplo a seguir cria um volume de dados compartilhado chamado sqlvolume.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> Essa técnica para criar implicitamente um volume de dados no comando executar não funciona com versões anteriores do Docker. Nesse caso, use as etapas explícitas descritas na documentação do Docker, [criando e montando um contêiner de volume de dados](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Mesmo que você pare e remova esse contêiner, o volume de dados persiste. Você pode exibi-lo com `docker volume ls` o comando.

```bash
docker volume ls
```

Se você criar outro contêiner com o mesmo nome de volume, o novo contêiner usará os mesmos dados de SQL Server contidos no volume.

Para remover um contêiner de volume de dados, `docker volume rm` use o comando.

> [!WARNING]
> Se você excluir o contêiner de volume de dados, qualquer SQL Server dados no contêiner será excluído *permanentemente* .

### <a name="backup-and-restore"></a>Backup e restauração

Além dessas técnicas de contêiner, você também pode usar as técnicas padrão de backup e restauração do SQL Server. Você pode usar arquivos de backup para proteger seus dados ou mover os dados para outra instância de SQL Server. Para obter mais informações, consulte [backup e restauração SQL Server bancos de dados no Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se você criar backups, certifique-se de criar ou copiar os arquivos de backup fora do contêiner. Caso contrário, se o contêiner for removido, os arquivos de backup também serão excluídos.

## <a name="execute-commands-in-a-container"></a>Executar comandos em um contêiner

Se você tiver um contêiner em execução, poderá executar comandos dentro do contêiner de um terminal de host.

Para obter a execução da ID do contêiner:

```bash
docker ps
```

Para iniciar um terminal Bash na execução do contêiner:

```bash
docker exec -it <Container ID> /bin/bash
```

Agora você pode executar comandos como se estivesse executando-os no terminal dentro do contêiner. Quando terminar, digite `exit`. Isso é encerrado na sessão de comando interativo, mas o contêiner continua a ser executado.

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

## <a name="copy-files-into-a-container"></a>Copiar arquivos em um contêiner

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
## <a id="tz"></a>Configurar o fuso horário

Para executar SQL Server em um contêiner do Linux com um fuso horário específico, configure a variável de ambiente do **TZ** . Para localizar o valor de TimeZone correto, execute o comando **tzselect** de um prompt do Linux bash:

```bash
tzselect
```

Depois de selecionar o fuso horário, o **tzselect** exibe uma saída semelhante à seguinte:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Você pode usar essas informações para definir a mesma variável de ambiente em seu contêiner do Linux. O exemplo a seguir mostra como executar SQL Server em um contêiner no `Americas/Los_Angeles` fuso horário:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>Executar uma imagem de contêiner de SQL Server específica

Há cenários em que você talvez não queira usar a imagem de contêiner SQL Server mais recente. Para executar uma imagem de contêiner SQL Server específica, use as seguintes etapas:

1. Identifique a **marca** do Docker para a versão que você deseja usar. Para exibir as marcas disponíveis, consulte [a página do Hub MSSQL-Server-Linux Docker](https://hub.docker.com/_/microsoft-mssql-server).

2. Efetuar pull da imagem de contêiner de SQL Server com a marca. Por exemplo, para efetuar pull da imagem RC1 `<image_tag>` , substitua o comando a `rc1`seguir por.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para executar um novo contêiner com essa imagem, especifique o nome da marca no `docker run` comando. No comando a seguir, substitua `<image_tag>` pela versão que você deseja executar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Essas etapas também podem ser usadas para fazer downgrade de um contêiner existente. Por exemplo, talvez você queira reverter ou fazer downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer o downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas na [seção atualização](#upgrade), mas especifique o nome da marca da versão mais antiga ao executar o novo contêiner.

## <a id="version"></a>Verificar a versão do contêiner

Se você quiser saber a versão do SQL Server em um contêiner do Docker em execução, execute o comando a seguir para exibi-lo. Substituir `<Container ID or name>` pela ID ou nome do contêiner de destino. Substitua `<YourStrong!Passw0rd>` pela senha de SQL Server do logon SA.

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

Você também pode identificar a versão SQL Server e o número de Build para uma imagem de contêiner de destino do Docker. O comando a seguir exibe a versão SQL Server e informações de compilação para a imagem **Microsoft/MSSQL-Server-Linux: 2017-Latest** . Ele faz isso executando um novo contêiner com uma variável de ambiente **PAL_PROGRAM_INFO = 1**. O contêiner resultante é fechado instantaneamente e o comando `docker rm` o Remove.

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

## <a id="upgrade"></a>Atualizar SQL Server em contêineres

Para atualizar a imagem de contêiner com o Docker, primeiro identifique a marca da versão para a atualização. Receba esta versão do registro com o `docker pull` comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Isso atualiza a imagem de SQL Server para os novos contêineres que você criar, mas ele não atualiza SQL Server em nenhum contêiner em execução. Para fazer isso, você deve criar um novo contêiner com a mais recente SQL Server imagem de contêiner e migrar os dados para esse novo contêiner.

1. Verifique se você está usando uma das [técnicas de persistência de dados](#persist) para o contêiner de SQL Server existente. Isso permite que você inicie um novo contêiner com os mesmos dados.

1. Pare o contêiner SQL Server com o `docker stop` comando.

1. Crie um novo contêiner de SQL Server `docker run` com o e especifique um diretório de host mapeado ou um contêiner de volume de dados. Certifique-se de usar a marca específica para a atualização do SQL Server. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

   > [!IMPORTANT]
   > Há suporte para a atualização apenas entre RC1, RC2 e GA no momento.

1. Verifique os bancos de dados e os data no novo contêiner.

1. Opcionalmente, remova o contêiner antigo com `docker rm`.

## <a id="troubleshooting"></a> Solução de problemas

As seções a seguir fornecem sugestões de solução de problemas para a execução de SQL Server em contêineres.

### <a name="docker-command-errors"></a>Erros de comando do Docker

Se você receber erros para qualquer `docker` comando, verifique se o serviço do Docker está em execução e tente executar com permissões elevadas.

Por exemplo, no Linux, você pode receber o seguinte erro ao executar `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se você receber esse erro no Linux, tente executar os mesmos comandos precedidos com `sudo`. Se isso falhar, verifique se o serviço do Docker está em execução e inicie-o se necessário.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

No Windows, verifique se você está iniciando o PowerShell ou o prompt de comando como administrador.

### <a name="sql-server-container-startup-errors"></a>Erros de inicialização de contêiner SQL Server

Se o contêiner de SQL Server falhar ao ser executado, tente os seguintes testes:

- Se você receber um erro como ' **falha ao criar o ponto de extremidade CONTAINER_NAME na ponte de rede. Erro ao iniciar o proxy: escutar TCP 0.0.0.0:1433 BIND: o endereço já está em uso. '** , você está tentando mapear a porta de contêiner 1433 para uma porta que já está em uso. Isso pode acontecer se você estiver executando o SQL Server localmente no computador host. Isso também pode acontecer se você iniciar dois contêineres de SQL Server e tentar mapeá-los para a mesma porta de host. Se isso acontecer, use o `-p` parâmetro para mapear a porta de contêiner 1433 para uma porta de host diferente. Por exemplo: 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- Se você receber um erro como **"tem permissão negada ao tentar se conectar ao soquete do daemon do Docker em UNIX:///var/run/Docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial UNIX/var/run/Docker.sock: Connect: permissão negada** ' ao tentar iniciar um contêiner, em seguida, adicione o usuário ao grupo do Docker no Ubuntu. Em seguida, faça logoff e logon novamente, pois essa alteração afetará novas sessões. 

   ```bash
    usermod -aG docker $USER
    ```
- Verifique se há alguma mensagem de erro do contêiner.

    ```bash
    docker logs e69e056c702d
    ```

- Verifique se você atende aos requisitos mínimos de memória e disco especificados na seção [pré-requisitos](quickstart-install-connect-docker.md#requirements) do artigo de início rápido.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo sqlservr no contêiner é executado como raiz.

- Examine os [SQL Server os logs de erros e de instalação](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar capturas de despejo

Se o processo de SQL Server estiver falhando dentro do contêiner, você deverá criar um novo contêiner com **SYS_PTRACE** habilitado. Isso adiciona a funcionalidade do Linux para rastrear um processo, o que é necessário para criar um arquivo de despejo em uma exceção. O arquivo de despejo pode ser usado pelo suporte para ajudar a solucionar o problema. O comando de execução do Docker a seguir habilita esse recurso.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Falhas de conexão de SQL Server

Se você não conseguir se conectar à instância do SQL Server em execução no seu contêiner, tente os seguintes testes:

- Verifique se o contêiner de SQL Server está em execução examinando a coluna **status** da `docker ps -a` saída. Caso contrário, use `docker start <Container ID>` para iniciá-lo.

- Se você mapeou para uma porta de host não padrão (não 1433), verifique se está especificando a porta na cadeia de conexão. Você pode ver o mapeamento de porta na coluna **portas** da `docker ps -a` saída. Por exemplo, o comando a seguir conecta o sqlcmd a um contêiner escutando na porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se você usou `docker run` com um volume de dados mapeado existente ou um contêiner de volume de dados, SQL Server ignora `MSSQL_SA_PASSWORD`o valor de. Em vez disso, a senha de usuário do SA pré-configurado é usada no SQL Server dados no volume de dados ou no contêiner de volume de dados. Verifique se você está usando a senha SA associada aos dados aos quais você está anexando.

- Examine os [SQL Server os logs de erros e de instalação](#errorlogs).

### <a name="sql-server-availability-groups"></a>SQL Server grupos de disponibilidade

Se você estiver usando o Docker com grupos de disponibilidade SQL Server, haverá dois requisitos adicionais.

- Mapeie a porta usada para comunicação de réplica (padrão 5022). Por exemplo, especifique `-p 5022:5022` como parte `docker run` do comando.

- Defina explicitamente o nome do host do contêiner `-h YOURHOSTNAME` com o parâmetro `docker run` do comando. Esse nome de host é usado quando você configura seu grupo de disponibilidade. Se você não especificá- `-h`lo com, o padrão será a ID do contêiner.

### <a id="errorlogs"></a>SQL Server a instalação e os logs de erros

Você pode examinar os SQL Server os logs de erros e de instalação no **/var/opt/MSSQL/log**. Se o contêiner não estiver em execução, primeiro inicie o contêiner. Em seguida, use um prompt de comando interativo para inspecionar os logs.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Na sessão bash dentro de seu contêiner, execute os seguintes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se você montou um diretório de host para **/var/opt/MSSQL** quando criou o contêiner, poderá procurar no subdiretório de **log** no caminho mapeado no host.

## <a name="next-steps"></a>Próximas etapas

Introdução às imagens de contêiner SQL Server 2017 no Docker por meio do guia de [início rápido](quickstart-install-connect-docker.md).

Além disso, consulte o [repositório MSSQL-Docker GitHub](https://github.com/Microsoft/mssql-docker) para obter recursos, comentários e problemas conhecidos.

[Explorar a alta disponibilidade para contêineres de SQL Server](sql-server-linux-container-ha-overview.md)
