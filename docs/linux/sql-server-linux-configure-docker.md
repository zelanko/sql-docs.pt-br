---
title: Opções de configuração para o SQL Server no Docker | Microsoft Docs
description: Explore as diferentes formas de usar e interagir com o SQL Server 2017 e 2019 imagens de contêiner de visualização no Docker. Isso inclui dados persistentes, copiando arquivos e solução de problemas.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 8b7f256aec6fc01500f5c98709086a69815fd6ef
ms.sourcegitcommit: b2a29f9659f627116d0a92c03529aafc60e1b85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59516512"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurar imagens de contêiner do SQL Server no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar e usar o [imagem de contêiner mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) com o Docker. Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este artigo enfoca especificamente usando a imagem mssql-server-linux. A imagem do Windows não é abordada, mas você pode aprender mais sobre ele na [página de Hub do Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

Para efetuar pull e executar o Docker imagens de contêiner para o SQL Server 2017 e o SQL Server 2019 visualização, siga os pré-requisitos e as etapas em início rápido a seguir:

- [Executar a imagem de contêiner do SQL Server 2017 com o Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Executar a imagem de contêiner de visualização de 2019 do SQL Server com o Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Este artigo de configuração fornece cenários de uso adicionais nas seções a seguir.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> Executar imagens de contêiner com base em RHEL

Toda a documentação sobre imagens de contêiner do SQL Server Linux apontam para contêineres baseados no Ubuntu. Começando com o SQL Server 2019 preview, você pode usar contêineres com base em Red Hat Enterprise Linux (RHEL). Alterar o repositório de contêiner do **mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu** à **mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4** em todos os seus comandos do docker.

Por exemplo, o comando a seguir extrai o contêiner de visualização mais recente do SQL Server 2019 que usa RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> Executar imagens de contêiner de produção

O guia de início rápido na seção anterior é executado a edição de desenvolvedor gratuita do SQL Server do Hub do Docker. A maioria das informações ainda se aplica se você quiser executar imagens de contêiner, como as edições Enterprise, Standard ou Web de produção. No entanto, há algumas diferenças são descritas aqui.

- Você só pode usar o SQL Server em um ambiente de produção se você tiver uma licença válida. Você pode obter uma licença de produção do SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). Licenças do SQL Server Standard e Enterprise Edition estão disponíveis por meio [licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/default.aspx).


- A imagem de contêiner do desenvolvedor pode ser configurada para executar as edições de produção. Use as etapas a seguir para executar edições de produção:

Examine os requisitos e executar procedimentos [quickstart](quickstart-install-connect-docker.md). Você deve especificar sua edição de produção com o **MSSQL_PID** variável de ambiente. O exemplo a seguir mostra como executar a imagem de contêiner do SQL Server 2017 mais recente para o Enterprise Edition:

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
      > By passing the value **Y** to the environment variable **ACCEPT_EULA** and an edition value to **MSSQL_PID**, you are expressing that you have a valid and existing license for the edition and version of SQL Server that you intend to use. You also agree that your use of SQL Server software running in a Docker container image will be governed by the terms of your SQL Server license.

      > [!NOTE]
      > For a full list of possible values for **MSSQL_PID**, see [Configure SQL Server settings with environment variables on Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar o SQL Server em um contêiner de qualquer um fora do contêiner ou de dentro do contêiner. As seções a seguir explicam os dois cenários. 

### <a name="tools-outside-the-container"></a>Ferramentas de fora do contêiner

Você pode se conectar à instância do SQL Server em seu computador Docker de qualquer ferramenta externa do macOS, Windows ou Linux que dá suporte a conexões de SQL. Algumas ferramentas comuns incluem:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-manage-ssms.md)

O exemplo a seguir usa **sqlcmd** para se conectar ao SQL Server em execução em um contêiner do Docker. O endereço IP na cadeia de conexão é o endereço IP do computador host que está executando o contêiner.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se tiver mapeado a uma porta de host que não era o padrão **1433**, adicione-à cadeia de caracteres de conexão. Por exemplo, se você especificou `-p 1400:1433` em seu `docker run` de comando, em seguida, conecte-se explicitamente, especifique a porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Ferramentas dentro do contêiner

Começando com o SQL Server 2017 preview, o [ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md) estão incluídos na imagem de contêiner. Se você anexar à imagem com um prompt de comando interativo, você pode executar as ferramentas localmente.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo a seguir `e69e056c702d` é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Você não precisa sempre especificar a id de contêiner inteiro. Você só precisará especificar caracteres suficientes para identificá-lo exclusivamente. Portanto, neste exemplo, pode ser suficiente para usar `e6` ou `e69` em vez da id completa.

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. Observe que a sqlcmd não está no caminho por padrão, portanto, você precisa especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, digite `exit`.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a name="run-multiple-sql-server-containers"></a>Executar vários contêineres do SQL Server

