---
title: Instalação autônoma para SQL Server no Red Hat Enterprise Linux
titleSuffix: SQL Server
description: Exemplo de script do SQL Server – Instalação autônoma no Red Hat Enterprise Linux
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 696ba88a9f2d5f29de8dc3afb45af8c392f2de68
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "67910442"
---
# <a name="sample-unattended-sql-server-installation-script-for-red-hat-enterprise-linux"></a>Exemplo: Script de instalação autônoma do SQL Server para o Red Hat Enterprise Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este script Bash de exemplo instala o SQL Server 2017 no RHEL (Red Hat Enterprise Linux) sem entrada interativa. Ele fornece exemplos de como instalar o mecanismo de banco de dados, as ferramentas de linha de comando do SQL Server, o SQL Server Agent e executa etapas de pós-instalação. Opcionalmente, é possível instalar a pesquisa de texto completo e criar um usuário administrativo.

> [!TIP]
> Se você não precisar de um script de instalação autônoma, a maneira mais rápida de instalar o SQL Server será seguir o [início rápido para Red Hat](quickstart-install-connect-red-hat.md). Para outras informações sobre instalação, confira [Diretrizes de instalação do SQL Server em Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

- É necessário ter pelo menos 2 GB de memória para executar o SQL Server em Linux.
- O sistema de arquivos deve ser **XFS** ou **EXT4**. Não há suporte para outros sistemas de arquivos, como **BTRFS**.
- Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Exemplo de script
Salve o script de exemplo em um arquivo e, em seguida, para personalizá-lo, substitua os valores de variável no script. Você também pode definir qualquer uma das variáveis de script como variáveis de ambiente, contanto que você remova-as do arquivo de script.

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_ENABLE_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo

echo Installing SQL Server...
sudo yum install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y yum install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional Enable SQL Server Agent :
if [ ! -z $SQL_ENABLE_AGENT ]
then
  echo Enable SQL Server Agent...
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo yum install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring firewall to allow traffic on port 1433...
sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
sudo firewall-cmd --reload

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
#echo Setting trace flags...
#sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after making configuration changes:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 5s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

## <a name="running-the-script"></a>Executar o script

Para executar o script

1. Cole o exemplo em seu editor de texto favorito e salve-o com um nome fácil de memorizar, como `install_sql.sh`.

1. Personalize `MSSQL_SA_PASSWORD`, `MSSQL_PID` e qualquer uma das outras variáveis que você gostaria de alterar.

1. Marcar o script como executável

   ```bash
   chmod +x install_sql.sh
   ```

1. Executar o script

   ```bash
   ./install_sql.sh
   ```

## <a name="understanding-the-script"></a>Noções básicas sobre o script

A primeira coisa que o script Bash faz é definir algumas variáveis.  Elas podem ser variáveis de script (como o exemplo) ou variáveis de ambiente.  A variável `MSSQL_SA_PASSWORD` é **exigida** pela instalação do SQL Server, as outras são variáveis personalizadas criadas para o script.  O script de exemplo executa as seguintes etapas:

1. Importe as chaves GPG públicas da Microsoft.

1. Registre os repositórios da Microsoft no SQL Server e as ferramentas de linha de comando.

1. Atualizar os repositórios locais

1. Instalar o SQL Server

1. Configure o SQL Server com o ```MSSQL_SA_PASSWORD``` e aceite automaticamente o Contrato de Licença de Usuário Final.

1. Aceite automaticamente o Contrato de Licença de Usuário Final para as ferramentas de linha de comando do SQL Server, instale-as e instale o pacote unixodbc-dev.

1. Adicione as ferramentas de linha de comando do SQL Server ao caminho para ter facilidade de uso.

1. Instale o SQL Server Agent se a variável de script ```SQL_INSTALL_AGENT``` estiver definida como ativa por padrão.

1. Opcionalmente, instale a pesquisa de texto completo do SQL Server, se a variável ```SQL_INSTALL_FULLTEXT``` estiver definida.

1. Desbloqueie a porta 1433 para TCP no firewall do sistema, necessária para se conectar ao SQL Server de outro sistema.

1. Opcionalmente, defina sinalizadores de rastreamento para o rastreamento de deadlock. (requer a remoção da marca de comentário das linhas)

1. Agora o SQL Server está instalado; para torná-lo operacional, reinicie o processo.

1. Verifique se o SQL Server está instalado corretamente ao ocultar mensagens de erro.

1. Crie um usuário administrador do servidor se ```SQL_INSTALL_USER``` e ```SQL_INSTALL_USER_PASSWORD``` e ambos estiverem definidos.

## <a name="next-steps"></a>Próximas etapas

Simplifique várias instalações autônomas e crie um script Bash autônomo que define variáveis de ambiente adequadas.  É possível remover as variáveis usadas pelo script de exemplo e colocá-las no próprio script Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Em seguida, execute o script Bash da seguinte maneira:
```bash
. ./my_script_name.sh
```

Para saber mais sobre o SQL Server em Linux, confira [Visão geral do SQL Server em Linux](sql-server-linux-overview.md).
