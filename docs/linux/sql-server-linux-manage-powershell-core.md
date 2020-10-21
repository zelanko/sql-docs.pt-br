---
title: Gerenciar o SQL Server em Linux com o PowerShell Core
description: Saiba mais sobre o SQL Server PowerShell examinando alguns exemplos de como usar o SQL Server PowerShell com o PS Core (PowerShell Core) no macOS e no Linux.
ms.date: 04/22/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: vanto
ms.openlocfilehash: d9df9281926008ddac99b6827c41a0b6e73b2290
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115594"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>Gerenciar o SQL Server em Linux com o PowerShell Core

Este artigo apresenta o [SQL Server PowerShell](../powershell/sql-server-powershell.md) e descreve alguns exemplos de como usá-lo com o PS Core (PowerShell Core) no macOS e no Linux. O PowerShell Core agora é um projeto de software livre no [GitHub](https://github.com/powershell/powershell).

## <a name="cross-platform-editor-options"></a>Opções de editor multiplataforma

Todas as etapas do PowerShell Code abaixo funcionarão em um terminal regular ou você pode executá-las em um terminal no VS Code ou no Azure Data Studio.  O VS Code e o Azure Data Studio estão disponíveis no macOS e no Linux.  Para saber mais sobre o Azure Data Studio, confira [este início rápido](../azure-data-studio/quickstart-sql-server.md).  Talvez convenha considerar o uso da [extensão do PowerShell](../azure-data-studio/extensions/powershell-extension.md) para ele.

## <a name="installing-powershell-core"></a>Instalar o PowerShell Core

Para saber mais sobre como instalar o PowerShell Core em várias plataformas compatíveis e experimentais, confira os artigos a seguir:

- [Instalar o PowerShell Core no Windows](/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Instalar o PowerShell Core no Linux](/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalar o PowerShell Core no macOS](/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [Instalar o PowerShell Core no ARM](/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>Instalar o módulo SqlServer

O módulo `SqlServer` é mantido na [Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer/). Ao trabalhar com o SQL Server, você sempre deve usar a versão mais recente do módulo SqlServer do PowerShell.

Para instalar o módulo SqlServer, abra uma sessão do PowerShell Core e execute o código a seguir:

```powerhsell
Install-Module -Name SqlServer
```

Para saber mais sobre como instalar o módulo SqlServer da Galeria do PowerShell, confira esta [página](../powershell/download-sql-server-ps-module.md).

## <a name="using-the-sqlserver-module"></a>Usar o módulo SqlServer

Vamos começar iniciando o PowerShell Core.  Se você estiver no macOS ou no Linux, abra uma *sessão de terminal* em seu computador e digite **pwsh** para iniciar uma nova sessão do PowerShell Core.  No Windows, use <kbd>Win</kbd>+<kbd>R</kbd> e digite `pwsh` para iniciar uma nova sessão do PowerShell Core.

```
pwsh
```

O SQL Server fornece um módulo do PowerShell chamado **SqlServer**. Você pode usar o módulo **SqlServer** para importar os componentes do SQL Server (provedor e cmdlets do SQL Server) para um ambiente ou um script do PowerShell.

Copie e cole o seguinte comando no prompt do PowerShell para importar o módulo **SqlServer** para a sessão atual do PowerShell:

```powershell
Import-Module SqlServer
```

Digite o seguinte comando no prompt do PowerShell para verificar se o módulo **SqlServer** foi importado corretamente:

```powershell
Get-Module -Name SqlServer
```

O PowerShell deverá exibir informações semelhantes à seguinte saída:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Conectar-se ao SQL Server e obter informações do servidor

As etapas a seguir usam o PowerShell Core para se conectar à sua Instância do SQL Server em Linux e exibir algumas propriedades de servidor.

Copie e cole os comandos a seguir no prompt do PowerShell. Quando você executar esses comandos, o PowerShell:
- Exibem uma caixa de diálogo que solicita o nome do host ou o endereço IP de sua instância
- Exibirá a caixa de diálogo *Solicitação de credenciais do PowerShell*, que solicita as credenciais. É possível usar o *nome de usuário do SQL* e a *senha do SQL* para se conectar à sua instância do SQL Server em Linux
- Usará o cmdlet **Get-SqlInstance** para se conectar ao **Servidor** e exibir algumas propriedades

Opcionalmente, você pode simplesmente substituir a variável `$serverInstance` pelo endereço IP ou pelo nome do host da Instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

O PowerShell deverá exibir informações semelhantes à seguinte saída:

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> Se nada for exibido para esses valores, a conexão com a Instância do SQL Server de destino provavelmente terá falhado. Verifique se você pode usar as mesmas informações de conexão para se conectar no SQL Server Management Studio. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="using-the-sql-server-powershell-provider"></a>Usar o provedor do SQL Server PowerShell

Outra opção para se conectar à Instância do SQL Server é usar o [Provedor do SQL Server PowerShell](../powershell/sql-server-powershell-provider.md).  Usar esse provedor permite que você navegue pela Instância do SQL Server de forma semelhante a como se estivesse navegando pela estrutura de árvore do Pesquisador de Objetos, mas na cmdline.  Por padrão, esse provedor é apresentado como um PSDrive chamado `SQLSERVER:\`, que você poderá usar para se conectar às Instâncias do SQL Server às quais sua conta de domínio tem acesso e navegar por elas.  Confira [Etapas de configuração](./sql-server-linux-active-directory-auth-overview.md#configuration-steps) para obter informações sobre como configurar a autenticação do Active Directory para o SQL Server em Linux.

Use também a autenticação SQL com o Provedor SQL Server PowerShell. Para fazer isso, use o cmdlet `New-PSDrive` para criar um PSDrive e forneça as credenciais apropriadas para se conectar.

No exemplo abaixo, você verá um exemplo de como criar um PSDrive usando a autenticação SQL.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

Você pode confirmar se a unidade foi criada executando o cmdlet `Get-PSDrive`.

```powershell
Get-PSDrive
```

Depois de criar o PSDrive, comece a navegar por ele.

```powershell
dir SQLonDocker:\Databases
```

Veja a seguir a aparência da saída.  Você pode notar que esta saída é semelhante ao que o SSMS exibirá no nó Bancos de dados.  Ele exibe os bancos de dados de usuário, mas não os bancos de dados do sistema.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

Se você precisar ver todos os bancos de dados da instância, uma opção será usar o cmdlet `Get-SqlDatabase`.

## <a name="get-databases"></a>Obter bancos de dados

Um cmdlet importante para conhecer é o `Get-SqlDatabase`.  Para muitas operações que envolvem um banco de dados ou objetos dentro de um banco de dados, o cmdlet `Get-SqlDatabase` pode ser usado.  Se você fornecer valores para os parâmetros `-ServerInstance` e `-Database`, somente esse objeto de banco de dados será recuperado.  No entanto, se você especificar somente o parâmetro `-ServerInstance`, uma lista completa de todos os bancos de dados nessa instância será retornada.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

Veja um exemplo do que pode ser retornado pelo comando Get-SqlDatabase acima:

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>Examinar os logs de erros do SQL Server

As etapas a seguir usam o PowerShell Core para examinar os logs de erros e se conectar à sua Instância do SQL Server em Linux.

Copie e cole os comandos a seguir no prompt do PowerShell. Pode levar alguns minutos para que eles sejam executados. Esses comandos executam as seguintes etapas:
- Exibem uma caixa de diálogo que solicita o nome do host ou o endereço IP de sua instância
- Exibem a caixa de diálogo *Solicitação de credenciais do PowerShell*, que solicita as credenciais. É possível usar o *nome de usuário do SQL* e a *senha do SQL* para se conectar à sua instância do SQL Server em Linux
- Usam o cmdlet **Get-SqlErrorLog** para se conectar à Instância do SQL Server em Linux e recuperar os logs de erros desde **Ontem**

Opcionalmente, você pode substituir a variável `$serverInstance` pelo endereço IP ou pelo nome do host da Instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>Explorar os cmdlets disponíveis no momento no PS Core
Embora o módulo SqlServer tenha 109 cmdlets disponíveis no Windows PowerShell no momento, apenas 62, dos 109, estão disponíveis no PSCore. Uma lista completa dos 62 cmdlets disponíveis no momento está incluída abaixo.  Para obter uma documentação detalhada de todos os cmdlets no módulo SqlServer, confira a [referência de cmdlet](/powershell/module/sqlserver/) do SqlServer.

O comando a seguir mostrará todos os cmdlets disponíveis na versão do PowerShell que você está usando.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
Sort-Object -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Invoke-SqlAssessment
- Get-SqlAssessmentItem
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Read-SqlXEvent
- Convert-UrnToPath

## <a name="see-also"></a>Confira também
- [SQL Server PowerShell](../powershell/sql-server-powershell.md)