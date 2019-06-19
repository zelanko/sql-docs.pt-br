---
title: DDL, funções, procedimentos armazenados e exibições de FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85e0c761f5dc784698b3aed361ce50488a93e366
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010096"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>DDL, funções, procedimentos armazenados e exibições de FileTable
  Lista as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e os objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram adicionados ou alterados para oferecer suporte ao recurso FileTable no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A coluna de Status nas tabelas a seguir indica se o item é novo no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ou se estava presente em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mas foi alterado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para dar suporte à pesquisa semântica.  
  
 Para obter a lista de instruções e objetos de banco de dados que oferecem suporte ao FILESTREAM, consulte [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md).  
  
##  <a name="ddl"></a> Instruções DDL (linguagem de definição de dados) Transact-SQL  
  
|Object|Status|Mais Informações|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|Alterado|[Habilitar os pré-requisitos para o FileTable](enable-the-prerequisites-for-filetable.md)<br /><br /> [Gerenciar FileTables](manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|Alterado|[Criar, alterar e remover FileTables](create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|Alterado|[Habilitar os pré-requisitos para FileTable](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|Alterado|[Criar, alterar e remover FileTables](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [Argumentos de RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|Alterado||  
  
##  <a name="func"></a> Funções  
  
|Object|Status|Mais Informações|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**Adicionado**|[Trabalhar com diretórios e caminhos em FileTables](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> Procedimentos armazenados  
  
|Object|Status|Mais Informações|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**Adicionado**|[Gerenciar FileTables](manage-filetables.md)|  
  
##  <a name="cv"></a> Exibições do catálogo  
  
|Object|Status|Mais Informações|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**Adicionado**|[Habilitar os pré-requisitos para FileTable](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**Adicionado**|[Criar, alterar e remover FileTables](create-alter-and-drop-filetables.md)<br /><br /> [Gerenciar FileTables](manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**Adicionado**|[Gerenciar FileTables](manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Alterado|[Gerenciar FileTables](manage-filetables.md)|  
  
##  <a name="dmv"></a> Exibições de gerenciamento dinâmico  
  
|Object|Status|Mais Informações|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**Adicionado**|[Gerenciar FileTables](manage-filetables.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](manage-filetables.md)  
  
  
