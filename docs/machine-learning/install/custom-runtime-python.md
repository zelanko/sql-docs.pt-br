---
title: Instalar um runtime personalizado de Python
description: Saiba como instalar um runtime personalizado de Python para o SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ca8827f5dcee9b25d873ac7fed83679480bedb44
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91227260"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>Instalar um runtime personalizado de Python para o SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como instalar um runtime personalizado para executar scripts de Python com o SQL Server. O runtime personalizado para Python pode ser utilizado nos seguintes cenários:

+ Uma instalação do SQL Server com estrutura de extensibilidade.

+ Uma instalação dos Serviços de Machine Learning com o SQL Server 2019. A extensão de linguagem pode ser usada com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) após a conclusão de algumas etapas de configuração adicionais.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Este artigo descreve como instalar um runtime personalizado para Python no Windows. Para instalar no Linux, confira [Instalar um runtime personalizado de Python para o SQL Server em Linux](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true).

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

Antes de instalar um runtime personalizado de Python, instale o seguinte:

+ [SQL Server 2019 para Windows CU3 ou posterior](../../database-engine/install-windows/install-sql-server.md).

  > [!NOTE]
  > O runtime personalizado de Python requer a CU (Atualização Cumulativa) 3 ou posterior para o SQL Server 2019.

+ [Extensões de Linguagem do SQL Server no Windows com a estrutura de extensibilidade](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md).

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-windows"></a>Adicionar Extensões de Linguagem do SQL Server para Windows

> [!NOTE]
> Se você tem os Serviços de Machine Learning instalados no SQL Server 2019, a estrutura de extensibilidade já está instalada e você pode ignorar esta etapa.

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server.

1. Inicie o assistente de instalação do SQL Server 2019.
  
1. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.
    
    ![Instalação do SQL Server 2019 CU3 ou posterior](../install/media/2019setup-installation-page-mlsvcs.png) 

1. Na página **Seleção de Recursos** , selecione estas opções:
  
    - **Serviços do Mecanismo de Banco de Dados**
  
        Para usar as Extensões de Linguagem com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.
  
    - **Serviços de Machine Learning e Extensões de Linguagem**
   
       Selecione **Serviços de Machine Learning e Extensões de Linguagem**. Não é necessário selecionar o Python.

    ![Recursos da instalação do SQL Server 2019 CU3 ou posteriores](../install/media/sql-feature-selection.png) 

1. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.
  
    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning e Extensões de Linguagem

1. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).


## <a name="install-python-37"></a>Instale o Python 3.7 

