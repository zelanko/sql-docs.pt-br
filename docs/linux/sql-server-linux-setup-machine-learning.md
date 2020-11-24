---
title: Instalar no Linux
titleSuffix: SQL Server Machine Learning Services
description: 'Aprenda como instalar Serviços de Machine Learning do SQL Server (R, Python) em Linux: Red Hat, Ubuntu e SUSE.'
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 03/05/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc671271d3e998e0329236c6c567438db1a5c48a
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869997"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Instalar Serviços do Machine Learning do SQL Server (R e Python) em Linux

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

Este artigo explica como instalar o [Serviços de Machine Learning do SQL Server](../machine-learning/index.yml) no Linux. Os scripts Python e R podem ser executados no banco de dados usando os Serviços de Machine Learning.

> [!NOTE]
> Os Serviços de Machine Learning são instalados por padrão em Clusters de Big Data do SQL Server. Para obter mais informações, confira [Usar os Serviços de Machine Learning (Python e R) em Clusters de Big Data](../big-data-cluster/machine-learning-services.md)

<a name="mro"></a>

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

* [Instale o SQL Server em Linux](sql-server-linux-setup.md) e confirme a instalação.

* Verifique os repositórios do SQL Server no Linux das extensões do Python e do R. 
  Se você já configurou repositórios de origem para a instalação do mecanismo de banco de dados, execute os comandos de instalação de pacote **mssql-mlservices** usando o mesmo registro de repositório.

  Você pode instalar o SQL Server no Red Hat Enterprise Linux (RHEL), no SUSE Linux Enterprise Server (SLES) e no Ubuntu. Para obter mais informações, confira [a seção Plataformas com suporte nas Diretrizes de instalação para SQL Server em Linux](sql-server-linux-setup.md#supportedplatforms).

* (Somente para R) O Microsoft R Open (MRO) fornece a distribuição base do R para o recurso de R no SQL Server e é um pré-requisito para usar o RevoScaleR, o MicrosoftML e outros pacotes de R instalados com os Serviços de Machine Learning.
    * A versão necessária é MRO 3.5.2.
    * Escolha entre as duas abordagens a seguir para instalar o MRO:
        * Baixe o MRO tarball do MRAN, descompacte-o e execute seu script install.sh. Você poderá seguir as [instruções de instalação no MRAN](https://mran.microsoft.com/releases/3.5.2) se quiser essa abordagem.
        * Registre o repositório **packages.microsoft.com**, conforme descrito abaixo, para instalar a distribuição do MRO: microsoft-r-open-mro e microsoft-r-open-mkl. 
    * Confira as seções de instalação abaixo para saber como instalar o MRO.

* Você deve ter uma ferramenta para executar comandos T-SQL. 

  * Você pode usar o [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md), uma ferramenta de banco de dados gratuita que é executada no Linux, no Windows e no macOS.

## <a name="package-list"></a>Lista de pacotes

Em um dispositivo conectado à Internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador de pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis, mas para R e Python, você especifica pacotes que fornecem a instalação com todos os recursos ou a instalação com o mínimo de recursos.

Pacotes de instalação disponíveis:

| Nome do pacote | Aplica-se a | Descrição |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos | Estrutura de extensibilidade usada para executar o Python e o R. |
| microsoft-openmpi  | Python, R | Interface de Passagem de Mensagem usada pelas bibliotecas do Rev* para paralelização no Linux. |
| mssql-mlservices-python | Python | Distribuição open-source do Anaconda e do Python. |
|mssql-mlservices-mlm-py  | Python | *Instalação completa*. Fornece revoscalepy, microsoftml, modelos pré-treinados para personalização de imagem e análise de sentimentos de texto.| 
|mssql-mlservices-packages-py  | Python | *Instalação mínima*. Fornece revoscalepy e microsoftml. <br/>Exclui modelos pré-treinados. | 
| [microsoft-r-open*](#mro) | R | Distribuição open-source do R composta por três pacotes. |
|mssql-mlservices-mlm-r  | R | *Instalação completa*. Fornece: RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelos pré-treinados para personalização de imagem e análise de sentimento de texto.| 
|mssql-mlservices-packages-r  | R | *Instalação mínima*. Fornece RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Exclui modelos pré-treinados. |

<a name="RHEL"></a>

## <a name="install-on-rhel"></a>Instalar no RHEL

Siga as etapas abaixo para instalar os Serviços de Machine Learning do SQL Server no Red Hat Enterprise Linux (RHEL).

### <a name="install-mro-on-rhel"></a>Instalar o MRO no RHEL

Os comandos a seguir registram o repositório que fornece o MRO. Após o registro, os comandos para instalar outros pacotes do R, como mssql-mlservices-mml-r, incluirão automaticamente o MRO como uma dependência de pacote.
```bash
# Import the Microsoft repository key

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

Opções de instalação para Python e R:

*  Instale o suporte a idiomas de acordo com os seus requisitos (um ou vários idiomas).
*  A *instalação completa* fornece todos os recursos disponíveis, incluindo modelos de machine learning pré-treinados.
*  A *instalação mínima* exclui os modelos, mas ainda tem toda a funcionalidade.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

### <a name="full-installation"></a>Instalação completa

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Extensões (Python, R)
*  Bibliotecas de aprendizado de máquina
*  Modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="minimum-installation"></a>Instalação mínima

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Bibliotecas principais do Revo*
*  Bibliotecas de aprendizado de máquina

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Instalação no Ubuntu

Siga as etapas abaixo para instalar os Serviços de Machine Learning do SQL Server no Ubuntu.

### <a name="install-mro-on-ubuntu"></a>Instalação do MRO no Ubuntu

Os comandos a seguir registram o repositório que fornece o MRO. Após o registro, os comandos para instalar outros pacotes do R, como mssql-mlservices-mml-r, incluirão automaticamente o MRO como uma dependência de pacote.

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

Opções de instalação para Python e R:

*  Instale o suporte a idiomas de acordo com os seus requisitos (um ou vários idiomas).
*  A *instalação completa* fornece todos os recursos disponíveis, incluindo modelos de machine learning pré-treinados.
*  A *instalação mínima* exclui os modelos, mas ainda tem toda a funcionalidade.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. 

### <a name="full-installation"></a>Instalação completa 

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Extensões do Python
*  Extensões de R
*  Bibliotecas de aprendizado de máquina
*  Modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="minimum-installation"></a>Instalação mínima 

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Bibliotecas principais do Revo*
*  Bibliotecas de aprendizado de máquina

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-sles"></a>Instalar no SLES

Siga as etapas abaixo para instalar os Serviços de Machine Learning do SQL Server no SUSE Linux Enterprise Server (SLES).

### <a name="install-mro-on-sles"></a>Instalar o MRO no SLES

Os comandos a seguir registram o repositório que fornece o MRO. Após o registro, os comandos para instalar outros pacotes do R, como mssql-mlservices-mml-r, incluirão automaticamente o MRO como uma dependência de pacote.

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SLES in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Opções de instalação para Python e R:

*  Instale o suporte a idiomas de acordo com os seus requisitos (um ou vários idiomas).
*  A *instalação completa* fornece todos os recursos disponíveis, incluindo modelos de machine learning pré-treinados.
*  A *instalação mínima* exclui os modelos, mas ainda tem toda a funcionalidade.

### <a name="full-installation"></a>Instalação completa 

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Extensões para Python e R
*  Bibliotecas de aprendizado de máquina
*  Modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
sudo zypper install mssql-mlservices-mlm-py
sudo zypper install mssql-mlservices-mlm-r
```

### <a name="minimum-installation"></a>Instalação mínima 

Inclui:
*  Python open-source
*  R open-source
*  Estrutura de extensibilidade
*  Microsoft-openmpi
*  Bibliotecas principais do Revo*
*  Bibliotecas de aprendizado de máquina 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
sudo zypper install mssql-mlservices-packages-py
sudo zypper install mssql-mlservices-packages-r
```

## <a name="post-install-config-required"></a>Configuração pós-instalação (obrigatória)

A configuração adicional é principalmente por meio da [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).

1. Após a conclusão da instalação do pacote, execute a instalação de mssql-conf e siga os prompts para definir a senha SA e escolher sua edição. Execute esta etapa somente se você ainda não tiver configurado o SQL Server em Linux. 

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Aceite os contratos de licença para as extensões do R e do Python open-source. Use o seguinte comando:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
   A instalação detecta os pacotes mssql-mlservices e solicita a aceitação do EULA (se não foi aceito anteriormente) quando `mssql-conf setup` é executado. Para obter mais informações sobre os parâmetros do EULA, confira [Configurar o SQL Server com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Habilite o acesso à rede de saída. O acesso à rede de saída está desabilitado por padrão. Para habilitar as solicitações de saída, defina a propriedade booliana "outboundnetworkaccess" usando a ferramenta mssql-conf. Para obter mais informações, confira [Configurar o SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Somente para a integração de recursos do R, defina a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

   + Edite ou crie um arquivo `.bash_profile` no diretório base do usuário, adicionando a linha `export MKL_CBWR="AUTO"` ao arquivo.

   + Execute esse arquivo digitando `source .bash_profile` em um prompt de comando de Bash.

5. Reinicie o serviço SQL Server Launchpad e a instância do mecanismo de banco de dados para ler os valores atualizados no arquivo INI. Uma mensagem de notificação é exibida quando uma configuração relacionada à extensibilidade é modificada.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Habilite a execução de script externo usando o Azure Data Studio ou outra ferramenta como o SQL Server Management Studio (somente Windows) que executa Transact-SQL.

   ```sql
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Reinicie o serviço de Launchpad novamente.

## <a name="verify-installation"></a>Verifique a instalação

As bibliotecas do R (MicrosoftML, RevoScaleR e outras) podem ser encontradas em `/opt/mssql/mlservices/libraries/RServer`.

As bibliotecas do Python (microsoftml e revoscalepy) podem ser encontradas em `/opt/mssql/mlservices/libraries/PythonServer`.

Para validar a instalação:

* Execute um script T-SQL que executa um procedimento armazenado do sistema invocando o Python ou o R com uma ferramenta de consulta. 

* Execute o comando do SQL a seguir para testar a execução do R no SQL Server. Erros? Tente executar uma reinicialização do serviço, `sudo systemctl restart mssql-server.service`.
  ```sql
  EXEC sp_execute_external_script   
  @language =N'R', 
  @script=N' 
  OutputDataSet <- InputDataSet', 
  @input_data_1 =N'SELECT 1 AS hello' 
  WITH RESULT SETS (([hello] int not null)); 
  GO 
  ```
 
* Execute o comando do SQL a seguir para testar a execução do Python no SQL Server. 
 
  ```sql
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

## <a name="unattended-installation"></a>Instalação autônoma

Usando a [instalação autônoma](sql-server-linux-setup.md#unattended) do mecanismo de banco de dados, adicione os pacotes para mssql-mlservices e EULAs.

 Use um dos parâmetros do EULA específicos do mlservices para as distribuições do R e do Python open-source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

O EULA completo está documentado em [Configurar o SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalação offline

Siga as instruções de [Instalação offline](sql-server-linux-setup.md#offline) para conhecer as etapas da instalação dos pacotes. Localize o site de download e baixe os pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Várias das ferramentas de gerenciamento de pacotes fornecem comandos que podem ajudá-lo a determinar as dependências do pacote. Para yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.

 
### <a name="download-site"></a>Site de download

Baixe pacotes em [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos os pacotes mlservices para o Python e o R são colocados com o pacote do mecanismo de banco de dados. A versão básica para os pacotes mlservices é 9.4.6. Lembre-se de que os pacotes do microsoft-r-open estão em um [repositório diferente](#mro).

### <a name="rhel7-paths"></a>Caminhos RHEL/7

|Pacote|Local de download|
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 

### <a name="ubuntu1604-paths"></a>Caminhos do Ubuntu/16.04

|Pacote|Local de download|
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

### <a name="sles12-paths"></a>Caminhos SLES/12

|Pacote|Local de download|
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

Selecione as extensões que deseja usar e baixe os pacotes necessários para uma linguagem específica. Os nomes de arquivos incluem informações da plataforma no sufixo.

### <a name="package-list"></a>Lista de pacotes

Dependendo de quais extensões você deseja usar, baixe os pacotes necessários para uma linguagem específica. Os nomes de arquivos exatos incluem informações de plataforma no sufixo, mas os nomes de arquivo abaixo devem ser próximos o suficiente para que você determine quais arquivos serão obtidos.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial do Python: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../machine-learning/tutorials/python-clustering-model.md)

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../machine-learning/tutorials/r-taxi-classification-introduction.md)