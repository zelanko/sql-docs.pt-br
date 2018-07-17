---
title: IS_SRVROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: 65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c6e72a58e17eb584cd0420f04ec10e2b479069fb
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781647"
---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é membro da função de servidor especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *role* **'**  
 É o nome da função de servidor que está sendo verificada. *role* é **sysname**.  
  
 Os valores válidos de *role* são funções de servidor definidas pelo usuário e as seguintes funções de servidor fixas:  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> público|  
|processadmin||  
  
 **'** *login* **'**  
 É o nome do logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a verificar. *login* é **sysname**, com um padrão de NULL. Se nenhum valor for especificado, o resultado será baseado no contexto de Execução atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|*logon* não é um membro de *role*.<br /><br /> No [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], essa instrução sempre retorna 0.|  
|1|*login* é um membro de *role*.|  
|NULL|*role* ou *login* não é válido ou você não tem permissão para exibir a associação de função.|  
  
## <a name="remarks"></a>Remarks  
 Use IS_SRVROLEMEMBER para determinar se o usuário atual pode executar uma ação que exige as permissões da função de servidor.  
  
 Se um logon do Windows, como Contoso\Mary5, estiver especificado para *login* **IS_SRVROLEMEMBER** retornará **NULL**, a não ser que o logon tenha concedido ou negado acesso direto ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o parâmetro *login* opcional não for fornecido e o *login* for um logon do domínio do Windows, ele poderá ser um membro de função de servidor fixa por meio da associação em um grupo do Windows. Para resolver essas associações indiretas, IS_SRVROLEMEMBER solicita informações de associação do grupo do Windows no controlador de domínio. Se o controlador de domínio não estiver acessível ou não responder, **IS_SRVROLEMEMBER** retornará informações de associação de função por conta apenas para o usuário e seus grupos locais. Se o usuário especificado não for o usuário atual, o valor retornado por IS_SRVROLEMEMBER poderá ser diferente da última atualização de dados do autenticador (como o Active Directory) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o parâmetro de logon opcional for fornecido, o logon de Windows que está sendo consultado deverá estar presente em sys.server_principals ou IS_SRVROLEMEMBER retornará NULL. Isso indica que o logon não é válido.  
  
 Quando o parâmetro de logon é um logon de domínio ou baseado em um grupo do Windows e o controlador de domínio está inacessível, as chamadas para IS_SRVROLEMEMBER falham e podem retornar dados incorretos ou incompletos.  
  
 Se o controlador de domínio não estiver disponível, a chamada para IS_SRVROLEMEMBER retornará informações precisas quando o princípio do Windows puder ser autenticado localmente, como uma conta do Windows local ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_SRVROLEMEMBER** sempre retorna 0 quando um grupo do Windows é usado como o argumento de logon do banco de dados, e esse grupo do Windows é um membro de outro grupo do Windows que é, por sua vez, um membro da função de servidor especificada.  
  
 A configuração UAC (Controle de Conta de Usuário) também pode levar ao retorno de resultados diferentes. Isso dependeria do fato de usuário ter acessado o servidor como um membro de grupo do Windows ou como um usuário específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, a função de servidor fixa **sysadmin** tem a permissão **CONTROL SERVER**. Se o usuário tiver a permissão **CONTROL SERVER**, mas não for membro da função, essa função relatará corretamente que o usuário não é membro da função **sysadmin**, mesmo que o usuário tenha as mesmas permissões.  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se o usuário atual é membro do grupo do Windows especificado ou da função de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md). Para determinar se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um membro de uma função de banco de dados, use [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
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
  
 O exemplo a seguir indica se o logon de domínio Pat é membro da função de servidor fixa **diskadmin**.  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
