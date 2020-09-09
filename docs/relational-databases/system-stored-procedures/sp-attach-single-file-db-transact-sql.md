---
description: sp_attach_single_file_db (Transact-SQL)
title: sp_attach_single_file_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7774b738dd8ec6fc0619bc8f72fa85c9ab0db349
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541969"
---
# <a name="sp_attach_single_file_db-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Anexa um banco de dados que tem apenas um arquivo de dados para o servidor atual. **sp_attach_single_file_db** não pode ser usado com vários arquivos de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] É recomendável que você use criar *database_name* de banco de dados para anexar em vez disso. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). Não use este procedimento em um banco de dados replicado.  
  
> [!IMPORTANT]  
>  Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'` É o nome do banco de dados a ser anexado ao servidor. O nome deve ser exclusivo. *dbname* é **sysname**, com um padrão de NULL.  
  
`[ @physname = ] 'physical_name'` É o nome físico, incluindo o caminho, do arquivo de banco de dados. *physical_name* é **nvarchar (260)**, com um padrão de NULL.  
  
> [!NOTE]  
>  Este argumento mapeia para o parâmetro FILENAME da instrução CREATE DATABASE. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
 Quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Use **sp_attach_single_file_db** somente em bancos de dados que foram desanexados anteriormente do servidor usando uma operação **sp_detach_db** explícita ou em bancos de dados copiados.  
  
 **sp_attach_single_file_db** funciona apenas em bancos de dados que têm um único arquivo de log. Quando **sp_attach_single_file_db** anexa o banco de dados ao servidor, ele cria um novo arquivo de log. Se o banco de dados for somente leitura, o arquivo de log será criado em seu local anterior.  
  
> [!NOTE]  
>  Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
 Não use este procedimento em um banco de dados replicado.  
  
## <a name="permissions"></a>Permissões  
 Para obter informações sobre como as permissões são tratadas quando um banco de dados é anexado, consulte [create database &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desanexa [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, então, anexa um arquivo de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para o servidor atual.  
  
```  
USE master;  
GO  
EXEC sp_detach_db @dbname = 'AdventureWorks2012';  
EXEC sp_attach_single_file_db @dbname = 'AdventureWorks2012',   
    @physname =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_detach_db ](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpfile ](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
