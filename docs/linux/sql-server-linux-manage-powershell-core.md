---
title: Gerenciar o SQL Server no Linux com o PowerShell Core | Microsoft Docs
description: Este artigo fornece uma visão geral de como usar o PowerShell Core com o SQL Server no Linux.
ms.date: 04/22/2019
ms.reviewer: jroth
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: craigg
ms.openlocfilehash: 242e3ab70d41df4d774400034f361b31289d97c9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713149"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>Gerenciar o SQL Server no Linux com o PowerShell Core

Este artigo apresenta [SQL Server PowerShell](../powershell/sql-server-powershell.md) e orienta você por meio de alguns exemplos sobre como usá-lo com o PowerShell Core (Core PS) no macOS e Linux. O PowerShell Core agora é um projeto de código-fonte aberto no [GitHub](https://github.com/powershell/powershell).

## <a name="cross-platform-editor-options"></a>Opções do editor de plataforma cruzada

Todas as etapas abaixo do PowerShell Core funcionará em um terminal regular ou você pode executá-los em um terminal no VS Code ou o estúdio de dados do Azure.  VS Code e o Azure Data Studio estão disponíveis no macOS e Linux.  Para obter mais informações sobre o estúdio de dados do Azure, consulte [este guia de início rápido](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server).  Talvez você queira considerar o uso de [extensão do PowerShell](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension) para ele.

## <a name="installing-powershell-core"></a>Instalar o PowerShell Core

Para obter mais informações sobre como instalar o PowerShell Core em várias plataformas com suporte e experimentais, consulte os seguintes artigos:

- [Instalar o PowerShell Core no Windows](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Instalar o PowerShell Core no Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalar o PowerShell Core no macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [Instalar o PowerShell Core no ARM](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>Instalar o módulo do SqlServer

O `SqlServer` módulo é mantido na [da Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer/). Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do módulo do SqlServer PowerShell.

Para instalar o módulo do SqlServer, abra uma sessão do PowerShell Core e execute o seguinte código:

```powerhsell
Install-Module -Name SqlServer
```

Para obter mais informações sobre como instalar o módulo do SqlServer na Galeria do PowerShell, consulte este [página](../powershell/download-sql-server-ps-module.md).

## <a name="using-the-sqlserver-module"></a>Usando o módulo do SqlServer

Vamos começar iniciando o PowerShell Core.  Se você estiver no macOS ou Linux, abra uma *sessão de terminal* em seu computador e digitar **pwsh** para iniciar uma nova sessão do PowerShell Core.  No Windows, use <kbd>Win</kbd>+<kbd>R</kbd>e o tipo `pwsh` para iniciar uma nova sessão do PowerShell Core.

```
pwsh
```

O SQL Server fornece um módulo PowerShell nomeado **SqlServer**. Você pode usar o **SqlServer** module para importar os componentes do SQL Server (provedor do SQL Server e cmdlets) em um ambiente do PowerShell ou o script.

Copie e cole o seguinte comando no prompt do PowerShell para importar os **SqlServer** módulo na sua sessão atual do PowerShell:

```powershell
Import-Module SqlServer
```

Digite o seguinte comando no prompt do PowerShell para verificar se o **SqlServer** módulo foi importado corretamente:

```powershell
Get-Module -Name SqlServer
```

O PowerShell deve exibir informações semelhantes à seguinte saída:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Conecte-se ao SQL Server e obter informações do servidor

As etapas a seguir usam o PowerShell Core para se conectar à instância do SQL Server no Linux e exibir algumas propriedades de servidor.

Copie e cole os seguintes comandos no prompt do PowerShell. Quando você executa esses comandos, PowerShell será:
- Exibir uma caixa de diálogo que solicitará o nome do host ou endereço IP da sua instância
- Exibição de *solicitação de credencial do PowerShell* caixa de diálogo, que solicitará as credenciais. Você pode usar sua *nome de usuário do SQL* e *senha SQL* para se conectar à instância do SQL Server no Linux
- Use o **Get-SqlInstance** para se conectar à **Server** e exibir algumas propriedades

Opcionalmente, você pode substituir apenas a `$serverInstance` variável com o endereço IP ou o nome do host da instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

O PowerShell deve exibir informações semelhantes à seguinte saída:

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> Se nada for exibido para esses valores, a conexão à instância do SQL Server de destino mais provável falha. Certifique-se de que você pode usar as mesmas informações de conexão para conectar-se do SQL Server Management Studio. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="using-the-sql-server-powershell-provider"></a>Usando o provedor do SQL Server PowerShell

Outra opção para conectar-se à instância do SQL Server é usar o [provedor do SQL Server PowerShell](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Usando o provedor permite que você navegue semelhante a como se você foram navegando na estrutura de árvore no Pesquisador de objetos, mas no cmdline de instância do SQL Server.  Por padrão esse provedor é apresentado como um PSDrive chamado `SQLSERVER:\` que você pode usar para conectar-se e navegar de instâncias do SQL Server à qual sua conta de domínio tenha acesso.  Ver [etapas de configuração](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) para obter informações sobre como configurar a autenticação do Active Directory para o SQL Server no Linux.

Você também pode usar a autenticação do SQL com o provedor do SQL Server PowerShell. Para fazer isso, use o `New-PSDrive` cmdlet para criar um novo PSDrive e fornecer as credenciais apropriadas para se conectar.

No exemplo a seguir, você verá um exemplo de como criar um novo PSDrive usando a autenticação do SQL.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

Você pode confirmar que a unidade foi criada executando o `Get-PSDrive` cmdlet.

```powershell
Get-PSDrive
```

Depois de criar seu novo PSDrive, você pode iniciar navegando-lo.

```powershell
dir SQLonDocker:\Databases
```

Aqui está a saída de aparência.  Você pode notar que essa saída é semelhante a que o SSMS exibirá no nó bancos de dados.  Ele exibe os bancos de dados do usuário, mas não os bancos de dados do sistema.

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

Se você precisar ver todos os bancos de dados em sua instância, uma opção é usar o `Get-SqlDatabase` cmdlet.

## <a name="get-databases"></a>Obter bancos de dados

É um cmdlet importante saber o `Get-SqlDatabase`.  Para muitas operações que envolvem um banco de dados ou objetos dentro de um banco de dados, o `Get-SqlDatabase` cmdlet pode ser usado.  Se você fornecer valores para ambas as `-ServerInstance` e `-Database` parâmetros, apenas esse objeto de um banco de dados serão recuperados.  No entanto, se você especificar apenas o `-ServerInstance` parâmetro, uma lista completa de todos os bancos de dados nessa instância será retornada.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

Aqui está um exemplo de como o que pode ser retornado pelo comando Get-SqlDatabase acima:

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

## <a name="examine-sql-server-error-logs"></a>Examine os logs de erros do SQL Server

As etapas a seguir usam o PowerShell Core para examinar o erro logs conectar-se em sua instância do SQL Server no Linux.

Copie e cole os seguintes comandos no prompt do PowerShell. Ele podem levar alguns minutos para ser executado. Esses comandos execute as seguintes etapas:
- Exibir uma caixa de diálogo que solicitará o nome do host ou endereço IP da sua instância
- Exibição de *solicitação de credencial do PowerShell* caixa de diálogo que solicitará as credenciais. Você pode usar sua *nome de usuário do SQL* e *senha SQL* para se conectar à instância do SQL Server no Linux
- Use o **Get-SqlErrorLog** logs de cmdlet para se conectar à instância do SQL Server no Linux e recuperar de erro desde **ontem**

Opcionalmente, você pode substituir o `$serverInstance` variável com o endereço IP ou o nome do host da instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>Explore os cmdlets disponíveis atualmente no principal PS
Enquanto o módulo do SqlServer atualmente tem 106 cmdlets disponíveis no Windows PowerShell, 59 somente do 106 estão disponíveis em PSCore. Uma lista completa dos 59 cmdlets disponíveis no momento está incluída abaixo.  Para obter documentação detalhada de todos os cmdlets no módulo SqlServer, consulte o SqlServer [referência de cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/).

O comando a seguir mostra todos os cmdlets disponíveis na versão do PowerShell que você está usando.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
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
- Convert-UrnToPath

## <a name="see-also"></a>Confira também
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
