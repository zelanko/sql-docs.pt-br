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
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487128"
---
# <a name="permissions-hierarchy-database-engine"></a>Hierarquia de permissões (Mecanismo de Banco de Dados)
  O [!INCLUDE[ssDE](../../../includes/ssde-md.md)] gerencia uma coleção hierárquica de entidades que podem ser protegidas com permissões. Essas entidades são conhecidas como *protegíveis*. Os protegíveis mais proeminentes são servidores e bancos de dados, mas podem ser definidas permissões discretas em um nível muito mais específico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regula as ações de entidades de segurança em protegíveis verificando se as permissões apropriadas foram concedidas.

 A ilustração a seguir mostra todas as relações entre as hierarquias de permissões do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .

 ![Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados](../../database-engine/media/wj-security-layers.gif "Diagrama de hierarquias de permissões do Mecanismo de Banco de Dados")

## <a name="chart-of-sql-server-permissions"></a>Gráfico de permissões do SQL Server
 Para obter um gráfico [!INCLUDE[ssDE](../../../includes/ssde-md.md)] de tamanho de [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf)pôster de todas as permissões em formato pdf, consulte .

## <a name="working-with-permissions"></a>Trabalhando com permissões
 As permissões podem ser manipuladas com as conhecidas consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] GRANT, DENY e REVOKE. Informações sobre permissões são visíveis nas exibições de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) e [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) . Há também suporte para informações de permissões de consulta usando funções internas.

## <a name="see-also"></a>Consulte Também
 A garantia de [permissões de](permissions-database-engine.md) [servidor SQL](securing-sql-server.md) &#40;mecanismo de banco de dados&#41;[securables](securables.md) [principals &#40;mecanismo de banco de dados&#41;](authentication-access/principals-database-engine.md) GRANT &#40;[Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) REVOGAR &#40;[Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql) NEGAR &#40;[Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql) HAS_PERMS_BY_NAME &#40;[Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql) [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) [sys.server_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) [sys.&#41;database_permissions &#40;&#40;](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)


