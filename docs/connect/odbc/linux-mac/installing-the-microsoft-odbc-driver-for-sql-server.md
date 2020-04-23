---
title: Instalar o Microsoft ODBC Driver for SQL Server (Linux)
description: Saiba como instalar o Microsoft ODBC Driver for SQL Server em clientes Linux para permitir a conectividade com o banco de dados.
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26c8282ec5afe00c3f23987fb82e3759c77c76e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487777"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-linux"></a>Instalar o Microsoft ODBC Driver for SQL Server (Linux)

Este artigo explica como instalar o Microsoft ODBC Driver for SQL Server em Linux. Também inclui instruções para as ferramentas de linha de comando opcionais para o SQL Server (`bcp` e `sqlcmd`) e os cabeçalhos de desenvolvimento unixODBC.

Este artigo fornece comandos para instalar o driver ODBC por meio do shell Bash. Caso deseje baixar os pacotes diretamente, confira [Baixar o ODBC Driver for SQL Server](../download-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-17"></a><a id="17"></a> Microsoft ODBC 17

As seções a seguir explicam como instalar o Microsoft ODBC Driver 17 por meio do shell Bash para diferentes distribuições do Linux.

- [Alpine Linux](#alpine17)
- [Debian](#debian17)
- [Red Hat Enterprise Linux e Oracle](#redhat17)
- [SUSE Linux Enterprise Server](#suse17)
- [Ubuntu](#ubuntu17)

> [!IMPORTANT]
> Se você tiver instalado o pacote v17 `msodbcsql` que estava disponível brevemente, deverá removê-lo antes de instalar o pacote `msodbcsql17`. Isso evitará conflitos. O pacote `msodbcsql17` pode ser instalado lado a lado com o pacote `msodbcsql` v13.

### <a name="alpine-linux"></a><a id="alpine17"></a> Alpine Linux

```bash
#Download the desired package(s)
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.apk


#(Optional) Verify signature, if 'gpg' is missing install it using 'apk add gnupg':
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.sig

curl https://packages.microsoft.com/keys/microsoft.asc  | gpg --import -
gpg --verify msodbcsql17_17.5.2.1-1_amd64.sig msodbcsql17_17.5.2.1-1_amd64.apk
gpg --verify mssql-tools_17.5.2.1-1_amd64.sig mssql-tools_17.5.2.1-1_amd64.apk


#Install the package(s)
sudo apk add --allow-untrusted msodbcsql17_17.5.2.1-1_amd64.apk
sudo apk add --allow-untrusted mssql-tools_17.5.2.1-1_amd64.apk
```

> [!NOTE]
> A versão 17.5 ou posterior do driver é necessária para compatibilidade com o Alpine.

### <a name="debian"></a><a id="debian17"></a> Debian

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
# optional: kerberos library for debian-slim distributions
sudo apt-get install libgssapi-krb5-2
```

> [!NOTE]
> É possível substituir a configuração da variável de ambiente "ACCEPT_EULA" pela configuração da variável debconf "msodbcsql/ACCEPT_EULA" em vez de: `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

### <a name="red-hat-enterprise-server-and-oracle-linux"></a><a id="redhat17"></a> Red Hat Enterprise Server e Oracle Linux

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8 and Oracle Linux 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a><a id="suse17"></a> SUSE Linux Enterprise Server

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu"></a><a id="ubuntu17"></a> Ubuntu

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.10
curl https://packages.microsoft.com/config/ubuntu/19.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

> [!NOTE]
> - Versão do driver 17.2 ou posterior é necessária para suporte ao Ubuntu 18.04.
> - Versão do driver 17.3 ou posterior é necessária para suporte ao Ubuntu 18.10.

> [!NOTE]
> É possível substituir a configuração da variável de ambiente "ACCEPT_EULA" pela configuração da variável debconf "msodbcsql/ACCEPT_EULA" em vez de: `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

## <a name="previous-versions"></a>Versões anteriores

As seções a seguir fornecem instruções sobre como instalar versões anteriores do Microsoft ODBC Driver no Linux. As seguintes versões de driver são abordadas:

- [Microsoft ODBC Driver 13.1 for SQL Server](#13.1)
- [Microsoft ODBC Driver 13 for SQL Server](#13)
- [Microsoft ODBC Driver 11 for SQL Server](#11)

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

As seções a seguir explicam como instalar o Microsoft ODBC Driver 13.1 por meio do shell Bash para diferentes distribuições do Linux.

### <a name="debian-8"></a>Debian 8

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

## <a name="odbc-13"></a><a id="13"></a> ODBC 13

As seções a seguir explicam como instalar o Microsoft ODBC Driver 13 por meio do shell Bash para diferentes distribuições do Linux.

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>Instalação offline

Se você preferir/precisar que o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 seja instalado em um computador sem conexão de Internet, precisará resolver as dependências do pacote manualmente. O [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 tem as seguintes dependências diretas:
- Ubuntu: libc6 (>= 2.21), libstdc++6 (>= 4.9), libkrb5-3, libcurl3, openssl, debconf (>= 0.5), unixodbc (>= 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SUSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Por sua vez, cada um desses pacotes tem suas próprias dependências, que podem ou não estar presentes no sistema. Para uma solução geral para esse problema, confira a documentação do gerenciador de pacotes de distribuição: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian) e [SUSE](https://en.opensuse.org/Portal:Zypper)

Também é comum baixar manualmente todos os pacotes dependentes e colocá-los juntos no computador de instalação, então instalar manualmente cada pacote por vez, terminando com o pacote [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7

- Baixe o `msodbcsql` `.rpm` mais recente em [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/).
- Instale as dependências e o driver.
  
```bash
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04

- Baixe o `msodbcsql` `.deb` mais recente em [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/).
- Instale as dependências e o driver.

```bash
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

- Baixe o `msodbcsql` `.rpm` mais recente em [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/).
- Instale as dependências e o driver.

```bash
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Depois de concluir a instalação do pacote, confirme se o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 pode encontrar todas as dependências executando ldd e inspecionando a saída para ver se há bibliotecas ausentes:

```bash
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```

## <a name="odbc-11"></a><a id="11"></a> ODBC 11

As seções a seguir explicam como instalar o Microsoft ODBC Driver 11 no Linux. Antes de poder usar o driver, instale o Gerenciador de Driver unixODBC. Para obter mais informações, veja [Instalação do Gerenciador de Driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md).

### <a name="installation-steps"></a>Etapas de instalação  

> [!IMPORTANT]  
> Estas instruções referem-se ao `msodbcsql-11.0.2270.0.tar.gz`, que é o arquivo de instalação para o Red Hat Linux. Se estiver instalando a Versão Prévia para SUSE Linux, o nome do arquivo será `msodbcsql-11.0.2260.0.tar.gz`.  
  
Para instalar o driver:

1. Verifique se você tem permissão de raiz.  

2. Altere o diretório em que o download colocou o arquivo `msodbcsql-11.0.2270.0.tar.gz`. Verifique se você tem o arquivo \*.tar.gz que corresponde à sua versão do Linux. Para extrair os arquivos, execute o seguinte comando: `tar xvzf msodbcsql-11.0.2270.0.tar.gz`.  
  
3. Altere para o diretório `msodbcsql-11.0.2270.0`. Lá, você deverá ver um arquivo chamado **install.sh**.  
  
4. Para ver uma lista das opções de instalação disponíveis, execute o seguinte comando: **./install.sh**.  
  
5. Faça um backup de **odbcinst.ini**. A instalação do driver atualiza o **odbcinst.ini**. O odbcinst.ini contém a lista de drivers que estão registrados com o Gerenciador de Driver unixODBC. Para descobrir a localização do odbcinst.ini em seu computador, execute o seguinte comando: ```odbc_config --odbcinstini```.  
  
6. Antes de instalar o driver, execute o seguinte comando: `./install.sh verify`. A saída de `./install.sh verify` informa se o seu computador tem o software necessário para suporte ao driver ODBC em Linux.  
  
7. Quando estiver pronto para instalar o driver ODBC no Linux, execute o comando: `./install.sh install`. Se precisar especificar um comando de instalação (`bin-dir` ou `lib-dir`), especifique o comando após a opção **install**.  
  
8. Depois de ler o contrato de licença, digite **YES** para continuar com a instalação.  
  
A instalação coloca o driver em `/opt/microsoft/msodbcsql/11.0.2270.0`. O driver e seus arquivos de suporte devem estar no `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Para verificar se o driver Microsoft ODBC em Linux foi registrado com êxito, execute o seguinte comando: ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```.  
  
### <a name="uninstall"></a>Desinstalar  
  
Você pode desinstalar o ODBC Driver 11 no Linux executando os seguintes comandos:  
  
1. `rm -f /usr/bin/sqlcmd`
  
2. `rm -f /usr/bin/bcp`  
  
3. `rm -rf /opt/microsoft/msodbcsql`  
  
4. `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="driver-files"></a>Arquivos do driver

O driver ODBC no Linux consiste nos seguintes componentes:

|Componente|Descrição|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X ou libmsodbcsql-13.X.so.X.X|O arquivo de biblioteca dinâmica (`so`) do objeto compartilhado que contém toda a funcionalidade do driver. Esse arquivo é instalado em `/opt/microsoft/msodbcsql17/lib64/` para o Driver 17 e em `/opt/microsoft/msodbcsql/lib64/` para o Driver 13.|  
|`msodbcsqlr17.rll` ou `msodbcsqlr13.rll`|O arquivo de recursos que acompanha a biblioteca do driver. Esse arquivo é instalado em `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|O arquivo de cabeçalho que contém todas as novas definições necessárias para usar o driver.<br /><br /> **Observação:**  Você não pode referenciar msodbcsql.h e odbcss.h no mesmo programa.<br /><br /> msodbcsql.h é instalado em `/opt/microsoft/msodbcsql17/include/` para o Driver 17 e em `/opt/microsoft/msodbcsql/include/` para o Driver 13. |
|LICENSE.txt|O arquivo de texto que contém os termos do Contrato de Licença do Usuário Final. Esse arquivo é colocado no `/usr/share/doc/msodbcsql17/` para o Driver 17 e em `/usr/share/doc/msodbcsql/` para o Driver 13.|
|RELEASE_NOTES|O arquivo de texto que contém as notas sobre a versão. Esse arquivo é colocado no `/usr/share/doc/msodbcsql17/` para o Driver 17 e em `/usr/share/doc/msodbcsql/` para o Driver 13.|

## <a name="resource-file-loading"></a>Carregamento de arquivo de recursos

O driver precisa carregar o arquivo de recurso para funcionar. Esse arquivo é denominado `msodbcsqlr17.rll` ou `msodbcsqlr13.rll`, dependendo da versão do driver. O local do arquivo `.rll` é relativo ao local do driver em si (`so` ou `dylib`), conforme observado na tabela acima. A partir da versão 17.1, o driver também tentará carregar o `.rll` do diretório padrão se o carregamento do caminho relativo falhar. O caminho do arquivo de recurso padrão no Linux é `/opt/microsoft/msodbcsql17/share/resources/en_US/`.

## <a name="troubleshooting"></a>Solução de problemas

Caso não possa estabelecer uma conexão com o SQL Server usando o driver ODBC, confira o artigo sobre problemas conhecidos em [Solução de problemas de conexão](known-issues-in-this-version-of-the-driver.md#connectivity).

## <a name="next-steps"></a>Próximas etapas

Depois de instalar o driver, experimente o [aplicativo de exemplo C++ ODBC](../../odbc/cpp-code-example-app-connect-access-sql-db.md). Para obter mais informações sobre como desenvolver aplicativos ODBC, confira [Desenvolver aplicativos](../../../odbc/reference/develop-app/developing-applications.md).

Para obter mais informações, confira as [notas sobre a versão](release-notes-odbc-sql-server-linux-mac.md) e os [requisitos do sistema](system-requirements.md) do driver ODBC.
