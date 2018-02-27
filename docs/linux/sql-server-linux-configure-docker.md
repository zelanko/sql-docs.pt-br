---
title: "Opções de configuração para o SQL Server 2017 no Docker | Microsoft Docs"
description: "Explore diferentes maneiras de usar e interagir com o SQL Server 2017 imagens de contêiner no Docker. Isso inclui dados persistentes, copiando arquivos e solução de problemas."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/15/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: 70ed897c26211945987b81c179f7310a1437b482
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2018
---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>Configurar imagens de contêiner de 2017 do SQL Server no Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar e usar o [imagem de contêiner mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) com o Docker. Esta imagem consiste no SQL Server em execução no Linux, com base no Ubuntu 16.04. Ela pode ser usada com o Docker Engine 1.8 ou superior no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este artigo se concentra especificamente nos usando a imagem mssql-server-linux. A imagem do Windows não é coberta, mas você pode aprender mais sobre ele no [página de Hub do Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

Para efetuar pull e executar o Docker imagem de contêiner para o SQL Server 2017, siga os pré-requisitos e as etapas em início rápido a seguir:

- [Executar a imagem de contêiner de 2017 do SQL Server com o Docker](quickstart-install-connect-docker.md)

Este artigo de configuração fornece cenários de uso adicionais nas seções a seguir.

## <a id="production"></a> Executar produção imagens de contêiner

Início rápido na seção anterior é executada a edição gratuita do desenvolvedor do SQL Server do Hub do Docker. A maioria das informações ainda se aplica se você deseja executar imagens de contêiner, como as edições Enterprise, Standard ou Web de produção. No entanto, há algumas diferenças são descritas aqui.

- Você só pode usar SQL Server em um ambiente de produção se você tiver uma licença válida. Você pode obter uma licença de produção do SQL Server Express gratuita [aqui](https://go.microsoft.com/fwlink/?linkid=857693). SQL Server Standard e Enterprise Edition licenças estão disponíveis por meio de [Microsoft Volume Licensing](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx).

- Imagens de contêiner do SQL Server de produção devem ser extraídas de [Docker repositório](https://store.docker.com). Se você ainda não tiver um, crie uma conta no repositório do Docker.

- A imagem de contêiner de desenvolvedor no repositório do Docker pode ser configurada para executar edições produção. Use as etapas a seguir para executar edições de produção:

   1. Primeiro, faça logon sua id de docker da linha de comando.

      ```bash
      docker login
      ```

   1. Em seguida, você precisa obter o desenvolvedor livre imagem de contêiner no armazenamento do Docker. Vá para [https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux), clique em **prosseguir para a conclusão**e siga as instruções.

   1. Examine os requisitos e executar procedimentos no [quickstart](quickstart-install-connect-docker.md). Mas há duas diferenças. Você deve receber a imagem **repositório/microsoft/mssql-server-linux:\<nome da marca\>**  de armazenamento do Docker. E você deve especificar a edição de produção com o **MSSQL_PID** variável de ambiente. O exemplo a seguir mostra como executar a imagem de contêiner de 2017 do SQL Server mais recente para o Enterprise Edition:

      ```bash
      docker run --name sqlenterprise \
         -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
         -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
         -d store/microsoft/mssql-server-linux:2017-latest
      ```

      ```PowerShell
      docker run --name sqlenterprise `
         -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
         -e "MSSQL_PID=Enterprise" -p 1433:1433 `
         -d "store/microsoft/mssql-server-linux:2017-latest"
      ```

      > [!IMPORTANT]
      > Ao passar o valor **Y** à variável de ambiente **ACCEPT_EULA** e um valor de edição para **MSSQL_PID**, são expressar a que você tem uma licença válida e existente para a edição e versão do SQL Server que você pretende usar. Você também concorda que o uso do software do SQL Server em execução em uma imagem de contêiner de Docker será regido pelos termos de sua licença do SQL Server.

      > [!NOTE]
      > Para obter uma lista completa de valores possíveis para **MSSQL_PID**, consulte [as configurações de configurar o SQL Server com variáveis de ambiente em Linux](sql-server-linux-configure-environment-variables.md).

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar o SQL Server em um contêiner de seja fora do contêiner ou de dentro do contêiner. As seções a seguir explicam os dois cenários. 

### <a name="tools-outside-the-container"></a>Ferramentas fora do contêiner

Você pode se conectar à instância do SQL Server na máquina Docker de qualquer ferramenta externa de macOS, Windows ou Linux que oferece suporte a conexões de SQL. Algumas ferramentas comuns incluem:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SSMS (SQL Server Management Studio) no Windows](sql-server-linux-develop-use-ssms.md)

O exemplo a seguir usa **sqlcmd** para se conectar ao SQL Server em execução em um contêiner do Docker. O endereço IP na cadeia de conexão é o endereço IP do computador host que esteja executando o contêiner.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se você mapear uma porta de host que não era o padrão **1433**, adicionar essa porta para a cadeia de caracteres de conexão. Por exemplo, se você tiver especificado `-p 1400:1433` em sua `docker run` de comando, em seguida, conecte-se explicitamente, especifique a porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Ferramentas dentro do contêiner

Começando com o SQL Server de 2017 CTP 2.0, o [ferramentas de linha de comando do SQL Server](sql-server-linux-setup-tools.md) estão incluídos na imagem do contêiner. Se você anexar a imagem com um prompt de comando interativo, você pode executar as ferramentas localmente.

1. Use o comando `docker exec -it` para iniciar um shell bash interativo dentro do contêiner em execução. No exemplo a seguir `e69e056c702d` é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Sempre, você não precisa especificar a id de contêiner inteiro. Você só precisa especificar caracteres suficientes para identificá-lo exclusivamente. Portanto, neste exemplo, talvez seja suficiente para usar `e6` ou `e69` em vez da id completa.

2. Quando estiver dentro do contêiner, conecte-se localmente com a sqlcmd. Observe que sqlcmd não está no caminho por padrão, você precisará especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, digite `exit`.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair do shell bash interativo.

## <a name="run-multiple-sql-server-containers"></a>Executar vários contêineres de SQL Server

O docker fornece uma maneira de executar vários contêineres de SQL Server no mesmo computador host. Essa é a abordagem para cenários que exigem várias instâncias do SQL Server no mesmo host. Cada contêiner deve expor em si em uma porta diferente.

O exemplo a seguir cria dois contêineres de SQL Server e mapeá-las para portas **1401** e **1402** no computador host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d microsoft/mssql-server-linux:2017-latest
```

Agora há duas instâncias do SQL Server em execução em contêineres separados. Clientes podem se conectar a cada instância do SQL Server usando o endereço IP do host do Docker e o número da porta para o contêiner.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="persist"></a> Manter seus dados

Suas alterações de configuração do SQL Server e os arquivos de banco de dados são persistentes no contêiner, mesmo se você reiniciar o contêiner com `docker stop` e `docker start`. No entanto, se você remover o contêiner com `docker rm`, tudo no contêiner é excluído, incluindo o SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para manter os arquivos de banco de dados, mesmo se os contêineres associados são excluídos.

> [!IMPORTANT]
> Para o SQL Server, é importante que você compreenda a persistência de dados no Docker. Além de discussão nesta seção, consulte a documentação do Docker em [como gerenciar dados em contêineres do Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório de host como volume de dados

A primeira opção é um diretório de montagem no seu host como um volume de dados em seu contêiner. Para fazer isso, use o `docker run` com o `-v <host directory>:/var/opt/mssql` sinalizador. Isso permite que os dados sejam restaurados entre as execuções de contêiner.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

Essa técnica também permite que você compartilhe e exibir os arquivos no host fora do Docker.

> [!IMPORTANT]
> Não há suporte para o mapeamento do volume do host para o Docker no Mac com o SQL Server na imagem do Linux no momento. Use contêineres de volume de dados. Essa restrição é específica para o `/var/opt/mssql` directory. Lendo de funciona um diretório montado corretamente. Por exemplo, você pode montar um diretório de host usando – v no Mac e restaurar um backup de um arquivo. bak que reside no host.

### <a name="use-data-volume-containers"></a>Use contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados, especificando um nome de volume em vez de um diretório de host com o `-v` parâmetro. O exemplo a seguir cria um volume de dados compartilhado denominado **sqlvolume**.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
```

> [!NOTE]
> Essa técnica para criar implicitamente um volume de dados em que o comando run não funciona com versões anteriores do Docker. Nesse caso, use as etapas explícitas descritas na documentação do Docker, [criar e montar um contêiner de volume de dados](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Mesmo se você para e remove este contêiner, mantém o volume de dados. Você pode exibi-lo com o `docker volume ls` comando.

```bash
docker volume ls
```

Se você criar outro contêiner com o mesmo nome de volume, o novo contêiner usa os mesmos dados do SQL Server contidos no volume.

Para remover um contêiner de volume de dados, use o `docker volume rm` comando.

> [!WARNING]
> Se você excluir o contêiner de volume de dados, todos os dados do SQL Server no contêiner serão *permanentemente* excluído.

### <a name="backup-and-restore"></a>Backup e restauração

Além dessas técnicas de contêiner, também pode usar o backup do SQL Server standard e técnicas de restauração. Você pode usar arquivos de backup para proteger seus dados ou para mover os dados para outra instância do SQL Server. Para obter mais informações, consulte [Backup e restauração do SQL Server bancos de dados no Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se você criar backups, certifique-se de criar ou copiar os arquivos de backup fora do contêiner. Caso contrário, se o contêiner for removido, os arquivos de backup também são excluídos.

## <a name="execute-commands-in-a-container"></a>Executar comandos em um contêiner

Se você tiver um contêiner em execução, você pode executar comandos dentro do contêiner de um host de terminal.

Para obter a ID do contêiner executar:

```bash
docker ps
```

Para iniciar um bash terminal no contêiner executar:

```bash
docker exec -ti <Container ID> /bin/bash
```

Agora você pode executar comandos como se você estiver executando-los no terminal dentro do contêiner. Quando terminar, digite `exit`. Isso será encerrado na sessão de comando interativo, mas seu contêiner continuará a ser executado.

## <a name="copy-files-from-a-container"></a>Copie os arquivos de um contêiner

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

## <a name="run-a-specific-sql-server-container-image"></a>Executar uma imagem de contêiner específica do SQL Server

Há cenários em que você talvez não queira usar a imagem de contêiner mais recente do SQL Server. Para executar uma imagem de contêiner específica do SQL Server, use as seguintes etapas:

1. Identificar o Docker **marca** para a versão que você deseja usar. Para exibir as marcas disponíveis, consulte [a página de hub do Docker mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Baixe a imagem de contêiner de SQL Server com a marca. Por exemplo, para receber a imagem do RC1, substitua `<image_tag>` no comando a seguir com `rc1`.

   ```bash
   docker pull microsoft/mssql-server-linux:<image_tag>
   ```

1. Para executar um novo contêiner com essa imagem, especifique o nome da marca das `docker run` comando. No comando a seguir, substitua `<image_tag>` com a versão que você deseja executar.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
   ```

Essas etapas também podem ser usadas para fazer o downgrade de um contêiner existente. Por exemplo, você pode deseja reverter ou fazer o downgrade de um contêiner em execução para solução de problemas ou teste. Para fazer o downgrade de um contêiner em execução, você deve estar usando uma técnica de persistência para a pasta de dados. Siga as mesmas etapas descritas no [atualizar seção](#upgrade), mas especificar o nome da marca da versão anterior, quando você executar o novo contêiner.

> [!IMPORTANT]
> Upgrade e downgrade só são suportadas entre RC1 e RC2 neste momento.

## <a id="upgrade"></a> Atualize o SQL Server em contêineres

Para atualizar a imagem de contêiner com Docker, primeiro identifique a marca para a versão para a atualização. Chamar esta versão do registro com o `docker pull` comando:

```bash
docker pull microsoft/mssql-server-linux:<image_tag>
```

Isso atualiza a imagem do SQL Server para quaisquer novos contêineres que você criar, mas ele não será atualizado do SQL Server em qualquer contêiner em execução. Para fazer isso, você deve criar um novo contêiner com a imagem de contêiner mais recente do SQL Server e migrar os dados para esse novo contêiner.

1. Verifique se você estiver usando um do [técnicas de persistência de dados](#persist) para seu contêiner existente do SQL Server. Isso permite que você inicie um novo contêiner com os mesmos dados.

1. Pare o contêiner do SQL Server com o `docker stop` comando.

1. Criar um novo contêiner de SQL Server com `docker run` e especifique um diretório de host mapeada ou um contêiner de volume de dados. Certifique-se de usar a marca específica para a atualização do SQL Server. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

   > [!IMPORTANT]
   > Somente há suporte para atualização entre RC1, RC2 e GA neste momento.

1. Verifique se seus bancos de dados e os dados no novo contêiner.

1. Opcionalmente, remova o recipiente antigo com `docker rm`.

## <a id="troubleshooting"></a> Solução de problemas

As seções a seguir fornecem sugestões de solução de problemas para executar o SQL Server em contêineres.

### <a name="docker-command-errors"></a>Erros de comando do docker

Se você obtiver erros de qualquer `docker` comandos, certifique-se de que o serviço do docker está em execução e tente executar com permissões elevadas.

Por exemplo, no Linux, você pode obter o seguinte erro ao executar `docker` comandos:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se você receber esse erro no Linux, execute os mesmos comandos precedidos de `sudo`. Se isso falhar, verifique se o serviço do docker está em execução e inicie-o se necessário.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

No Windows, verifique se você estiver iniciando o PowerShell ou o prompt de comando como administrador.

### <a name="sql-server-container-startup-errors"></a>Erros de inicialização do contêiner do SQL Server

Se o contêiner do SQL Server falhar na execução, tente os seguintes testes:

- Se você receber um erro, como **' Falha ao criar o ponto de extremidade CONTAINER_NAME na ponte de rede. Erro ao iniciar o proxy: associação de 0.0.0.0:1433 escuta tcp: endereço já está em uso.'** , em seguida, você está tentando mapear a porta 1433 do contêiner para uma porta que já está em uso. Isso pode acontecer se você estiver executando o SQL Server localmente no computador host. Ele também pode ocorrer se você iniciar dois contêineres de SQL Server e tente mapear ambos na mesma porta de host. Se isso acontecer, use o `-p` parâmetro para mapear a porta 1433 do contêiner para uma porta de host diferente. Por exemplo: 

    ```bash
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d microsoft/mssql-server-linux:2017-latest`.
    ```

- Verifique se há mensagens de erro do contêiner.

    ```bash
    docker logs e69e056c702d
    ```

- Certifique-se de que você atende aos requisitos mínimos de memória e disco especificados no [requisitos](#requirements) seção deste tópico.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo de sqlservr no contêiner é executado como raiz.

- Examine o [os logs de erro e de instalação do SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Habilitar a captura de despejo

Se o processo do SQL Server estiver falhando dentro do contêiner, você deve criar um novo contêiner com **SYS_PTRACE** habilitado. Isso adiciona a capacidade de Linux para rastrear um processo, o que é necessário para a criação de um arquivo de despejo de memória em uma exceção. O arquivo de despejo pode ser usado pelo suporte para ajudar a solucionar o problema. O seguinte comando docker run habilita esse recurso.

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux:2017-latest
```

### <a name="sql-server-connection-failures"></a>Falhas de conexão do SQL Server

Se você não pode se conectar à instância do SQL Server em execução em seu contêiner, tente os seguintes testes:

- Certifique-se de que o contêiner do SQL Server está em execução, observando a **STATUS** coluna o `docker ps -a` saída. Se não, use `docker start <Container ID>` para iniciá-lo.

- Se você tiver mapeado para uma porta de host não padrão (não 1433), verifique se que você está especificando a porta em sua cadeia de conexão. Você pode ver o mapeamento de porta no **portas** coluna o `docker ps -a` saída. Por exemplo, o comando a seguir conecta sqlcmd em um contêiner de escuta na porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se você usou `docker run` com um volume de dados existente ou o contêiner de volume de dados, o SQL Server ignora o valor de `MSSQL_SA_PASSWORD`. Em vez disso, a senha de usuário pré-configurado SA é usada de dados do SQL Server no volume de dados ou no contêiner de volume de dados. Verifique se você está usando a senha associada com os dados que você está anexando a.

- Examine o [os logs de erro e de instalação do SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Grupos de disponibilidade do SQL Server

Se você estiver usando o Docker com grupos de disponibilidade do SQL Server, há dois requisitos adicionais.

- Mapeie a porta que é usada para comunicação de réplica (padrão 5022). Por exemplo, especificar `-p 5022:5022` como parte de sua `docker run` comando.

- Definir explicitamente o nome de host do contêiner com o `-h YOURHOSTNAME` parâmetro o `docker run` comando. Esse nome de host é usado quando você configurar o grupo de disponibilidade. Se você não especificar com `-h`, o padrão é a ID do contêiner.

### <a id="errorlogs"></a> Logs de erro e de instalação do SQL Server

Você pode examinar a instalação do SQL Server e os logs de erro na **/var/opt/mssql/log**. Se o contêiner não está em execução, abra primeiro o contêiner. Em seguida, use um prompt de comando interativo para inspecionar os logs.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Da sessão bash dentro de seu contêiner, execute os seguintes comandos:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se você montou a um diretório de host **/var/opt/mssql** quando você criou seu contêiner, em vez disso, você pode procurar **log** subdiretório no caminho mapeado no host.

## <a name="next-steps"></a>Próximas etapas

Introdução ao SQL Server 2017 imagens de contêiner no Docker por meio de [quickstart](quickstart-install-connect-docker.md).

Além disso, consulte o [repositório do GitHub mssql docker](https://github.com/Microsoft/mssql-docker) para recursos, comentários e problemas conhecidos.
