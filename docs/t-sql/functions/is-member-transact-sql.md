---
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 472d8f1cc258fdc57ef454fbb35f51e3f83b288d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica se o usuário atual é membro do grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows especificado ou da função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *grupo* **'**  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 É o nome do grupo do Windows que está sendo verificado; deve estar no formato *domínio*\\*grupo*. *grupo* é **sysname**.  
  
 **'** *função* **'**  
 É o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função que está sendo verificada. *função* é **sysname** e podem incluir o banco de dados fixa de funções ou funções definidas pelo usuário, mas não funções de servidor.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 IS_MEMBER retorna os seguintes valores.  
  
|Valor de retorno|Description|  
|------------------|-----------------|  
|0|Usuário atual não é um membro de *grupo* ou *função*.|  
|1|Usuário atual é membro do *grupo* ou *função*.|  
|NULL|O *grupo* ou *função* não é válido. Quando consultado por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon que usa uma função de aplicativo, retorna NULL para um grupo do Windows.|  
  
 IS_MEMBER determina a associação do grupo Windows examinando um token de acesso que é criado pelo Windows. O token de acesso não reflete alterações na associação do grupo feitas após a conexão de um usuário em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A associação ao grupo do Windows não pode ser consultada por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por uma função de aplicativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para adicionar e remover membros de uma função de banco de dados, use [ALTER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). Para adicionar e remover membros de uma função de servidor, use [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, o **db_owner** função fixa de banco de dados tem o **banco de dados de controle** permissão. Se o usuário tiver o **banco de dados de controle** permissão mas não é um membro da função, essa função relatará corretamente que o usuário não é um membro do **db_owner** função, mesmo que o usuário tenha a mesma permissões.  
  
 Membros de **sysadmin** função de servidor fixa insira cada banco de dados como o **dbo** usuário. Verificação de permissões de membro do **sysadmin** a função de servidor fixa, verifica as permissões para **dbo**, não o logon original. Como **dbo** não pode ser adicionado a uma função de banco de dados e não existem em grupos do Windows, **dbo** sempre retornará 0 (ou NULL se a função não existir).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é um membro de uma função de banco de dados, use [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md). Para determinar se um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é um membro de uma função de servidor, use [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir verifica se o usuário atual é um membro de uma função de banco de dados ou de um grupo de domínio do Windows.  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

