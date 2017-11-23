---
title: sp_detach_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
caps.latest.revision: "86"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c50a0b30d69e88047ea614052cebc0105ed7c4a7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desanexa um banco de dados que não está em uso atualmente em uma instância de servidor e, opcionalmente, executa UPDATE STATISTICS em todas as tabelas antes de desanexar.  
  
> [!IMPORTANT]  
>  Para que um banco de dados replicado seja desanexado, é preciso que ele seja não publicado. Para obter mais informações, consulte "Comentários", posteriormente neste tópico.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname =** ] **'***database_name***'**  
 É o nome do banco de dados a ser desanexado. *Database_Name* é um **sysname** valor, com um valor padrão de NULL.  
  
 [  **@skipchecks =** ] **'***skipchecks***'**  
 Especifica se UPDATE STATISTIC deve ser ignorado ou executado. *skipchecks* é um **nvarchar (10)** valor, com um valor padrão de NULL. Para ignorar UPDATE STATISTICS, especifique **true**. Para executar explicitamente UPDATE STATISTICS, especifique **false**.  
  
 Por padrão, UPDATE STATISTICS é executado para atualizar as informações sobre os dados nas tabelas e os índices. A execução de UPDATE STATISTICS é útil para bancos de dados que serão movidos para mídias somente leitura.  
  
 [  **@keepfulltextindexfile=** ] **'***KeepFulltextIndexFile***'**  
 Especifica se o arquivo de índice de texto completo associado ao banco de dados que está sendo desanexado não será descartado durante a operação de desanexação. *KeepFulltextIndexFile* é um **nvarchar (10)** valor com um padrão de **true**. Se *KeepFulltextIndexFile* é **false**, todos os arquivos de índice de texto completo associado com o banco de dados e os metadados do índice de texto completo são removidos, a menos que o banco de dados é somente leitura. Se for NULL ou **true**, texto completo relacionadas a metadados são mantidos.  
  
> [!IMPORTANT]  
>  O **@keepfulltextindexfile**  parâmetro será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não use esse parâmetro em desenvolvimentos novos e modifique, assim que possível, os aplicativos que atualmente o usam.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Quando um banco de dados é desanexado, todos os metadados são descartados. Se o banco de dados padrão de qualquer conta de logon, o banco de dados **mestre** torna-se o seu banco de dados padrão.  
  
> [!NOTE]  
>  Para obter informações sobre como exibir o banco de dados padrão de todas as contas de logon, consulte [sp_helplogins &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md). Se você tiver as permissões necessárias, você pode usar [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) para atribuir um novo banco de dados padrão para um logon.  
  
## <a name="restrictions"></a>Restrições  
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
  
 Por exemplo, a seguinte `ALTER DATABASE` instrução obtém acesso exclusivo para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] depois de desconectarem todos os usuários atuais do banco de dados do banco de dados.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  Para forçar atuais usuários de banco de dados imediatamente ou após um número especificado de segundos, também usam a opção ROLLBACK: ALTER DATABASE *database_name* SET SINGLE_USER WITH ROLLBACK *rollback_option*. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="reattaching-a-database"></a>Reanexando um banco de dados  
 Os arquivos desanexados permanecem e podem ser anexados novamente com o uso de CREATE DATABASE (com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG). Os arquivos podem ser movidos para outro servidor, onde podem ser anexados.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** fixo de função de servidor ou a associação a **db_owner** função do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desanexa o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados com *skipchecks* definido como true.  
  
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
  
  
