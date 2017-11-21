---
title: "Permissões de grupo de disponibilidade GRANT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 154c99ddfb9f3a69a4a9eeae35f20c5e9720100d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-availability-group-permissions-transact-sql"></a>Permissões de grupo de disponibilidade GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Concede permissões em um grupo de disponibilidade AlwaysOn.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser concedida em um grupo de disponibilidade. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 NO grupo de disponibilidade **::***availability_group_name*  
 Especifica o grupo de disponibilidade no qual a permissão está sendo concedida. O qualificador de escopo (**::**) é necessária.  
  
 PARA \<server_principal >  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual a permissão está sendo concedida.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do qual o principal que executa esta consulta deriva seu direito de conceder a permissão.  
  
## <a name="remarks"></a>Comentários  
 Permissões no escopo do servidor podem ser concedidas somente quando o banco de dados atual é **mestre**.  
  
 Informações sobre grupos de disponibilidade estão visíveis no [availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) exibição do catálogo. Informações sobre permissões de servidor são visíveis no [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição de catálogo e obter informações sobre as entidades de servidor é visível no [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição do catálogo.  
  
 Um grupo de disponibilidade é um nível de servidor protegível. As permissões mais específicas e limitadas que podem ser concedidas em um grupo de disponibilidade são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de grupo de disponibilidade|Implícito na permissão de grupo de disponibilidade|Implícito na permissão de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 Para um gráfico de todos os [!INCLUDE[ssDE](../../includes/ssde-md.md)] permissões, consulte [pôster de permissão do mecanismo de banco de dados](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no grupo de disponibilidade ou a permissão ALTER ANY AVAILABILITY GROUP no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. Concedendo a permissão VIEW DEFINITION em um grupo de disponibilidade  
 O exemplo a seguir concede a permissão `VIEW DEFINITION` no grupo de disponibilidade `MyAg` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon `ZArifin`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. Concedendo a permissão TAKE OWNERSHIP com GRANT OPTION  
 O exemplo a seguir concede a permissão `TAKE OWNERSHIP` no grupo de disponibilidade `MyAg` para o usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `PKomosinski` com `GRANT OPTION`.  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. Concedendo a permissão CONTROL em um grupo de disponibilidade  
 O exemplo a seguir concede a permissão `CONTROL` no grupo de disponibilidade `MyAg` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuário `PKomosinski`. CONTROL permite o controle completo de logon do grupo de disponibilidade, embora eles não sejam o proprietário do grupo de disponibilidade. Para alterar a propriedade, consulte [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Permissões de grupo de disponibilidade REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [Negar permissões de grupo de disponibilidade &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys. availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Exibições de catálogo &#40; grupos de disponibilidade AlwaysOn Transact-SQL &#41; ](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [Permissões &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

