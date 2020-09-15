---
title: Implantar contêineres do SQL Server no Docker e conectar-se a eles
description: Explore como o SQL Server pode ser implantado em contêineres do Docker e saiba mais sobre as várias ferramentas disponíveis para se conectar ao SQL Server dentro e fora do contêiner
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 228c5a9f468ad7f82f6ca9c291a532466a5441df
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511553"
---
# <a name="deploy-and-connect-to-sql-server-docker-containers"></a>Implantar contêineres do SQL Server no Docker e conectar-se a eles

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo explica como implantar contêineres do SQL Server no Docker e se conectar a eles.

Para ver outros cenários de implantação, confira:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes – Clusters de Big Data](../big-data-cluster/deploy-get-started.md)

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

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar o SQL Server em um contêiner de fora ou de dentro do contêiner. As seções a seguir explicam os dois cenários.

### <a name="tools-outside-the-container"></a>Ferramentas fora do contêiner

Você pode se conectar à instância do SQL Server em seu computador do Docker usando qualquer ferramenta externa do macOS, do Windows ou do Linux que seja compatível com conexões SQL. Algumas ferramentas comuns incluem:

- [Azure Data Studio](../azure-data-studio/quickstart-sql-server.md)
- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-manage-ssms.md)

O exemplo a seguir usa o **sqlcmd** para conectar-se ao SQL Server em execução em um contêiner do Docker. O endereço IP na cadeia de conexão é o endereço IP do computador host que está executando o contêiner.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```
::: zone-end

Se você tiver mapeado uma porta de host que não era a porta padrão **1433**, adicione essa porta à cadeia de conexão. Por exemplo, se você especificar `-p 1400:1433` em seu comando `docker run`, conecte-se explicitamente especificando a porta 1400.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```
::: zone-end

### <a name="tools-inside-the-container"></a>Ferramentas dentro do contêiner

Do SQL Server 2017, as [ferramentas de linha de comando SQL Server](sql-server-linux-setup-tools.md) são incluídas na imagem de contêiner. Se você anexar a imagem com um prompt de comando interativo, poderá executar as ferramentas localmente.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo `e69e056c702d` a seguir está é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Você nem sempre precisa especificar toda a ID do contêiner. Você só precisa especificar caracteres suficientes para identificá-la exclusivamente. Portanto, neste exemplo, talvez seja suficiente usar `e6` ou `e69`, em vez da ID completa. Para descobrir a ID do contêiner, execute o comando `docker ps -a`.

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. A sqlcmd não está no caminho por padrão, portanto, você precisará especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, digite `exit`.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a name="check-the-container-version"></a><a id="version"></a> Verificar a versão do contêiner

Se você quiser saber a versão do SQL Server em um contêiner do Docker em execução, execute o comando a seguir para exibi-la. Substitua `<Container ID or name>` pela ID ou pelo nome do contêiner de destino. Substitua `<YourStrong!Passw0rd>` pela senha do SQL Server do logon SA.

::: zone pivot="cs1-bash"
```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
-S localhost -U SA -P '<YourStrong!Passw0rd>' \
-Q 'SELECT @@VERSION'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
-S localhost -U SA -P "<YourStrong!Passw0rd>" `
-Q "SELECT @@VERSION"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd ^
-S localhost -U SA -P "<YourStrong!Passw0rd>" ^
-Q "SELECT @@VERSION"
```
::: zone-end

Você também pode identificar a versão e o número de build do SQL Server para uma imagem de contêiner de destino do Docker. O comando a seguir exibe informações de versão e build do SQL Server para a imagem **mcr.microsoft.com/mssql/server:2017-latest**. Ele faz isso executando um novo contêiner com uma variável de ambiente **PAL_PROGRAM_INFO = 1**. O contêiner resultante é fechado instantaneamente e o comando `docker rm` o remove.

::: zone pivot="cs1-bash"
```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
-ti mcr.microsoft.com/mssql/server:2019-latest && \
sudo docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
-ti mcr.microsoft.com/mssql/server:2019-latest; `
docker rm sqlver
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e PAL_PROGRAM_INFO=1 --name sqlver ^
-ti mcr.microsoft.com/mssql/server:2019-latest && ^
docker rm sqlver
```
::: zone-end

