---
title: Cmdlet Add-RoleMember | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d10c7c9db41ec9e6f6f6e779b12e62f62e3b3b36
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="add-rolemember-cmdlet"></a>Cmdlet Add-RoleMember

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Adicionar um membro a uma função específica de um banco de dados de tabela ou multidimensional do Analysis Services.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Add-RoleMember adiciona um membro válido a uma função de banco de dados existente. Somente funções de banco de dados são permitidas. Você não pode usar este cmdlet para adicionar membros a uma função de servidor.  
  
 Você pode adicionar somente um membro por vez, que pode ser uma conta de usuário ou de grupo.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-membername-string"></a>-MemberName \<cadeia de caracteres >  
 Especifica o nome do usuário ou grupo do Windows a ser adicionado à função.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-string"></a>-Banco de dados \<cadeia de caracteres >  
 Especifica o banco de dados ao qual a função pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-rolename-string"></a>-RoleName \<cadeia de caracteres >  
 Especifica a função à qual você está adicionando os membros.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<cadeia de caracteres >  
 Especifica o objeto Microsoft.AnalysisServices.Role ao qual o membro deve ser adicionado. Use este parâmetro como uma alternativa para os parâmetros –Database e –RoleName quando você desejar fornecer a função de banco de dados por pipeline.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true (ByPropertyName)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando adiciona uma conta de usuário de domínio do Windows à função Leitor, para o banco de dados AdventureWorks em execução em uma instância padrão local.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 A linha 1 adiciona todas as funções de banco de dados do banco de dados AWTEST ao pipeline. A linha 2, onde você digita $roles no prompt, mostra a matriz de funções. A linha 3 adiciona o usuário do Windows adventure-works\bobh como membro da primeira função da matriz.  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando adiciona uma conta de usuário de domínio do Windows à primeira função de uma matriz, onde a matriz é criada por meio da listagem dos filhos da pasta Funções, no contexto de um banco de dados específico (AWTEST).  
  

  
  
