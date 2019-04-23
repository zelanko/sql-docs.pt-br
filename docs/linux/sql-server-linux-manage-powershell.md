---
title: Gerenciar o SQL Server no Linux com o PowerShell | Microsoft Docs
description: Este artigo fornece uma visão geral do uso do PowerShell no Windows com o SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 903d2d89ca0d551cbb78cfb69dd305f852f62313
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158762"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usar o PowerShell no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta [SQL Server PowerShell](../powershell/sql-server-powershell.md) e orienta você por meio de alguns exemplos sobre como usá-lo com o SQL Server no Linux. Suporte do PowerShell para SQL Server está disponível atualmente no Windows, portanto, você pode usá-lo quando você tiver um computador Windows que pode se conectar a uma instância remota do SQL Server no Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Instalar a versão mais recente do PowerShell do SQL no Windows

[SQL PowerShell](../powershell/download-sql-server-ps-module.md) no Windows é mantida na Galeria do PowerShell. Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do módulo do SqlServer PowerShell.

## <a name="before-you-begin"></a>Antes de começar

Leia as [problemas conhecidos](sql-server-linux-release-notes.md) para o SQL Server no Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Inicie o PowerShell e importe as *sqlserver* módulo

Vamos começar iniciando o PowerShell no Windows. Abra uma *prompt de comando* em seu computador Windows e digitar **PowerShell** para iniciar uma nova sessão do Windows PowerShell.

```
PowerShell
```

O SQL Server fornece um módulo Windows PowerShell nomeado **SqlServer** que você pode usar para importar os componentes do SQL Server (provedor do SQL Server e cmdlets) em um ambiente do PowerShell ou o script.

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

Vamos usar o PowerShell no Windows para se conectar à instância do SQL Server no Linux e exibir algumas propriedades de servidor.

Copie e cole os seguintes comandos no prompt do PowerShell. Quando você executa esses comandos, PowerShell será:
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo que solicitará as credenciais (*nome de usuário do SQL* e *senha SQL*) para se conectar ao SQL Server instância no Linux
- Criar uma instância das [Server](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.server.aspx) objeto
- Conectar-se para o **Server** e exibir algumas propriedades

Lembre-se de substituir **\<your_server_instance\>** com o endereço IP ou o nome do host da instância do SQL Server no Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

## <a name="examine-sql-server-error-logs"></a>Examine os logs de erros do SQL Server

Vamos usar o PowerShell no Windows para examinar os logs de erros se conectar em sua instância do SQL Server no Linux. Também usaremos os **Out-GridView** logs de cmdlet para mostrar informações de erro em uma exibição do modo de exibição de grade.

Copie e cole os seguintes comandos no prompt do PowerShell. Ele podem levar alguns minutos para ser executado. Esses comandos faça o seguinte:
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo que solicitará as credenciais (*nome de usuário do SQL* e *senha SQL*) para se conectar ao SQL Server instância no Linux
- Use o **Get-SqlErrorLog** logs de cmdlet para se conectar à instância do SQL Server no Linux e recuperar de erro desde **ontem**
- Direcionar a saída para o **Out-GridView** cmdlet

Lembre-se de substituir **\<your_server_instance\>** com o endereço IP ou o nome do host da instância do SQL Server no Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Confira também
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
