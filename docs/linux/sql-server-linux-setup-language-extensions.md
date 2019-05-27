---
title: Instalar extensões de linguagem (Java) do SQL Server no Linux | Microsoft Docs
description: Saiba como instalar extensões de linguagem (Java) do SQL Server no Red Hat, Ubuntu e SUSE.
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b694cde8784a1607c85ed9ab7dfcc4d770a6d938
ms.sourcegitcommit: 3b266dc0fdf1431fdca6b2ad34ae5fd38abe9f69
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66186809"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Instalar extensões de linguagem do SQL Server de 2019 (Java) no Linux

Extensões de linguagem são um complemento para o mecanismo de banco de dados. Embora você possa [instalar o mecanismo de banco de dados e extensões de linguagem simultaneamente](#install-all), ele é uma prática recomendada para instalar e configurar o mecanismo de banco de dados do SQL Server pela primeira vez, para que você possa resolver quaisquer problemas antes de adicionar mais componentes. 

Siga as etapas neste artigo para instalar a extensão da linguagem Java.

Local do pacote para as extensões Java está em repositórios de código-fonte do SQL Server Linux. Se você já configurou os repositórios de código-fonte para a instalação do mecanismo de banco de dados, você pode executar o **mssql-server-extensibilidade-java** comandos de instalação usando o mesmo registro do repositório do pacote.

Também há suporte para extensões de linguagem em contêineres do Linux. Nós não oferecemos contêineres de criado previamente com extensões de linguagem, mas você pode criar um dos contêineres do SQL Server usando o [um modelo de exemplo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Desinstalar o CTP anterior

A lista de pacotes foi alterado pela última várias versões CTP, resultando em menos de pacotes. Recomendamos a desinstalação do CTP 2. x para remover todos os pacotes anteriores antes de instalar o CTP 3.0. Não há suporte para a instalação lado a lado de várias versões.

### <a name="1-confirm-package-installation"></a>1. Confirme a instalação do pacote

Você talvez queira verificar a existência de uma instalação anterior como uma primeira etapa. Os arquivos a seguir indicam uma instalação existente: checkinstallextensibility.sh, exthost, barra inicial.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Desinstalar pacotes de 2. x CTP anteriores

Desinstale o nível mais baixo do pacote. Qualquer pacote de upstream dependente de um pacote de nível inferior será desinstalado automaticamente.

  + Para a integração do Java, remover **mssql-server-extensibilidade-java**

Comandos para remover os pacotes são exibidos na tabela a seguir.

| Plataforma  | Comando (s) de remoção de pacote | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-30-install"></a>3. Prosseguir com a instalação do CTP 3.0

Instale com o nível mais alto de pacote usando as instruções neste artigo para seu sistema operacional.

Para cada conjunto de específicas do sistema operacional de instruções de instalação *mais alto nível de pacote* seja **exemplo 1: instalação completa** para o conjunto completo de pacotes, ou **exemplo 2: instalação mínima**  o menor número de pacotes necessários para uma instalação viável.

1. Execute os comandos de instalação usando os gerenciadores de pacotes e a sintaxe para a sua distribuição do Linux: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ A versão do Linux deve ser [suportados pelo SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), mas não inclui o mecanismo do Docker. As versões com suporte incluem:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Você deve ter uma ferramenta para executar comandos do T-SQL. Um editor de consultas é necessário para configuração de pós-instalação e validação. É recomendável [Studio do Azure Data](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), um download gratuito que é executado no Linux.

## <a name="package-list"></a>Lista de pacotes

Em um dispositivo conectado à internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador do pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis.

| Nome do pacote | Aplica-se a | Descrição |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos os idiomas | Estrutura de extensibilidade usada para executar o código Java. |
|mssql-server-extensibility-java | Java | Extensão de Java para o carregamento de um ambiente de execução do Java. Não há bibliotecas adicionais ou pacotes para Java. |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>Instalar extensões de linguagem

Você pode instalar extensões de linguagem e Java no Linux por meio da instalação **mssql-server-extensibilidade-java**. Quando você instala **mssql-server-extensibilidade-java**, o pacote instala automaticamente o JRE 8 se ele não ainda estiver instalado. Ele também adicionará o caminho da JVM para uma variável de ambiente chamada de variável.

> [!Note]
> Em um servidor conectado à internet, as dependências de pacote são baixadas e instaladas como parte da instalação do pacote principal. Se seu servidor não estiver conectado à internet, consulte mais detalhes na [instalação offline](#offline-install).

### <a name="redhat-install-command"></a>Comando de instalação do RedHat

Você pode instalar extensões de linguagem para Java em RedHat usando o comando a seguir.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Comando de instalação do Ubuntu

Você pode instalar extensões de linguagem para Java no Ubuntu usando o comando a seguir.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. Além disso, algumas imagens do docker do Ubuntu podem não ter a opção de transporte apt https. Para instalá-lo, use `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>Comando de instalação do SUSE

Você pode instalar extensões de linguagem para Java no SUSE usando o comando a seguir.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuração de pós-instalação (obrigatória)

1. Conceder permissões no Linux

    Você não precisa executar essa etapa se você estiver usando bibliotecas externas. A maneira recomendada de trabalho está usando bibliotecas externas. Para obter ajuda sobre como criar uma biblioteca externa do seu arquivo jar, consulte [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    Se você não estiver usando bibliotecas externas, você precisa fornecer permissões para executar as classes Java em seu jar do SQL Server.

    Para conceder a leitura e executar o acesso a um arquivo jar, execute o seguinte **chmod** comando no arquivo jar. É recomendável sempre colocar seus arquivos de classe em um pote quando você trabalha com o SQL Server. Para obter ajuda na criação de um jar, consulte [como criar um arquivo jar](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files).

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    Você também precisará conceder permissões de mssql_satellite arquivo jar para leitura/execução.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    Configuração adicional é principalmente por meio de [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

2. Adicione a conta de usuário mssql usada para executar o serviço SQL Server. Isso é necessário se você ainda não executou a instalação anteriormente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. Habilite o acesso de rede de saída. Acesso de rede de saída está desabilitado por padrão. Para habilitar solicitações de saída, defina o "outboundnetworkaccess" propriedade booleana usando a ferramenta mssql-conf. Para obter mais informações, consulte [configurar o SQL Server no Linux com o mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Reinicie o serviço Launchpad do SQL Server e a instância do mecanismo de banco de dados para ler os valores atualizados no arquivo INI. Lembra você de uma mensagem de reinicialização sempre que uma configuração de extensibilidade é modificada.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Habilitar a execução do script externo usando o Studio de dados do Azure ou outra ferramenta como SQL Server Management Studio (somente Windows) que executa o Transact-SQL.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. Reinicie o `mssql-launchpadd` de serviço novamente.

7. Para cada banco de dados que você deseja usar extensões de linguagem no, você precisa registrar a linguagem externa com [IDIOMAS EXTERNOS criar](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="verify-installation"></a>Verifique a instalação

Integração de recursos do Java não inclui bibliotecas, mas você pode executar `grep -r JRE_HOME /etc` para confirmar a criação da variável de ambiente JAVA_HOME.

Para validar a instalação, execute um script T-SQL que executa um sistema Java de invocação de procedimento armazenado. Você precisará de uma ferramenta de consulta para essa tarefa. O estúdio de dados do Azure é uma boa opção. Outras comumente usadas ferramentas, como SQL Server Management Studio ou o PowerShell são somente para Windows. Se você tiver um computador Windows com essas ferramentas, você deve usá-lo para se conectar à sua instalação do Linux do mecanismo de banco de dados.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>Instalação completa do SQL Server e extensões de linguagem

Você pode instalar e configurar o mecanismo de banco de dados e extensões de linguagem em um procedimento acrescentando pacotes Java e parâmetros em um comando que instala o mecanismo de banco de dados.

1. Forneça uma linha de comando que inclui o mecanismo de banco de dados, além de recursos de extensão da linguagem.

  Você pode adicionar Java instalar de extensibilidade para um mecanismo de banco de dados.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. Aceite os contratos de licença e conclua a configuração de pós-instalação. Use o **mssql-conf** ferramenta para essa tarefa.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Você será solicitado a aceitar o contrato de licença para o mecanismo de banco de dados, escolha uma edição e definir a senha de administrador. 

4. Reinicie o serviço, se solicitado a fazê-lo.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Instalação autônoma

Usando o [instalação autônoma](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended) para o mecanismo de banco de dados, adicione os pacotes para o mssql-server-extensibilidade-java.

<a name="offline-install"></a>


## <a name="offline-installation"></a>Instalação offline

Siga as [instalação Offline](sql-server-linux-setup.md#offline) instruções para obter etapas sobre como instalar os pacotes. Localizar seu site de download e, em seguida, baixe pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Muitas das ferramentas de gerenciamento de pacote fornecem comandos que podem ajudá-lo a determinam as dependências do pacote. Para o yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.

#### <a name="download-site"></a>Site de download

Você pode baixar os pacotes a partir [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos os pacotes para Java são colocados com o pacote do mecanismo de banco de dados. 

#### <a name="redhat7-paths"></a>RedHat/7 caminhos

|||
|--|----|
| pacotes de extensibilidade/MSSQL-java | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 caminhos

|||
|--|----|
| pacotes de extensibilidade/MSSQL-java | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>Caminhos do SUSE 12

|||
|--|----|
| pacotes de extensibilidade/MSSQL-java | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>Lista de pacotes

Dependendo de quais extensões que você deseja usar, baixar os pacotes necessários para um idioma específico. Nomes de arquivo exatos incluem informações de plataforma no sufixo, mas os nomes de arquivo abaixo devem ser próximos o suficiente para que você possa determinar quais arquivos para obter.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>Limitações em versões CTP

Extensibilidade de extensões de linguagem e Java no Linux ainda está em desenvolvimento ativo. Os recursos a seguir ainda não estão habilitados na versão de visualização.

+ Autenticação implícita atualmente não está disponível no Linux neste momento, o que significa que você não pode se conectar novamente para o servidor do Java em andamento para acessar dados ou outros recursos.


### <a name="resource-governance"></a>Governança de recursos

Há uma paridade entre Linux e Windows para [governança de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para pools de recursos externos, mas as estatísticas [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tem no momento diferentes unidades no Linux. Unidades são alinhados em um CTP futuro.
 
| Nome da coluna   | Descrição | O valor no Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | A quantidade máxima de memória usada para o pool de recursos. | No Linux, essa estatística é originada do subsistema de memória de CGroups, onde o valor é memory.max_usage_in_bytes |
|write_io_count | O total SS de gravação emitidas desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de blkio CGroups, onde o valor da linha de gravação é blkio.throttle.io_serviced | 
|read_io_count | O total lidas emitidas desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de blkio CGroups, onde o valor da linha de leitura é blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | O usuário kernel tempo de CPU cumulativo em milissegundos desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de cpuacct CGroups, onde o valor da linha do usuário é cpuacct.stat |  
|total_cpu_user_ms | O tempo de usuário de CPU cumulativo em milissegundos desde que as estatísticas do administrador de recursos foram redefinidas.| No Linux, essa estatística é originada do subsistema de cpuacct CGroups, onde o valor no valor de linha do sistema é cpuacct.stat | 
|active_processes_count | O número de processos externos em execução no momento da solicitação.| No Linux, essa estatística é originada do subsistema de pids GGroups, onde o valor é pids.current | 

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de Java podem começar com alguns exemplos simples e aprender as Noções básicas de como funciona o Java com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Expressões regulares com Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)