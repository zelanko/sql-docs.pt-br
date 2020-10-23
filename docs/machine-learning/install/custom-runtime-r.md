---
title: Instalar runtime personalizado de R
description: Saiba como instalar um runtime personalizado de R para o SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8f3ee552c2e58fa295d4a0094430bfca4ef3dcac
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155086"
---
# <a name="install-an-r-custom-runtime-for-sql-server"></a>Instalar um runtime personalizado de R para o SQL Server

[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como instalar um runtime personalizado para executar scripts de R com o SQL Server. O runtime personalizado usa tecnologia de extensão de linguagem baseada em uma estrutura de extensibilidade para executar código externo. O runtime personalizado para R pode ser utilizado nos seguintes cenários:

+ Uma instalação do SQL Server com estrutura de extensibilidade.

+ Uma instalação dos Serviços de Machine Learning com o SQL Server 2019. A extensão de linguagem pode ser usada com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) após a conclusão de algumas etapas de configuração adicionais.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Este artigo descreve como instalar um runtime personalizado para R no Windows. Para instalar no Linux, confira [Instalar um runtime personalizado de R para o SQL Server em Linux](custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true)

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

Antes de instalar um runtime personalizado de R, instale o seguinte:

+ [SQL Server 2019 para Windows (Atualização Cumulativa 3 ou posterior)](../../database-engine/install-windows/install-sql-server.md).

+ [Extensões de Linguagem do SQL Server no Windows com a estrutura de extensibilidade](../../language-extensions/install/windows-java.md).

