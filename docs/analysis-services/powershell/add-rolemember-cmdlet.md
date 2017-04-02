---
title: "Cmdlet Add-RoleMember | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Cmdlet Add-RoleMember
  Adicionar um membro a uma função específica de um banco de dados de tabela ou multidimensional do Analysis Services.  
  
## Sintaxe  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## Description  
 O cmdlet Add-RoleMember adiciona um membro válido a uma função de banco de dados existente. Somente funções de banco de dados são permitidas. Você não pode usar este cmdlet para adicionar membros a uma função de servidor.  
  
 Você pode adicionar somente um membro por vez, que pode ser uma conta de usuário ou de grupo.  
  
## Parâmetros  
  
### -MemberName \<string>  
 Especifica o nome do usuário ou grupo do Windows a ser adicionado à função.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -Database \<string>  
 Especifica o banco de dados ao qual a função pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -RoleName \<string>  
 Especifica a função à qual você está adicionando os membros.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -DatabaseRole \<string>  
 Especifica o objeto Microsoft.AnalysisServices.Role ao qual o membro deve ser adicionado. Use este parâmetro como uma alternativa para os parâmetros –Database e –RoleName quando você desejar fornecer a função de banco de dados por pipeline.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true (ByPropertyName)|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## Exemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando adiciona uma conta de usuário de domínio do Windows à função Leitor, para o banco de dados AdventureWorks em execução em uma instância padrão local.  
  
## Exemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 A linha 1 adiciona todas as funções de banco de dados do banco de dados AWTEST ao pipeline. A linha 2, onde você digita $roles no prompt, mostra a matriz de funções. A linha 3 adiciona o usuário do Windows adventure-works\bobh como membro da primeira função da matriz.  
  
## Exemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando adiciona uma conta de usuário de domínio do Windows à primeira função de uma matriz, onde a matriz é criada por meio da listagem dos filhos da pasta Funções, no contexto de um banco de dados específico (AWTEST).  
  
## Consulte também  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Gerenciar modelos tabulares usando o PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  