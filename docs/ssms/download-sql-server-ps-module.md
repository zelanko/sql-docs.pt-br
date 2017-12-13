---
title: "Baixar o módulo do SQL Server PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: instalar o sql server powershell, baixar o sql server powershell
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7f6ab758ecd32d4d9bdb39d9157cbba9b38e73ba
ms.sourcegitcommit: b0c223ba0f78af5eb76948e68e2d1aab2e7b80c1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2017
---
# <a name="download-sql-server-powershell-module"></a>Baixar o módulo do SQL Server PowerShell
Como parte da versão 17.0 do SQL Server Management Studio, o módulo do SQL Server PowerShell agora é fornecido por meio da Galeria do PowerShell.  O módulo não está mais incluído no pacote de instalação do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões mais recentes, o módulo do SQL Server deve ser instalado no computador como uma etapa adicional.

Documentação completa sobre como instalar a versão mais recente do Windows Management Framework e como instalar os módulos do PowerShell em geral pode ser encontrado no site da [Galeria do PowerShell](https://www.powershellgallery.com/).

O comando do PowerShell para instalar o módulo do SQL Server é:

> Install-Module -Name SqlServer

Este comando instalará o módulo para todos os usuários do computador. Você precisará estar executando o processo do PowerShell como administrador.

> Install-Module -Name SqlServer -Scope CurrentUser

Este comando instalará o módulo para o usuário que executa o processo atual do PowerShell. Você não precisa estar executando o processo do PowerShell com direitos de administrador.

Se houver versões anteriores dos módulos do SQL Server PowerShell no computador, pode ser necessário fornecer o parâmetro “-AllowClobber”.  

Se estiver como administrador e a instalação do módulo para todos os usuários do computador

> Install-Module -Name SqlServer -AllowClobber

Se não é possível executar como administrador ou instalar somente para o usuário atual

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

Quando as versões atualizadas do módulo SqlServer estão disponíveis, você poderá atualizar a versão usando o comando Update-Module

> Update-Module -Name SqlServer

Para exibir as versões do módulo instalado no computador, você pode usar

> Get-Module SqlServer -ListAvailable

Para usar uma versão específica do módulo em seus scripts, você pode importá-lo com

> Import-Module SqlServer -Version 21.0.17178

As versões do módulo do SQL Server PowerShell fornecidas com a Galeria do PowerShell são compatíveis com controle de versão e exigem o PowerShell versão 5.0 ou superior. Você pode encontrar o módulo do SqlServer na [Galeria do PowerShell](https://www.powershellgallery.com/packages/Sqlserver/) 
