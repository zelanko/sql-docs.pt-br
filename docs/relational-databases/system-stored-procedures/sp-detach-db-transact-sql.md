---
title: sp_detach_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
author: stevestein
ms.author: sstein
ms.openlocfilehash: eec8b91bbb7d90483b627aebddb7088bc80cb1ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912890"
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desanexa um banco de dados que não está em uso atualmente em uma instância de servidor e, opcionalmente, executa UPDATE STATISTICS em todas as tabelas antes de desanexar.  
  
> [!IMPORTANT]  
>  Para que um banco de dados replicado seja desanexado, é preciso que ele seja não publicado. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'database_name'` É o nome do banco de dados a ser desanexado. *Database_Name* é um **sysname** valor, com um valor padrão de NULL.  
  
`[ @skipchecks = ] 'skipchecks'` Especifica se deve ignorar ou executar UPDATE STATISTIC. *skipchecks* é um **nvarchar (10)** valor, com um valor padrão de NULL. Para ignorar UPDATE STATISTICS, especifique **verdadeira**. Para executar explicitamente UPDATE STATISTICS, especifique **falsos**.  
  
 Por padrão, UPDATE STATISTICS é executado para atualizar as informações sobre os dados nas tabelas e os índices. A execução de UPDATE STATISTICS é útil para bancos de dados que serão movidos para mídias somente leitura.  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` Especifica se o arquivo de índice de texto completo associado com o banco de dados que está sendo desanexado não será descartado do banco de dados durante a operação de desanexação. *KeepFulltextIndexFile* é um **nvarchar (10)** valor com um padrão de **true**. Se *KeepFulltextIndexFile* é **falso**, todos os arquivos de índice de texto completo associado com o banco de dados e os metadados do índice de texto completo são descartados, a menos que o banco de dados é somente leitura. Se for NULL ou **verdadeira**, texto completo relacionadas a metadados são mantidos.  
  
> [!IMPORTANT]
>  O **@keepfulltextindexfile** parâmetro será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use esse parâmetro em desenvolvimentos novos e modifique, assim que possível, os aplicativos que atualmente o usam.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Quando um banco de dados é desanexado, todos os metadados são descartados. Se o banco de dados era o banco de dados padrão de quaisquer contas de logon **mestre** torna-se o seu banco de dados padrão.  
  
> [!NOTE]  
>  Para obter informações sobre como exibir o banco de dados padrão de todas as contas de logon, consulte [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md). Se você tiver as permissões necessárias, você pode usar [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para atribuir um novo banco de dados padrão para um logon.  
  
## <a name="restrictions"></a>Restrictions  
 Um banco de dados não pode ser desanexado se algum dos seguintes fatores for verdadeiro:  
  
-   O banco de dados está atualmente em uso. Para obter mais informações, consulte "Obtendo acesso exclusivo”, posteriormente neste tópico.  
  
-   Se duplicado, o banco de dados será publicado.  
  
     Antes de poder desanexar o banco de dados, você deve desabilitar a publicação executando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    >  Se não for possível usar **sp_replicationdboption**, você poderá remover a replicação executando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Há um instantâneo do banco de dados no banco de dados.  
  
     Antes de poder desanexar o banco de dados, você deve descartar todos os seus instantâneos. Para obter mais informações, veja [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
-   O banco de dados está sendo espelhado.  
  
     O banco de dados não pode ser desanexado até que a sessão de espelhamento de banco de dados seja encerrada. Para obter mais informações, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   O banco de dados é suspeito.  
  
     É preciso colocar um banco de dados suspeito em modo de emergência antes de poder desanexá-lo. Para obter mais informações sobre como colocar um banco de dados em modo de emergência, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   O banco de dados é um banco de dados de sistema.  
  
## <a name="obtaining-exclusive-access"></a>Obtendo acesso exclusivo  
 A desanexação de um banco de dados exige acesso exclusivo ao banco de dados. Se o banco de dados a ser dexanexado estiver em uso, antes que ele possa ser desanexado, defina o banco de dados como modo SINGLE_USER para obter acesso exclusivo.  
  
 Por exemplo, a seguinte `ALTER DATABASE` instrução obtém acesso exclusivo para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] depois que todos os usuários atuais se desconectar do banco de dados do banco de dados.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  Para forçar os usuários atuais do banco de dados imediatamente ou dentro de um número especificado de segundos, também pode usar a opção ROLLBACK: ALTER DATABASE *database_name* SET SINGLE_USER WITH ROLLBACK *rollback_option*. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="reattaching-a-database"></a>Reanexando um banco de dados  
 Os arquivos desanexados permanecem e podem ser anexados novamente com o uso de CREATE DATABASE (com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG). Os arquivos podem ser movidos para outro servidor, onde podem ser anexados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** fixa função de servidor ou associação na **db_owner** função do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desanexa o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] do banco de dados com *skipchecks* definido como true.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 O exemplo a seguir desanexa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e mantém os arquivos de índice de texto completo e os metadados de índice de texto completo. Esse comando executa UPDATE STATISTICS, que é o comportamento padrão.  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md)  
  
  
