---
title: Baixar o módulo do SQL Server PowerShell
description: Saiba como instalar o módulo do SqlServer PowerShell, que fornece cmdlets que dão suporte aos recursos mais recentes do SQL e contém versões atualizadas dos cmdlets no módulo SQLPS.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, aanelson
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 3165a56d93ba78c387be0cdd23ef0c225b31c336
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714064"
---
# <a name="install-the-sql-server-powershell-module"></a>Instalar o módulo SQL Server PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este artigo fornece orientações para instalar o módulo do **SqlServer** PowerShell.

## <a name="powershell-modules-for-sql-server"></a>Módulos PowerShell para SQL Server

Há dois módulos do SQL Server PowerShell:

- **SqlServer**: O módulo SqlServer inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL. O módulo também contém versões atualizadas dos cmdlets no **SQLPS**. Para baixar o módulo SqlServer, vá para [Módulo SqlServer na Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver).

- **SQLPS**: o SQLPS é o módulo usado pelo [SQL Agent](sql-server-powershell.md#sql-server-agent) para executar trabalhos do Agent em etapas de trabalho do agente por meio do subsistema PowerShell.

> [!NOTE]
> As versões do módulo do **SqlServer** na Galeria do PowerShell são compatíveis com controle de versão e exigem o PowerShell na versão 5.0 ou superior.

Para tópicos de ajuda, vá para:

- Cmdlets [SqlServer](https://docs.microsoft.com/powershell/module/sqlserver).
- Cmdlets [SQLPS](https://docs.microsoft.com/powershell/module/sqlps).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

O [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) não instala nenhum desses módulos do PowerShell. Para usar o PowerShell com o SSMS, instale o módulo **SqlServer** da [Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver).

> [!NOTE]
> Com SSMS 16.x, uma versão anterior do módulo **SqlServer** é incluída no SSMS (SQL Server Management Studio)

## <a name="azure-data-studio"></a>Azure Data Studio

O [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) não instala nenhum desses módulos do PowerShell. Para usar o PowerShell com o Azure Data Studio, instale o módulo **SqlServer** da [Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver).

É possível usar a [extensão do PowerShell](../azure-data-studio/powershell-extension.md), que fornece suporte avançado ao editor do PowerShell no Azure Data Studio.

## <a name="installing-or-updating-the-sqlserver-module"></a>Como instalar ou atualizar o módulo SqlServer

Para instalar o módulo **SqlServer** da Galeria do PowerShell, inicie uma sessão do [PowerShell](/powershell/scripting/overview) como administrador. Inicie também o Azure Data Studio como administrador e executar esses comandos em uma sessão do PowerShell no terminal integrado.

Use também *Install-Module SQLServer -Scope CurrentUser* para executar permissões elevadas. Esse cmdlet é útil para usuários que não são administradores no respectivo ambiente. No entanto, como o escopo é limitado ao usuário atual, os outros usuários do mesmo computador não podem usar o módulo.

### <a name="install-the-sqlserver-module"></a>Instalar o módulo SqlServer

Execute o seguinte comando em sua sessão do PowerShell com o objetivo de instalar o módulo SqlServer para todos os usuários:

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>Exibir as versões instaladas do módulo SqlServer

Execute o comando a seguir para conferir as versões do módulo SqlServer que foram instaladas

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>Instalar para o usuário atual e não como administrador

Caso não consiga executar a sessão do PowerShell como administrador, instale para o usuário atual usando o seguinte comando:

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>Substituir uma versão anterior do módulo SqlServer

Também é possível usar o comando `Install-Module` para substituir uma versão anterior.

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> O PowerShell sempre usa o módulo mais recente instalado.

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>Atualizar a versão instalada do módulo SqlServer

Quando as versões atualizadas do módulo **SqlServer** estiverem disponíveis será possível instalar a versão mais recente usando o seguinte comando:

```powershell
Install-Module -Name SqlServer -AllowClobber
```

É possível usar o comando `Update-Module` para instalar a versão mais recente do módulo SQL Server PowerShell, mas isso não removerá as versões mais antigas. Ele instala a versão mais recente lado a lado para permitir que você a experimente, porém os módulos mais antigos permanecem instalados.

No entanto, caso não queira manter as versões mais antigas do módulo, você poderá usar o comando `Uninstall-Module` para remover as versões anteriores.

Caso mais de uma versão esteja instalada é possível usar o seguinte comando para listá-las:

```powershell
Get-Module SqlServer -ListAvailable
```

É possível usar o seguinte comando para remover as versões mais antigas:

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>Solução de problemas

Se tiver problemas na instalação, consulte a [documentação Install-Module](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1) e a [referência Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>Como usar uma versão específica do módulo SqlServer

Para usar uma versão específica do módulo, importe-a com um número de versão específico, semelhante ao seguinte comando:

```powershell
Import-Module SqlServer -Version 21.1.18080
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>Versões de pré-lançamento do módulo SqlServer

As versões de pré-lançamento (ou "versão prévia") do módulo SqlServer podem estar disponíveis na Galeria do PowerShell.

> [!IMPORTANT]
> Essas versões podem ser descobertas e instaladas usando os cmdlets *Find-Module* e *Install-Module* atualizados que fazem parte do módulo [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet), passando pelo comutador *-AllowPrerelease*. Para usar esses cmdlets, instale o módulo PowerShellGet e abra uma nova sessão.

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>Descobrir as versões de pré-lançamento do módulo SqlServer

Para descobrir as versões de pré-lançamento (versão prévia) do módulo SqlServer, execute o seguinte comando:

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>Instalar uma versão de pré-lançamento específica do módulo SqlServer

Para instalar uma versão de pré-lançamento específica do módulo, instale-a com um número de versão específico.

Você pode tentar usar o seguinte comando:

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>SQL Server PowerShell no Linux

Visite [Gerenciar o SQL Server em Linux com o PowerShell Core](../linux/sql-server-linux-manage-powershell-core.md) para saber como instalar o SQL Server PowerShell no Linux.

## <a name="other-modules"></a>Outros módulos

- [Az.Sql](https://www.powershellgallery.com/packages/Az.Sql/) – Cmdlets do serviço SQL para o Azure Resource Manager no Windows PowerShell e no PowerShell Core.

- [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc/) – Módulo com recursos de DSC para implantação e configuração do Microsoft SQL Server.

## <a name="next-steps"></a>Próximas etapas

[SQL Server PowerShell](sql-server-powershell.md)