Docker fornece uma maneira de executar vários contêineres do SQL Server no mesmo computador host. Essa é a abordagem para cenários que exigem várias instâncias do SQL Server no mesmo host. Cada contêiner deve expor em si em uma porta diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

O exemplo a seguir cria dois contêineres do SQL Server 2017 e mapeá-las para portas **1401** e **1402** na máquina host.

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

O exemplo a seguir cria dois contêineres de visualização do SQL Server 2019 e mapeá-las para portas **1401** e **1402** na máquina host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

Agora há duas instâncias do SQL Server em execução em um contêiner separado. Clientes podem se conectar a cada instância do SQL Server usando o endereço IP do host do Docker e o número da porta para o contêiner.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> Criar um contêiner personalizado

É possível criar seus próprios [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) para criar um contêiner personalizado do SQL Server. Para obter mais informações, consulte [uma demonstração que combina o SQL Server e um aplicativo de nó](https://github.com/twright-msft/mssql-node-docker-demo-app). Se você criar seu próprio Dockerfile, lembre-se do processo de primeiro plano, porque esse processo controla a vida útil do contêiner. Se for encerrada, o contêiner será desligado. Por exemplo, se você quiser executar um script e iniciar o SQL Server, certifique-se de que o processo do SQL Server é o comando mais à direita. Todos os outros comandos são executados em segundo plano. Isso é ilustrado no seguinte comando dentro de um Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se você revertido os comandos no exemplo anterior, o contêiner seria desligamento quando o script faça-my-sql-commands.sh é concluída.

## <a id="persist"></a> Manter seus dados

Suas alterações de configuração do SQL Server e os arquivos de banco de dados são persistidos no contêiner, mesmo se você reiniciar o contêiner com `docker stop` e `docker start`. No entanto, se você remover o contêiner com `docker rm`, tudo no contêiner for excluído, incluindo o SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para persistir seus arquivos de banco de dados, mesmo se os contêineres associados são excluídos.

> [!IMPORTANT]
> Para o SQL Server, é essencial que você conheça a persistência de dados no Docker. Além da discussão nesta seção, consulte a documentação do Docker no [como gerenciar dados em contêineres do Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório do host como volume de dados

A primeira opção é um diretório de montagem em seu host como um volume de dados em seu contêiner. Para fazer isso, use o `docker run` com o `-v <host directory>:/var/opt/mssql` sinalizador. Isso permite que os dados a ser restaurado entre as execuções do contêiner.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

Essa técnica também permite que você compartilhe e exibir os arquivos no host fora do Docker.

> [!IMPORTANT]
> Não há suporte para mapeamento de volume de host para o Docker no Mac com o SQL Server na imagem do Linux no momento. Use contêineres de volume de dados. Essa restrição é específica para o `/var/opt/mssql` directory. Lendo uma funciona de diretório montado corretamente. Por exemplo, você pode montar um diretório do host usando - v no Mac e restaurar um backup de um arquivo. bak que reside no host.

### <a name="use-data-volume-containers"></a>Usar contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados, especificando um nome de volume, em vez de um diretório de host com o `-v` parâmetro. O exemplo a seguir cria um volume de dados compartilhado denominado **sqlvolume**.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```
::: moniker-end

> [!NOTE]
> Essa técnica para criar implicitamente um volume de dados em que o comando de execução não funciona com versões mais antigas do Docker. Nesse caso, use as etapas descritas na documentação do Docker, a explícitas [criando e montando um contêiner de volume de dados](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Mesmo se você para e remove este contêiner, mantém o volume de dados. Você pode exibi-la com o `docker volume ls` comando.

```bash
docker volume ls
```

Se você, em seguida, crie outro contêiner com o mesmo nome de volume, o novo contêiner usa os mesmos dados do SQL Server contidos no volume.

Para remover um contêiner de volume de dados, use o `docker volume rm` comando.

> [!WARNING]
> Se você excluir o contêiner de volume de dados, todos os dados do SQL Server no contêiner serão *permanentemente* excluído.

### <a name="backup-and-restore"></a>Backup e restauração

Além dessas técnicas de contêiner, você pode também usar o backup do SQL Server standard e técnicas de restauração. Você pode usar arquivos de backup para proteger seus dados ou para mover os dados para outra instância do SQL Server. Para obter mais informações, consulte [Backup e restauração do SQL Server databases no Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se você criar backups, certifique-se criar ou copiar os arquivos de backup fora do contêiner. Caso contrário, se o contêiner for removido, os arquivos de backup também são excluídos.

## <a name="execute-commands-in-a-container"></a>Executar comandos em um contêiner

Se você tiver um contêiner em execução, você pode executar comandos dentro do contêiner de um host de terminal.

Para obter a ID do contêiner executar:

```bash
docker ps
```

Para iniciar um bash, terminal em que o contêiner seja executado:

```bash
docker exec -ti <Container ID> /bin/bash
```

Agora você pode executar comandos como se você estiver executando-os no terminal dentro do contêiner. Quando terminar, digite `exit`. Isso sai da sessão de comando interativo, mas o contêiner continuará a ser executado.

## <a name="copy-files-from-a-container"></a>Copiar arquivos de um contêiner

Para copiar um arquivo para fora do contêiner, use o seguinte comando:

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

Para copiar um arquivo no contêiner, use o seguinte comando:

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

Para executar o SQL Server em um contêiner do Linux com um fuso horário específico, configurar o **TZ** variável de ambiente. Para localizar o valor de fuso horário correto, execute as **tzselect** comando em um prompt de bash do Linux:

```bash
tzselect
```

Depois de selecionar o fuso horário, **tzselect** exibe uma saída semelhante à seguinte:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

Você pode usar essas informações para definir a mesma variável de ambiente em seu contêiner do Linux. O exemplo a seguir mostra como executar o SQL Server em um contêiner no `Americas/Los_Angeles` fuso horário:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```
::: moniker-end

## <a id="tags"></a> Executar uma imagem de contêiner específica do SQL Server

Há cenários em que você não poderá usar a imagem de contêiner mais recente do SQL Server. Para executar uma imagem de contêiner do SQL Server específica, use as seguintes etapas:

1. Identificar o Docker **marca** para a versão que você deseja usar. Para exibir as marcas disponíveis, consulte [a página de hub do Docker mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server).

2. Extraia a imagem de contêiner do SQL Server com a marca. Por exemplo, para efetuar pull da imagem do RC1, substitua `<image_tag>` no comando a seguir com `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para executar um novo contêiner com essa imagem, especifique o nome da marca no `docker run` comando. No comando a seguir, substitua `<image_tag>` com a versão que você deseja executar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Essas etapas também podem ser usadas para fazer o downgrade de um contêiner existente. Por exemplo, você pode deseja reverter ou fazer downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer o downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas na [seção de atualização](#upgrade), mas especificar o nome da marca da versão mais antiga, quando você executar o novo contêiner.

## <a id="version"></a> Verificar a versão do contêiner

Se você quiser saber a versão do SQL Server em um contêiner de docker em execução, execute o seguinte comando para exibi-lo. Substitua `<Container ID or name>` com o nome ou ID do contêiner de destino. Substitua `<YourStrong!Passw0rd>` com a senha para o logon SA do SQL Server.

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

Você também pode identificar a versão do SQL Server e número para uma imagem de contêiner do docker de destino da compilação. O comando a seguir exibe as informações de versão e compilação do SQL Server para o **microsoft/mssql-server-linux:2017-mais recente** imagem. Ele faz isso executando um novo contêiner com uma variável de ambiente **PAL_PROGRAM_INFO = 1**. O contêiner resultante é encerrado imediatamente e o `docker rm` comando remove-lo.

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

## <a id="upgrade"></a> Atualize o SQL Server em contêineres

Para atualizar a imagem de contêiner com Docker, primeiro identifique a marca para a versão para a atualização. Esta versão de pull do registro com o `docker pull` comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Isso atualiza a imagem do SQL Server para quaisquer novos contêineres que você cria, mas não atualiza do SQL Server em todos os contêineres em execução. Para fazer isso, você deve criar um novo contêiner com a imagem de contêiner mais recente do SQL Server e migre seus dados para esse novo contêiner.

1. Verifique se você estiver usando um dos [técnicas de persistência de dados](#persist) para seu contêiner do SQL Server existente. Isso permite que você inicie um novo contêiner com os mesmos dados.

1. Pare o contêiner do SQL Server com o `docker stop` comando.

1. Criar um novo contêiner do SQL Server com `docker run` e especifique um diretório mapeado do host ou um contêiner de volume de dados. Certifique-se de usar a marca específica para a atualização do SQL Server. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

   > [!IMPORTANT]
   > Somente há suporte para atualização entre RC1 e RC2 GA neste momento.

1. Verifique se seus bancos de dados e os dados no novo contêiner.

1. Opcionalmente, remova o contêiner antigo com `docker rm`.

## <a id="troubleshooting"></a> Solução de problemas

As seções a seguir fornecem sugestões de solução de problemas para executar o SQL Server em contêineres.

### <a name="docker-command-errors"></a>Erros de comando do docker

Se você obtiver erros de qualquer `docker` comandos, certifique-se de que o serviço do docker está em execução e tente executar com permissões elevadas.

Por exemplo, no Linux, você poderá receber o seguinte erro durante a execução `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se você receber esse erro no Linux, tente executar os mesmos comandos precedidos com `sudo`. Se isso falhar, verifique se o serviço do docker está em execução e iniciá-lo se necessário.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

No Windows, verifique se que você estiver iniciando o PowerShell ou o prompt de comando como administrador.

### <a name="sql-server-container-startup-errors"></a>Erros de inicialização do contêiner do SQL Server

Se o contêiner do SQL Server falhar na execução, tente os seguintes testes:

- Se você receber um erro, como **' Falha ao criar o ponto de extremidade CONTAINER_NAME ponte de rede. Erro ao iniciar o proxy: bind do escuta tcp 0.0.0.0:1433: endereço já está em uso.'** , em seguida, você está tentando mapear a porta 1433 do contêiner para uma porta que já está em uso. Isso pode acontecer se você estiver executando o SQL Server localmente no computador host. Isso também pode acontecer se você iniciar dois contêineres do SQL Server e tente mapear ambos na mesma porta de host. Se isso acontecer, use o `-p` parâmetro para mapear a porta 1433 do contêiner para uma porta de host diferente. Por exemplo:  

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu`.
```

::: moniker-end

- Verifique se há mensagens de erro do contêiner.

    ```bash
    docker logs e69e056c702d
    ```

- Certifique-se de que você atende aos requisitos mínimos de memória e disco especificados na [pré-requisitos](quickstart-install-connect-docker.md#requirements) seção do artigo de início rápido.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo sqlservr no contêiner é executado como raiz.

- Examine os [logs de erro e a instalação do SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Permitir a captura de despejo

Se o processo do SQL Server estiver falhando dentro do contêiner, você deve criar um novo contêiner com **SYS_PTRACE** habilitado. Isso adiciona a capacidade de Linux para um processo, que é necessário para criar um arquivo de despejo em uma exceção de rastreamento. O arquivo de despejo pode ser usado pelo suporte para ajudar a solucionar o problema. O seguinte comando docker run habilita esse recurso.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Falhas de conexão do SQL Server

Se você não pode se conectar à instância do SQL Server em execução em seu contêiner, tente os seguintes testes:

- Certifique-se de que seu contêiner do SQL Server está em execução examinando a **STATUS** coluna o `docker ps -a` saída. Caso contrário, use `docker start <Container ID>` para iniciá-lo.

- Se você mapeada para uma porta de host não padrão (não 1433), verifique se que você está especificando a porta em sua cadeia de conexão. Você pode ver o mapeamento de porta na **portas** coluna o `docker ps -a` saída. Por exemplo, o comando a seguir conecta sqlcmd em um contêiner escutando na porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se você usou `docker run` com um volume de dados mapeados existente ou o contêiner de volume de dados, o SQL Server ignora o valor de `MSSQL_SA_PASSWORD`. Em vez disso, a senha de usuário SA pré-configurados é usada de dados do SQL Server no contêiner de volume de dados ou volume de dados. Verifique se que você está usando a senha de SA associada aos dados que você está anexando a.

- Examine os [logs de erro e a instalação do SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de disponibilidade do SQL Server

Se você estiver usando o Docker com grupos de disponibilidade do SQL Server, há dois requisitos adicionais.

- Mapear a porta que é usada para comunicação de réplica (padrão 5022). Por exemplo, especifique `-p 5022:5022` como parte de seu `docker run` comando.

- Definir explicitamente o nome de host do contêiner com o `-h YOURHOSTNAME` parâmetro do `docker run` comando. Esse nome de host é usado quando você configura seu grupo de disponibilidade. Se você não especificá-lo com `-h`, o padrão é a ID do contêiner.

### <a id="errorlogs"></a> Logs de erro e a instalação do SQL Server

Você pode examinar o programa de instalação do SQL Server e logs de erro no **/var/opt/mssql/log**. Se o contêiner não está em execução, inicie primeiro o contêiner. Em seguida, use um prompt de comando interativo para inspecionar os logs.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Na sessão do bash do seu contêiner, execute os seguintes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se você tiver montado um diretório do host para **/var/opt/mssql** quando você criou seu contêiner, em vez disso, você pode procurar na **log** subdiretório no caminho mapeado no host.

## <a name="next-steps"></a>Próximas etapas

Comece com imagens de contêiner do SQL Server 2017 no Docker por meio de [quickstart](quickstart-install-connect-docker.md).

Além disso, consulte a [repositório do GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para recursos, comentários e problemas conhecidos.

[Explore a alta disponibilidade para contêineres do SQL Server](sql-server-linux-container-ha-overview.md)
