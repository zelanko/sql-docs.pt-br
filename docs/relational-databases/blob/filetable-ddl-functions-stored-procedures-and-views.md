---
title: "DDL, fun&#231;&#245;es, procedimentos armazenados e exibi&#231;&#245;es de FileTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FileTables [SQL Server], objetos de banco de dados"
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# DDL, fun&#231;&#245;es, procedimentos armazenados e exibi&#231;&#245;es de FileTable
  Lista as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram adicionados ou alterados para oferecer suporte ao recurso FileTable no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A coluna de Status nas tabelas a seguir indica se o item é novo no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ou se estava presente em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mas foi alterado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para dar suporte à pesquisa semântica.  
  
 Para obter a lista de instruções e objetos de banco de dados que oferecem suporte ao FILESTREAM, consulte [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Instruções DDL (linguagem de definição de dados) Transact-SQL  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)|Alterado|[Habilitar os pré-requisitos para FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Alterado|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|Alterado|[Habilitar os pré-requisitos para FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Alterado|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)<br /><br /> [Argumentos de RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)|Alterado||  
  
##  <a name="func"></a> Funções  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> Procedimentos armazenados  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../Topic/sp_kill_filestream_non_transacted_handles%20\(Transact-SQL\).md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> Exibições do catálogo  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**Adicionado**|[Habilitar os pré-requisitos para FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**Adicionado**|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|Alterado|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> Exibições de gerenciamento dinâmico  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
## Consulte também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  