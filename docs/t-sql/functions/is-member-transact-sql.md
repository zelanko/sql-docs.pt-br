---
description: IS_MEMBER (Transact-SQL)
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47b04ac5bbaf5463ffaba4a5d2f29ce940ec64a0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97422132"
---
# <a name="is_member-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Indica se o usuário atual é membro do grupo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows especificado ou da função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não há suporte para a função IS_MEMBER em grupos do Azure Active Directory.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 **'** *group* **'**  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 É o nome do grupo do Windows que está sendo verificado; deve estar no formato *Domain*\\*Group*. *group* é **sysname**.  
  
 **'** *role* **'**  
 É o nome da função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de servidor que está sendo verificada. *role* é **sysname** e pode incluir funções fixas ou funções definidas pelo usuário do banco de dados, mas não funções de servidor.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 IS_MEMBER retorna os seguintes valores.  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|O usuário atual não é membro do *group* ou *role*.|  
|1|O usuário atual é membro do *group* ou *role*.|  
|NULO|O *group* ou a *role* não é válido. Quando consultado por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon que usa uma função de aplicativo, retorna NULL para um grupo do Windows.|  
  
 IS_MEMBER determina a associação do grupo Windows examinando um token de acesso que é criado pelo Windows. O token de acesso não reflete alterações na associação do grupo feitas após a conexão de um usuário em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A associação ao grupo do Windows não pode ser consultada por um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por uma função de aplicativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para adicionar e remover membros de uma função de banco de dados, use [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md). Para adicionar e remover membros de uma função de servidor, use [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Essa função avalia a associação de função, não a permissão subjacente. Por exemplo, a função de banco de dados fixa **db_owner** tem a permissão **CONTROL DATABASE**. Se o usuário tiver a permissão **CONTROL DATABASE**, mas não for membro da função, essa função relatará corretamente que o usuário não é membro da função **db_owner**, mesmo que o usuário tenha as mesmas permissões.  
  
 Membros da função fixa de servidor **sysadmin** entram em cada banco de dados como o usuário **dbo**. Verificar permissões de membro da função fixa de servidor **sysadmin** verifica as permissões para **dbo**, não o logon original. Como **dbo** não pode ser adicionado a uma função de banco de dados e não existem em grupos do Windows, **dbo** sempre retornará 0 (ou NULL, se a função não existir).  
  
## <a name="related-functions"></a>Funções relacionadas  
 Para determinar se outro logon em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um membro de uma função de banco de dados, use [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md). Para determinar se um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é membro de uma função de servidor, use [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir verifica se o usuário atual é um membro de uma função de banco de dados ou de um grupo de domínio do Windows.  
  
```sql  
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
  
  
