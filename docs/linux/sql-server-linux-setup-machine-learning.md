---
title: Instalar Serviços do Machine Learning do SQL Server (R, Python) em Linux
description: Saiba como instalar os Serviços de Machine Learning do SQL Server (R, Python) no Red Hat, no Ubuntu e no SUSE.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f578ae9dbc60b255959de406999feb8b68171389
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476197"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-on-linux"></a>Instalar Serviços do Machine Learning do SQL Server 2019 (R, Python) em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Os [Serviços de Machine Learning do SQL Server](../advanced-analytics/index.yml) são executados em sistemas operacionais Linux desta versão prévia do SQL Server 2019 em diante. Siga as etapas neste artigo para instalar as extensões de aprendizado de máquina para R e Python.

As extensões de aprendizado de máquina e programação são um complemento no mecanismo de banco de dados. Embora seja possível [instalar o mecanismo de banco de dados e os Serviços de Machine Learning simultaneamente](#install-all) a melhor prática é instalar e configurar o mecanismo de banco de dados do SQL Server primeiro para que você possa resolver problemas antes de adicionar mais componentes. 

A localização do pacote das extensões do R e do Python está nos repositórios de origem do Linux do SQL Server. Se você já configurou repositórios de origem para a instalação do mecanismo de banco de dados, execute os comandos de instalação de pacote **mssql-mlservices** usando o mesmo registro de repositório.

Também há suporte para Serviços de Machine Learning em contêineres do Linux. Não fornecemos contêineres pré-criados com as Serviços de Machine Learning, mas você pode criar um com base nos contêineres de SQL Server usando [um modelo disponível no GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Desinstalar o CTP anterior

A lista de pacotes foi alterada nas últimas versões de CTP, resultando em menos pacotes. Recomendamos desinstalar o CTP 2.x para remover todos os pacotes anteriores antes de instalar o CTP 3.2. Não há suporte para a instalação lado a lado de várias versões.

### <a name="1-confirm-package-installation"></a>1. Confirmar instalação do pacote

Você pode verificar a existência de uma instalação anterior como uma primeira etapa. Os seguintes arquivos indicam uma instalação existente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Desinstalar pacotes CTP 2.x anteriores

Desinstale no nível mais baixo do pacote. Qualquer pacote upstream dependente de um pacote de nível inferior é desinstalado automaticamente.

  + Para a integração com o R, remova **microsoft-r-open***
  + Para integração com o Python, remova **mssql-mlservices-python**

Os comandos para remover os pacotes aparecem na tabela a seguir.

| Plataforma  | Comando(s) de remoção de pacote | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> O Microsoft R Open 3.4.4 é composto por dois ou três pacotes, dependendo da versão CTP instalada anteriormente. (O pacote foreachiterators foi combinado com o pacote MRO principal no CTP 2.2.) Se qualquer um desses pacotes permanecer após a remoção do microsoft-r-open-mro-3.4.4, você deverá removê-los individualmente.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3. Continuar com a instalação do CTP 3.2

Instale no nível mais alto do pacote usando as instruções neste artigo relativas ao seu sistema operacional.

Para cada conjunto de instruções de instalação específicas do sistema operacional, o *nível mais alto de pacote* é o **Exemplo 1 – instalação completa** para o conjunto completo de pacotes ou **Exemplo 2 – instalação mínima** para o número mínimo de pacotes necessários para uma instalação viável.

1. Para a integração com o R, comece com o [MRO](#mro), pois ele é um pré-requisito. A integração do R não será instalada sem ele.

2. Execute os comandos de instalação usando os gerenciadores de pacotes e a sintaxe para seu sistema operacional: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ A versão do Linux deve ser [compatível com o SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), sem incluir o Docker Engine. As versões com suporte incluem:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (Somente R) O [Microsoft R Open](#mro) fornece a distribuição base do R para o recurso R no SQL Server

+ Você deve ter uma ferramenta para executar comandos T-SQL. Um editor de consultas é necessário para a configuração e a validação pós-instalação. Recomendamos o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), um download gratuito que é executado no Linux.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Instalação do Microsoft R Open (MRO)

A distribuição base do R da Microsoft é um pré-requisito para usar o RevoScaleR, o MicrosoftML e outros pacotes do R instalados com os Serviços de Machine Learning.

A versão necessária é MRO 3.5.2.

Escolha entre as duas abordagens a seguir para instalar o MRO:

+ Baixe o MRO tarball do MRAN, descompacte-o e execute seu script install.sh. Você poderá seguir as [instruções de instalação no MRAN](https://mran.microsoft.com/releases/3.5.2) se quiser essa abordagem.

+ Como alternativa, registre o repositório **packages.microsoft.com** conforme descrito abaixo para instalar os dois pacotes que abrangem a distribuição do MRO: microsoft-r-open-mro e microsoft-r-open-mkl. 

Os comandos a seguir registram o repositório que fornece o MRO. Após o registro, os comandos para instalar outros pacotes do R, como mssql-mlservices-mml-r, incluirão automaticamente o MRO como uma dependência de pacote.

#### <a name="mro-on-ubuntu"></a>MRO no Ubuntu

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

#### <a name="mro-on-rhel"></a>MRO no RHEL

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

Em um dispositivo conectado à Internet, os pacotes são baixados e instalados independentemente do mecanismo de banco de dados usando o instalador de pacote para cada sistema operacional. A tabela a seguir descreve todos os pacotes disponíveis, mas para R e Python, você especifica pacotes que fornecem a instalação com todos os recursos ou a instalação com o mínimo de recursos.

| Nome do pacote | Aplica-se a | Descrição |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos | Estrutura de extensibilidade usada para executar o código do R e do Python. |
| microsoft-openmpi  | Python, R | Interface de transmissão de mensagens usada pelas bibliotecas Revo* para paralelização no Linux. |
| mssql-mlservices-python | Python | Distribuição open-source do Anaconda e do Python. |
|mssql-mlservices-mlm-py  | Python | *Instalação completa*. Fornece revoscalepy, microsoftml, modelos pré-treinados para personalização de imagem e análise de sentimentos de texto.| 
|mssql-mlservices-packages-py  | Python | *Instalação mínima*. Fornece revoscalepy e microsoftml. <br/>Exclui modelos pré-treinados. | 
| [microsoft-r-open*](#mro) | R | Distribuição open-source do R composta por três pacotes. |
|mssql-mlservices-mlm-r  | R | *Instalação completa*. Fornece RevoScaleR, MicrosoftML, sqlRUtils, olapR, modelos pré-treinados para personalização de imagem e análise de sentimentos de texto.| 
|mssql-mlservices-packages-r  | R | *Instalação mínima*. Fornece RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Exclui modelos pré-treinados. | 
|mssql-mlservices-mml-py  | Apenas CTP 2.0-2.1 | Obsoleto no CTP 2.2 devido à consolidação do pacote do Python no mssql-mslservices-python. Fornece revoscalepy. Exclui modelos pré-treinados e microsoftml.| 
|mssql-mlservices-mml-r  | Apenas CTP 2.0-2.1 | Obsoleto no CTP 2.2 devido à consolidação do pacote do R no mssql-mslservices-python. Fornece RevoScaleR, sqlRUtils, olapR. Exclui modelos pré-treinados e MicrosoftML.  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>Comandos do RedHat

Você pode instalar o suporte a idiomas em qualquer combinação necessária (um ou vários idiomas). Para R e Python, há dois pacotes entre os quais escolher. Um fornece todos os recursos disponíveis, caracterizados como *instalação completa*. A opção alternativa exclui os modelos de aprendizado de máquina previamente treinados e é considerada a *instalação mínima*.

> [!Tip]
> Se possível, execute `yum clean all` para atualizar os pacotes no sistema antes da instalação.

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa 

Inclui R e Python de open-source, estrutura de extensibilidade, microsoft-openmpi, extensões (R, Python), com bibliotecas de aprendizado de máquina e modelos pré-treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima 

Inclui R e Python open-source, estrutura de extensibilidade, microsoft-openmpi, bibliotecas principais do Revo* e bibliotecas de aprendizado de máquina para R e Python. Exclui os modelos pré-treinados.

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Comandos do Ubuntu

Você pode instalar o suporte a idiomas em qualquer combinação necessária (um ou vários idiomas). Para R e Python, há dois pacotes entre os quais escolher. Um fornece todos os recursos disponíveis, caracterizados como *instalação completa*. A opção alternativa exclui os modelos de aprendizado de máquina previamente treinados e é considerada a *instalação mínima*.

> [!Tip]
> Se possível, execute `apt-get update` para atualizar os pacotes no sistema antes da instalação. Além disso, algumas imagens do Docker do Ubuntu podem não ter a opção https apt transport. Para instalá-la, use `apt-get install apt-transport-https`.

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa 

Inclui R e Python de open-source, estrutura de extensibilidade, microsoft-openmpi, extensões (R, Python), com bibliotecas de aprendizado de máquina e modelos pré-treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima 

Inclui R e Python open-source, estrutura de extensibilidade, microsoft-openmpi, bibliotecas principais do Revo* e bibliotecas de aprendizado de máquina para R e Python. Exclui os modelos pré-treinados. 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>Comandos SUSE

Você pode instalar o suporte a idiomas em qualquer combinação necessária (um ou vários idiomas). Para R e Python, há dois pacotes entre os quais escolher. Um fornece todos os recursos disponíveis, caracterizados como *instalação completa*. A opção alternativa exclui os modelos de aprendizado de máquina previamente treinados e é considerada a *instalação mínima*.

### <a name="example-1----full-installation"></a>Exemplo 1 – instalação completa 

Inclui R e Python de open-source, estrutura de extensibilidade, microsoft-openmpi, extensões (R, Python), com bibliotecas de aprendizado de máquina e modelos pré-treinados para R e Python. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>Exemplo 2 – instalação mínima 

Inclui R e Python open-source, estrutura de extensibilidade, microsoft-openmpi, bibliotecas principais do Revo* e bibliotecas de aprendizado de máquina para R e Python. Exclui os modelos pré-treinados. 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>Configuração pós-instalação (obrigatória)

A configuração adicional é principalmente por meio da [ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md).


1. Adicione a conta de usuário mssql usada para executar o serviço SQL Server. Isso será necessário se você não tiver executado a instalação anteriormente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Aceite os contratos de licença para R e Python open-source. Há várias maneiras de fazer isso. Se você tiver aceito anteriormente o licenciamento do SQL Server e agora estiver adicionando as extensões do R ou do Python, o seguinte comando será o seu consentimento com seus termos:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   Um fluxo de trabalho alternativo é que, se você ainda não aceitou o contrato de licenciamento do mecanismo de banco de dados do SQL Server, a instalação detectará os pacotes mssql-mlservices e solicitará a aceitação do EULA quando o `mssql-conf setup` for executado. Para obter mais informações sobre os parâmetros do EULA, confira [Configurar o SQL Server com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

3. Habilite o acesso à rede de saída. O acesso à rede de saída está desabilitado por padrão. Para habilitar as solicitações de saída, defina a propriedade booliana "outboundnetworkaccess" usando a ferramenta mssql-conf. Para obter mais informações, confira [Configurar o SQL Server em Linux com mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Somente para a integração de recursos do R, defina a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

   + Edite ou crie um arquivo chamado **.bash_profile** no diretório base do usuário, adicionando a linha `export MKL_CBWR="AUTO"` ao arquivo.

   + Execute esse arquivo digitando `source .bash_profile` em um prompt de comando de Bash.

5. Reinicie o serviço SQL Server Launchpad e a instância do mecanismo de banco de dados para ler os valores atualizados no arquivo INI. Uma mensagem de reinicialização lembrará você sempre que uma configuração relacionada à extensibilidade for modificada.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Habilite a execução de script externo usando o Azure Data Studio ou outra ferramenta como o SQL Server Management Studio (somente Windows) que executa Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Reinicie o serviço de Launchpad novamente.

## <a name="verify-installation"></a>Verifique a instalação

As bibliotecas do R (MicrosoftML, RevoScaleR e outras) podem ser encontradas em `/opt/mssql/mlservices/libraries/RServer`.

As bibliotecas do Python (microsoftml e revoscalepy) podem ser encontradas em `/opt/mssql/mlservices/libraries/PythonServer`.

Para validar a instalação, execute um script T-SQL que executa um procedimento armazenado do sistema que invoca o R ou o Python. Você precisará de uma ferramenta de consulta para essa tarefa. O Azure Data Studio é uma boa opção. Outras ferramentas usadas com frequência, como o SQL Server Management Studio ou PowerShell, funcionam somente no Windows. Se você tem um computador Windows com essas ferramentas, use-o para conectar-se à instalação do Linux do mecanismo de banco de dados.

Execute o comando do SQL a seguir para testar a execução do R no SQL Server. Se o script não for executado, tente uma reinicialização do serviço, `sudo systemctl restart mssql-server.service`.

```r
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

## <a name="chained-combo-install"></a>Instalação "combinada" encadeada

Você pode instalar e configurar o mecanismo de banco de dados e os Serviços de Machine Learning em um procedimento acrescentando pacotes e parâmetros R e Python a um comando que instala o mecanismo de banco de dados. 

1. Para a integração do R, instale o [Microsoft R Open](#mro) como um pré-requisito. Ignore esta etapa se você não estiver instalando o recurso do R.

2. Forneça uma linha de comando que inclua o mecanismo de banco de dados, além dos recursos de extensão de linguagem.

  Você pode adicionar um único recurso, como a integração do Python, a uma instalação do mecanismo de banco de dados.

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  Ou adicione ambas as extensões (R, Python).

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. Aceite os contratos de licença e conclua a configuração pós-instalação. Use a ferramenta **mssql-conf** para esta tarefa.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Você será solicitado a aceitar o contrato de licença do mecanismo de banco de dados, escolher uma edição e definir a senha do administrador. Você também será solicitado a aceitar o contrato de licença para Serviços de Machine Learning.

4. Reinicie o serviço, se solicitado a fazê-lo.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Instalação autônoma

Usando a [instalação autônoma](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) do mecanismo de banco de dados, adicione os pacotes para mssql-mlservices e EULAs.

Lembre-se de que a instalação ou a ferramenta mssql-conf solicita a aceitação do contrato de licença. Se você já tiver configurado o mecanismo de banco de dados do SQL Server e aceito seu EULA, use um dos parâmetros de EULA específicos do mlservices para as distribuições do R e Python open-source:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

Todas as possíveis permutas de aceitação do EULA são documentadas em [Configurar o SQL Server em Linux com a ferramenta mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## <a name="offline-installation"></a>Instalação offline

Siga as instruções de [Instalação offline](sql-server-linux-setup.md#offline) para conhecer as etapas da instalação dos pacotes. Localize o site de download e baixe os pacotes específicos usando a lista de pacotes abaixo.

> [!Tip]
> Várias das ferramentas de gerenciamento de pacotes fornecem comandos que podem ajudá-lo a determinar as dependências do pacote. Para yum, use `sudo yum deplist [package]`. Para o Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido por `dpkg -I [package name].deb`.


#### <a name="download-site"></a>Site de download

Você pode baixar pacotes de [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos os pacotes mlservices para R e Python são colocados com o pacote do mecanismo de banco de dados. A versão base para os pacotes mlservices é 9.4.5 (para CTP 2.0) 9.4.6 (para CTP 2.1 e posterior). Lembre-se de que os pacotes do microsoft-r-open estão em um [repositório diferente](#mro).

#### <a name="rhel7-paths"></a>Caminhos RHEL/7

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Caminhos do Ubuntu/16.04

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>Caminhos SLES/12

|||
|--|----|
| Pacotes mssql/mlservices | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| Pacotes microsoft-r-open | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>Lista de pacotes

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

## <a name="add-more-rpython-packages"></a>Adicionar mais pacotes do R/Python 
 
Você pode instalar outros pacotes do R e do Python e usá-los no script que é executado no SQL Server 2019.

### <a name="r-packages"></a>Pacotes do R 
 
1. Inicie uma sessão do R.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. Instale um pacote do R chamado [glue](https://mran.microsoft.com/package/glue) para a instalação do pacote de teste.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   Como alternativa, você pode instalar um pacote R da linha de comando 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. Importe o pacote R em [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Pacotes do Python 
 
1. Instale um pacote do Python chamado [httpie](https://httpie.org/) usando pip. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. Importe o pacote Python em [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>Limitações nas versões de CTP

A integração do R e do Python no Linux ainda está em desenvolvimento ativo. Os recursos a seguir ainda não estão habilitados na versão prévia.

+ A autenticação implícita não está disponível em Serviços de Machine Learning em Linux no momento, o que significa que você não pode se conectar de volta ao servidor de um script do R ou do Python em andamento para acessar dados ou outros recursos. 

### <a name="resource-governance"></a>Governança de recursos

Há paridade entre o Linux e o Windows para [Governança de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para pools de recursos externos, mas as estatísticas para [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) atualmente têm unidades diferentes no Linux. As unidades serão alinhadas em uma CTP futura.
 
| Nome da coluna   | Descrição | Valor no Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | A quantidade máxima de memória usada para o pool de recursos. | No Linux, essa estatística é originada do subsistema de memória CGroups, em que o valor é memory.max_usage_in_bytes |
|write_io_count | O total de E/Ss de gravação emitidas desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada no subsistema CGroups blkio, em que o valor na linha de gravação é blkio.throttle.io_serviced | 
|read_io_count | O total de E/S lidas emitidas desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada no subsistema CGroups blkio, em que o valor na linha de leitura é blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | O tempo do kernel do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas. | No Linux, essa estatística é originada do subsistema CGroups cpuacct, em que o valor na linha do usuário é cpuacct.stat |  
|total_cpu_user_ms | O tempo de do usuário da CPU cumulativo em milissegundos desde que as estatísticas do Resource Governor foram redefinidas.| No Linux, essa estatística é originada do subsistema CGroups cpuacct, em que o valor na linha do sistema é cpuacct.stat | 
|active_processes_count | O número de processos externos em execução no momento da solicitação.| No Linux, essa estatística é originada do subsistema de pids GGroups, em que o valor é pids.current | 

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Tutorial: Executar o R no T-SQL](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, confira [Tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