Os comandos anteriores exibem informações de versão semelhantes à seguinte saída:

```output
sqlservr
  Version 15.0.4063.15
  Build ID 8a3bb4cca325e1d0b3071b3a193f6a1d74b440fbd95d2fb18881651a5b9ec8e8
  Build Type release
  Git Version 0335c462
  Built at Fri Aug 28 04:50:27 GMT 2020

PAL
  Build ID cc5ceea1b3d294f7d0166f99932f98c7eacfaaa81bcd7cf23c6a89f785829b63
  Build Type release
  Git Version ae9d66dff
  Built at Fri Aug 28 04:46:48 GMT 2020

Packages
  system.security                         6.2.9200.10,unset,
  system.certificates                     6.2.9200.10,unset,
  secforwarderxplat                       15.0.4063.15
  sqlservr                                15.0.4063.15
  system.common                           10.0.17134.1246.202005133
  system.netfx                            4.7.2.461814
  system                                  6.2.9200.10,unset,
  sqlagent                                15.0.4063.15
```

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> Executar uma imagem de contêiner específica do SQL Server

> [!NOTE]
> Do SQL Server 2019 CU3 em diante, há suporte para Ubuntu 18.04. Recupere uma lista de todas as marcas disponíveis para mssql/server em <https://mcr.microsoft.com/v2/mssql/server/tags/list>.

Há cenários em que você talvez não queira usar a imagem de contêiner do SQL Server mais recente. Para executar uma imagem de contêiner do SQL Server específica, use as seguintes etapas:

1. Identifique a **tag** do Docker para a versão que você deseja usar. Para ver todas as tags disponíveis, confira a [página do Docker Hub do mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server).

2. Efetue pull da imagem de contêiner do SQL Server com a tag. Por exemplo, para efetuar pull da imagem 2019-CU7-ubuntu-18.04, substitua `<image_tag>` no comando a seguir por `2019-CU7-ubuntu-18.04`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Para executar um novo contêiner com essa imagem, especifique o nome da tag no comando `docker run`. No comando a seguir, substitua `<image_tag>` pela versão que você deseja executar.

   ::: zone pivot="cs1-bash"
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```
   ::: zone-end

Essas etapas também podem ser usadas para fazer downgrade de um contêiner existente. Por exemplo, talvez você queira reverter ou fazer downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas na [seção de atualização](#upgrade), mas especifique o nome da tag da versão mais antiga ao executar o novo contêiner.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> Executar imagens de contêiner baseadas em RHEL

A documentação para as imagens de contêiner do SQL Server Linux apontam para contêineres baseados em Ubuntu. Do SQL Server 2019 em diante, você pode usar contêineres com base em RHEL (Red Hat Enterprise Linux). Um exemplo da imagem para RHEL será semelhante a **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8**.

Por exemplo, o seguinte comando extrai a Atualização Cumulativa 1 do contêiner do SQL Server 2019 que usa o RHEL 8:

::: zone pivot="cs1-bash"
```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```
::: zone-end

::: moniker-end

## <a name="run-production-container-images"></a><a id="production"></a> Executar imagens de contêiner de produção

O [guia de início rápido](quickstart-install-connect-docker.md) da seção anterior executa a edição Developer gratuita do SQL Server no Docker Hub. A maioria das informações ainda se aplica se você deseja executar imagens de contêiner de produção, como as edições Enterprise, Standard ou Web. No entanto, há algumas diferenças descritas aqui.

- Você só poderá usar o SQL Server em um ambiente de produção se tiver uma licença válida. Você pode obter uma licença de produção do SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). As licenças do SQL Server Standard e do Enterprise Edition estão disponíveis por meio do [Licenciamento por Volume da Microsoft](https://www.microsoft.com/licensing/default.aspx).

- A imagem de contêiner da edição Developer também pode ser configurada para executar as edições de produção. Use as seguintes etapas para executar as edições de produção:

Examine os requisitos e os procedimentos de execução no [guia de início rápido](quickstart-install-connect-docker.md). Você deve especificar sua edição de produção com a variável de ambiente **MSSQL_PID**. O exemplo a seguir mostra como executar a imagem de contêiner mais recente do SQL Server 2017 para a Enterprise Edition:

::: zone pivot="cs1-bash"
```bash
docker run --name sqlenterprise \
-e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
-e 'MSSQL_PID=Enterprise' -p 1433:1433 \
-d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
-e "MSSQL_PID=Enterprise" -p 1433:1433 `
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run --name sqlenterprise `
-e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" ^
-e "MSSQL_PID=Enterprise" -p 1433:1433 ^
-d "mcr.microsoft.com/mssql/server:2019-latest"
```
::: zone-end

> [!IMPORTANT]
> Ao passar o valor **Y** para a variável de ambiente **ACCEPT_EULA** e um valor de edição para **MSSQL_PID**, você está expressando que tem uma licença válida e existente para a edição e a versão do SQL Server que você pretende usar. Você também concorda que o uso do software SQL Server em execução em uma imagem de contêiner do Docker será regido pelos termos de sua licença do SQL Server.

> [!NOTE]
> Para obter uma lista completa de valores possíveis para o **MSSQL_PID**, confira [Definir configurações do SQL Server com variáveis de ambiente no Linux](sql-server-linux-configure-environment-variables.md).

## <a name="run-multiple-sql-server-containers"></a><a id="multiple"></a>Executar vários contêineres do SQL Server

O Docker fornece uma maneira de executar vários contêineres do SQL Server no mesmo computador host. Use essa abordagem para cenários que exigem várias instâncias do SQL Server no mesmo host. Cada contêiner deve expor-se em uma porta diferente.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

O exemplo a seguir cria dois contêineres SQL Server 2017 e os mapeia para as portas **1401** e **1402** no computador host.

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```
::: zone-end

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

