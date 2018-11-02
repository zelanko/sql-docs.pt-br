---
title: Instalar o SQL Server com a Desired State Configuration do PowerShell | Microsoft Docs
description: Saiba como instalar o SQL Server usando a DSC (Desired State Configuration) do PowerShell.
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16d425d8eb66a950f432fa3ef9c68a8e68a78d22
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148471"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>Instalar o SQL Server com a Desired State Configuration do PowerShell

Quantas vezes você usou a interface de instalação do SQL Server clicando nos mesmos botões, inserindo as mesmas informações, sem parar para pensar direito nessas ações? E quando a instalação é concluída, você finalmente percebe que esqueceu de especificar algo importante como, por exemplo, o grupo do DBA na função sysadmin. E então, você precisa gastar seu precioso tempo entrando no modo de usuário único, adicionando os usuários ou grupos apropriados e, enfim, ativando novamente o SQL backup no modo de multiusuário e testando. E o pior é que agora a confiança de toda a instalação fica abalada. "O que mais eu esqueci?" Eu mesmo já estive nessa situação mais de uma vez.

Entre na [DSC (Desired State Configuration) do PowerShell](https://docs.microsoft.com/powershell/dsc/overview). Usando a DSC, é possível criar um modelo de configuração que poderá ser reutilizado em centenas de milhares de servidores. Dependendo do build, pode ser necessário ajustar alguns dos parâmetros de configuração, mas isso não é um problema, porque ainda é possível manter todas as configurações padrão em vigor. O interessante é que esse processo elimina a possibilidade de esquecer de inserir um parâmetro importante, por exemplo, depois de passar uma noite em claro cuidando dos filhos.

Neste artigo, explorarei a configuração inicial de uma instância autônoma do SQL Server 2017 no Windows Server 2016 usando o recurso de DSC SqlServerDsc. Algum conhecimento prévio sobre DSC poderá ser útil, porque eu não explorarei como funciona a DSC.

Os seguintes itens são necessários para este passo a passo:

- Um computador executando o Windows Server 2016
- A mídia de instalação do SQL Server 2017
- O recurso de DSC SqlServerDsc (a versão 10.0.0.0 é a atual no momento da escrita deste artigo)

## <a name="prerequisites"></a>Prerequisites

Na maioria dos casos, a DSC é usada para lidar com pré-requisitos. No entanto, no caso desta demonstração, lidarei com os pré-requisitos manualmente.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>Instalar o recurso de DSC SqlServerDsc

O recurso de DSC [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) pode ser baixado da [Galeria do PowerShell](https://www.powershellgallery.com/) usando o cmdlet [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1). _Observação: verifique se o PowerShell está em execução "Como Administrador" para instalar o módulo._

```PowerShell
Install-Module -Name SqlServerDsc
```

Obter a mídia de instalação do SQL Server 2017 Baixe a mídia de instalação do SQL Server 2017 no servidor. Eu baixei o SQL Server 2017 Enterprise da minha Assinatura do Visual Studio e copiei a ISO para "C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso".

Agora, a ISO precisa ser extraída para um diretório.

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

Crie a função de configuração que será chamada para gerar os documentos [MOF (Managed Object Format)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-).

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>Módulos

Importe os módulos na sessão atual. Esses módulos informam ao documento de configuração como compilar os documentos MOF e informam ao mecanismo de DSC como aplicar os documentos MOF no servidor.

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>Recursos

#### <a name="net-framework"></a>.NET Framework

O SQL Server baseia-se no .NET Framework, portanto, é necessário garantir que ele esteja instalado antes de instalar o SQL Server. O recurso WindowsFeature é utilizado para instalar o recurso Net-Framework-45-Core do Windows.

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

O recurso SqlSetup é usado para informar à DSC como instalar o SQL Server. Os parâmetros necessários para uma instalação básica são:

- **InstanceName**: o nome da instância. Utilize o MSSQLSERVER para uma instância padrão.
- **Features**: os recursos a serem instalados. Neste exemplo, estou instalando somente o recurso SQLEngine.
- **SourcePath**: o caminho para a mídia de instalação do SQL. Neste exemplo, eu armazenei a mídia de instalação do SQL em "C:\SQL2017". Um compartilhamento de rede pode ser utilizado para minimizar o espaço usado no servidor.
- **SQLSysAdminAccounts**: os usuários ou grupos que devem ser membros da função sysadmin. Neste exemplo, estou concedendo o acesso de sysadmin ao grupo local Administradores. _Observação: essa configuração não é recomendada em um ambiente de alta segurança._

Uma lista completa e uma descrição dos parâmetros disponíveis no SqlSetup estão disponíveis no [repositório SqlServerDsc do GitHub](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup).

O recurso SqlSetup é estranho, porque ele só instala o SQL e NÃO MANTÉM as configurações que são aplicadas. Por exemplo, se as SQLSysAdminAccounts forem especificadas no momento da instalação, um administrador poderá adicionar ou remover logons de/para a função sysadmin e o recurso SqlSetup não se preocupará. Se você desejar que a DSC imponha a associação da função sysadmin, o recurso [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) deverá ser utilizado.

#### <a name="complete-configuration"></a>Concluir a configuração

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

Execute dot-source no script de configuração:

```PowerShell
. .\SQLInstallConfiguration.ps1
```

Execute a função de configuração:

```PowerShell
SQLInstall
```

Um diretório será criado no diretório de trabalho chamado "SQLInstall" e conterá uma chamada ao arquivo "localhost.mof". Um exame do conteúdo do MOF mostrará a configuração DSC compilada.

### <a name="deploy-the-configuration"></a>Implantar a configuração

Para iniciar a implantação da DSC do SQL Server, chame o cmdlet Start-DscConfiguration. Os parâmetros fornecidos para o cmdlet são:

- **Path**: o caminho para a pasta que contém os documentos MOF a serem implantados. (por exemplo "C:\SQLInstall")
- **Wait**: aguardar a conclusão do trabalho de configuração.
- **Force**: substituir as configurações DSC existentes.
- **Verbose**: mostrar a saída detalhada. É útil ao publicar uma configuração pela primeira vez para auxiliar na solução de problemas.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

Conforme a configuração for sendo aplicada, a saída detalhada mostrará o que está acontecendo e passará uma sensação de que ALGO está acontecendo. Desde que nenhum erro (texto vermelho) seja gerado quando a mensagem "Operação 'Invoke CimMethod' concluída." for exibida na tela, o SQL estará instalado.

## <a name="validate-installation"></a>Validar a instalação

### <a name="dsc"></a>DSC

Os cmdlets [Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) podem ser utilizados para determinar se o estado atual do servidor, neste caso, a instalação do SQL, atende ao estado desejado. O resultado de Test-DscConfiguration deve ser "True".

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>Services

A listagem de serviços agora deve retornar os serviços do SQL Server

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

[Visão geral da Desired State Configuration do Windows PowerShell](https://docs.microsoft.com/powershell/dsc/overview)

[Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[Instalar o SQL Server usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
