---
title: Ajuda do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 67633bcfad7c18679dae93de6e5541f3000a1ccc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779098"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  Há várias origens de informações sobre como usar o provedor e os cmdlets do provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para Windows PowerShell. Isso inclui a ajuda que está disponível no ambiente Windows PowerShell.  
  
## <a name="before-you-begin"></a>Antes de começar  
 Para saber mais sobre o Windows PowerShell, consulte o [Guia de Introdução do Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).  
  
 Para obter uma visão geral do provedor e os cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , veja [SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="help-in-the-windows-powershell-environment"></a>Ajude no ambiente de Windows PowerShell  
 Use o cmdlet **Get-Help** para obter ajuda no ambiente Windows PowerShell. **Get-Help** fornece ajuda básica para a linguagem Windows PowerShell e os diversos cmdlets e provedores disponíveis no Windows PowerShell.  
  
 Para obter mais informações sobre as maneiras como você pode usar **Get-Help**, consulte [Get-Help: Obtendo ajuda](https://go.microsoft.com/fwlink/?LinkId=102136).  
  
### <a name="sql-server-powershell-provider-help"></a>Ajuda do provedor do SQL Server PowerShell  
 O provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell implementa várias pastas em uma unidade virtual SQLSERVER, como as pastas SQLSERVER:\SQL e SQLSERVER:\DAC. Cada pasta é associada com um dos modelos de objeto de gerenciamento do SQL Server. Enquanto você puder listar os métodos e propriedades associadas com cada nó em um caminho de SQL Server, não poderá obter ajuda por eles no ambiente PowerShell. Para obter uma tabela das pastas com links para a referência de programação associada, consulte [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  
  
### <a name="invoke-sqlcmd-help"></a>Ajuda do Invoke-Sqlcmd  
 O cmdlet **Invoke-Sqlcmd** usa como entrada qualquer consulta ou arquivo de script que possa ser executado pelo utilitário **sqlcmd** . Você pode usar **Get-Help** para obter informações sobre **Invoke-Sqlcmd** e seus parâmetros, mas não há cobertura de **Get-Help** para consultas **sqlcmd** .  
  
 A entrada *-Query* ou *-QueryFromFile* pode conter:  
  
-   Variáveis e comandos do**sqlcmd** . Para obter informações sobre essas variáveis e comandos, consulte a seção Comentários de [sqlcmd Utility](../tools/sqlcmd-utility.md).  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] . Para obter mais informações sobre a linguagem [!INCLUDE[tsql](../includes/tsql-md.md)], veja [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference).  
  
-   Instruções XQuery. Para obter mais informações sobre a linguagem XQuery com suporte no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], veja [Referência de linguagem XQuery &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server).  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>Obtenha Ajuda para um cmdlet de SQL Server  
 **Para obter Ajuda para um cmdlet**  
  
-   Execute Get-Help especificando o nome do cmdlet e o nível de ajuda a ser retornada.  
  
### <a name="example-cmdlet-get-help"></a>Exemplo: cmdlet Get-Help  
 Os seguintes exemplos retornam vários níveis de ajuda para **Invoke-Sqlcmd**:  
  
```  
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>Obtenha uma lista de provedores  
 **Para obter uma lista de provedores ativos**  
  
1.  Execute Get-Help especificando a categoria de provedor.  
  
 Para obter mais informações sobre como obter ajuda do provedor no Windows PowerShell, consulte [Unidades e Provedores](https://go.microsoft.com/fwlink/?LinkId=102137).  
  
### <a name="example-get-a-list-of-providers"></a>Exemplo: Obtenha uma lista de provedores  
 Esse código retorna uma lista de provedores habilitados atualmente em sua sessão do Windows PowerShell:  
  
```  
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>Obter ajuda sobre o provedor do SQL Server  
 **Para obter ajuda sobre o provedor**  
  
1.  Execute Get-Help especificando o nome SQL Server  
  
### <a name="example-get-sql-server-provider-help"></a>Exemplo: Obtenha ajuda de provedor do SQL Server  
 Este exemplo retorna informações básicas sobre o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
```  
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>Listar métodos e propriedades  
 **Para listar os métodos e propriedades para um nó em um caminho de provedor do SQL Server**  
  
1.  O CD para um nó no caminho do SQL Server ou crie uma variável definida para esse local.  
  
2.  Execute o **Get-Member** cmdlet com o parâmetro - Type definido como métodos ou propriedades  
  
### <a name="examples-listing-methods-and-properties"></a>Exemplos: Listando métodos e propriedades  
 Este exemplo lista os métodos com suporte para o nó Bancos de Dados:  
  
```  
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 Esse exemplo lista as propriedades de uma variável que foi definida como um objeto Tabela SMO:  
  
```  
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)   
 [Usar cmdlets do Mecanismo de Banco de Dados](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
