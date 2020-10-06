---
description: sp_attach_db (Transact-SQL)
title: sp_attach_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_db_TSQL
- sp_attach_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_db
ms.assetid: 59bc993e-7913-4091-89cb-d2871cffda95
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 79c3d518798c53342e67bfa42ce430d9ffe8e07a
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753448"
---
# <a name="sp_attach_db-transact-sql"></a>sp_attach_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Anexa um banco de dados a um servidor.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] É recomendável que você use criar *database_name* de banco de dados para anexar em vez disso. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md).  
  
> [!NOTE]  
>  Para recompilar vários arquivos de log quando um ou mais têm um novo local, use CREATE DATABASE *database_name* for ATTACH_REBUILD_LOG.  
  
> [!IMPORTANT]  
>  Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_attach_db [ @dbname= ] 'dbname'  
    , [ @filename1= ] 'filename_n' [ ,...16 ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbnam_ '` É o nome do banco de dados a ser anexado ao servidor. O nome deve ser exclusivo. *dbname* é **sysname**, com um padrão de NULL.  
  
`[ @filename1 = ] 'filename_n'` É o nome físico, incluindo o caminho, de um arquivo de banco de dados. *filename_n* é **nvarchar (260)**, com um padrão de NULL. Podem ser especificados até 16 nomes de arquivo. Os nomes de parâmetro começam em ** \@ arquivo1** e incrementam para ** \@ filename16**. A lista de nomes de arquivo deve incluir, pelo menos, o arquivo primário. O arquivo primário contém as tabelas de sistema que apontam para outros arquivos no banco de dados. A lista também deve incluir quaisquer arquivos que tenham sido movidos depois que o banco de dados foi desanexado.  
  
> [!NOTE]  
>  Este argumento mapeia para o parâmetro FILENAME da instrução CREATE DATABASE. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md).  
>   
>  Quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O procedimento armazenado **sp_attach_db** só deve ser executado em bancos de dados que foram desanexados anteriormente do servidor de banco de dados usando uma operação **sp_detach_db** explícita ou em bancos de dados copiados. Se você precisar especificar mais de 16 arquivos, use criar *database_name* de banco de dados para anexar ou criar banco de dados *database_name* FOR_ATTACH_REBUILD_LOG. Para obter mais informações, consulte [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md).  
  
 Considera-se que todo arquivo não especificado esteja em seu último local conhecido. Para usar um arquivo em um local diferente, você deve especificar o novo local.  
  
 Um banco de dados criado por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser anexado em versões anteriores.  
  
> [!NOTE]  
>  Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
 Ao anexar um banco de dados replicado que tenha sido copiado, em vez de desanexado, considere o seguinte:  
  
-   Se você anexar o banco de dados à mesma instância e versão de servidor como banco de dados original, nenhuma etapa adicional será necessária.  
  
-   Se anexar o banco de dados à mesma instância de servidor, mas com uma versão atualizada, você deverá executar [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) para atualizar a replicação depois que a operação de anexação tiver sido concluída.  
  
-   Se você anexar o banco de dados a uma instância de servidor diferente, independentemente da versão, deverá executar [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para remover a replicação depois que a operação de anexação tiver sido concluída.  
  
 Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave.  
  
## <a name="permissions"></a>Permissões  
 Para obter informações sobre como as permissões são tratadas quando um banco de dados é anexado, consulte [create database &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir anexa arquivos de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ao servidor atual.  
  
```  
EXEC sp_attach_db @dbname = N'AdventureWorks2012',   
    @filename1 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf',   
    @filename2 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_detach_db ](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpfile ](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_removedbreplication ](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
