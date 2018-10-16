---
title: Baixar o módulo do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 10/08/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- instalar o sql server powershell, baixar o sql server powershell
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40873fe63b897da52fc9a7d440a8568872431d72
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851751"
---
# <a name="install-sql-server-powershell-module"></a>Instalar o módulo do SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo fornece orientações para instalar o módulo do **SqlServer** PowerShell.
> [!NOTE]
> Há dois módulos do SQL Server PowerShell: 
> * **SQLPS** esse módulo está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**.
> * **SqlServer**: esse módulo inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL. O módulo também contém versões atualizadas dos cmdlets no **SQLPS**. 

As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da [Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver).
A versão atual do módulo do **SqlServer** é 21.0.17279. Isso se baseia na versão v140 do Microsoft.SQLServer.SMO.  
Se você estiver procurando por uma versão do módulo que dá suporte à próxima versão do SQL Server (com base na versão v150 do Microsoft.SQLServer.SMO), consulte a seção na parte inferior desta página sobre como obter versões de pré-lançamento do módulo. A versão de pré-lançamento mais recente do módulo é 21.1.18040-preview.

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

> [!NOTE]
> Versões de pré-lançamento (ou "versão prévia") do módulo podem estar disponíveis na Galeria do PowerShell. Eles podem ser descobertos e instalados usando-se os cmdlets *Find-Module* e *Install-Module* atualizados que fazem parte do módulo [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet)), passando a opção *- AllowPrerelease*.
>
> Para descobrir a versão prévia/de pré-lançamento do módulo, você pode executar o seguinte comando:
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> Para instalar uma versão prévia/de pré-lançamento específica do módulo, você pode instalá-lo com um número de versão específico semelhante ao seguinte:
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

As versões do módulo do **SqlServer** na Galeria do PowerShell são compatíveis com controle de versão e exigem o PowerShell na versão 5.0 ou superior. 

* [Módulo do SqlServer na Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver) 
* [Cmdlets do SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets do SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
