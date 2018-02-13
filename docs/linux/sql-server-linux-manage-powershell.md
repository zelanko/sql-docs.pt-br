---
title: Gerenciar o SQL Server no Linux com o PowerShell | Microsoft Docs
description: "Este artigo fornece uma visão geral do uso do PowerShell no Windows com o SQL Server no Linux."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.workload: Inactive
ms.openlocfilehash: f7324a270323950444741cfe713ad0eb5f01aa10
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Use o PowerShell no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta [do SQL Server PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) e orienta você por alguns exemplos sobre como usá-lo com o SQL Server 2017 no Linux. Suporte do PowerShell para SQL Server está disponível atualmente no Windows, portanto você pode usá-lo quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Instale a versão mais recente do SQL PowerShell no Windows

[SQL PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) no Windows está incluído no [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md). Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do SSMS e do PowerShell do SQL. A versão mais recente do SSMS está sempre atualizada e otimizados e funciona atualmente com o SQL Server 2017 em Linux. Para baixar e instalar a versão mais recente, consulte [baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para se manter atualizado, a versão mais recente do SSMS avisa você quando há uma nova versão disponível para download.

## <a name="before-you-begin"></a>Antes de começar

Leitura de [problemas conhecidos](sql-server-linux-release-notes.md) para SQL Server 2017 no Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Inicie o PowerShell e importar o *sqlserver* módulo

Vamos começar iniciando o PowerShell no Windows. Abra um *prompt de comando* em seu computador com Windows e digitar **PowerShell** para iniciar uma nova sessão do Windows PowerShell.

```
PowerShell
```

O SQL Server fornece um módulo do Windows PowerShell chamado **SqlServer** que você pode usar para importar os componentes do SQL Server (provedor do SQL Server e cmdlets) em um ambiente do PowerShell ou script.

Copie e cole o seguinte comando no prompt do PowerShell para importar o **SqlServer** módulo na sua sessão atual do PowerShell:

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
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Conecte-se ao SQL Server e obter informações do servidor

Vamos usar o PowerShell no Windows para se conectar à instância do SQL Server 2017 no Linux e exibir algumas propriedades de servidor.

Copie e cole os seguintes comandos no prompt do PowerShell. Quando você executar esses comandos, PowerShell serão:
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo que solicita as credenciais (*nome de usuário do SQL* e *senha SQL*) para se conectar ao seu servidor de SQL 2017 instância no Linux
- Carregar o assembly do SQL Server Management Objects (SMO)
- Criar uma instância do [Server](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.server.aspx) objeto
- Conecte-se para o **Server** e exibir algumas propriedades

Lembre-se de substituir  **\<your_server_instance\>**  com o endereço IP ou o nome do host de sua instância do SQL Server 2017 no Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Load the SMO assembly and create a Server object
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO') | out-null
$server = New-Object ('Microsoft.SqlServer.Management.Smo.Server') $serverInstance

# Set credentials
$server.ConnectionContext.LoginSecure=$false
$server.ConnectionContext.set_Login($credential.UserName)
$server.ConnectionContext.set_SecurePassword($credential.Password)

# Connect to the Server and get a few properties
$server.Information | Select-Object Edition, HostPlatform, HostDistribution | Format-List
# done
```

O PowerShell deve exibir informações semelhantes à seguinte saída:

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> Se nada for exibido para esses valores, a conexão à instância do SQL Server de destino provavelmente serão falhou. Certifique-se de que você pode usar as mesmas informações de conexão para conectar-se do SQL Server Management Studio. Em seguida, examine as [recomendações de solução de problemas de conexão](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="examine-sql-server-error-logs"></a>Examine os logs de erros do SQL Server

Vamos usam PowerShell no Windows para examinar os logs de erros de conexão na instância do SQL Server 2017 no Linux. Também usaremos o **Out-GridView** logs de cmdlet para mostrar informações de erro em uma exibição de grade.

Copie e cole os seguintes comandos no prompt do PowerShell. Ele podem levar alguns minutos para ser executado. Esses comandos faça o seguinte:
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo que solicita as credenciais (*nome de usuário do SQL* e *senha SQL*) para se conectar ao seu servidor de SQL 2017 instância no Linux
- Use o **Get-SqlErrorLog** cmdlet para se conectar à instância do SQL Server 2017 no Linux e recuperar erro logs desde **ontem**
- Direcionar a saída para o **Out-GridView** cmdlet

Lembre-se de substituir  **\<your_server_instance\>**  com o endereço IP ou o nome do host de sua instância do SQL Server 2017 no Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Consulte também
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
