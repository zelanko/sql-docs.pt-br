---
title: Gerenciar o SQL Server em Linux com o PowerShell
description: Este artigo fornece uma visão geral do uso do PowerShell no Windows com o SQL Server em Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 52db0986bb6af34e1dc034d95146a96d3fdcf246
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68000122"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usar o PowerShell no Windows para gerenciar o SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta o [SQL Server PowerShell](../powershell/sql-server-powershell.md) e descreve alguns exemplos de como usá-lo com o SQL Server em Linux. O suporte do PowerShell para o SQL Server está atualmente disponível no Windows, no macOS e no Linux. Este artigo explica como usar um computador Windows para se conectar a uma Instância remota do SQL Server em Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Instalar a última versão do SQL PowerShell no Windows

O [SQL PowerShell](../powershell/download-sql-server-ps-module.md) no Windows é mantido na Galeria do PowerShell. Ao trabalhar com o SQL Server, você sempre deve usar a versão mais recente do módulo SqlServer do PowerShell.

## <a name="before-you-begin"></a>Antes de começar

Leia os [Problemas conhecidos](sql-server-linux-release-notes.md) do SQL Server em Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Iniciar o PowerShell e importar o módulo *sqlserver*

Vamos começar iniciando o PowerShell no Windows. Use <kbd>Win</kbd>+<kbd>R</kbd> no computador Windows e digite **PowerShell** para iniciar uma nova sessão do Windows PowerShell.

```
PowerShell
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

Vamos usar o PowerShell no Windows para se conectar à sua Instância do SQL Server em Linux e exibir algumas propriedades de servidor.

Copie e cole os comandos a seguir no prompt do PowerShell. Quando você executar esses comandos, o PowerShell:
- Exibem uma caixa de diálogo que solicita o nome do host ou o endereço IP de sua instância
- Exibem a caixa de diálogo de *solicitação de credenciais do Windows PowerShell*, que solicitará as credenciais. É possível usar o *nome de usuário do SQL* e a *senha do SQL* para se conectar à sua instância do SQL Server em Linux
- Usará o cmdlet **Get-SqlInstance** para se conectar ao **Servidor** e exibir algumas propriedades

Opcionalmente, você pode simplesmente substituir a variável `$serverInstance` pelo endereço IP ou pelo nome do host da Instância do SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

Outra opção para se conectar à Instância do SQL Server é usar o [Provedor do SQL Server PowerShell](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Esse provedor permite que você navegue pela Instância do SQL Server de forma semelhante a como se estivesse navegando pela estrutura de árvore do Pesquisador de Objetos, mas na cmdline.  Por padrão, esse provedor é apresentado como um PSDrive chamado `SQLSERVER:\`, que você poderá usar para se conectar às Instâncias do SQL Server às quais sua conta de domínio tem acesso e navegar por elas.  Confira [Etapas de configuração](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) para obter informações sobre como configurar a autenticação do Active Directory para o SQL Server em Linux.

Use também a autenticação SQL com o Provedor SQL Server PowerShell. Para fazer isso, use o cmdlet `New-PSDrive` para criar um novo PSDrive e forneça as credenciais apropriadas para se conectar.

Neste exemplo abaixo, você verá um exemplo de como criar um PSDrive usando a autenticação SQL.

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

Veja a seguir a aparência da saída.  Você pode notar que a saída é semelhante ao que o SSMS exibirá no nó Bancos de dados.  Ele exibe os bancos de dados de usuário, mas não os bancos de dados do sistema.

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

Se você precisar ver todos os bancos de dados da instância, uma opção será usar o cmdlet [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase).

## <a name="examine-sql-server-error-logs"></a>Examinar os logs de erros do SQL Server

As etapas a seguir usam o PowerShell no Windows para examinar os logs de erros e se conectar à sua Instância do SQL Server em Linux. Também usaremos o cmdlet **Out-GridView** para mostrar informações dos logs de erros em uma exibição de grade.

Copie e cole os comandos a seguir no prompt do PowerShell. Pode levar alguns minutos para que eles sejam executados. Esses comandos fazem o seguinte:
- Exibem uma caixa de diálogo que solicita o nome do host ou o endereço IP de sua instância
- Exibem a caixa de diálogo de *solicitação de credenciais do Windows PowerShell*, que solicitará as credenciais. É possível usar o *nome de usuário do SQL* e a *senha do SQL* para se conectar à sua instância do SQL Server em Linux
- Usam o cmdlet **Get-SqlErrorLog** para se conectar à Instância do SQL Server em Linux e recuperar os logs de erros desde **Ontem**
- Direcionam a saída para o cmdlet **Out-GridView**

Opcionalmente, você pode substituir a variável `$serverInstance` pelo endereço IP ou pelo nome do host da Instância do SQL Server.

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
