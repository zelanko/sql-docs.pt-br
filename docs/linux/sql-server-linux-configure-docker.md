---
title: "Opções de configuração para o SQL Server 2017 no Docker | Microsoft Docs"
description: "Explore diferentes maneiras de usar e interagir com o SQL Server 2017 imagens de contêiner no Docker. Isso inclui dados persistentes, copiando arquivos e solução de problemas."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f87c28e4d2ba7689d422ccf2f1a903765a39f27a
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-2017-container-images-on-docker"></a>Configurar imagens de contêiner de 2017 do SQL Server no Docker

Este tópico explica como configurar e usar o [imagem de contêiner mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) com o Docker. Esta imagem consiste em execução no Linux, com base no Ubuntu 16.04 do SQL Server. Ele pode ser usado com o mecanismo do Docker 1.8 + no Linux ou no Docker para Mac/Windows.

> [!NOTE]
> Este tópico enfoca especialmente usando a imagem mssql-server-linux. A imagem do Windows não é coberta, mas você pode aprender mais sobre ele no [página de Hub do Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows/).

## <a name="pull-and-run-the-container-image"></a>Pull e executar a imagem de contêiner

Para efetuar pull e executar o Docker imagem de contêiner para o SQL Server 2017, siga os pré-requisitos e as etapas no tutorial de início rápido do seguinte:

- [Executar a imagem de contêiner de 2017 do SQL Server com o Docker](quickstart-install-connect-docker.md)

Este tópico de configuração fornece conexão adicional e cenários de uso nas seções a seguir.

## <a name="connect-and-query"></a>Conectar e consultar

Você pode se conectar e consultar o SQL Server em um contêiner de seja fora do contêiner ou de dentro do contêiner. As seções a seguir explicam os dois cenários. 

### <a name="tools-outside-the-container"></a>Ferramentas fora do contêiner

Você pode se conectar à instância do SQL Server na máquina Docker de qualquer ferramenta externa de macOS, Windows ou Linux que oferece suporte a conexões de SQL. Algumas ferramentas comuns incluem:

- [Sqlcmd](sql-server-linux-setup-tools.md)
- [Código do Visual Studio](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) no Windows](sql-server-linux-develop-use-ssms.md)

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

1. Use o `docker exec -it` comando para iniciar um shell bash interativo dentro de seu contêiner em execução. No exemplo a seguir `e69e056c702d` é a ID do contêiner.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Sempre, você não precisa especificar a id de contêiner inteiro. Você só precisa especificar caracteres suficientes para identificá-lo exclusivamente. Portanto, neste exemplo, talvez seja suficiente para usar `e6` ou `e69` em vez da id completa.

2. Uma vez dentro do contêiner, conecte-se localmente com o sqlcmd. Observe que sqlcmd não está no caminho por padrão, você precisará especificar o caminho completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Quando terminar com o sqlcmd, digite `exit`.

4. Quando terminar com o prompt de comando interativo, digite `exit`. O contêiner continuará a ser executado depois que você sair shell bash interativo.

## <a name="run-multiple-sql-server-containers"></a>Executar vários contêineres de SQL Server

O docker fornece uma maneira de executar vários contêineres de SQL Server no mesmo computador host. Essa é a abordagem para cenários que exigem várias instâncias do SQL Server no mesmo host. Cada contêiner deve expor em si em uma porta diferente.

O exemplo a seguir cria dois contêineres de SQL Server e mapeá-las para portas **1401** e **1402** no computador host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1401:1433 -d microsoft/mssql-server-linux
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1402:1433 -d microsoft/mssql-server-linux
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

## <a id="persist"></a>Manter seus dados

Suas alterações de configuração do SQL Server e os arquivos de banco de dados são persistentes no contêiner, mesmo se você reiniciar o contêiner com `docker stop` e `docker start`. No entanto, se você remover o contêiner com `docker rm`, tudo no contêiner é excluído, incluindo o SQL Server e seus bancos de dados. A seção a seguir explica como usar **volumes de dados** para manter os arquivos de banco de dados, mesmo se os contêineres associados são excluídos.

