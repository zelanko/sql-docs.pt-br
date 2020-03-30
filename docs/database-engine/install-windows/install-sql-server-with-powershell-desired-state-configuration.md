---
title: 'Instalar: Desired State Configuration do PowerShell'
description: Saiba como instalar o SQL Server usando a DSC (Desired State Configuration) do PowerShell.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7e7b3f2d8673972100e01413e5688353cb7c87a6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75258979"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>Instalar o SQL Server com a Desired State Configuration do PowerShell

Você já passou pela interface de instalação do SQL Server apenas selecionado os mesmos botões, inserindo as mesmas informações e sem parar para pensar melhor? A instalação foi concluída, mas você esqueceu de especificar o grupo DBA na função **sysadmin**. Em seguida, você precisava realizar estas ações:
* Soltar no modo de usuário único.
* Adicionar os usuários ou grupos adequados.
* Reative o SQL Server o no modo de multiusuário.
* Testar. 

E o pior é que agora a confiança de toda a instalação fica abalada. "O que mais eu esqueci?" você pode se perguntar.

Leia sobre a [DSC (Desired State Configuration) do PowerShell](/powershell/scripting/dsc/overview/overview). Usando a DSC, você cria um modelo de configuração que pode ser reutilizado em centenas de milhares de servidores. Dependendo do build, você talvez precise ajustar alguns dos parâmetros de configuração. Porém, isso não é um problema significativo, pois você pode manter todas as configurações padrão em vigor. Isso elimina a possibilidade de você esquecer-se de inserir um parâmetro importante.

Este artigo explora a configuração inicial de uma instância autônoma do SQL Server 2017 no Windows Server 2016 usando o recurso de DSC **SqlServerDsc**. Algum conhecimento prévio de DSC é útil, pois não exploramos como funciona a DSC.

Os seguintes itens são necessários para este passo a passo:

- Um computador que executa o Windows Server 2016.
- A mídia de instalação do SQL Server 2017.
- O recurso de DSC **SqlServerDsc**.

## <a name="prerequisites"></a>Pré-requisitos

Na maioria dos casos, a DSC é usada para lidar com pré-requisitos. Porém, no caso desta demonstração, lidaremos com os pré-requisitos manualmente.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>Instalar o recurso de DSC SqlServerDsc

Baixe o recurso do DSC [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) da [Galeria do PowerShell](https://www.powershellgallery.com/) usando o cmdlet [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1). 

> [!NOTE]
> Verifique se o PowerShell está em execução **Como Administrador** para instalar o módulo.

```PowerShell
Install-Module -Name SqlServerDsc
```

### <a name="get-the-sql-server-2017-installation-media"></a>Obtenha a mídia de instalação do SQL Server 2017
Baixe a mídia de instalação do SQL Server 2017 para o servidor. Baixamos SQL Server 2017 Enterprise de uma Assinatura do Visual Studio e copiamos o arquivo ISO para `C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso`.

Agora, o ISO precisa ser extraído para um diretório:

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>Criar a configuração

### <a name="configuration"></a>Configuração

Crie a função de configuração que será chamada para gerar os documentos [MOF (Managed Object Format)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-):

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>Módulos

Importe os módulos na sessão atual. Esses módulos informam o documento de configuração como compilar os documentos MOF. Eles também informam o mecanismo de DSC sobre como aplicar os documentos MOF no servidor:

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>Recursos

#### <a name="net-framework"></a>.NET Framework

O SQL Server se baseia no .NET Framework. Portanto, precisamos verificar se ele está instalado antes de instalarmos o SQL Server. O recurso **WindowsFeature** é usado para instalar o recurso **Net-Framework-45-Core** do Windows:

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

O recurso **SqlSetup** é usado para informar à DSC como instalar o SQL Server. Os parâmetros necessários para uma instalação básica são os seguintes:

- **InstanceName**. O nome da instância. Use **MSSQLSERVER** para uma instância padrão.
- **Recursos**. Os recursos a serem instalados. Neste exemplo, instalamos somente o recurso **SQLEngine**.
- **SourcePath**. O caminho para a mídia de instalação do SQL. Neste exemplo, armazenamos a mídia de instalação do SQL em `C:\SQL2017`. Um compartilhamento de rede pode minimizar o espaço usado no servidor.
- **SQLSysAdminAccounts**. Os usuários ou grupos que devem ser membros da função **sysadmin**. Neste exemplo, concedemos o acesso de **sysadmin** ao grupo local Administradores. 

> [!NOTE]
> Não recomendamos essa configuração em um ambiente de alta segurança.

Uma lista completa e uma descrição dos parâmetros disponíveis no **SqlSetup** estão disponíveis no [repositório SqlServerDsc do GitHub](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup).

O recurso **SqlSetup** instala somente o SQL Server e **não** mantém as configurações aplicadas. Um exemplo será se **SQLSysAdminAccounts** forem especificadas no momento da instalação. Um administrador pode adicionar ou remover entradas a ou da função **sysadmin**. Porém, o recurso **SqlSetup** não será afetado. Se desejar que o DSC imponha a associação da função **sysadmin**, use os recursos [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole).

#### <a name="finish-configuration"></a>Concluir a configuração

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>Criar e implantar

### <a name="compile-the-configuration"></a>Compilar a configuração

Execute dot source no script de configuração:

```PowerShell
. .\SQLInstallConfiguration.ps1
```

Execute a função de configuração:

```PowerShell
SQLInstall
```

Um diretório chamado **SQLInstall** é criado no diretório de trabalho. Ele contém um arquivo chamado **localhost.mof**. Examine o conteúdo do MOF, que mostra a configuração de DSC compilada.

### <a name="deploy-the-configuration"></a>Implantar a configuração

Para iniciar a implantação da DSC do SQL Server, chame o cmdlet **Start-DscConfiguration**. Os parâmetros a seguir são fornecidos para o cmdlet:

- **Path**. O caminho para a pasta que contém os documentos MOF para implantar. Um exemplo é `C:\SQLInstall`.
- **Wait**. Espere a conclusão do trabalho de configuração.
- **Force**. Substitua todas as configurações de DSC existentes.
- **Verbose**. Mostre a saída detalhada. É útil ao efetuar push de uma configuração pela primeira vez para auxiliar na solução de problemas.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

Conforme a configuração é aplicada, a saída detalhada mostra o que está acontecendo. Desde que não sejam gerados erros (texto vermelho), quando **Operação 'Invoke CimMethod' concluída** aparecer na tela, o SQL Server deverá estar instalado.

## <a name="validate-installation"></a>Validar a instalação

### <a name="dsc"></a>DSC

Os cmdlets [Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) podem determinar se o estado atual do servidor cumpre o estado desejado. Neste caso, é a instalação do SQL Server. O resultado de **Test-DscConfiguration** deve ser **True**:

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>Serviços

A lista de serviços agora retorna os serviços do SQL Server:

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>Confira também

[Visão geral da Desired State Configuration do Windows PowerShell](/powershell/scripting/dsc/overview/overview)

[Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[Instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
