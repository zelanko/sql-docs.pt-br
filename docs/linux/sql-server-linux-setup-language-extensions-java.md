---
title: Instalar a Extensão de Linguagem Java no Linux
titleSuffix: SQL Server Language Extensions
description: Saiba como instalar a Extensão de Linguagem Java do SQL Server no Red Hat, Ubuntu e SUSE Linux.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e859a445bf4283f7f3d56e04997525ac2823193a
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94585078"
---
# <a name="install-sql-server-java-language-extension-on-linux"></a>Instalar a Extensão de Linguagem Java do SQL Server no Linux

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

Saiba como instalar o componente [Extensão de Linguagem Java](../language-extensions/java-overview.md) do SQL Server no Linux. A Extensão de Linguagem Java faz parte das [Extensões de Linguagem do SQL Server](../language-extensions/language-extensions-overview.md) e é um complemento do mecanismo de banco de dados. 

Embora seja possível [instalar o mecanismo de banco de dados e as extensões de linguagem simultaneamente](#install-all) a melhor prática é instalar e configurar o mecanismo de banco de dados do SQL Server primeiro para que você possa resolver problemas antes de adicionar mais componentes.

## <a name="prerequisites"></a>Pré-requisitos

+ A versão do Linux deve ser [compatível com o SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), sem incluir o Docker Engine. As versões com suporte incluem:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)
   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Você deve ter uma ferramenta para executar comandos T-SQL. Um editor de consultas é necessário para a configuração e a validação pós-instalação. Recomendamos o [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-2017&preserve-view=true#get-azure-data-studio-for-linux), um download gratuito que é executado no Linux.

+ A localização do pacote das extensões Java está nos repositórios de origem do Linux do SQL Server. Se você já configurou repositórios de origem para a instalação do mecanismo de banco de dados, execute os comandos de instalação de pacote **mssql-server-extensibility-java** usando o mesmo registro de repositório.

+ As extensões de linguagem também são compatíveis com contêineres do Linux. Não fornecemos contêineres pré-criados com as extensões de linguagem, mas você pode criar um com base nos contêineres de SQL Server usando [um modelo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

+ As Extensões de Linguagem e os [Serviços de Machine Learning](../machine-learning/index.yml) são instalados por padrão em Clusters de Big Data do SQL Server. Se você usar Clusters de Big Data, não precisará seguir as etapas neste artigo. Para obter mais informações, confira [Usar Serviços de Machine Learning (Python e R) em Clusters de Big Data](../big-data-cluster/machine-learning-services.md).

## <a name="package-list"></a>Lista de pacotes

Em um dispositivo conectado à Internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador de pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis.

| Nome do pacote | Aplica-se a | Descrição |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos os idiomas | Estrutura de extensibilidade usada para a extensão de linguagem Java |
|mssql-server-extensibility-java | Java | Estrutura de extensibilidade usada para a extensão de linguagem Java, incluindo suporte a um runtime Java |

<a name="RHEL"></a>

## <a name="install-java-language-extension"></a>Instalar a Extensão de Linguagem Java

Você pode instalar extensões de linguagem e Java no Linux instalando **mssql-server-extensibility-java**. Quando você instala o **mssql-server-extensibility-java**, o pacote instala automaticamente o JRE 11 caso ainda não esteja instalado. Ele também adicionará o caminho da JVM a uma variável de ambiente chamada JRE_HOME.

> [!Note]
> Em um servidor conectado à Internet, as dependências de pacote são baixadas e instaladas como parte da instalação do pacote principal. Se o servidor não estiver conectado à Internet, confira mais detalhes na [instalação offline](#offline-install).

### <a name="redhat-install-command"></a>Comando de instalação do RedHat

Você pode instalar as extensões de linguagem para Java no RedHat usando o comando a seguir.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Comando de instalação do Ubuntu

Você pode instalar as extensões de linguagem para Java no Ubuntu usando o comando a seguir.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. Além disso, algumas imagens do Docker do Ubuntu podem não ter a opção https apt transport. Para instalá-la, use `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>Comando de instalação do SUSE

Você pode instalar as extensões de linguagem para Java no SUSE usando o comando a seguir.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuração pós-instalação (obrigatória)

1. Conceder permissões no Linux

    Você não precisará executar esta etapa se estiver usando bibliotecas externas. A maneira recomendada de trabalhar é usar bibliotecas externas. Para obter ajuda na criação de uma biblioteca externa com base no arquivo jar, confira [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md)

    Se você não estiver usando bibliotecas externas, será necessário fornecer permissões ao SQL Server para executar as classes Java em seu jar.

    Para permitir acesso de leitura e execução a um arquivo jar, execute o seguinte comando **chmod** no arquivo jar. É recomendável sempre colocar seus arquivos de classe em um jar ao trabalhar com SQL Server. Para obter ajuda para criar um jar, confira [Como criar um arquivo jar](../language-extensions/how-to/create-a-java-jar-file-from-class-files.md).

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    Você também precisa conceder permissões de mssql_satellite ao arquivo jar para ler/executar.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    A configuração adicional é principalmente por meio da [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

2. Adicione a conta de usuário mssql usada para executar o serviço SQL Server. Isso será necessário se você não tiver executado a instalação anteriormente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. Habilite o acesso à rede de saída. O acesso à rede de saída está desabilitado por padrão. Para habilitar as solicitações de saída, defina a propriedade booliana "outboundnetworkaccess" usando a ferramenta mssql-conf. Para obter mais informações, confira [Configurar o SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Reinicie o serviço SQL Server Launchpad e a instância do mecanismo de banco de dados para ler os valores atualizados no arquivo INI. Uma mensagem de reinicialização lembrará você sempre que uma configuração relacionada à extensibilidade for modificada.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Habilite a execução de script externo usando o Azure Data Studio ou outra ferramenta como o SQL Server Management Studio (somente Windows) que executa Transact-SQL.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. Reinicie o serviço `mssql-launchpadd` novamente.

7. Para cada banco de dados no qual você deseja usar extensões de linguagem, é necessário registrar a linguagem externa com [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md).

## <a name="register-external-language"></a>Registrar linguagem externa

Para cada banco de dados no qual você deseja usar extensões de linguagem, é necessário registrar a linguagem externa com [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md).

O exemplo a seguir adiciona uma linguagem externa chamada Java a um banco de dados no SQL Server em Linux.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', 
    FILE_NAME = 'javaextension.so', 
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"/opt/mssql/lib/zulu-jre-11"}')
```
Para a extensão Java, a variável de ambiente "JRE_HOME" é usada para determinar o caminho para localizar e inicializar a JVM.

A ddl CREATE EXTERNAL LANGUAGE fornece um parâmetro (ENVIRONMENT_VARIABLES) para definir variáveis de ambiente especificamente para o processo que hospeda a extensão. Essa é a maneira recomendada e mais eficaz de definir variáveis de ambiente exigidas por extensões de linguagem externa.

Para obter mais informações, confira [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md).

## <a name="verify-installation"></a>Verifique a instalação

A integração de recursos do Java não inclui bibliotecas, mas você pode executar `grep -r JRE_HOME /etc` para confirmar a criação da variável de ambiente JAVA_HOME.

Para validar a instalação, execute um script T-SQL que executa um procedimento armazenado do sistema que invoca o Java. Você precisará de uma ferramenta de consulta para essa tarefa. O Azure Data Studio é uma boa opção. Outras ferramentas usadas com frequência, como o SQL Server Management Studio ou PowerShell, funcionam somente no Windows. Se você tem um computador Windows com essas ferramentas, use-o para conectar-se à instalação do Linux do mecanismo de banco de dados.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-java-language-extension"></a>Instalação completa do SQL Server e da Extensão de Linguagem Java

Você pode instalar e configurar o mecanismo de banco de dados e a Extensão de Linguagem Java em um procedimento acrescentando pacotes e parâmetros Java em um comando que instala o mecanismo de banco de dados.

1. Forneça uma linha de comando que inclua o mecanismo de banco de dados, além dos recursos de extensão de linguagem.

    Você pode adicionar a extensibilidade do Java a uma instalação do mecanismo de banco de dados.

    ```bash
    sudo yum install -y mssql-server mssql-server-extensibility-java 
    ```

1. Aceite os contratos de licença e conclua a configuração pós-instalação. Use a ferramenta **mssql-conf** para esta tarefa.

    ```bash
    sudo /opt/mssql/bin/mssql-conf setup
    ```

    Você será solicitado a aceitar o contrato de licença do mecanismo de banco de dados, escolher uma edição e definir a senha do administrador. 

1. Reinicie o serviço, se solicitado a fazê-lo.

    ```bash
    sudo systemctl restart mssql-server.service
    ```

## <a name="unattended-installation"></a>Instalação autônoma

Use a [instalação autônoma](./sql-server-linux-setup.md#unattended) do Mecanismo de Banco de Dados e adicione os pacotes a **mssql-server-extensibility-java**.

<a name="offline-install"></a>

## <a name="offline-installation"></a>Instalação offline

Siga as instruções de [Instalação offline](sql-server-linux-setup.md#offline) para conhecer as etapas da instalação dos pacotes. Localize o site de download e baixe os pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Várias das ferramentas de gerenciamento de pacotes fornecem comandos que podem ajudá-lo a determinar as dependências do pacote. Para yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.

#### <a name="download-site"></a>Site de download

Você pode baixar os pacotes em [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos os pacotes para Java são colocados com o pacote do mecanismo de banco de dados.

#### <a name="redhat7-paths"></a>Caminhos do RedHat/7

|Pacote|Local de download|
|--|----|
| Pacotes mssql/extensibility-java | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |

#### <a name="ubuntu1604-paths"></a>Caminhos do Ubuntu/16.04

|Pacote|Local de download|
|--|----|
| Pacotes mssql/extensibility-java | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |

#### <a name="suse12-paths"></a>Caminhos do SUSE/12

|Pacote|Local de download|
|--|----|
| Pacotes mssql/extensibility-java | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |

#### <a name="package-list"></a>Lista de pacotes
Dependendo de quais extensões você deseja usar, baixe os pacotes necessários para uma linguagem específica. Os nomes de arquivos exatos incluem informações de plataforma no sufixo, mas os nomes de arquivo abaixo devem ser próximos o suficiente para que você determine quais arquivos serão obtidos.

```
# Core packages
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations"></a>Limitações

A autenticação implícita não está disponível no Linux no momento, o que significa que você não pode se conectar de volta ao servidor de um Java em andamento para acessar dados ou outros recursos.

### <a name="resource-governance"></a>Governança de recursos

Há paridade entre o Linux e o Windows para [Governança de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para pools de recursos externos, mas as estatísticas para [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) atualmente têm unidades diferentes no Linux.

| Nome da coluna   | Descrição | Valor no Linux |
|---------------|--------------|---------------|
|peak_memory_kb | A quantidade máxima de memória usada para o pool de recursos. | No Linux, essa estatística é originada do subsistema de memória CGroups, em que o valor é memory.max_usage_in_bytes |
|write_io_count | O total de E/Ss de gravação emitidas desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada no subsistema CGroups blkio, em que o valor na linha de gravação é blkio.throttle.io_serviced |
|read_io_count | O total de E/S lidas emitidas desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada no subsistema CGroups blkio, em que o valor na linha de leitura é blkio.throttle.io_serviced |
|total_cpu_kernel_ms | O tempo do kernel do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada do subsistema CGroups cpuacct, em que o valor na linha do usuário é cpuacct.stat |  
|total_cpu_user_ms | O tempo de do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas.| No Linux, essa estatística é originada do subsistema CGroups cpuacct, em que o valor na linha do sistema é cpuacct.stat |
|active_processes_count | O número de processos externos em execução no momento da solicitação.| No Linux, essa estatística é obtida do subsistema de pids CGroups, em que o valor é pids.current |

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Java podem começar com alguns exemplos simples e aprender os fundamentos de como o Java funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Expressões regulares com Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)