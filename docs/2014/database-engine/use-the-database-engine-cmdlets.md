---
title: Usar cmdlets do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
caps.latest.revision: 24
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 845b99288bc000d1bf6adf5f48c6ad5d3099c415
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117234"
---
# <a name="use-the-database-engine-cmdlets"></a>Usar cmdlets do Mecanismo de Banco de Dados
  Os cmdlets Windows PowerShell são comandos de função única que normalmente contêm uma convenção de nomenclatura formada por verbo-substantivo, como **Get-Help** ou **Set-MachineName**. O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para Windows PowerShell fornece cmdlets específicos para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="database-engine-cmdlets"></a>cmdlets do Mecanismo de Banco de Dados  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa alguns cmdlets para o [!INCLUDE[ssDE](../includes/ssde-md.md)]. Estes cmdlets são usados para executar principalmente scripts Transact-SQL existentes de novos scripts PowerShell, avaliar políticas de gerenciamento baseadas em política e ajudar a especificar identificadores do SQL Server em caminhos do provedor do SQL Server.  
  
 A maioria dos scripts do Windows PowerShell funcionam com o [!INCLUDE[ssDE](../includes/ssde-md.md)] usando o provedor do SQL Server PowerShell e os modelos de objeto de gerenciamento do SQL Server. Para saber mais, confira [SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="get-cmdlet-help"></a>Obter a ajuda do cmdlet  
 No ambiente Windows PowerShell, o cmdlet **Get-Help** fornece informações de ajuda para cada cmdlet. O**Get-Help** retorna informações como sintaxe, definições de parâmetro, tipos de entrada e saída e uma descrição da ação executada pelo cmdlet. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../2014/database-engine/get-help-sql-server-powershell.md).  
  
### <a name="partial-parameter-names"></a>Nomes de parâmetro parciais  
 Você não tem que especificar o nome inteiro de um parâmetro cmdlet. Você só tem que especificar uma parte suficiente do nome para separá-lo exclusivamente dos outros parâmetros que são suportados pelo cmdlet. Por exemplo, estes exemplos mostram três modos de especificar o parâmetro **Invoke-Sqlcmd -QueryTimeout** :  
  
```  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>Tarefas cmdlet do Mecanismo de Banco de Dados  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve o uso de **Invoke-Sqlcmd** para executar scripts **sqlcmd** ou comandos contendo [!INCLUDE[tsql](../includes/tsql-md.md)] ou instruções XQuery. Ele pode aceitar a entrada **sqlcmd** como um parâmetro de entrada da cadeia de caracteres do caractere ou como o nome de um arquivo de script a ser aberto.|[cmdlet Invoke-Sqlcmd](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|Descreve o uso de **Invoke-PolicyEvaluation** para relatar se um conjunto de destino de objetos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é compatível com as condições definidas em políticas de gerenciamento baseadas em políticas. Opcionalmente, o cmdlet pode ser usado para reconfigurar qualquer opção definível nos objetos de destino que não obedecem às condições de políticas.|[cmdlet Invoke-PolicyEvaluation](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
|Descreve como usar `Encode-Sqlname` e `Decode-Sqlname` para tratar identificadores SQL Server que contêm caracteres não suportados em caminhos do Windows PowerShell.|[Codificar e decodificar identificadores do SQL Server](../powershell/encode-and-decode-sql-server-identifiers.md)|  
|Descreve como usar `Convert-UrnToPath` para converter um SQL Server gerenciamento objeto URN Uniform Resource Name () para o caminho de provedor do SQL Server equivalente.|[Converter URNs em caminhos do Provedor do SQL Server](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [Visão geral dos Cmdlets do PowerShell para grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  