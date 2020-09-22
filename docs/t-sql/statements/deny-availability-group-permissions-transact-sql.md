---
title: Permissões de grupo de disponibilidade DENY
description: Negue permissões em um Grupo de Disponibilidade Always On.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- permissions [SQL Server], availability group
- DENY statement, availability groups
- denying permissions, [SQL Server], availability groups
ms.assetid: bda60b36-a0b9-4c20-80c1-6a5cb1d638a5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c5f94122daad6d7dba18e391e6f5c8998bb01acd
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688892"
---
# <a name="deny-availability-group-permissions-transact-sql"></a>Permissões de grupo de disponibilidade DENY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Nega permissões em um Grupo de Disponibilidade AlwaysOn no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DENY permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *permission*  
 Especifica uma permissão que pode ser negada em um grupo de disponibilidade. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ON AVAILABILITY GROUP **::** _availability_group_name_  
 Especifica o grupo de disponibilidade no qual a permissão está sendo negada. O qualificador de escopo ( **::** ) é obrigatório.  
  
 TO \<server_principal>  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual a permissão está sendo negada.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do qual o principal que executa esta consulta deriva seu direito de negar a permissão.  
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo de servidor podem ser negadas somente quando o banco de dados atual é **mestre**.  
  
 Informações sobre grupos de disponibilidade são visíveis na exibição do catálogo [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md). As informações sobre permissões de servidor estão visíveis na exibição do catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) e as informações sobre entidades de segurança do servidor estão visíveis na exibição do catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Um grupo de disponibilidade é um nível de servidor protegível. As permissões mais específicas e limitadas que podem ser negadas em um grupo de disponibilidade são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de grupo de disponibilidade|Implícito na permissão de grupo de disponibilidade|Implícito na permissão de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONECTAR|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no grupo de disponibilidade ou a permissão ALTER ANY AVAILABILITY GROUP no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-denying-view-definition-permission-on-an-availability-group"></a>a. Negando a permissão VIEW DEFINITION em um grupo de disponibilidade  
 O exemplo a seguir nega a permissão `VIEW DEFINITION` no grupo de disponibilidade `MyAg` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon `ZArifin`.  
  
```sql  
USE master;  
DENY VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-the-cascade-option"></a>B. Negando a permissão TAKE OWNERSHIP com CASCADE OPTION  
 O exemplo a seguir nega a permissão `TAKE OWNERSHIP` no grupo de disponibilidade `MyAg` para o usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`PKomosinski` com a opção `CASCADE`.  
  
```sql  
USE master;  
DENY TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões REVOKE do grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [Permissões GRANT de grupo de disponibilidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Exibições de catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
