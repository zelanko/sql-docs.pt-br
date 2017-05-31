---
title: Migrar para um banco de dados parcialmente independente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7d2228b3a1baf08376e1cb5ec862bf89f8a4e2d8
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="migrate-to-a-partially-contained-database"></a>Migrar para um banco de dados independente parcialmente
  Este tópico discute como preparar para alterar para o modelo de banco de dados independente parcialmente e, em seguida, fornece as etapas de migração.  
  
 **Neste tópico:**  
  
-   [Preparando para migrar um banco de dados](#prepare)  
  
-   [Habilitar bancos de dados independentes](#enable)  
  
-   [Convertendo um banco de dados para parcialmente independente](#convert)  
  
-   [Migrando usuários para usuários de bancos de dados independentes](#users)  
  
##  <a name="prepare"></a> Preparando para migrar um banco de dados  
 Analise os itens a seguir se desejar migrar um banco de dados para o modelo de banco de dados independente parcialmente.  
  
-   Você deve entender o modelo de banco de dados independente parcialmente. Para obter mais informações, veja [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md).  
  
-   Você deve entender os riscos que são exclusivos para bancos de dados independentes parcialmente. Para saber mais, veja [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
-   Bancos de dados independentes não oferecem suporte à replicação, Change Data Capture ou controle de alterações. Confirme que o banco de dados não usa estes recursos.  
  
-   Analise a lista de recursos de banco de dados que são modificados para bancos de dados independentes parcialmente. Para obter mais informações, veja [Recursos modificados &#40;Banco de dados independente&#41;](../../relational-databases/databases/modified-features-contained-database.md).  
  
-   Consulte [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) para localizar recursos ou objetos independentes no banco de dados. Para obter mais informações, consulte:  
  
-   Monitore o XEvent **database_uncontained_usage** para ver quando são usados recursos dependentes.  
  
##  <a name="enable"></a> Habilitar bancos de dados independentes  
 Os bancos de dados independentes devem ser habilitados na instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], antes de os bancos de dados independentes poderem ser criados.  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Habilitando bancos de dados independentes usando Transact-SQL  
 O exemplo a seguir habilita bancos de dados independentes na instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>Habilitando bancos de dados independentes usando o Management Studio  
 O exemplo a seguir habilita bancos de dados independentes na instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.  
  
2.  Na página **Avançado** , na seção **Retenção** , defina a opção **Habilitar Bancos de Dados Independentes** como **True**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> Convertendo um banco de dados para parcialmente independente  
 Um banco de dados é convertido para um banco de dados independente alterando a opção **CONTAINMENT** .  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Convertendo um banco de dados para independente parcialmente usando Transact-SQL  
 O exemplo a seguir converte um banco de dados chamado `Accounting` para um banco de dados independente parcialmente.  
  
```tsql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Convertendo um banco de dados para independente parcialmente usando Management Studio  
 O exemplo a seguir converte um banco de dados para um banco de dados independente parcialmente.  
  
1.  No Pesquisador de Objetos, expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados que será convertido e clique em **Propriedades**.  
  
2.  Na página **Opções** , altere a opção **Tipo de retenção** para **Parcial**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="users"></a> Migrando usuários para usuários de bancos de dados independentes  
 O exemplo a seguir migra todos os usuários baseados em logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usuários de bancos de dados independentes com senhas. O exemplo exclui os logons que não estão habilitados. O exemplo deve ser executado no banco de dados independente.  
  
```tsql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)  
  
  
