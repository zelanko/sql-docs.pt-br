---
title: Baixar o módulo do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: scripting
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- instalar o sql server powershell, baixar o sql server powershell
ms.assetid: ''
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35969e26d8ca363acd3ada589c4c594553e9a507
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321737"
---
# <a name="install-sql-server-powershell-module"></a>Instalar o módulo do SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo fornece orientações para instalar o módulo do **SqlServer** PowerShell.

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL. As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.

Para instalar o módulo do **SqlServer** da Galeria do PowerShell, inicie uma sessão do [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) e use os comandos a seguir. Se tiver problemas na instalação, consulte a [documentação Install-Module](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) e a [referência Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

Para instalar o módulo do **SqlServer**:

```Install-Module -Name SqlServer```

Se houver versões anteriores do módulo do **SqlServer** no computador, você poderá usar `Update-Module` (posteriormente neste artigo), ou fornecer o `-AllowClobber` parâmetro:  

```Install-Module -Name SqlServer -AllowClobber```

Caso não consiga executar a sessão do PowerShell como administrador, você poderá instalar no usuário atual:

```Install-Module -Name SqlServer -Scope CurrentUser```

Quando as versões atualizadas do módulo do **SqlServer** estiverem disponíveis, você poderá atualizar a versão usando `Update-Module`:

```Update-Module -Name SqlServer```

Para exibir as versões do módulo instalado:

```Get-Module SqlServer -ListAvailable```

Para usar uma versão específica do módulo, você pode importá-lo com um número de versão específico semelhante ao seguinte:

```Import-Module SqlServer -Version 21.0.17178```


As versões do módulo do **SqlServer** na Galeria do PowerShell são compatíveis com controle de versão e exigem o PowerShell na versão 5.0 ou superior. 

* [Módulo do SqlServer na Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver) 
* [Cmdlets do SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets do SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
