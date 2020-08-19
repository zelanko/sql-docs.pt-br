---
description: DDL de FileTable, funções, procedimentos armazenados e exibições
title: Funções FileTable, procedimentos armazenados, exibições | Microsoft Docs
descriptions: Learn which Transact-SQL statements and which SQL Server functions, stored procedures, and views have been added or changed to support the FileTable feature.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f1736422ff6ff81a7e48931b390acc710abf41b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448895"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>DDL de FileTable, funções, procedimentos armazenados e exibições

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Lista as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram adicionados ou alterados para oferecer suporte ao recurso FileTable no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A coluna de Status nas tabelas a seguir indica se o item é novo no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ou se estava presente em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mas foi alterado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para dar suporte à pesquisa semântica.  
  
 Para obter a lista de instruções e objetos de banco de dados que oferecem suporte ao FILESTREAM, consulte [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Instruções DDL (linguagem de definição de dados) Transact-SQL  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)|Alterado|[Habilitar os pré-requisitos para o FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Alterado|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|Alterado|[Habilitar os pré-requisitos para o FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Alterado|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|Alterado||  
  
##  <a name="functions"></a><a name="func"></a> Funções  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> Procedimentos armazenados  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> Exibições do catálogo  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**Adicionado**|[Habilitar os pré-requisitos para o FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**Adicionado**|[Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|Alterado|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> Exibições de gerenciamento dinâmico  
  
|Objeto|Status|Mais informações|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**Adicionado**|[Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
