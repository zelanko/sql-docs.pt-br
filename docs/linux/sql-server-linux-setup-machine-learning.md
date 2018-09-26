---
title: Instalar o SQL Server serviços de Machine Learning (R, Python, Java) no Linux | Microsoft Docs
description: Este artigo descreve como instalar os serviços SQL Server Machine Learning (R, Python, Java) no Red Hat e Ubuntu.
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5d10e6646d83d90af60aa748a8265a069d961443
ms.sourcegitcommit: c3e233c13ebb6fbee60723590179da00802c3f3a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47058925"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>Instalar o SQL Server de 2019 serviços de Machine Learning (R, Python, Java) no Linux

[Serviços do SQL Server Machine Learning](../advanced-analytics/what-is-sql-server-machine-learning.md) é executado em sistemas operacionais Linux nesta versão de visualização do SQL Server 2019. Siga as etapas neste artigo para instalar a extensão de programação Java, ou a aprendizado de máquina extensões para R e Python. 

Aprendizado de máquina e extensões de programação é um complemento para o mecanismo de banco de dados. Embora você possa [instalar o mecanismo de banco de dados e os serviços de Machine Learning simultaneamente](#install-all), ele é uma prática recomendada para instalar e configurar o mecanismo de banco de dados do SQL Server pela primeira vez, para que você possa resolver quaisquer problemas antes de adicionar mais componentes. 

Local do pacote das extensões de R, Python e Java estão em repositórios de código-fonte do SQL Server Linux. Se você já configurou instalar de repositórios de código-fonte para o mecanismo de banco de dados, você pode executar comandos de instalação do pacote usando o mesmo registro do repositório mssql-mlservices.

## <a name="prerequisites"></a>Prerequisites

+ Sistema operacional Linux deve ser [suportados pelo SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), em execução no local ou em um contêiner do Docker.

+ Você deve ter uma instância do mecanismo de banco de dados do SQL Server de 2019 em: 

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Para R somente [Microsoft R Open](#mro) para pacotes de R mlsservices mssql. 

<a name="mro"></a>

### <a name="microsoft-r-open-mro"></a>Microsoft R Open MRO)

Distribuição de R base da Microsoft é um pré-requisito para usar o RevoScaleR, MicrosoftML e outros pacotes de R instalados com os serviços de aprendizado de máquina.

Os comandos a seguir registre o repositório fornecendo MRO. Após o registro, os comandos para instalar outros pacotes de R incluirá automaticamente MRO como uma dependência de pacote.

#### <a name="on-ubuntu"></a>No Ubuntu

```bash
# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 18.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb
```

#### <a name="on-rhel"></a>No RHEL

```bash
# Set the location of the package repo at the "prod" directory
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
```
#### <a name="on-suse"></a>No SUSE

```bash
# Set the location of the package repo
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com
```

## <a name="package-list"></a>Lista de pacotes

Em um dispositivo conectado à internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador do pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis, mas para instalações conectados à internet, você só precisa *um* pacote R ou Python para obter uma combinação específica de recursos.

| Nome do pacote | Aplica-se a | Description |
|--------------|----------|-------------|
|MSSQL-server-extensibilidade  | Todos | Estrutura de extensibilidade usada para executar código R, Python ou Java. |
|MSSQL-server-extensibilidade-java | Java | Extensão de Java para o carregamento de um ambiente de execução do Java. Não há bibliotecas adicionais ou pacotes para Java. |
| Microsoft openmpi  | Python, R | Interface usada pelas bibliotecas de Revo * para paralelização no Linux de transmissão de mensagens. |
| Microsoft-r-open | R | Distribuição de software livre do R. |
| MSSQL-mlservices-python | Python | Distribuição do código-fonte aberto do Anaconda e Python. |
|MSSQL-mlservices mlm py  | Python | Instalação completa. Fornece modelos para análise de sentimento de texto e personalização de imagem revoscalepy, microsoftml, pré-treinados.| 
|MSSQL-mlservices mml py  | Python | Instalação parcial. Fornece revoscalepy, microsoftml. <br/>Exclui modelos previamente treinados. | 
|MSSQL-mlservices pacotes py  | Python | Instalação parcial. Fornece revoscalepy. <br/>Exclui o microsoftml e modelos previamente treinados. | 
|MSSQL-mlservices-mlm-r  | R | Instalação completa. Fornece modelos para análise de sentimento de texto e personalização de imagem RevoScaleR, MicrosoftML, sqlRUtils, olapR, pré-treinados.| 
|MSSQL-mlservices-mml-r  | R | Instalação parcial. Fornece o RevoScaleR, MicrosoftML, sqlRUtils, olapR. <br/>Exclui modelos previamente treinados.  |
|MSSQL-mlservices pacotes r  | R | Instalação parcial. Fornece o RevoScaleR, sqlRUtils, olapR. <br/>Exclui modelos previamente treinados e MicrosoftML. | 

<a name="RHEL"></a>

## <a name="rhel-commands"></a>Comandos do RHEL

Instalar qualquer *uma* pacote R, além de qualquer *um* pacote do Python e Java, se você quiser que esse recurso. Cada pacote de R e Python inclui um pacote de recursos. Escolha o pacote que fornece o conjunto de recursos que você precisa. Pacotes dependentes são incluídos automaticamente.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. Para R e Python, se você quiser que algo entre mínimo e completo install -, como bibliotecas de aprendizado de máquina, mas sem os modelos previamente treinados - substituir `mssql-mlservices-mml-r-9.4.5*` e `mssql-mlservices-mml-py-9.4.5*` em vez disso.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.5*
sudo yum install mssql-mlservices-mlm-r-9.4.5* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi Revo * bibliotecas principais para R e Python, Java extension. Exclui modelos previamente treinados e bibliotecas para R e Python de aprendizado de máquina. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.5*
sudo yum install mssql-mlservices-packages-r-9.4.5*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos do Ubuntu

Instalar qualquer *uma* pacote R, além de qualquer *um* pacote do Python e Java, se você quiser que esse recurso. Cada pacote de R e Python inclui um pacote de recursos. Escolha o pacote que fornece o conjunto de recursos que você precisa. Pacotes dependentes são incluídos automaticamente.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. Além disso, algumas imagens do docker do Ubuntu podem não ter a opção de transporte apt https. Para instalá-lo, use `apt-get install apt-transport-https`.

### <a name="prerequisite-for-1804"></a>Pré-requisito para 18.04

Executar o mssql mlservices bibliotecas do R no Ubuntu 18.04 exige **libpng12** do Linux Kernel arquiva. Este pacote não está mais incluído na distribuição padrão e deve ser instalado manualmente. Para obter essa biblioteca, execute os seguintes comandos:

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-01_1.2.54-1ubuntu1_amd64.deb
```

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. Para R e Python, se você quiser que algo entre completo e o mínimo, instale -, como bibliotecas de aprendizado de máquina, mas sem os modelos previamente treinados - substitua mssql-mlservices-mml-r e mssql-mlservices mml py.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi Revo * bibliotecas principais para R e Python, Java extension. Exclui modelos previamente treinados e bibliotecas para R e Python de aprendizado de máquina. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandos do SUSE

Instalar qualquer *uma* pacote R, além de qualquer *um* pacote do Python e Java, se você quiser que esse recurso. Cada pacote de R e Python inclui um pacote de recursos. Escolha o pacote que fornece o conjunto de recursos que você precisa. Pacotes dependentes são incluídos automaticamente. 

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. Para R e Python, se você quiser que algo entre mínimo e completo install -, como bibliotecas de aprendizado de máquina, mas sem os modelos previamente treinados - substituir `mssql-mlservices-mml-r-9.4.5*` e `mssql-mlservices-mml-py-9.4.5*` em vez disso.

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.5*
sudo zypper install mssql-mlservices-mlm-r-9.4.5* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi Revo * bibliotecas principais para R e Python, Java extension. Exclui modelos previamente treinados e bibliotecas para R e Python de aprendizado de máquina. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.5*
sudo zypper install mssql-mlservices-packages-r-9.4.5*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuração de pós-instalação (obrigatória)

Configuração adicional é principalmente por meio de [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Adicione a conta de usuário mssql usada para executar o serviço Launchpad do SQL Server.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

2. Aceite os contratos de licença para software livre R e Python. Há várias maneiras de fazer isso. Se anteriormente você aceita o licenciamento do SQL Server e agora está adicionando as extensões de R ou Python, o comando a seguir é o seu consentimento para seus termos:

  ```bash
  # Run as SUDO or root
  # Use set + EULA 
    sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
  ```

  Um fluxo de trabalho alternativo é que, se você ainda não aceitou o mecanismo de banco de dados do SQL Server, contrato de licença, a instalação detecta o mssql mlservices pacotes e solicitará a aceitação do EULA quando `mssql-conf setup` é executado. Para obter mais informações sobre parâmetros de termos de licença, consulte [configurar o SQL Server com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Reinicie o serviço Launchpad do SQL Server e a instância do mecanismo de banco de dados.

  ```bash
  systemctl restart mssql-launchpadd

  systemctl restart mssql-server.service
  ```

4. Habilite a execução do script externo no SQL Server Management Studio ou outra ferramenta que executa o Transact-SQL. 

  ```bash
  EXEC sp_configure 'external scripts enabled', 1 
  RECONFIGURE WITH OVERRIDE 
  ```

## <a name="verify-installation"></a>Verifique a instalação

Bibliotecas do R (MicrosoftML, RevoScaleR e outros) podem ser encontradas em `/opt/mssql/mlservices/libraries/RServer`.

Bibliotecas do Python (microsoftml e revoscalepy) podem ser encontradas em `/opt/mssql/mlservices/libraries/PythonServer`.

Usando uma ferramenta de consulta do SQL Server, execute o seguinte comando SQL para testar a execução de R no SQL Server. Se o script não for executado, tente reiniciar o serviço, `sudo systemctl restart mssql-server`.

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
Execute o seguinte comando SQL para testar a execução do Python no SQL Server. 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-installation"></a>Instalação encadeada

Você pode instalar e configurar o mecanismo de banco de dados e os serviços de Machine Learning em um procedimento acrescentando pacotes de R, Python ou Java e parâmetros em um comando que instala o mecanismo de banco de dados. 

O exemplo a seguir está uma ilustração do "modelo" de uma instalação de pacote combinado aparência usando o Gerenciador de pacotes Yum:

```bash
sudo yum install -y mssql-sqlserver mssql-server-extensibility-java 
```

O exemplo instala o mecanismo de banco de dados e adiciona a extensão da linguagem Java, que extrai o pacote de estrutura de extensibilidade como uma dependência. Todos os pacotes usados neste exemplo são encontrados no mesmo caminho. Se você estivesse adicionando pacotes de R, o registro para o repositório de pacotes da microsoft-r-open seria necessário.

Após a instalação, lembre-se de usar a ferramenta de mssql-conf para configurar toda a instalação e aceite os contratos de licenciamento. EULAs inaceitável para componentes de software livre R e Python são detectadas automaticamente e você será solicitado a aceitar, juntamente com o EULA para o SQL Server.

```bash
sudo /opt/mssql/bin/mssql-conf setup MSSQL_PID=Developer 
```

## <a name="unattended-installation"></a>Instalação autônoma

Usando o [instalação autônoma](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) para o mecanismo de banco de dados, adicione os pacotes para mlservices mssql e os EULAs.

Lembre-se de que a instalação ou a ferramenta mssql-conf solicita a aceitação do contrato de licença. Se você já configurou o mecanismo de banco de dados do SQL Server e aceitou a EULA, use um dos parâmetros de EULA mlservices específicas para as distribuições de software livre R e Python:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Todas as possíveis permutações de aceitação do EULA estão documentadas em [configurar o SQL Server no Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalação offline

Siga as [instalação Offline](sql-server-linux-setup.md#offline) instruções para obter etapas sobre como instalar os pacotes. Localizar seu site de download e, em seguida, baixe pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Muitas das ferramentas de gerenciamento de pacote fornecem comandos que podem ajudá-lo a determinam as dependências do pacote. Para o yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Site de download

Você pode baixar os pacotes a partir [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos os pacotes de mlservices para Java, Python e R estão localizados no pacote do mecanismo de banco de dados. Versão de base para os pacotes de mlservices é 9.4.5. Os pacotes de micrososoft-r-open estão em uma pasta diferente.

#### <a name="rhel7-paths"></a>Caminhos RHEL/7

|||
|--|----|
| MSSQL/mlservices pacotes | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| pacotes de r-open-Microsoft | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 caminhos

|||
|--|----|
| MSSQL/mlservices pacotes | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| pacotes de r-open-Microsoft | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Caminhos SLES 12

|||
|--|----|
| MSSQL/mlservices pacotes | [ https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| pacotes de r-open-Microsoft | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Lista de pacotes

Dependendo de quais extensões que você deseja usar, baixar os pacotes necessários para um idioma específico. Nomes de arquivo exatos incluem informações de plataforma, mas os nomes de arquivo abaixo devem ser próximos o suficiente para que você possa determinar quais arquivos para obter.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-foreachiterators-3.4.4
microsoft-r-open-mkl-3.4.4
microsoft-r-open-mro-3.4.4
mssql-mlservices-packages-r-9.4.5
mssql-mlservices-mlm-r-9.4.5
mssql-mlservices-mml-r-9.4.5

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.5
mssql-mlservices-packages-py-9.4.5
mssql-mlservices-mlm-py-9.4.5
mssql-mlservices-mml-py-9.4.5 
```

## <a name="add-more-rpython-packages"></a>Adicionar mais pacotes de R/Python 
 
Você pode instalar outros pacotes de R e Python e usá-los no script que é executado no SQL Server de 2019.

### <a name="r-packages"></a>Pacotes de R 
 
1. Inicie uma sessão de R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Instalar um pacote de R chamado [cola](https://mran.microsoft.com/package/glue) para testar a instalação do pacote.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   Como alternativa, você pode instalar um pacote R da linha de comando 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. Importar o pacote de R no [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Pacotes do Python 
 
1. Instalar um pacote do Python chamado [httpie](https://httpie.org/) usando pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importar o pacote do Python em [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-20"></a>Limitações no CTP 2.0

Existem as seguintes limitações nesta versão CTP.

+ Autenticação implícita atualmente não está disponível nos serviços de aprendizado de máquina no Linux neste momento, o que significa que você não pode se conectar novamente para o servidor de um script de R ou Python em andamento para acessar dados ou outros recursos. 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) (para armazenar pacotes de R no banco de dados) não está disponível no Linux e não oferece suporte a Python.  

### <a name="resource-governance"></a>Governança de recursos

Há uma paridade entre Linux e Windows para [governança de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para pools de recursos externos, mas as estatísticas [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tem no momento diferentes unidades no Linux. Unidades são alinhados em um CTP futuro.
 
| Nome da coluna   | Description | O valor no Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | A quantidade máxima de memória usada para o pool de recursos. | No Linux, essa estatística é originada do subsistema de memória de CGroups, onde o valor é memory.max_usage_in_bytes |
|write_io_count | O total SS de gravação emitidas desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de blkio CGroups, onde o valor da linha de gravação é blkio.throttle.io_serviced | 
|read_io_count | O total lidas emitidas desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de blkio CGroups, onde o valor da linha de leitura é blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | O usuário kernel tempo de CPU cumulativo em milissegundos desde que as estatísticas do administrador de recursos foram redefinidas. | No Linux, essa estatística é originada do subsistema de cpuacct CGroups, onde o valor da linha do usuário é cpuacct.stat |  
|total_cpu_user_ms | O tempo de usuário de CPU cumulativo em milissegundos desde que as estatísticas do administrador de recursos foram redefinidas.| No Linux, essa estatística é originada do subsistema de cpuacct CGroups, onde o valor no valor de linha do sistema é cpuacct.stat | 
|active_processes_count | O número de processos externos em execução no momento da solicitação.| No Linux, essa estatística é originada do subsistema de pids GGroups, onde o valor é pids.current | 

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores do R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem aprender como usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores do Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
