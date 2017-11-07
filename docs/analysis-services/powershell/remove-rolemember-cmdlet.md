---
title: Cmdlet Remove-RoleMember | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c093787d86398acaaeaca8f282e1f588c3e726d7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="remove-rolemember-cmdlet"></a>Cmdlet Remove-RoleMember

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Remova um membro da função especificada de um banco de dados do Analysis Services.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Remove-RoleMember remove um membro existente de uma função de um banco de dados do Analysis Services.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-membername-string"></a>-MemberName \<cadeia de caracteres >  
 Especifica o nome do usuário ou grupo do Windows a ser removido da função.  
  
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
 Especifica a função da qual você está removendo os membros.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<cadeia de caracteres >  
 Especifica o objeto Microsoft.AnalysisServices.Role do qual o membro está sendo removido. Use este parâmetro como uma alternativa para os parâmetros –Database e –RoleName quando você desejar fornecer a função de banco de dados por pipeline.  
  
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
 Nenhum.  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando remova uma conta de usuário de domínio do Windows da função Leitor, para o banco de dados AdventureWorks em execução em uma instância padrão local.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 A linha 1 adiciona todas as funções de banco de dados do banco de dados AWTEST ao pipeline. A linha 2, onde você digita $roles no prompt, mostra a matriz de funções. A linha 3 remove o usuário do Windows "adventure-works\bobh" da primeira função da matriz.  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando remove uma conta de usuário de domínio do Windows da primeira função de uma matriz, onde a matriz é criada por meio da listagem dos filhos da pasta Funções, no contexto de um banco de dados específico (AWTEST).  
  

  
  

