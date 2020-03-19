---
title: Instalar Serviços do Machine Learning do SQL Server (R, Python) em Linux
description: 'Aprenda como instalar Serviços de Machine Learning do SQL Server (R, Python) em Linux: Red Hat, Ubuntu e SUSE.'
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf474ff8a7587c916591e6d7ba4dc82052b516f7
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937656"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Instalar Serviços do Machine Learning do SQL Server (R e Python) em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como instalar o [Serviços de Machine Learning do SQL Server](../advanced-analytics/index.yml) no Linux. Os scripts Python e R podem ser executados no banco de dados usando os Serviços de Machine Learning.

[!NOTE]
> Os Serviços de Machine Learning são instalados por padrão em Clusters de Big Data do SQL Server. Para obter mais informações, confira [Usar os Serviços de Machine Learning (Python e R) em Clusters de Big Data](../big-data-cluster/machine-learning-services.md)

## <a name="what-are-machine-learning-services"></a>O que são os Serviços de Machine Learning

Os Serviços de Machine Learning são um complemento de recurso do mecanismo de banco de dados.

Instale e configure o Mecanismo de Banco de Dados do SQL Server primeiro para resolver os problemas antes de adicionar mais componentes.

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

[Instale o SQL Server em Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup) e confirme a instalação.

* Verifique os repositórios do SQL Server no Linux das extensões do Python e do R. 
* Se você já configurou repositórios de origem para a instalação do mecanismo de banco de dados, execute os comandos de instalação de pacote **mssql-mlservices** usando o mesmo registro de repositório.

* O [Microsoft R Open](#mro) fornece a distribuição base do R para o recurso R no SQL Server

* Você deve ter uma ferramenta para executar comandos T-SQL. 
* Um editor de consultas é necessário para a configuração e a validação pós-instalação. 
* Recomendamos o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), um download gratuito que é executado no Linux.


<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalação do Microsoft R Open (MRO)

A distribuição base do R da Microsoft é um pré-requisito para usar o RevoScaleR, o MicrosoftML e outros pacotes do R instalados com os Serviços de Machine Learning.

A versão necessária é MRO 3.5.2.

Escolha entre as duas abordagens a seguir para instalar o MRO:

+ Baixe o MRO tarball do MRAN, descompacte-o e execute seu script install.sh. Você poderá seguir as [instruções de instalação no MRAN](https://mran.microsoft.com/releases/3.5.2) se quiser essa abordagem.

+ Registre o repositório **packages.microsoft.com**, conforme descrito abaixo, para instalar a distribuição do MRO: microsoft-r-open-mro e microsoft-r-open-mkl. 

<a name="RHEL"></a>

## <a name="install-on-redhat"></a>Instalação no Red Hat

### <a name="install-mro-on-red-hat"></a>Instalação (MRO) no Red Hat

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

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  extensões (Python, R)
*  bibliotecas de aprendizado de máquina
*  modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  bibliotecas principais do Revo*
*  bibliotecas de aprendizado de máquina

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Instalação no Ubuntu

### <a name="install-mro-on-ubuntu"></a>Instalação (MRO) no Ubuntu

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

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa 

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  Extensões do Python
*  Extensões de R
*  bibliotecas de aprendizado de máquina
*  modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima 

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  bibliotecas principais do Revo*
*  bibliotecas de aprendizado de máquina

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-suse"></a>Instalação no SUSE

### <a name="install-mro-on-susesles"></a>Instalação (MRO) no SUSE (SLES)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Opções de instalação para Python e R:

*  Instale o suporte a idiomas de acordo com os seus requisitos (um ou vários idiomas).
*  A *instalação completa* fornece todos os recursos disponíveis, incluindo modelos de machine learning pré-treinados.
*  A *instalação mínima* exclui os modelos, mas ainda tem toda a funcionalidade.

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa 

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  extensões para Python e R
*  bibliotecas de aprendizado de máquina
*  modelos pré-treinados para Python e R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima 

Inclui:
*  Python open-source
*  R open-source
*  estrutura de extensibilidade
*  microsoft-openmpi
*  bibliotecas principais do Revo*
*  bibliotecas de aprendizado de máquina 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configuração pós-instalação (obrigatória)

A configuração adicional é principalmente por meio da [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Adicione a conta de usuário mssql usada para executar o serviço SQL Server.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Aceite os contratos de licença para as extensões do R e do Python open-source. Use o seguinte comando:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. A instalação detecta os pacotes mssql-mlservices e solicita a aceitação do EULA (se não foi aceito anteriormente) quando `mssql-conf setup` é executado. Para obter mais informações sobre os parâmetros do EULA, confira [Configurar o SQL Server com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

4. Habilite o acesso à rede de saída. O acesso à rede de saída está desabilitado por padrão. Para habilitar as solicitações de saída, defina a propriedade booliana "outboundnetworkaccess" usando a ferramenta mssql-conf. Para obter mais informações, confira [Configurar o SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. Somente para a integração de recursos do R, defina a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

   + Edite ou crie um arquivo `named.bash_profile` no diretório base do usuário, adicionando a linha `export MKL_CBWR="AUTO"` ao arquivo.

   + Execute esse arquivo digitando `source.bash_profile` em um prompt de comando de Bash.

6. Reinicie o serviço SQL Server Launchpad e a instância do mecanismo de banco de dados para ler os valores atualizados no arquivo INI. Uma mensagem de notificação é exibida quando uma configuração relacionada à extensibilidade é modificada.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. Habilite a execução de script externo usando o Azure Data Studio ou outra ferramenta como o SQL Server Management Studio (somente Windows) que executa Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Reinicie o serviço de Launchpad novamente.

## <a name="verify-installation"></a>Verifique a instalação

As bibliotecas do R (MicrosoftML, RevoScaleR e outras) podem ser encontradas em `/opt/mssql/mlservices/libraries/RServer`.

As bibliotecas do Python (microsoftml e revoscalepy) podem ser encontradas em `/opt/mssql/mlservices/libraries/PythonServer`.

Para validar a instalação:

- Execute um script T-SQL que executa um procedimento armazenado do sistema invocando o Python ou o R com uma ferramenta de consulta. 

Para o Windows, use: 
*  Azure Data Studio
*  SQL Server Management Studio ou PowerShell

Se você tem um computador Windows com essas ferramentas, use-o para conectar-se à instalação do Linux do mecanismo de banco de dados.

Execute o comando do SQL a seguir para testar a execução do R no SQL Server. Erros? Tente executar uma reinicialização do serviço, `sudo systemctl restart mssql-server.service`.

```
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
Execute o comando do SQL a seguir para testar a execução do Python no SQL Server. 
 
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

## <a name="unattended-installation"></a>Instalação autônoma

Usando a [instalação autônoma](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) do mecanismo de banco de dados, adicione os pacotes para mssql-mlservices e EULAs.

 Use um dos parâmetros do EULA específicos do mlservices para as distribuições do R e do Python open-source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

O EULA completo está documentado em [Configurar o SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalação offline

Siga as instruções de [Instalação offline](sql-server-linux-setup.md#offline) para conhecer as etapas da instalação dos pacotes. Baixe pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Várias das ferramentas de gerenciamento de pacotes fornecem comandos que podem ajudá-lo a determinar as dependências do pacote. Para yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Site de download

Baixe pacotes em [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos os pacotes mlservices para o Python e o R são colocados com o pacote do mecanismo de banco de dados. A versão básica para os pacotes mlservices é 9.4.6. Lembre-se de que os pacotes do microsoft-r-open estão em um [repositório diferente](#mro).

#### <a name="rhel7-paths"></a>Caminhos RHEL/7

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Caminhos do Ubuntu/16.04

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Caminhos SLES/12

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## <a name="package-list"></a>Lista de pacotes

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

Selecione as extensões que deseja usar e baixe os pacotes necessários para uma linguagem específica. Os nomes de arquivos incluem informações da plataforma no sufixo.

Lista de arquivos:

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

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
