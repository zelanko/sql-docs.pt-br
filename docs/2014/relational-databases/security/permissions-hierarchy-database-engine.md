---
title: Hierarquia de permissões (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9a04e5595e509de63b362b31b240e113e635581d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063169"
---
# <a name="permissions-hierarchy-database-engine"></a>Hierarquia de permissões (Mecanismo de Banco de Dados)
  O [!INCLUDE[ssDE](../../../includes/ssde-md.md)] gerencia uma coleção hierárquica de entidades que podem ser protegidas com permissões. Essas entidades são conhecidas como *protegíveis*. Os protegíveis mais proeminentes são servidores e bancos de dados, mas podem ser definidas permissões discretas em um nível muito mais específico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regula as ações de entidades de segurança em protegíveis verificando se as permissões apropriadas foram concedidas.

 A ilustração a seguir mostra todas as relações entre as hierarquias de permissões do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .

 ![Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados](../../database-engine/media/wj-security-layers.gif "Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados")

## <a name="chart-of-sql-server-permissions"></a>Gráfico de permissões do SQL Server
 Para um gráfico de tamanho de pôster de todas [!INCLUDE[ssDE](../../../includes/ssde-md.md)] as permissões no formato PDF, consulte [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf) .

## <a name="working-with-permissions"></a>Trabalhando com permissões
 As permissões podem ser manipuladas com as conhecidas consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] GRANT, DENY e REVOKE. Informações sobre permissões são visíveis nas exibições de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) e [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) . Há também suporte para informações de permissões de consulta usando funções internas.

## <a name="see-also"></a>Consulte Também
 [Protegendo SQL Server](securing-sql-server.md) [permissões &#40;mecanismo de banco de dados&#41;as](permissions-database-engine.md) [Securables](securables.md) [entidades protegíveis &#40;](authentication-access/principals-database-engine.md) mecanismo de banco de dados&#41;[conceder &#40;o TRANSACT-](/sql/t-sql/statements/grant-transact-sql) sql&#41;[revogar &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql) [negar &#40;transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql) HAS_PERMS_BY_NAME &#40;o [transact](/sql/t-sql/functions/has-perms-by-name-transact-sql) -SQL&#41;[Sys. fn_builtin_permissions](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) &#40;Transact-SQL&#41;[Sys. server_permissions &#40;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql)&#41;sys [. database_permissions &#40;Transact-](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) SQL


