---
title: IS_SRVROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs: TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: "65"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 342eadd8e537611cc292c95ebfa41b98c222c920
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é membro da função de servidor especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *função* **'**  
 É o nome da função de servidor que está sendo verificada. *função* é **sysname**.  
  
 Os valores válidos para *função* são funções de servidor definidas pelo usuário e funções de servidor fixas do seguinte:  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> público|  
|processadmin||  
  
 **'** *login* **'**  
 É o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon para verificar. *logon* é **sysname**, com um padrão NULL. Se nenhum valor for especificado, o resultado é baseado no contexto de execução atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
|Valor de retorno|Description|  
|------------------|-----------------|  
|0|*logon* não é um membro de *função*.<br /><br /> Em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa instrução sempre retorna 0.|  
|1|*logon* é um membro de *função*.|  
|NULL|*função* ou *login* não é válido, ou você não tem permissão para exibir a associação de função.|  
  
## <a name="remarks"></a>Comentários  
 UseIS_SRVROLEMEMBER para determinar se o usuário atual pode executar uma ação que requer permissões da função de servidor.  
  
 Se um logon do Windows, como Contoso\Mary5, é especificado para *login*, **IS_SRVROLEMEMBER** retorna **nulo**, a menos que o logon foi concedido ou negado acesso direto ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o valor opcional *login* parâmetro não for fornecido e se *logon* é um logon de domínio do Windows, pode ser um membro de uma função de servidor fixa através da participação em um grupo do Windows. Para resolver essas associações indiretas, IS_SRVROLEMEMBER solicita informações de associação do grupo do Windows no controlador de domínio. Se o controlador de domínio está inacessível ou não responder, **IS_SRVROLEMEMBER** retorna informações de associação de função por conta para o usuário e seus grupos locais apenas. Se o usuário especificado não for o usuário atual, o valor retornado por IS_SRVROLEMEMBER poderá ser diferente da última atualização de dados do autenticador (como o Active Directory) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o parâmetro de logon opcional for fornecido, o logon de Windows que está sendo consultado deverá estar presente em sys.server_principals ou IS_SRVROLEMEMBER retornará NULL. Isso indica que o logon não é válido.  
  
 Quando o parâmetro de logon é um logon de domínio ou baseado em um grupo do Windows e o controlador de domínio está inacessível, chamadas para IS_SRVROLEMEMBER falharão e poderão retornar dados incorretos ou incompletos.  
  
 Se o controlador de domínio não estiver disponível, a chamada para IS_SRVROLEMEMBER retornará informações precisas quando o princípio do Windows puder ser autenticado localmente, como uma conta do Windows local ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_SRVROLEMEMBER** sempre retorna 0 quando um grupo do Windows é usado como o argumento de logon, e esse grupo do Windows é um membro de outro grupo do Windows que, por sua vez, é um membro da função de servidor especificado.  
  
 A configuração de controle de conta de usuário (UAC) também pode causar os retornar resultados diferentes. Isso dependeria do fato de usuário ter acessado o servidor como um membro de grupo do Windows ou como um usuário específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, o **sysadmin** a função de servidor fixa tem o **CONTROL SERVER** permissão. Se o usuário tiver o **CONTROL SERVER** permissão mas não é um membro da função, essa função relatará corretamente que o usuário não é um membro do **sysadmin** função, mesmo que o usuário tenha a mesma permissões.  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se o usuário atual é um membro do grupo do Windows especificado ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de banco de dados, use [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Para determinar se um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é um membro de uma função de banco de dados, use [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DEFINITION na função de servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir indica se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do usuário atual é membro da função de servidor fixa `sysadmin`.  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 O exemplo a seguir indica se o logon de domínio Pat é membro do **diskadmin** função de servidor fixa.  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>Consulte também  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