O exemplo a seguir cria dois contêineres SQL Server 2019 e os mapeia para as portas **1401** e **1402** no computador host.

::: zone pivot="cs1-bash"
```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```
::: zone-end

::: moniker-end

Agora, há duas instâncias do SQL Server em execução em contêineres separados. Os clientes podem se conectar a cada instância do SQL Server usando o endereço IP do host do Docker e o número da porta do contêiner.

::: zone pivot="cs1-bash"
```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```
::: zone-end

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> Atualizar o SQL Server em contêineres

Para atualizar a imagem de contêiner com o Docker, primeiro identifique a tag de versão para a atualização. Receba esta versão do Registro com o comando `docker pull`:

```command
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Isso atualiza a imagem do SQL Server para os novos contêineres que você criar, mas não atualiza o SQL Server em nenhum contêiner em execução. Para fazer isso, você deve criar um novo contêiner com a imagem de contêiner mais recente do SQL Server e migrar os dados para esse novo contêiner.

1. Verifique se você está usando uma das [técnicas de persistência de dados](sql-server-linux-docker-container-configure.md#persist) para o contêiner do SQL Server existente. Isso permite que você inicie um novo contêiner com os mesmos dados.

1. Interrompa o contêiner do SQL Server com o comando `docker stop`.

1. Crie um novo contêiner do SQL Server com `docker run` e especifique um diretório de host mapeado ou um contêiner de volume de dados. Use a tag específica para a atualização do SQL Server. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

   > [!IMPORTANT]
   > Há suporte para a atualização apenas entre RC1, RC2 e GA no momento.

1. Verifique os bancos de dados e os dados no novo contêiner.

1. Opcionalmente, remova o contêiner antigo com `docker rm`.

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- Comece a usar as imagens de contêiner do SQL Server 2017 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-2017)

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- Comece a usar as imagens de contêiner do SQL Server 2019 no Docker acompanhando o [guia de início rápido](quickstart-install-connect-docker.md?view=sql-server-ver15)

::: moniker-end

- [Referenciar uma configuração e uma personalização adicionais em contêineres do Docker](sql-server-linux-docker-container-configure.md)

- Confira o [repositório GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) para obter recursos e comentários e problemas conhecidos

- [Solução de problemas de contêineres do SQL Server no Docker](sql-server-linux-docker-container-troubleshooting.md)

- [Explorar alta disponibilidade para contêineres do SQL Server](sql-server-linux-container-ha-overview.md)

- [Proteger contêineres do SQL Server no Docker](sql-server-linux-docker-container-security.md)
