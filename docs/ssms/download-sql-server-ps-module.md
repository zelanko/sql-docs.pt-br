---
title: "Baixar o módulo do SQL Server PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalar o sql server powershell, baixar o sql server powershell
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>Baixar o módulo do SQL Server PowerShell
Como parte da versão 17.0 do SQL Server Management Studio, o módulo do SQL Server PowerShell agora é fornecido por meio da Galeria do PowerShell.  O módulo não está mais incluído no pacote de instalação do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões mais recentes, o módulo do SQL Server deve ser instalado no computador como uma etapa adicional.

Documentação completa sobre como instalar a versão mais recente do Windows Management Framework e como instalar os módulos do PowerShell em geral pode ser encontrado no site da [Galeria do PowerShell](https://www.powershellgallery.com/).

O comando do PowerShell para instalar o módulo do SQL Server é:

> Install-module -Name SqlServer -Scope CurrentUser

Se houver versões anteriores dos módulos do SQL Server PowerShell no computador, pode ser necessário fornecer o parâmetro “-AllowClobber”.  

As versões do módulo do SQL Server PowerShell fornecidas com a Galeria do PowerShell são compatíveis com controle de versão e exigem o PowerShell versão 5.0 ou superior.

