---
title: IS_ROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb52e3460ed6c39d619453e370df310d530dd6a6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Indica se um princípio de banco de dados especificado é um membro da função de banco de dados especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *função* **'**  
 É o nome da função de banco de dados que está sendo verificada. *função* é **sysname**.  
  
 **'** *database_principal* **'**  
 É o nome do usuário do banco de dados, da função do banco de dados ou da função do aplicativo a verificar. *database_principal* é **sysname**, com um padrão NULL. Se nenhum valor for especificado, o resultado será baseado no contexto de execução atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
|Valor de retorno|Description|  
|------------------|-----------------|  
|0|*database_principal* não é um membro de *função*.|  
|1|*database_principal* é um membro de *função*.|  
|NULL|*database_principal* ou *função* não é válido, ou você não tem permissão para exibir a associação de função.|  
  
## <a name="remarks"></a>Comentários  
 Use IS_ROLEMEMBER para determinar se o usuário atual pode executar uma ação que requer as permissões da função do banco de dados.  
  
 Se *database_principal* se baseia em um logon do Windows, como Contoso\Mary5, IS_ROLEMEMBER retornará NULL, a menos que o *database_principal* foi concedido ou negado acesso direto ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o valor opcional *database_principal* parâmetro não for fornecido e se o *database_principal* baseia-se em um logon de domínio do Windows, ele poderá ser um membro de uma função de banco de dados por meio da associação em um grupo do Windows . Para resolver essas associações indiretas, IS_ROLEMEMBER solicita informações de associação do grupo do Windows no controlador de domínio. Se o controlador de domínio não estiver acessível ou não responder, IS_ROLEMEMBER retornará informações de associação de função por conta apenas para o usuário e seus grupos locais. Se o usuário especificado não for o usuário atual, o valor retornado por IS_ROLEMEMBER poderá ser diferente da última atualização de dados do autenticador (como o Active Directory) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o valor opcional *database_principal* parâmetro for fornecido, o banco de dados principal que está sendo consultado deve estar presente em sys. database_principals ou IS_ROLEMEMBER retornará NULL. Isso indica que o *database_principal* não é válido neste banco de dados.  
  
 Quando o *database_principal* parâmetro é baseado em um logon de domínio ou com base em um grupo do Windows e o controlador de domínio está inacessível, chamadas para IS_ROLEMEMBER falharão e poderão retornar dados incorretos ou incompletos.  
  
 Se o controlador de domínio não estiver disponível, a chamada para IS_ROLEMEMBER retornará informações precisas quando o princípio do Windows puder ser autenticado localmente, como uma conta do Windows local ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_ROLEMEMBER** sempre retorna 0 quando um grupo do Windows é usado como o argumento de banco de dados principal, e esse grupo do Windows é um membro de outro grupo do Windows que, por sua vez, é um membro da função de banco de dados especificado.  
  
 O controle de conta de usuário (UAC) encontrada no [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e Windows Server 2008 também podem retornar resultados diferentes. Isso dependeria do fato de usuário ter acessado o servidor como um membro de grupo do Windows ou como um usuário específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, o **db_owner** função fixa de banco de dados tem o **banco de dados de controle** permissão. Se o usuário tiver o **banco de dados de controle** permissão mas não é um membro da função, essa função relatará corretamente que o usuário não é um membro do **db_owner** função, mesmo que o usuário tenha a mesma permissões.  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se o usuário atual é um membro do grupo do Windows especificado ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de banco de dados, use [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Para determinar se um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é um membro de uma função de servidor, use [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DEFINITION na função de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir indica se o usuário atual é membro da função de banco de dados fixa `db_datareader`.  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar função &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [Remover função &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [Criar função de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [Remover função de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

