---
title: Gerenciar o SQL Server no Linux com o PowerShell
description: Este artigo fornece uma visão geral do uso do PowerShell no Windows com o SQL Server no Linux.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 21ce61a823281c5e6688bcfb8aee96d296cb671d
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834930"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usar o PowerShell no Windows para gerenciar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta [SQL Server PowerShell](../powershell/sql-server-powershell.md) e orienta você por meio de alguns exemplos sobre como usá-lo com o SQL Server no Linux. Suporte do PowerShell para SQL Server está disponível atualmente no Windows, MacOS e Linux. Este artigo orienta você por meio de uma máquina do Windows para se conectar a uma instância remota do SQL Server no Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Instalar a versão mais recente do PowerShell do SQL no Windows

[SQL PowerShell](../powershell/download-sql-server-ps-module.md) no Windows é mantida na Galeria do PowerShell. Ao trabalhar com o SQL Server, você deve usar sempre a versão mais recente do módulo do SqlServer PowerShell.

## <a name="before-you-begin"></a>Antes de começar

Leia as [problemas conhecidos](sql-server-linux-release-notes.md) para o SQL Server no Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Inicie o PowerShell e importe as *sqlserver* módulo

Vamos começar iniciando o PowerShell no Windows. Use <kbd>Win</kbd>+<kbd>R</kbd>, em seu computador Windows e digitar **PowerShell** para iniciar uma nova sessão do Windows PowerShell.

```
PowerShell
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

Vamos usar o PowerShell no Windows para se conectar à instância do SQL Server no Linux e exibir algumas propriedades de servidor.

Copie e cole os seguintes comandos no prompt do PowerShell. Quando você executa esses comandos, PowerShell será:
- Exibir uma caixa de diálogo que solicitará o nome do host ou endereço IP da sua instância
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo, que solicitará as credenciais. Você pode usar sua *nome de usuário do SQL* e *senha SQL* para se conectar à instância do SQL Server no Linux
- Use o **Get-SqlInstance** para se conectar à **Server** e exibir algumas propriedades

Opcionalmente, você pode substituir apenas a `$serverInstance` variável com o endereço IP ou o nome do host da instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
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

## <a name="using-the-sql-server-powershell-provider"></a>Usando o provedor do SQL Server PowerShell

Outra opção para conectar-se à instância do SQL Server é usar o [provedor do SQL Server PowerShell](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Esse provedor permite que você navegue semelhante a como se você foram navegando na estrutura de árvore no Pesquisador de objetos, mas no cmdline de instância do SQL Server.  Por padrão esse provedor é apresentado como um PSDrive chamado `SQLSERVER:\` que você pode usar para conectar-se e navegar de instâncias do SQL Server à qual sua conta de domínio tenha acesso.  Ver [etapas de configuração](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) para obter informações sobre como configurar a autenticação do Active Directory para o SQL Server no Linux.

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

Aqui está a saída de aparência.  Você pode observar que a saída é semelhante a que o SSMS exibirá no nó bancos de dados.  Ele exibe os bancos de dados do usuário, mas não os bancos de dados do sistema.

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

Se você precisar ver todos os bancos de dados em sua instância, uma opção é usar o [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet.

## <a name="examine-sql-server-error-logs"></a>Examine os logs de erros do SQL Server

As etapas a seguir usam o PowerShell no Windows para examinar o erro logs conectar-se em sua instância do SQL Server no Linux. Também usaremos os **Out-GridView** logs de cmdlet para mostrar informações de erro em uma exibição do modo de exibição de grade.

Copie e cole os seguintes comandos no prompt do PowerShell. Ele podem levar alguns minutos para ser executado. Esses comandos faça o seguinte:
- Exibir uma caixa de diálogo que solicitará o nome do host ou endereço IP da sua instância
- Exibição de *solicitação de credencial do Windows PowerShell* caixa de diálogo, que solicitará as credenciais. Você pode usar sua *nome de usuário do SQL* e *senha SQL* para se conectar à instância do SQL Server no Linux
- Use o **Get-SqlErrorLog** logs de cmdlet para se conectar à instância do SQL Server no Linux e recuperar de erro desde **ontem**
- Direcionar a saída para o **Out-GridView** cmdlet

Opcionalmente, você pode substituir o `$serverInstance` variável com o endereço IP ou o nome do host da instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Confira também
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [Cmdlets do SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
