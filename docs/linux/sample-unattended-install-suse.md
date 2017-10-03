---
title: "Instalação autônoma do SQL Server no SUSE Linux Enterprise Server | Microsoft Docs"
description: "Exemplo de Script do SQL Server - instalação autônoma no SUSE Linux Enterprise Server"
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: e181fb02497f1673a8993687d159f6636aca4959
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="sample-unattended-sql-server-installation-script-for-suse-linux-enterprise-server"></a>Exemplo: De script de instalação autônoma do SQL Server para SUSE Linux Enterprise Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Esse exemplo de script de Bash instala 2017 do SQL Server no SUSE Linux Enterprise Server (SLES) v12 SP2 sem entrada interativa. Ele fornece exemplos de instalação do mecanismo de banco de dados, ferramentas de linha de comando do SQL Server, SQL Server Agent e executa as etapas de pós-instalação. Opcionalmente, você pode instalar a pesquisa de texto completo e criar um usuário administrativo.

> [!TIP]
> Se você não precisar de um script de instalação autônoma, a maneira mais rápida para instalar o SQL Server é seguir o [tutorial de início rápido para SLES](quickstart-install-connect-suse.md). Para outras informações de configuração, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

- É necessário pelo menos 3,25 GB de memória para executar o SQL Server no Linux.
- O sistema de arquivos deve ser **XFS** ou **EXT4**. Outros sistemas de arquivos, como **BTRFS**, não têm suporte.
- Para outros requisitos de sistema, consulte [requisitos de sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> SQL Server 2017 requer libsss_nss_idmap0, que não é fornecido pelos repositórios SLES padrão. Você pode instalá-lo do SDK SLES v12 SP2.

## <a name="sample-script"></a>Exemplo de script

```bash
#!/bin/bash

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

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
sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
sudo zypper --gpg-auto-import-keys refresh

#Add the SLES v12 SP2 SDK to obtain libsss_nss_idmap0
sudo SUSEConnect -p sle-sdk/12.2/x86_64

echo Installing SQL Server...
sudo zypper install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y zypper install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo zypper install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo zypper install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring SuSEfirewall2 to allow traffic on port 1433...
sudo SuSEfirewall2 open INT TCP 1433
sudo SuSEfirewall2 stop
sudo SuSEfirewall2 start

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

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

### <a name="running-the-script"></a>A execução do script

Para executar o script

1. Cole o exemplo em seu editor de texto favorito e salvá-lo com um nome fácil de lembrar, como `install_sql.sh`.

1. Personalizar `MSSQL_SA_PASSWORD`, `MSSQL_PID`e qualquer uma das outras variáveis com o qual você deseja alterar.

1. Marca o script como executável

   ```bash
   chmod +x install_sql.sh
   ```

1. Execute o script

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>Noções básicas sobre o script
A primeira coisa que o script Bash faz é definir algumas variáveis. Eles podem ser variáveis de script, como o exemplo a, ou variáveis de ambiente. A variável ``` MSSQL_SA_PASSWORD ``` é **necessária** pela instalação do SQL Server, os outros são variáveis personalizadas criadas para o script. O exemplo de script executa as seguintes etapas:

1. Importe as chaves públicas do Microsoft GPG.

1. Registre-se os repositórios do Microsoft SQL Server e as ferramentas de linha de comando.

1. Atualizar os repositórios locais

1. Instalar o SQL Server

1. Configurar o SQL Server com o ```MSSQL_SA_PASSWORD``` e aceitar automaticamente o contrato de licença do usuário final.

1. Automaticamente aceitar o contrato de licença de usuário final para ferramentas de linha de comando do SQL Server, instale-os e instale o pacote de desenvolvimento unixodbc.

1. Adicione ferramentas de linha de comando do SQL Server para o caminho da facilidade de uso.

1. Instalar o SQL Server Agent, se a variável de script ```SQL_INSTALL_AGENT``` for definida, em por padrão.

1. Opcionalmente, instalar a pesquisa de texto completo do SQL Server, se a variável ```SQL_INSTALL_FULLTEXT``` é definida.

1. Desbloquear a porta 1433 TCP no firewall do sistema, necessário para se conectar ao SQL Server de outro sistema.

1. Opcionalmente, defina os sinalizadores de rastreamento para rastreamento de deadlock. (requer uncommenting as linhas)

1. SQL Server agora está instalado, para tornar operacional, reiniciar o processo.

1. Verifique se o SQL Server está instalado corretamente, ocultando as mensagens de erro.

1. Criar um novo usuário de administrador do servidor se ```SQL_INSTALL_USER``` e ```SQL_INSTALL_USER_PASSWORD``` são definidas.

## <a name="next-steps"></a>Próximas etapas

Simplificar a várias instalações autônomas e criar um script de Bash autônomo que define as variáveis de ambiente apropriadas. Você pode remover qualquer uma das variáveis de script de exemplo usa e colocá-los em seus próprios scripts de Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Em seguida, execute o script de Bash da seguinte maneira:
```bash
. ./my_script_name.sh
```

Para obter mais informações sobre o SQL Server no Linux, consulte [do SQL Server na visão geral do Linux](sql-server-linux-overview.md).
