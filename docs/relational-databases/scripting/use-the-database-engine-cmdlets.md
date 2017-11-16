---
title: Usar cmdlets do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f73610b00bc4c7dd6e68128f841a3c7a1e6ed691
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="use-the-database-engine-cmdlets"></a>Usar cmdlets do Mecanismo de Banco de Dados
  Os cmdlets Windows PowerShell são comandos de função única que normalmente contêm uma convenção de nomenclatura formada por verbo-substantivo, como **Get-Help** ou **Set-MachineName**. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell fornece cmdlets específicos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="database-engine-cmdlets"></a>cmdlets do Mecanismo de Banco de Dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa alguns cmdlets para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Estes cmdlets são usados para executar principalmente scripts Transact-SQL existentes de novos scripts PowerShell, avaliar políticas de gerenciamento baseadas em política e ajudar a especificar identificadores do SQL Server em caminhos do provedor do SQL Server.  
  
 A maioria dos scripts do Windows PowerShell funcionam com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando o provedor do SQL Server PowerShell e os modelos de objeto de gerenciamento do SQL Server. Para saber mais, confira [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
### <a name="get-cmdlet-help"></a>Obter a ajuda do cmdlet  
 No ambiente Windows PowerShell, o cmdlet **Get-Help** fornece informações de ajuda para cada cmdlet. O**Get-Help** retorna informações como sintaxe, definições de parâmetro, tipos de entrada e saída e uma descrição da ação executada pelo cmdlet. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
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
|Descreve o uso de **Invoke-Sqlcmd** para executar scripts **sqlcmd** ou comandos contendo [!INCLUDE[tsql](../../includes/tsql-md.md)] ou instruções XQuery. Ele pode aceitar a entrada **sqlcmd** como um parâmetro de entrada da cadeia de caracteres do caractere ou como o nome de um arquivo de script a ser aberto.|[cmdlet Invoke-Sqlcmd](../../powershell/invoke-sqlcmd-cmdlet.md)|  
|Descreve o uso de **Invoke-PolicyEvaluation** para relatar se um conjunto de destino de objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é compatível com as condições definidas em políticas de gerenciamento baseadas em políticas. Opcionalmente, o cmdlet pode ser usado para reconfigurar qualquer opção definível nos objetos de destino que não obedecem às condições de políticas.|[cmdlet Invoke-PolicyEvaluation](../../powershell/invoke-policyevaluation-cmdlet.md)|  
|Descreve o uso de **Encode-Sqlname** e **Decode-Sqlname** para tratar identificadores SQL Server que contêm caracteres sem suporte em caminhos do Windows PowerShell.|[Codificar e decodificar identificadores do SQL Server](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|Descreve o uso de **Convert-UrnToPath** para converter um URN (Nome de Recurso Uniforme) de Objeto de Gerenciamento SQL Server no caminho de provedor SQL Server equivalente.|[Converter URNs em caminhos de provedor SQL Server](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
[Visão geral de cmdlets do PowerShell para grupos de disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)
  
  
