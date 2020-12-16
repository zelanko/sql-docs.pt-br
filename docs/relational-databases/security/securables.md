---
title: Protegíveis | Microsoft Docs
description: Saiba mais sobre os escopos protegíveis, que o sistema de autorização do Mecanismo de Banco de Dados do SQL Server usa para regular o acesso aos protegíveis.
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d780aa878779bf25a3854dbd0c7c392800f7039
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432197"
---
# <a name="securables"></a>Protegíveis
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Protegíveis são os recursos cujo acesso é regulado pelo sistema de autorização do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por exemplo, uma tabela é um protegível. Alguns protegíveis podem ser contidos dentro de outros, criando hierarquias aninhadas chamadas "escopos" que podem ser protegidos. Os escopos protegíveis são **servidor**, **banco de dados** e **esquema**.  
  
## <a name="securable-scope-server"></a>Escopo protegível: Servidor  
 O escopo protegível **servidor** contém os seguintes protegíveis:  
  
-   grupo de disponibilidade  
  
-   Ponto de extremidade  
  
-   Logon  
  
-   Função de servidor  
  
-   Banco de dados  
  
## <a name="securable-scope-database"></a>Escopo protegível: Banco de dados  
 O escopo protegível **banco de dados** contém os seguintes protegíveis:  
  
-   Função de aplicativo  
  
-   Assembly  
  
-   Chave assimétrica  
  
-   Certificado  
  
-   Contrato  
  
-   Catálogo de texto completo  
  
-   Lista de palavras irrelevantes completa  
  
-   Tipo de mensagem  
  
-   Associação de serviço remoto  
  
-   Função (banco de dados)  
  
-   Rota  
  
-   Esquema  
  
-   Lista de propriedades de pesquisa  
  
-   Serviço  
  
-   Chave simétrica  
  
-   Usuário  
  
## <a name="securable-scope-schema"></a>Escopo protegível: Esquema  
 O escopo protegível **esquema** contém os seguintes protegíveis:  
  
-   Type  
  
-   Coleção de esquemas XML  
  
-   Objeto – a classe de objeto tem os seguintes membros:  
  
    -   Agregado  
  
    -   Função  
  
    -   Procedimento  
  
    -   Fila  
  
    -   Sinônimo  
  
    -   Tabela  
  
    -   Visualizar 
    
    -   Tabela externa 
  
## <a name="controlling-access-to-a-securable"></a>Controlando o acesso a um protegível  
 A entidade que recebe permissão para um protegível é chamada de entidade de segurança. As entidades de segurança mais comuns são logons e usuários de banco de dados. O acesso a protegíveis é controlado pela concessão ou negação de permissões, ou pela adição de logons e usuários a funções que têm acesso. Para obter informações sobre como controlar permissões, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md), [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md), [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md), [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) e [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
> [!CAUTION]  
>  As permissões padrão concedidas aos objetos de sistema no momento da instalação são avaliadas cuidadosamente contra possíveis ameaças e não precisam ser alteradas como parte do sistema de proteção de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Qualquer alteração nas permissões nos objetos de sistema poderia limitar ou interromper a funcionalidade e potencialmente pode deixar a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um estado sem suporte.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)  
  
  
