---
title: Instalar o SQL Server serviços de Machine Learning (R, Python, Java) no Linux | Microsoft Docs
description: Este artigo descreve como instalar os serviços SQL Server Machine Learning (R, Python, Java) no Red Hat e Ubuntu.
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15a1a411672303fc8556927bcaf218052758744d
ms.sourcegitcommit: 2f5773f4bc02bfff4f2924226ac5651eb0c00924
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53553248"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>Instalar o SQL Server de 2019 serviços de Machine Learning (R, Python, Java) no Linux

[Serviços do SQL Server Machine Learning](../advanced-analytics/what-is-sql-server-machine-learning.md) é executado em sistemas operacionais Linux nesta versão de visualização do SQL Server 2019. Siga as etapas neste artigo para instalar a extensão de programação Java, ou a aprendizado de máquina extensões para R e Python. 

Aprendizado de máquina e extensões de programação é um complemento para o mecanismo de banco de dados. Embora você possa [instalar o mecanismo de banco de dados e os serviços de Machine Learning simultaneamente](#install-all), ele é uma prática recomendada para instalar e configurar o mecanismo de banco de dados do SQL Server pela primeira vez, para que você possa resolver quaisquer problemas antes de adicionar mais componentes. 

Local do pacote para as extensões de R, Python e Java estão em repositórios de código-fonte do SQL Server Linux. Se você já configurou os repositórios de código-fonte para a instalação do mecanismo de banco de dados, você pode executar o **mlservices mssql** comandos de instalação usando o mesmo registro do repositório do pacote.

## <a name="uninstall-previous-ctp"></a>Desinstalar o CTP anterior

A lista de pacotes foi alterado pela última várias versões CTP, resultando em menos de pacotes. Recomendamos a desinstalação do CTP 2.0 ou 2.1 para remover todos os pacotes anteriores antes de instalar o CTP 2.2 ou posterior. Não há suporte para a instalação lado a lado de várias versões.

### <a name="1-confirm-package-installation"></a>1. Confirme a instalação do pacote

Você talvez queira verificar a existência de uma instalação anterior como uma primeira etapa. Os arquivos a seguir indicam uma instalação existente: checkinstallextensibility.sh, exthost, barra inicial.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-ctp-20-or-21-packages"></a>2. Desinstalar o CTP 2.0 ou 2.1 pacotes

Desinstale o nível mais baixo do pacote. Qualquer pacote de upstream dependente de um pacote de nível inferior será desinstalado automaticamente.

  + Para a integração de R, remover **microsoft-r-open***
  + Para a integração do Python, remover **mssql-mlservices-python**
  + Para a integração do Java, remover **mssql-server-extensibilidade-java**

Comandos para remover os pacotes são exibidos na tabela a seguir.

| Plataforma  | Comando (s) de remoção de pacote | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python`<br/>`sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python`<br/>`sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`<br/>`sudo apt-get remove msssql-server-extensibility-java`|

> [!Note]
> Microsoft R Open é composto de três pacotes. Se qualquer um desses pacotes permanecem após a remoção de microsoft-r-open-mro-3.4.4, você deverá removê-los individualmente.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-22-install"></a>3. Prosseguir com a instalação do CTP 2.2

Instale com o nível mais alto de pacote usando as instruções neste artigo para seu sistema operacional.

Para cada conjunto de específicas do sistema operacional de instruções de instalação *mais alto nível de pacote* seja **exemplo 1: instalação completa** para o conjunto completo de pacotes, ou **exemplo 2: instalação mínima**  o menor número de pacotes necessários para uma instalação viável.

1. Para a integração de R, começar com [MRO](#mro) porque ele é um pré-requisito. Integração do R não será instalado sem ele.

2. Execute os comandos de instalação usando os gerenciadores de pacotes e a sintaxe para seu sistema operacional: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#SUSE)

## <a name="prerequisites"></a>Prerequisites

+ A versão do Linux deve ser [suportados pelo SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), em execução no local ou em um contêiner do Docker. As versões com suporte incluem:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (R) [Microsoft R Open](#mro) fornece a distribuição de R base para o recurso do R no SQL Server

+ Você deve ter uma ferramenta para executar comandos do T-SQL. Um editor de consultas é necessário para configuração de pós-instalação e validação. É recomendável [Studio do Azure Data](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), um download gratuito que é executado no Linux.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalação do Microsoft R Open MRO)

Distribuição de R base da Microsoft é um pré-requisito para usar o RevoScaleR, MicrosoftML e outros pacotes de R instalados com os serviços de aprendizado de máquina.

A versão necessária é MRO 3.4.4.

Escolha entre as duas abordagens a seguir para instalar o MRO:

+ Baixar o MRO tarball do MRAN, descompactá-lo e execute o script install.sh. Você pode seguir a [instruções de instalação no MRAN](https://mran.microsoft.com/releases/3.4.4) se você quiser que essa abordagem.

+ Como alternativa, registre-se a **packages.microsoft.com** repositório conforme descrito a seguir para instalar os três pacotes que compõem a distribuição MRO: mro microsoft-r-open, microsoft-r-open-mkl, e Microsoft-r-open-foreachiterators. 

Os comandos a seguir registre o repositório fornecendo MRO. Após o registro, os comandos para instalar outros pacotes de R, como mssql-mlservices-mml-r, incluirá automaticamente MRO como uma dependência de pacote.

#### <a name="mro-on-ubuntu"></a>MRO no Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Add the **azure-cli** repo to your apt sources list
AZ_REPO=$(lsb_release -cs)

echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>MRO no RHEL

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Create local `azure-cli` repository
sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'

# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>MRO no SUSE

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>Lista de pacotes

Em um dispositivo conectado à internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador do pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis, mas para R e Python, você especifica os pacotes que fornecem a instalação de recurso completo ou os recursos mínimos de instalação.

| Nome do pacote | Aplica-se a | Descrição |
|--------------|----------|-------------|
|MSSQL-server-extensibilidade  | Todos | Estrutura de extensibilidade usada para executar código R, Python ou Java. |
|MSSQL-server-extensibilidade-java | Java | Extensão de Java para o carregamento de um ambiente de execução do Java. Não há bibliotecas adicionais ou pacotes para Java. |
| Microsoft openmpi  | Python, R | Interface usada pelas bibliotecas de Revo * para paralelização no Linux de transmissão de mensagens. |
| MSSQL-mlservices-python | Python | Distribuição do código-fonte aberto do Anaconda e Python. |
|MSSQL-mlservices mlm py  | Python | *Instalação completa*. Fornece modelos para análise de sentimento de texto e personalização de imagem revoscalepy, microsoftml, pré-treinados.| 
|MSSQL-mlservices pacotes py  | Python | *Instalação mínima*. Fornece revoscalepy e microsoftml. <br/>Exclui modelos previamente treinados. | 
| [Microsoft-r-abrir *](#mro) | R | Distribuição de software livre do R, composto por três pacotes. |
|MSSQL-mlservices-mlm-r  | R | *Instalação completa*. Fornece modelos para análise de sentimento de texto e personalização de imagem RevoScaleR, MicrosoftML, sqlRUtils, olapR, pré-treinados.| 
|MSSQL-mlservices pacotes r  | R | *Instalação mínima*. Fornece o RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Exclui modelos previamente treinados. | 
|MSSQL-mlservices mml py  | Somente CTP 2.1 2.0 | Obsoleto no CTP 2.2 devido à consolidação de pacote do Python em mssql-mslservices-python. Fornece revoscalepy. Exclui o microsoftml e modelos previamente treinados.| 
|MSSQL-mlservices-mml-r  | Somente CTP 2.1 2.0 | Obsoleto no CTP 2.2 devido à consolidação de pacote de R em mssql-mslservices-python. Fornece o RevoScaleR, sqlRUtils, olapR. Exclui modelos previamente treinados e MicrosoftML.  |

<a name="RHEL"></a>

## <a name="rhel-commands"></a>Comandos do RHEL

Você pode instalar o suporte de linguagem em qualquer combinação, você precisa (único ou vários idiomas). Para R e Python, há dois pacotes para sua escolha. Um deles fornece todos os recursos disponíveis, caracterizados como os *instalação completa*. A opção alternativa exclui a modelos de aprendizado de máquina pré-treinados e é considerada o *instalação mínima*.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.6*
sudo yum install mssql-mlservices-mlm-r-9.4.6* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi, core Revo * bibliotecas e bibliotecas de aprendizado de máquina para R e Python e a extensão de Java. Exclui os modelos previamente treinados.

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.6*
sudo yum install mssql-mlservices-packages-r-9.4.6*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos do Ubuntu

Você pode instalar o suporte de linguagem em qualquer combinação, você precisa (único ou vários idiomas). Para R e Python, há dois pacotes para sua escolha. Um deles fornece todos os recursos disponíveis, caracterizados como os *instalação completa*. A opção alternativa exclui a modelos de aprendizado de máquina pré-treinados e é considerada o *instalação mínima*.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. Além disso, algumas imagens do docker do Ubuntu podem não ter a opção de transporte apt https. Para instalá-lo, use `apt-get install apt-transport-https`.

<!---
### Prerequisite for 18.04

Running mssql-mlservices R libraries on Ubuntu 18.04 requires **libpng12** from the Linux Kernel archives. This package is no longer included in the standard distribution and must be installed manually. To get this library, run the following commands:

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
```--->

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi, core Revo * bibliotecas e bibliotecas de aprendizado de máquina para R e Python e a extensão de Java. Exclui os modelos previamente treinados. 

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

Você pode instalar o suporte de linguagem em qualquer combinação, você precisa (único ou vários idiomas). Para R e Python, há dois pacotes para sua escolha. Um deles fornece todos os recursos disponíveis, caracterizados como os *instalação completa*. A opção alternativa exclui a modelos de aprendizado de máquina pré-treinados e é considerada o *instalação mínima*.

### <a name="example-1----full-installation"></a>Exemplo 1: instalação completa 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi extensões (R, Python, Java), com bibliotecas de aprendizado de máquina e modelos previamente treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.6*
sudo zypper install mssql-mlservices-mlm-r-9.4.6* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>Exemplo 2: instalação mínima 

Inclui código-fonte aberto R e Python, estrutura de extensibilidade, microsoft-openmpi, core Revo * bibliotecas e bibliotecas de aprendizado de máquina para R e Python e a extensão de Java. Exclui os modelos previamente treinados. 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.6*
sudo zypper install mssql-mlservices-packages-r-9.4.6*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuração de pós-instalação (obrigatória)

Configuração adicional é principalmente por meio de [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Adicione a conta de usuário mssql usada para executar o serviço SQL Server. Isso é necessário se você ainda não executou a instalação anteriormente.

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

3. Para R recurso Integração única, defina as **MKL_CBWR** variável de ambiente [garantir uma saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) cálculos da Intel MKL Math Kernel Library ().

  + Edite ou crie um arquivo chamado **. bash_profile** em seu diretório base do usuário, adicionando a linha `export MKL_CBWR="AUTO"` para o arquivo.

  + Execute esse arquivo digitando `source .bash_profile` em um prompt de comando do bash.

4. Reinicie o serviço Launchpad do SQL Server e a instância do mecanismo de banco de dados. 

  ```bash
  systemctl restart mssql-launchpadd

  systemctl restart mssql-server.service
  ```

5. Habilitar a execução do script externo usando o Studio de dados do Azure ou outra ferramenta como SQL Server Management Studio (somente Windows) que executa o Transact-SQL. 

  ```bash
  EXEC sp_configure 'external scripts enabled', 1 
  RECONFIGURE WITH OVERRIDE 
  ```

6. Reinicie o serviço Launchpad novamente.

## <a name="verify-installation"></a>Verifique a instalação

Bibliotecas do R (MicrosoftML, RevoScaleR e outros) podem ser encontradas em `/opt/mssql/mlservices/libraries/RServer`.

Bibliotecas do Python (microsoftml e revoscalepy) podem ser encontradas em `/opt/mssql/mlservices/libraries/PythonServer`.

Integração de recursos do Java não inclui bibliotecas, mas você pode executar `grep -r JAVA_HOME /etc` para confirmar a criação da variável de ambiente JAVA_HOME.

Para validar a instalação, execute um script T-SQL que executa um procedimento armazenado do sistema invocar R ou Python. Você precisará de uma ferramenta de consulta para essa tarefa. O estúdio de dados do Azure é uma boa opção. Outras comumente usadas ferramentas, como SQL Server Management Studio ou o PowerShell são somente para Windows. Se você tiver um computador Windows com essas ferramentas, você deve usá-lo para se conectar à sua instalação do Linux do mecanismo de banco de dados.

Execute o seguinte comando SQL para testar a execução de R no SQL Server. Se o script não for executado, tente reiniciar o serviço, `sudo systemctl restart mssql-server.service`.

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

## <a name="chained-combo-install"></a>Instala o encadeadas "combinação"

Você pode instalar e configurar o mecanismo de banco de dados e os serviços de Machine Learning em um procedimento acrescentando pacotes de R, Python ou Java e parâmetros em um comando que instala o mecanismo de banco de dados. 

1. Para a integração de R, instale [Microsoft R Open](#mro) como um pré-requisito. Ignore esta etapa se você não estiver instalando o recurso do R.

2. Forneça uma linha de comando que inclui o mecanismo de banco de dados, além de recursos de extensão da linguagem.

  Você pode adicionar um único recurso, como Java, instalar o integration, para um mecanismo de banco de dados.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

  Ou então, adicionar todas as extensões (Java, R, Python).

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java mssql-mlservices-packages-r-9.4.6* mssql-mlservices-packages-py-9.4.6*
  ```

3. Aceite os contratos de licença e conclua a configuração de pós-instalação. Use o **mssql-conf** ferramenta para essa tarefa.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Você será solicitado a aceitar o contrato de licença para o mecanismo de banco de dados, escolha uma edição e definir a senha de administrador. Você também precisará aceitar o contrato de licença de serviços do Machine Learning.

4. Reinicie o serviço, se solicitado a fazê-lo.

  ```bash
  sudo systemctl restart mssql-server.service
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

Você pode baixar os pacotes a partir [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos os pacotes de mlservices para Java, Python e R estão localizados no pacote do mecanismo de banco de dados. Versão de base para os pacotes de mlservices é 9.4.5 (para CTP 2.0) 9.4.6 (para CTP 2.1 e posterior). Lembre-se que os pacotes da microsoft-r-open estão em um [repositório diferente](#mro).

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

Dependendo de quais extensões que você deseja usar, baixar os pacotes necessários para um idioma específico. Nomes de arquivo exatos incluem informações de plataforma no sufixo, mas os nomes de arquivo abaixo devem ser próximos o suficiente para que você possa determinar quais arquivos para obter.

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
mssql-mlservices-packages-r-9.4.6.523
mssql-mlservices-mlm-r-9.4.6.523
mssql-mlservices-mml-r-9.4.6.523

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.6.523
mssql-mlservices-packages-py-9.4.6.523
mssql-mlservices-mlm-py-9.4.6.523
mssql-mlservices-mml-py-9.4.6.523
```

#### <a name="package-list-for-original-ctp-20-and-21"></a>Lista de pacotes para original CTP 2.0 e 2.1

Remove do CTP 2.2 **mlservices mssql-py mlm** e **mssql-mlservices-mlm-r** por meio da consolidação de pacote no **mssql-mlservices pacotes py** e **mssql-mlservices pacotes r**, respectivamente.

Se você precisar especificamente o original CTP 2.0 ou 2.1 pacotes, baixe os pacotes a seguir:

* Para o CTP 2.0, baixe as versões do pacote 9.4.5

* Para o CTP 2.1, baixe as versões do pacote 9.4.6.237


## <a name="add-more-rpython-packages"></a>Adicionar mais pacotes de R/Python 
 
Você pode instalar outros pacotes de R e Python e usá-los no script que é executado no SQL Server de 2019.

### <a name="r-packages"></a>Pacotes do R 
 
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

## <a name="limitations-in-ctp-releases"></a>Limitações em versões CTP

Integração de R, Python e Java no Linux ainda está em desenvolvimento ativo. Os recursos a seguir ainda não estão habilitados na versão de visualização.

+ Autenticação implícita atualmente não está disponível nos serviços de aprendizado de máquina no Linux neste momento, o que significa que você não pode se conectar novamente para o servidor de um script de R ou Python em andamento para acessar dados ou outros recursos. 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) (para armazenar pacotes de R no banco de dados) não está disponível no Linux e não oferece suporte a Python.  

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

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise no banco de dados para os desenvolvedores do R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem aprender como usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Execute o Python no T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores do Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