> [!IMPORTANT]
> Para o SQL Server, é importante que você compreenda a persistência de dados no Docker. Além de discussão nesta seção, consulte a documentação do Docker em [como gerenciar dados em contêineres do Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montar um diretório de host como volume de dados

A primeira opção é um diretório de montagem no seu host como um volume de dados em seu contêiner. Para fazer isso, use o `docker run` com o `-v <host directory>:/var/opt/mssql` sinalizador. Isso permite que os dados sejam restaurados entre as execuções de contêiner.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

Essa técnica também permite que você compartilhe e exibir os arquivos no host fora do Docker.

> [!IMPORTANT]
> Não há suporte para o mapeamento do volume do host para o Docker no Mac com o SQL Server na imagem do Linux no momento. Use contêineres de volume de dados. Essa restrição é específica para o `/var/opt/msql` directory. Lendo de funciona um diretório montado corretamente. Por exemplo, você pode montar um diretório de host usando – v no Mac e restaurar um backup de um arquivo. bak que reside no host.

### <a name="use-data-volume-containers"></a>Use contêineres de volume de dados

A segunda opção é usar um contêiner de volume de dados. Você pode criar um contêiner de volume de dados, especificando um nome de volume em vez de um diretório de host com o `-v` parâmetro. O exemplo a seguir cria um volume de dados compartilhado denominado **sqlvolume**.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v sqlvolume:/var/opt/mssql -d microsoft/mssql-server-linux
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

## <a name="upgrade-sql-server-in-containers"></a>Atualize o SQL Server em contêineres

Para atualizar a imagem de contêiner com Docker, puxe a versão mais recente do registro. Use o `docker pull` comando:

```bash
docker pull microsoft/mssql-server-linux:latest
```

Isso atualiza a imagem do SQL Server para quaisquer novos contêineres que você criar, mas ele não será atualizado do SQL Server em qualquer contêiner em execução. Para fazer isso, você deve criar um novo contêiner com a imagem de contêiner mais recente do SQL Server e migrar os dados para esse novo contêiner.

1. Primeiro, verifique se você estiver usando um do [técnicas de persistência de dados](#persist) para seu contêiner existente do SQL Server.

2. Pare o contêiner do SQL Server com o `docker stop` comando.

3. Criar um novo contêiner de SQL Server com `docker run` e especifique um diretório de host mapeada ou um contêiner de volume de dados. O novo contêiner agora usa uma nova versão do SQL Server com os dados existentes do SQL Server.

4. Verifique se seus bancos de dados e os dados no novo contêiner.

5. Opcionalmente, remova o recipiente antigo com `docker rm`.

## <a id="troubleshooting"></a>Solução de problemas

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
    docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1400:1433 -d microsoft/mssql-server-linux`.
    ```

- Verifique se há mensagens de erro do contêiner.

    ```bash
    docker logs e69e056c702d
    ```

- Certifique-se de que você atende aos requisitos mínimos de memória e disco especificados no [requisitos](#requirements) seção deste tópico.

- Se você estiver usando qualquer software de gerenciamento de contêiner, verifique se ele dá suporte a processos de contêiner em execução como raiz. O processo de sqlservr no contêiner é executado como raiz.

- Examine o [os logs de erro e de instalação do SQL Server](#errorlogs).

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

### <a id="errorlogs"></a>Logs de erro e de instalação do SQL Server

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

Introdução ao SQL Server 2017 imagens de contêiner no Docker por meio de [tutorial de início rápido](quickstart-install-connect-docker.md).

Além disso, consulte o [repositório do GitHub mssql docker](https://github.com/Microsoft/mssql-docker) para recursos, comentários e problemas conhecidos.

