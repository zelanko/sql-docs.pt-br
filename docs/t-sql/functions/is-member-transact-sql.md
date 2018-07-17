---
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5460e080b23470fd13f9c1e83f20b7ed58f01ac5
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785127"
---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica se o usuário atual é membro do grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows especificado ou da função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *group* **'**  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 É o nome do grupo do Windows que está sendo verificado; deve estar no formato *Domain*\\*Group*. *group* é **sysname**.  
  
 **'** *role* **'**  
 É o nome da função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de servidor que está sendo verificada. *role* é **sysname** e pode incluir funções fixas ou funções definidas pelo usuário do banco de dados, mas não funções de servidor.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_MEMBER retorna os seguintes valores.  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|O usuário atual não é membro do *group* ou *role*.|  
|1|O usuário atual é membro do *group* ou *role*.|  
|NULL|O *group* ou a *role* não é válido. Quando consultado por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon que usa uma função de aplicativo, retorna NULL para um grupo do Windows.|  
  
 IS_MEMBER determina a associação do grupo Windows examinando um token de acesso que é criado pelo Windows. O token de acesso não reflete alterações na associação do grupo feitas após a conexão de um usuário em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A associação ao grupo do Windows não pode ser consultada por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por uma função de aplicativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para adicionar e remover membros de uma função de banco de dados, use [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md). Para adicionar e remover membros de uma função de servidor, use [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, a função de banco de dados fixa **db_owner** tem a permissão **CONTROL DATABASE**. Se o usuário tiver a permissão **CONTROL DATABASE**, mas não for membro da função, essa função relatará corretamente que o usuário não é membro da função **db_owner**, mesmo que o usuário tenha as mesmas permissões.  
  
 Membros da função fixa de servidor **sysadmin** entram em cada banco de dados como o usuário **dbo**. Verificar permissões de membro da função fixa de servidor **sysadmin** verifica as permissões para **dbo**, não o logon original. Como **dbo** não pode ser adicionado a uma função de banco de dados e não existem em grupos do Windows, **dbo** sempre retornará 0 (ou NULL, se a função não existir).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se outro logon em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um membro de uma função de banco de dados, use [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md). Para determinar se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é membro de uma função de servidor, use [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