Instale o [Python 3.7]( https://www.python.org/downloads/release/python-379/) e adicione-o ao PATH.

![Adicionar o Python 3.7 ao caminho.](../install/media/python-379.png) **atualizar observação – observação**


#### <a name="install-pandas"></a>Instalar o pandas

Instale o pacote [pandas](https://pandas.pydata.org/) para Python em um prompt de comandos *com privilégios elevados*:

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>Atualizar as variáveis de ambiente do sistema

Adicione ou modifique PYTHONHOME como uma variável de ambiente do sistema.

+ Na caixa de pesquisa do Windows, digite "ambiente" e selecione **Editar as variáveis de ambiente do sistema**.
+ Na guia **Avançado**, selecione **Variáveis de Ambiente**.
+ Em **Variáveis do sistema**, selecione **Novo** para criar PYTHONHOME para apontar para o local de instalação do Python 3.7.
Se PYTHONHOME já existir, selecione **Editar** para apontar para o local de instalação do Python 3.7.
+ Selecione **OK** para fechar as janelas restantes.

![Criar variável do sistema PYTHONHOME.](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>Permitir acesso à pasta da instalação de Python personalizada

Execute os comandos **icacls** a seguir em um novo prompt de comandos *com privilégios elevados* para conceder o acesso de LEITURA E EXECUÇÃO a PYTHONHOME ao **Serviço SQL Server Launchpad** e à SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**). O nome de usuário do serviço Launchpad está no formato `NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME`, que é o nome da instância de seu SQL Server. Os comandos permitirão recursivamente acesso a todos os arquivos e pastas no caminho de diretório especificado.

Acrescente o nome da instância a `MSSQLLAUNCHPAD` (`MSSQLLAUNCHPAD$INSTANCENAME`). Neste exemplo, INSTANCENAME é a instância padrão `MSSQLSERVER`.

1. Conceder permissões ao **Nome de usuário do Serviço SQL Server Launchpad**.

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

Como alternativa, clique com o botão direito do mouse no serviço SQL Server Launchpad no aplicativo **Serviços** do sistema e clique no comando **Reiniciar**. Ou use o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md) para reiniciar o serviço.

## <a name="download-python-language-extension"></a>Baixar a extensão de linguagem Python

Baixe o [arquivo zip que contém a extensão da linguagem Python para Windows](https://github.com/microsoft/sql-server-language-extensions/releases). Recomendado o uso da versão de lançamento em produção. Use a versão de depuração em desenvolvimento ou teste, uma vez que ela fornece informações detalhadas de log para investigar os erros.

## <a name="register-external-language"></a>Registrar linguagem externa

Registre essa extensão da linguagem Python com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada banco de dados no qual deseja usá-la. Use o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) para se conectar ao SQL Server e execute o comando T-SQL a seguir. Modifique o caminho na instrução de maneira a refletir o local do arquivo zip da extensão de linguagem baixada (python-lang-extension.zip).

> [!NOTE]
> Python é uma palavra reservada. Use um nome diferente para o idioma externo, por exemplo, "myPython".

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

Você pode instalar o SQL Server no Red Hat Enterprise Linux (RHEL), no SUSE Linux Enterprise Server (SLES) e no Ubuntu. Para obter mais informações, confira [a seção Plataformas com suporte nas Diretrizes de instalação para SQL Server em Linux](../../linux/sql-server-linux-setup.md).

> [!NOTE]
> Este artigo descreve como instalar um runtime personalizado para Python no Linux. Para instalar no Windows, confira [Instalar um runtime personalizado de Python para o SQL Server no Windows](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true)

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

Antes de instalar um runtime personalizado de Python, instale o seguinte:

+ [SQL Server 2019 para Linux (Atualização Cumulativa 3 ou posterior)](../../linux/sql-server-linux-setup.md).
Ao instalar o SQL Server em Linux, é necessário configurar um repositório da Microsoft. Para obter mais informações, confira [configurando repositórios](../../linux/sql-server-linux-change-repo.md)

  > [!NOTE]
  > O runtime personalizado de Python requer a CU (Atualização Cumulativa) 3 ou posterior para o SQL Server 2019.

+ [Extensões de Linguagem do SQL Server no Linux com a estrutura de extensibilidade](../../linux/sql-server-linux-setup-language-extensions.md).

+ [Python 3.7](https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-linux"></a>Adicionar Extensões de Linguagem do SQL Server para Linux

> [!NOTE]
> Se você tem os Serviços de Machine Learning instalados no SQL Server 2019, o pacote **mssql-server-extensibility** de extensões de linguagem já está instalado e você pode ignorar esta etapa.

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server.

Use os comandos a seguir para instalar as Extensões de Linguagem, de acordo com sua versão do Linux.

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> Se possível, `update` para atualizar os pacotes no sistema antes da instalação. O Ubuntu pode não ter a opção de transporte https apt. Para instalá-la, use `apt-get install apt-transport-https`.

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

## <a name="install-python-37-and-pandas"></a>Instalar Python 3.7 e pandas

Instale o Python 3.7, a biblioteca libpython3.7 e o pacote pandas. 

Os seguintes comandos são exemplo para o Ubuntu:

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="using-a-custom-installation-of-python-37"></a>Usando uma instalação personalizada de Python 3.7

> [!NOTE]
> Se tiver instalado o Python no local padrão `/usr/lib/python3.7`, vá diretamente para a [próxima seção](#download-python-linux).

Se você criou sua própria versão do Python 3.7, use os comandos a seguir para que o SQL Server possa localizar e carregar sua instalação personalizada.

### <a name="update-the-environment-variables"></a>Atualizar as variáveis de ambiente

1. Edite o serviço mssql-launchpadd para adicionar a variável de ambiente PYTHONHOME ao arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + Insira o texto a seguir no arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` que é aberto. Defina o valor de PYTHONHOME como o caminho de instalação personalizada de Python.

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + Salve-o e feche-o.

2. Verifique se `libpython3.7m.so.1.0` pode ser carregado.

    + Crie um arquivo custom-python.conf em `/etc/ld.so.conf.d`.

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + No arquivo que é aberto, adicione o caminho para **libpython3.7m.so.1.0** da instalação personalizada do Python.

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + Salve e feche o novo arquivo.

    + Execute `ldconfig` e verifique se `libpython3.7m.so.1.0` pode ser carregado executando os comandos a seguir e verificando se todas as bibliotecas dependentes podem ser encontradas.

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>Permitir acesso à pasta do Python personalizado

Defina a opção `datadirectories` na seção de extensibilidade do arquivo /var/opt/mssql/mssql.conf como a instalação personalizada de Python.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>Reiniciar o serviço mssql-launchpadd

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a> Baixar a extensão de linguagem Python

Baixe o [arquivo zip que contém a extensão da linguagem Python para Linux](https://github.com/microsoft/sql-server-language-extensions/releases). Recomendado o uso da versão de lançamento em produção. Use a versão de depuração em desenvolvimento ou teste, uma vez que ela fornece informações detalhadas de log para investigar os erros.

## <a name="register-external-language"></a>Registrar linguagem externa

Registre essa extensão da linguagem Python com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada banco de dados no qual deseja usá-la. Use o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) para se conectar ao SQL Server e execute o comando T-SQL a seguir. 
Modifique o caminho na instrução de maneira a refletir o local do arquivo zip da extensão de linguagem baixada (python-lang-extension.zip).

> [!NOTE]
>Python é uma palavra reservada. Use um nome diferente para o idioma externo, por exemplo, "myPython".

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>Habilitar a execução de script externo no SQL Server

Um script externo em Python pode ser executado por meio do procedimento armazenado [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) executado no SQL Server. 

Para habilitar scripts externos, execute os comandos SQL a seguir usando o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) conectado ao SQL Server.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>Verificar a instalação da extensão de linguagem

Este script SQL testa a funcionalidade da extensão de linguagem instalada.

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>Verificar parâmetros e conjuntos de dados de diferentes tipos

Esse script testa tipos de dados diferentes para parâmetros de entrada/saída e conjuntos de dados.

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>Próximas etapas

+ [Estrutura de extensibilidade no SQL Server](../concepts/extensibility-framework.md)
+ [Visão geral das Extensões de Linguagem](../../language-extensions/language-extensions-overview.md)
