---
title: "Obter Ajuda do SQL Server PowerShell | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ajuda [PowerShell]"
  - "Ajuda [SQL Server], PowerShell"
  - "PowerShell [SQL Server], ajuda"
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Obter Ajuda do SQL Server PowerShell
  Há várias origens de informações sobre como usar o provedor e os cmdlets do provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell. Isso inclui a ajuda que está disponível no ambiente Windows PowerShell.  
  
## Antes de começar  
 Para saber mais sobre o Windows PowerShell, consulte o [Guia de Introdução do Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=217083).  
  
 Para obter uma visão geral do provedor e os cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
### Ajude no ambiente de Windows PowerShell  
 Use o cmdlet **Get-Help** para obter ajuda no ambiente Windows PowerShell. **Get-Help** fornece ajuda básica para a linguagem Windows PowerShell e os diversos cmdlets e provedores disponíveis no Windows PowerShell.  
  
 Para obter mais informações sobre os modos você pode usar **Get-Help**, veja [Get-Help: Obtendo Ajuda](http://go.microsoft.com/fwlink/?LinkId=102136).  
  
### Ajuda do provedor do SQL Server PowerShell  
 O provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell implementa várias pastas em uma unidade virtual SQLSERVER, como as pastas SQLSERVER:\SQL e SQLSERVER:\DAC. Cada pasta é associada com um dos modelos de objeto de gerenciamento do SQL Server. Enquanto você puder listar os métodos e propriedades associadas com cada nó em um caminho de SQL Server, não poderá obter ajuda por eles no ambiente PowerShell. Para obter uma tabela das pastas com links para a referência de programação associada, consulte [SQL Server PowerShell Provider](../../relational-databases/scripting/sql-server-powershell-provider.md).  
  
### Ajuda do Invoke-Sqlcmd  
 O cmdlet **Invoke-Sqlcmd** usa como entrada qualquer consulta ou arquivo de script que possa ser executado pelo utilitário **sqlcmd**. Você pode usar **Get-Help** para obter informações sobre **Invoke-Sqlcmd** e seus parâmetros, mas não há cobertura de **Get-Help** para consultas **sqlcmd**.  
  
 A entrada *-Query* ou *-QueryFromFile* pode conter:  
  
-   Variáveis e comandos do**sqlcmd** . Para obter informações sobre essas variáveis e comandos, consulte a seção Comentários de [sqlcmd Utility](../../tools/sqlcmd-utility.md).  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para obter mais informações sobre a linguagem [!INCLUDE[tsql](../../includes/tsql-md.md)], veja [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/transact-sql-reference-database-engine.md).  
  
-   Instruções XQuery. Para obter mais informações sobre a linguagem XQuery com suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Referência de linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
## Obtenha Ajuda para um cmdlet de SQL Server  
 **Para obter Ajuda para um cmdlet**  
  
-   Execute Get-Help especificando o nome do cmdlet e o nível de ajuda a ser retornada.  
  
### Exemplo: cmdlet Get-Help  
 Os seguintes exemplos retornam vários níveis de ajuda para **Invoke-Sqlcmd**:  
  
```  
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd –Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd –Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd –Syntax  
```  
  
## Obtenha uma lista de provedores  
 **Para obter uma lista de provedores ativos**  
  
1.  Execute Get-Help especificando a categoria de provedor.  
  
 Para obter mais informações sobre como obter ajuda do provedor no Windows PowerShell, consulte [Unidades e Provedores](http://go.microsoft.com/fwlink/?LinkId=102137).  
  
### Exemplo: obtenha uma lista de provedores  
 Esse código retorna uma lista de provedores habilitados atualmente em sua sessão do Windows PowerShell:  
  
```  
Get-Help -Category provider  
```  
  
## Obter ajuda sobre o provedor do SQL Server  
 **Para obter ajuda sobre o provedor**  
  
1.  Execute Get-Help especificando o nome SQL Server  
  
### Exemplo: Obtenha ajuda do provedor SQL Server  
 Este exemplo retorna informações básicas sobre o provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
Get-Help SQLServer  
```  
  
## Listar métodos e propriedades  
 **Para listar os métodos e propriedades para um nó em um caminho de provedor do SQL Server**  
  
1.  O CD para um nó no caminho do SQL Server ou crie uma variável definida para esse local.  
  
2.  Execute o cmdlet **Get-Member** com o parâmetro –Type definido como Métodos ou Propriedades  
  
### Exemplos: listando métodos e propriedades  
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
  
## Consulte também  
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Usar cmdlets do Mecanismo de Banco de Dados](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
  
  