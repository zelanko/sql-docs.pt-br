---
title: IS_ROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 71a3d8f8ce28fcc8918f2058d08f99df2982be5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086710"
---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Indica se um princípio de banco de dados especificado é um membro da função de banco de dados especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *role* **'**  
 É o nome da função de banco de dados que está sendo verificada. *role* é **sysname**.  
  
 **'** *database_principal* **'**  
 É o nome do usuário do banco de dados, da função do banco de dados ou da função do aplicativo a verificar. *database_principal* é **sysname**, com um padrão NULL. Se nenhum valor for especificado, o resultado será baseado no contexto de execução atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|*database_principal* não é um membro de *role*.|  
|1|*database_principal* é um membro de *role*.|  
|NULL|*database_principal* ou *role* não é válido ou você não tem permissão para exibir a associação de função.|  
  
## <a name="remarks"></a>Remarks  
 Use IS_ROLEMEMBER para determinar se o usuário atual pode executar uma ação que requer as permissões da função do banco de dados.  
  
 Se *database_principal* se basear em um logon do Windows, como Contoso\Mary5, IS_ROLEMEMBER retornará NULL, a menos que o *database_principal* tenha tido o acesso direto ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concedido ou negado.  
  
 Se o parâmetro *database_principal* opcional não for fornecido e se o *database_principal* se basear em um logon de domínio do Windows, ele poderá ser membro da função de banco de dados por meio da associação em um grupo do Windows. Para resolver essas associações indiretas, IS_ROLEMEMBER solicita informações de associação do grupo do Windows no controlador de domínio. Se o controlador de domínio não estiver acessível ou não responder, IS_ROLEMEMBER retornará informações de associação de função por conta apenas para o usuário e seus grupos locais. Se o usuário especificado não for o usuário atual, o valor retornado por IS_ROLEMEMBER poderá ser diferente da última atualização de dados do autenticador (como o Active Directory) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o parâmetro *database_principal* opcional for fornecido, a entidade de segurança do banco de dados que está sendo consultada deverá estar presente em sys.database_principals ou IS_ROLEMEMBER retornará NULL. Isso indica que o *database_principal* não é válido neste banco de dados.  
  
 Quando o parâmetro *database_principal* for baseado em um logon de domínio ou baseado em um grupo do Windows e o controlador de domínio não estiver acessível, as chamadas a IS_ROLEMEMBER falharão e poderão retornar dados incorretos ou incompletos.  
  
 Se o controlador de domínio não estiver disponível, a chamada para IS_ROLEMEMBER retornará informações precisas quando o princípio do Windows puder ser autenticado localmente, como uma conta do Windows local ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_ROLEMEMBER** sempre retorna 0 quando um grupo do Windows é usado como o argumento de entidade de segurança do banco de dados, e esse grupo do Windows é membro de outro grupo do Windows que é, por sua vez, membro da função de banco de dados especificada.  
  
 O UAC (Controle de Conta de Usuário) localizado no [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e no Windows Server 2008 também podem retornar resultados diferentes. Isso dependeria do fato de usuário ter acessado o servidor como um membro de grupo do Windows ou como um usuário específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, a função de banco de dados fixa **db_owner** tem a permissão **CONTROL DATABASE**. Se o usuário tiver a permissão **CONTROL DATABASE**, mas não for membro da função, essa função relatará corretamente que o usuário não é membro da função **db_owner**, mesmo que o usuário tenha as mesmas permissões.  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se o usuário atual é membro do grupo do Windows especificado ou da função de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md). Para determinar se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é membro de uma função de servidor, use [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
