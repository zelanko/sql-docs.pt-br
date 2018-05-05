---
title: Cmdlet Add-RoleMember | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a7da23c4c3597398be38cd4efd34f6ba21925405
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-rolemember-cmdlet"></a>Cmdlet Add-RoleMember
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

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
|Entradas|Nenhuma.|  
|Saídas|Nenhuma|  
  
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
  

  
  