+ [R versão 3.3 ou superior](https://cran.r-project.org/).

## <a name="add-sql-server-language-extensions-for-windows"></a>Adicionar Extensões de Linguagem do SQL Server para Windows

> [!NOTE]
> Se você tem os Serviços de Machine Learning instalados no SQL Server 2019, a estrutura de extensibilidade para extensões de linguagem com o serviço Launchpad já está instalada e você pode ignorar esta etapa.

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server.

1. Inicie o assistente de instalação do SQL Server 2019.

1. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

    ![Instalação do SQL Server 2019 CU3 ou posterior](../install/media/2019setup-installation-page-mlsvcs.png)

1. Na página **Seleção de Recursos** , selecione estas opções:

    - **Serviços do Mecanismo de Banco de Dados**

        Para usar as Extensões de Linguagem com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.

    - **Serviços de Machine Learning e Extensões de Linguagem**

       Selecione **Serviços de Machine Learning e Extensões de Linguagem**. Não é necessário selecionar o R.

    ![Recursos da instalação do SQL Server 2019 CU3 ou posteriores](../install/media/sql-feature-selection.png)

1. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.

    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning e Extensões de Linguagem

1. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

## <a name="install-r"></a>Instalar R

> [!NOTE]
>Para os Serviços de Machine Learning SQL, o R já está instalado na pasta **R_SERVICES** da instância do SQL Server. Por exemplo, "C:\Arquivos de Programas\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES". Se quiser continuar usando esse caminho como seu R_HOME, prossiga para a próxima etapa de instalação do Rcpp. Caso contrário, se quiser usar um runtime diferente de R, continue aqui para instalá-lo.

Instale o [R (3.3 ou superior)](https://cran.r-project.org/bin/windows/base/) e tome nota do caminho em que ele foi instalado. Esse caminho é seu **R_HOME**. Por exemplo, conforme mostrado aqui, R_HOME é "C:\Arquivos de Programas\R\R-4.0.2"

![Instalar o R personalizado](../install/media/custom-r-installation.png)

> [!NOTE]
>Nas instruções a seguir, % R_HOME% é o caminho para a instalação de R e deve ser substituído por esse valor.

## <a name="install-rcpp-package"></a>Instalar o pacote Rcpp

+ Localize o executável de R em %R_HOME%\bin. Por padrão, ele fica em `C:\Program Files\R\R-4.0.2\bin`.

+ Inicie o R de um prompt de comandos *com privilégios elevados*:

```CMD
%R_HOME%\bin\R.exe
```

Nesse prompt de R *com privilégios elevados* (%R_HOME%\bin\R.exe), execute o script a seguir para instalar o pacote Rcpp na pasta %R_HOME%\library.

```R
install.packages("Rcpp", lib="%R_HOME%/library");
```

## <a name="update-the-system-environment-variables"></a>Atualizar as variáveis de ambiente do sistema

1. Adicione ou modifique **R_HOME** como uma variável de ambiente do sistema.
    + Na caixa de pesquisa do Windows, digite "ambiente" e selecione **Editar as variáveis de ambiente do sistema**.
    + Na guia **Avançado**, selecione **Variáveis de Ambiente**.

    + Em **Variáveis do sistema**, selecione **Novo** para criar R_HOME.
    Para modificar, selecione **Editar** para alterá-la. Modifique seu valor de maneira a apontar para o caminho de instalação de R personalizado.

    ![Crie a variável de ambiente do sistema R_HOME.](../install/media/sys-env-r-home.png)

2. Atualize a variável de ambiente **PATH**.
    Acrescente o caminho para **R.dll** à variável de ambiente **PATH** do sistema. Selecione **PATH**, escolha **Editar** e adicione `%R_HOME%\bin\x64` à lista de caminhos.

    ![Acrescente à variável de ambiente do sistema PATH.](../install/media/sys-env-path-r.png)

3. Selecione **OK** para fechar as janelas restantes.

    Como alternativa, para definir essas variáveis de ambiente em um prompt de comandos *com privilégios elevados*, execute os comandos a seguir. Certifique-se de usar o caminho de instalação de R personalizado.

```CMD
setx /m R_HOME "path\to\installation\of\R"
setx /m PATH "path\to\installation\of\R\bin\x64;%PATH%"
```

## <a name="grant-access-to-the-custom-r-installation-folder"></a>Permitir acesso à pasta da instalação de R personalizada

> [!NOTE]
>Se tiver instalado o R no local padrão **C:\Arquivo de Programas\R\R-version**, ignore esta etapa.

Execute os comandos **icacls** em um novo prompt de comandos *com privilégios elevados* para conceder o acesso de LEITURA E EXECUÇÃO ao **Nome de usuário do Serviço SQL Server Launchpad** e à SID **S-1-15-2-1** (**TODOS OS PACOTES DE APLICATIVOS**). O nome de usuário do serviço Launchpad está no formato `NT Service\MSSQLLAUNCHPAD$INSTANCENAME`, em que `INSTANCENAME` é o nome da instância de seu SQL Server.

Os comandos permitirão recursivamente acesso a todos os arquivos e pastas no caminho de diretório especificado.

Acrescente o nome da instância a `MSSQLLAUNCHPAD` (`MSSQLLAUNCHPAD$INSTANCENAME`). Neste exemplo, `INSTANCENAME` é a instância padrão `MSSQLSERVER`.

1. Conceder permissões ao **Nome de usuário do Serviço SQL Server Launchpad**

    ```cmd
    icacls "%R_HOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T
    ```
2. Conceda permissões a **SID S-1-15-2-1**

    ```cmd
    icacls "%R_HOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.


```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

Como alternativa, clique com o botão direito do mouse no serviço SQL Server Launchpad no aplicativo **Serviços** do sistema e selecione o comando **Reiniciar**. Ou use o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md) para reiniciar o serviço.

## <a name="download-r-language-extension"></a>Baixar a extensão da linguagem R

Baixe o [arquivo zip que contém a extensão da linguagem R para Windows](https://github.com/microsoft/sql-server-language-extensions/releases). Recomendado o uso da versão de lançamento em produção. Use a versão de depuração em desenvolvimento ou teste, uma vez que ela fornece informações detalhadas de log para investigar os erros.

## <a name="register-external-language"></a>Registrar linguagem externa

Registre essa extensão da linguagem R com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada banco de dados no qual deseja usá-la. Use o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) para se conectar ao SQL Server e execute o comando T-SQL a seguir.
Modifique o caminho na instrução de maneira a refletir o local do arquivo zip da extensão de linguagem baixada (R-lang-extension.zip).

> [!NOTE]
>**R** é uma palavra reservada. Use um nome diferente para o idioma externo, por exemplo, "myR".

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

Você pode instalar o SQL Server no Red Hat Enterprise Linux (RHEL), no SUSE Linux Enterprise Server (SLES) e no Ubuntu. Para obter mais informações, confira [a seção Plataformas com suporte nas Diretrizes de instalação para SQL Server em Linux](../../linux/sql-server-linux-setup.md#supportedplatforms).

> [!NOTE]
> Este artigo descreve como instalar um runtime personalizado para R no Linux. Para instalar no Windows, confira [Instalar um runtime personalizado de R para o SQL Server no Windows](custom-runtime-r.md?view=sql-server-ver15&preserve-view=true)

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

Antes de instalar um runtime personalizado de R, instale o seguinte:

+ [SQL Server 2019 para Linux (Atualização Cumulativa 3 ou posterior)](../../linux/sql-server-linux-setup.md).
Antes de instalar o SQL Server em Linux, é necessário configurar um repositório da Microsoft. Para obter mais informações, confira [configurando repositórios](../../linux/sql-server-linux-change-repo.md).

+ [Extensões de Linguagem do SQL Server no Linux com a estrutura de extensibilidade](../../linux/sql-server-linux-setup-language-extensions-java.md).

+ [R versão 3.3 ou superior](https://cran.r-project.org/).

## <a name="add-sql-server-language-extensions-for-linux"></a>Adicionar Extensões de Linguagem do SQL Server para Linux

> [!NOTE]
> Se você tem os Serviços de Machine Learning instalados no SQL Server 2019, o pacote **mssql-server-extensibility** de extensões de linguagem já está instalado e você pode ignorar esta etapa.

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server.

Use os comandos a seguir para instalar as Extensões de Linguagem, de acordo com sua versão do Linux.

### <a name="ubuntu"></a>Ubuntu
> [!Tip]
> Se possível, `sudo apt-get update` para atualizar os pacotes no sistema antes da instalação. O Ubuntu pode não ter a opção de transporte https apt. Para instalá-la, use `sudo apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>Suse
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-r"></a>Instalar R

>[!NOTE]
>Para os Serviços de Machine Learning SQL, o R já está instalado em `/opt/microsoft/ropen/3.5.2/lib64/R`. Se quiser continuar usando esse caminho como seu R_HOME, prossiga para a próxima etapa de **instalação do Rcpp**. 

Se quiser usar um runtime diferente de R, você precisará remover `microsoft-r-open-mro` antes de continuar a instalar uma nova versão. Exemplo para o Ubuntu:

```bash
sudo apt remove microsoft-r-open-mro-3.5.2
```

Siga as [instruções](https://cran.r-project.org/bin/linux/) para concluir a instalação do R (3.3 ou posterior) para sua respectiva plataforma Linux. Por padrão, o R é instalado em **/usr/lib/R**. Esse caminho é seu **R_HOME**. Se você instalar o R em um local diferente, anote esse caminho como seu R_HOME.

Instruções de exemplo para o Ubuntu. Altere a URL do repositório abaixo para sua versão do R.

```bash
export DEBIAN_FRONTEND=noninteractive
sudo apt-get update
sudo apt-get --no-install-recommends -y install curl zip unzip apt-transport-https libstdc++6

# Add R CRAN repository. This repository works for R 4.0.x.
#
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran40/'
sudo apt-get update

# Install R runtime.
#
sudo apt-get -y install r-base-core
```

## <a name="install-rcpp-package"></a>Instalar o pacote Rcpp

Nas instruções a seguir, ${R_HOME} é o caminho para a instalação de R. 

+ Localize o binário de R em ${R_HOME}/bin. Por padrão, ele está em **/usr/lib/R/bin**.

+ Iniciar R

  ```bash
  sudo ${R_HOME}/bin/R
  ```

+ Nesse prompt de R *com privilégios elevados* (${R_HOME}/bin/R), execute o script a seguir para instalar o pacote **Rcpp** na pasta ${R_HOME}/library.

  ```R
  install.packages("Rcpp", lib = "${R_HOME}/library");
  ```

## <a name="using-a-custom-installation-of-r"></a>Usando uma instalação personalizada de R

> [!NOTE]
>Se tiver instalado o R no local padrão **/usr/lib/R**, ignore esta seção.

### <a name="update-the-environment-variables"></a>Atualizar as variáveis de ambiente

1. Edite o serviço mssql-launchpadd para adicionar a variável de ambiente R_HOME ao arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`

    ```bash
    sudo systemctl edit mssql-launchpadd
    ```

    + Insira o texto a seguir no arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` que é aberto. Defina o valor de R_HOME como o caminho de instalação personalizada de R.

    ```text
    [Service]
    Environment="R_HOME=/path/to/installation/of/R"
    ```

    + Salve-o e feche-o.

2. Certifique-se de que **libR.so** possa ser carregado.

    + Crie um arquivo custom-r.conf em **/etc/ld.so.conf.d**.

    ```bash
    sudo vi /etc/ld.so.conf.d/custom-r.conf
    ```

    + No arquivo que é aberto, adicione o caminho para **libR.so** da instalação personalizada de R.

    ```vi editor
    /path/to/installation/of/R/lib
    ```

    + Salve e feche o novo arquivo.

    + Execute `ldconfig` e verifique se **libR.so** pode ser carregado executando o comando a seguir e verificando se todas as bibliotecas dependentes podem ser encontradas.

    ```bash
    sudo ldconfig
    ldd /path/to/installation/of/R/lib/libR.so
    ```

### <a name="grant-access-to-the-custom-r-installation-folder"></a>Permitir acesso à pasta da instalação de R personalizada

Defina a opção `datadirectories` na seção de extensibilidade do arquivo /var/opt/mssql/mssql.conf como a instalação personalizada de R.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/R
```

### <a name="restart-mssql-launchpadd-service"></a>Reiniciar o serviço mssql-launchpadd

> [!NOTE]
>Se tiver instalado o R no local padrão **/usr/lib/R**, ignore esta etapa.

```bash
sudo systemctl restart mssql-launchpadd
```

## <a name="download-r-language-extension"></a>Baixar a extensão da linguagem R

Baixe o [arquivo zip que contém a extensão da linguagem R para Linux](https://github.com/microsoft/sql-server-language-extensions/releases). Recomendado o uso da versão de lançamento em produção. Use a versão de depuração em desenvolvimento ou teste, uma vez que ela fornece informações detalhadas de log para investigar os erros.

## <a name="register-external-language"></a>Registrar linguagem externa

Registre essa extensão da linguagem R com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada banco de dados no qual deseja usá-la. Use o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) para se conectar ao SQL Server e execute o comando T-SQL a seguir. 
Modifique o caminho na instrução de maneira a refletir o local do arquivo zip da extensão de linguagem baixada (r-lang-extension.zip).


> [!NOTE]
>**R** é uma palavra reservada. Use um nome diferente para o idioma externo, por exemplo, "myR".

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>Habilitar a execução de script externo no SQL Server

Um script externo em R pode ser executado por meio do procedimento armazenado [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) executado no SQL Server. 

Para habilitar scripts externos, execute os comandos SQL a seguir usando o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) conectado ao SQL Server.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="verify-language-extension-installation"></a>Verificar a instalação da extensão de linguagem

Este script SQL verifica a instalação bem-sucedida da extensão da linguagem R personalizada. A saída desse script deve exibir R_HOME, o caminho para R e a versão do runtime de R personalizado. Ela confirma que o script está usando o runtime personalizado.

```sql
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(R.home());
print(file.path(R.home("bin"), "R"));
print(R.version);
print("Hello RExtension!");'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>Verificar parâmetros e conjuntos de dados de diferentes tipos

Esse script testa tipos de dados diferentes para parâmetros de entrada/saída e conjuntos de dados.

```sql
DECLARE @sumVal INT = 12;
DECLARE @charVal VARCHAR(30) = N'Hello';
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(sumVal);
print(charVal);
sumVal <- sumVal + 300;
OutputDataSet <- InputDataSet;'
    ,@input_data_1 = N'select 1, cast(1.4 as real), ''Hi'', cast(''1'' as bit)'
    ,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
    ,@sumVal = @sumVal OUTPUT
    ,@charVal =  @charVal
WITH RESULT SETS ((intCol INT, doubleCol REAL, charCol CHAR(2), logicalCol BIT));
PRINT @sumVal;
```

## <a name="see-also"></a>Confira também

+ [Estrutura de extensibilidade no SQL Server](../concepts/extensibility-framework.md)
+ [Visão geral das Extensões de Linguagem](../../language-extensions/language-extensions-overview.md)